<script lang="ts">
  import { formatForURL } from '@lib/utils/tags';

  export let tags: string[];
</script>

<span>
  {#each tags.sort() as tag, i}
    <a href={`/tag/${formatForURL(tag)}`} aria-label={`View posts tagged with ${tag}`}>
      {tag}
    </a>
    {#if i < tags.length - 1}
      <span>, </span>
    {/if}
  {/each}
</span>

<style lang="scss">
  a {
    color: var(--color-accent);
    text-decoration: underline;
    display: inline-block;

    &:hover,
    &:focus {
      color: var(--color-link-hover);
    }
  }

  span {
    color: var(--color-accent);
  }
</style>
