<script>
    import { FormGroup, Input } from "sveltestrap";
    export let items;
    let query;

 async function search(query, items) {
    let result = [];
    for(let book in items){
        if(book.title.search(query) || book.author.search(query)){
            result.append(book);
        }
    }
    console.log(result);
 }
</script>

<FormGroup>
    <Input
        bind:value={query}
        type="search"
        name="search"
        id="exampleSearch"
        placeholder="search placeholder" />
  </FormGroup>