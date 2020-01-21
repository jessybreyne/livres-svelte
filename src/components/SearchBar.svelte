<script>
   import { FormGroup, Input } from "sveltestrap";
   export let items;


 async function search(query, items) {
   
 }
</script>

<FormGroup>
    <Input
      type="search"
      name="search"
      id="exampleSearch"
      placeholder="search placeholder" />
  </FormGroup>