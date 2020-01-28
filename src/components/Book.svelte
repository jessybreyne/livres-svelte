<script>
  import { onMount,onDestroy } from 'svelte';
  import { Col, Container, Row } from "sveltestrap";
  import PouchDB from "pouchdb-browser";
  export let book;
  export let array;
  export let current;
  export let indice;
  export let pageSize;
  export let bookEdit;
  export let open;
  let db;

  async function removeBook(id){
    let nb = (current-1)*pageSize+indice
    db.get(id).then(function(doc){ db.remove(doc);});
    array = array.slice(0,nb).concat(array.slice(nb +1))
  }

  onMount(
    async () => {
      db = new PouchDB("books")
    }
  );

  onDestroy(
   async () => {
     console.log("Objet removed")
   }
 );
 
 function editBook(book){
   bookEdit = book;
   open = true;
 }

function redirection(url){
   document.location.href=url;

 }
 
</script>


<style>
  paper-card {
    width: 100%;
    margin-top: 3px;
    margin-bottom: 3px;
    text-align:center;
  }
</style>

<Col lg='4' md='6' sm='12' class="mt-4">
    <paper-card heading={book.title} class="h-100">
        <img src="data:image/jpeg;base64, {book.img.data}" alt="{book.title}" title="{book.title}"/>
        <div class="card-content">
            Ecrit par {book.author} au prix de {book.price}
            <br>
            <button class="btn btn-danger" on:click={removeBook(book._id)}>Supprimer</button>
            <button class="btn btn-success" on:click={redirection(book.url)}>Acheter</button>
            <button class="btn btn-secondary" on:click={editBook(book)}>Editer</button>
        </div>
    </paper-card>
</Col>
