<script>
  import { paginate, LightPaginationNav } from 'svelte-paginate'
  import { Col, Container, Row } from "sveltestrap";
  export let book;
</script>

<style>
  paper-card {
    width: 100%;
    margin-top: 3px;
    margin-bottom: 3px;
  }
</style>

<Col lg='4' md='6' sm='12'>
    <paper-card heading={book.title}>
        <img src="data:image/jpeg;base64, {book.img.data}" alt="{book.title}" title="{book.title}"/>
        <div class="card-content">
            Ecrit par {book.author} au prix de {book.price}
        </div>
    </paper-card>
</Col>