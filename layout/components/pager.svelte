<script>
  export let currentPage, totalPages;
</script>
{currentPage}
<ul>
  {#if currentPage > 1}
    <li><a href="/" on:click={() => setCurrentPage(1)}>first</a></li>
    <li><a href="/{currentPage - 1}">previous</a></li>
  {/if}
  {#each [3,2,1] as i}
    {#if currentPage - i > 0}
      <li><a href="/{currentPage - i}">{currentPage - i}</a></li>
    {/if}
  {/each}
  <li><span>{currentPage}</span></li>
  {#each Array(3) as _, i}
    {#if currentPage + (i+1) <= totalPages}
      <li><a href="/{currentPage + (i+1)}">{currentPage + (i+1)}</a></li>
    {/if}
  {/each}
  {#if currentPage < totalPages}
    <li><a href="/{currentPage + 1}">next</a></li>
    <li><a href="/{totalPages}">last</li>
  {/if}
</ul>
