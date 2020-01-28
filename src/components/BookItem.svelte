<script>
  import { paginate, LightPaginationNav } from 'svelte-paginate'
  import { Col, Container, Row } from "sveltestrap";
  export let book;

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
            <button class="btn btn-success" on:click={redirection(book.url)}>Acheter</button>
        </div>
    </paper-card>
</Col>
