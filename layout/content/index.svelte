<script>
	export let title, intro, content, components, allContent;
	import Grid from '../components/grid.svelte';
  import Uses from "../components/template.svelte";
  import Pager from "../components/pager.svelte";

  $: currentPage = content.pager; // get the new "pager" key from the content source.
  let postsPerPage = 3;
  let allPosts = allContent.filter(content => content.type == "blog");
  let totalPosts = allPosts.length;
  let totalPages = Math.ceil(totalPosts / postsPerPage);
  $: postRangeHigh = currentPage * postsPerPage;
  $: postRangeLow = postRangeHigh - postsPerPage;
</script>

<h1>Pager Example</h1>

<section id="intro">
	{#each intro as paragraph}
		<p>{@html paragraph}</p>
	{/each}
</section>

{#each allPosts.sort((a,b) => a.filename.localeCompare(b.filename)) as post, i}
  {#if i >= postRangeLow && i < postRangeHigh}
    <h3>{post.filename}</h3>
  {/if}
{/each}

<Pager {currentPage} {totalPages} />

{#each allPosts as post, i}
  {#if true}
    {post.filename}<br />
  {/if}
{/each}

<div>
  <h3>Recent blog posts:</h3>
  <Grid items={allPosts} />
	<br />
</div>

<Uses type="index" />
