<script lang="ts">
  import { formatForURL } from '@lib/utils/tags';
  import PostTags from '@components/PostTags.svelte';

  export let date: string;
  export let tags: string[];

  function formatDate(date: string) {
    const options: Record<string, unknown> = { year: 'numeric', month: 'long', day: 'numeric' };
    const dateObject = new Date(date).toLocaleDateString('en-us', options);
    const formattedDate = dateObject;

    return formattedDate;
  }
</script>

<div class="post-meta">
  {formatDate(date)}
  {#if tags}
    in <PostTags {tags} />
  {/if}
</div>

<style>
  .post-meta {
    font-weight: var(--font-weight-light);
    color: var(--color-accent);
    padding-top: var(--size-base);
  }
</style>
