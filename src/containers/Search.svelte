<script>
    export let items;
    import Book from "../components/Book.svelte"
    import SearchBar from "../components/SearchBar.svelte"
    import { Row, Container } from "sveltestrap";

</script>

<Container>
      <SearchBar bind:items={items}/>
</Container>

