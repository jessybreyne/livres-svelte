<script>
  import { paginate, LightPaginationNav } from 'svelte-paginate'
  export let items;
  import Book from "../components/Book.svelte"
  import FormEdit from "../components/FormEdit.svelte"
  import { Row } from "sveltestrap";
  let currentPage = 1;
  let pageSize = 9;
  let bookEdit;
  let open;
  const toggle = () => (open = !open);
  $: paginatedItems = paginate({ items, pageSize, currentPage })
</script>
  <Row>
    {#each paginatedItems as book,i}
        <Book class="item" bind:book={book} bind:array={items} indice={i} pageSize={pageSize} current={currentPage} bind:bookEdit={bookEdit} bind:open={open}/>
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

  <FormEdit bind:books={items} collection='books' bind:book={bookEdit} bind:open={open} bind:toggle={toggle}/>

