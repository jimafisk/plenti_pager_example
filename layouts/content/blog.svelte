<script>
	export let title, body, author, date, store;
  import Uses from "../components/template.svelte";

  // Svelte store example:
  import { count } from '../scripts/stores.svelte';
  import Incrementer from '../components/incrementer.svelte';
  import Decrementer from '../components/decrementer.svelte';
  let count_value;
  const unsubscribe = count.subscribe(value => {
    count_value = value;
  });

  // Content driven dynamic components example:
  export let components, allLayouts;
</script>

<h1>{title}</h1>

<p><em>{#if author}Written by {author}{/if}{#if date}&nbsp;on {date}{/if}</em></p>

<div>
  {#each body as paragraph}
    <p>{@html paragraph}</p>
  {/each}
</div>

{#if store}
  <h3>The count is {count_value}</h3>
  <Incrementer/>
  <Decrementer/>  
{/if}

{#if components}
	{#each components as { title, component, fields }}
    <p>{title}</p>
		<svelte:component this="{allLayouts["layouts_components_" + component + "_svelte"]}" {...fields} />
	{/each}
{/if}

<Uses type="blog" />

<p><a href="/">Back home</a></p>
