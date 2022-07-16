<script>
	export let title, intro, content, components, allContent;
	import Grid from '../components/grid.svelte';
  import Uses from "../components/template.svelte";
  import Pager from "../components/pager.svelte";

  $: currentPage = content.pager ? content.pager : 1; // get the new "pager" key from the content source.
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

<div>
  <h3>Recent blog posts:</h3>
  <Grid items={allPosts} {postRangeLow} {postRangeHigh} />
	<br />
</div>

<Pager {currentPage} {totalPages} />

<Uses type="index" />
