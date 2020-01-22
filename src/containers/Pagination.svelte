<script>
  import { paginate, LightPaginationNav } from 'svelte-paginate'
  export let items;
  import Book from "../components/Book.svelte"
   import { Row } from "sveltestrap";
  let currentPage = 1;
  let pageSize = 9;
  $: paginatedItems = paginate({ items, pageSize, currentPage })
</script>
  <Row>
    {#each paginatedItems as book}
        <Book class="item" bind:book={book}/>
    {/each}
  </Row>
  <Row class="justify-content-md-center mt-5 mb-5">
    <LightPaginationNav 
    totalItems="{items.length}" 
    pageSize="{pageSize}" 
    currentPage="{currentPage}"
    limit="{1}"
    showStepOptions="{true}"
    on:setPage="{(e) => currentPage = e.detail.page}"/>
  </Row>
