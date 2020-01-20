<script>
  import { paginate, LightPaginationNav } from 'svelte-paginate'
  export let items;
  let currentPage = 1;
  let pageSize = 9;
  $: paginatedItems = paginate({ items, pageSize, currentPage })
</script>

    <LightPaginationNav 
    totalItems="{items.length}" 
    pageSize="{pageSize}" 
    currentPage="{currentPage}"
    limit="{1}"
    showStepOptions="{true}"
    on:setPage="{(e) => currentPage = e.detail.page}"/>
