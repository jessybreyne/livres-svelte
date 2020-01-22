<script>
    import { FormGroup, Input } from "sveltestrap";
    export let items;
    export let result = [];


    async function search(event) {
        let query = document.getElementById('search').value;
        
        for(let book of items){
            
            if(book.title.indexOf(query) >= 0 || book.author.indexOf(query) >= 0){
                result.push(book);
            }
        }
        console.log(result.length);
    }
</script>

<FormGroup>
    <Input on:keyup={search}
        
        type="search"
        name="search"
        id="search"
        placeholder="Rechercher" />
  </FormGroup>