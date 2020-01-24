<script>
  import { onMount,onDestroy } from 'svelte';
  import { Col, Container, Row } from "sveltestrap";
  import PouchDB from "pouchdb-browser";
  export let book;
  export let array;
  export let current;
  export let indice;
  export let pageSize;
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
            <button class="text-danger" on:click={removeBook(book._id)}>Supprimer</button>
            <a href='{book.url}' class="btn btn-success">Acheter</a>
        </div>
    </paper-card>
</Col>
