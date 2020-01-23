<script>
    import { FormGroup, Input, Row } from "sveltestrap";
    import BookItem from "../components/BookItem.svelte"

    export let items;

    let result;
    let query;

    $: search(query);

    async function search(query) {
        result = [];
        
        for(let book of items){
            
            if(book.title.indexOf(query) >= 0 || book.author.indexOf(query) >= 0){
                result.push(book);
            }
        }
        console.log(result.length);
    }
</script>

<FormGroup>
    <Input 
        bind:value={query}
        type="search"
        name="search"
        id="search"
        placeholder="Rechercher" />
  </FormGroup>

  <Row>
    {#each result as book}
        <BookItem class="item" bind:book={book}/>
    {/each}
  </Row>