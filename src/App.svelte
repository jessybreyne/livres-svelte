<script>
  import DB from "./DB.svelte";
  import "@polymer/paper-card";
  import "@material/mwc-button";
  import { Col, Container, Row } from "sveltestrap";
  import "@material/mwc-icon-button";
  import "@material/mwc-top-app-bar";
  let books = [];
</script>

<style>
  paper-card {
    width: 100%;
    margin-top: 3px;
    margin-bottom: 3px;
  }
</style>
<link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
<main>
   <DB bind:documents={books} initsrc="./books.json" collection="books"/>
   <mwc-top-app-bar>
    <mwc-icon-button icon="menu" slot="navigationIcon"></mwc-icon-button>
    <div slot="title">Title</div>
    <mwc-icon-button icon="file_download" slot="actionItems"></mwc-icon-button>
    <mwc-icon-button icon="print" slot="actionItems"></mwc-icon-button>
    <mwc-icon-button icon="favorite" slot="actionItems"></mwc-icon-button>
    <div><!-- content --></div>
  </mwc-top-app-bar>
  <Container>
    <Row>
    {#each books as book}
      <Col lg='4' md='6' sm='12'>
        <paper-card heading={book.title}>
          <img src="data:image/jpeg;base64, {book.img.data}" alt="{book.title}" title="{book.title}"/>
          <div class="card-content">
            Ecrit par {book.author} au prix de {book.price}
          </div>
        </paper-card>
      </Col>
    {/each}
    </Row>
  </Container>
</main>
