<script context="module" lang="ts">
  import { tag } from '@lib/stores';
  import PageHeader from '@components/PageHeader.svelte';
  interface IParam {
    tag: string;
  }
  interface IFetch {
    fetch: any;
    params: IParam;
    url: any;
  }

  export async function load({ fetch, params, url }: IFetch) {
    const page = parseInt(url.searchParams.get('page') !== null ? url.searchParams.get('page') : '1');
    const tagParam = params.tag;
    tag.set(tagParam);
    const response = await fetch(`/api/posts.json?page=${page}&tag=${tagParam}`);
    const posts = await response.json();

    return {
      status: response.status,
      props: {
        posts: posts.posts,
        postCount: posts.postCount,
        page: page,
        tagParam: tagParam,
      },
    };
  }
</script>

<script lang="ts">
  import Posts from '@components/Posts.svelte';
  import type { IPosts } from '@lib/types';

  export let posts: IPosts;
  export let page: number;
  export let tagParam: string;
  export let postCount: number;
</script>

<svelte:head>
  <title>Blog</title>
</svelte:head>

<PageHeader subtitle={`tagged with '${tagParam}'`}>Blog posts</PageHeader>

<Posts {posts} {page} tag={tagParam} {postCount} />
