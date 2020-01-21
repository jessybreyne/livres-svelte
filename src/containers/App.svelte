<script>
  import DB from "../components/DB.svelte";
  import Pagination from "./Pagination.svelte"
  import "@polymer/paper-card";
  import "@material/mwc-button";
  import { Col, Container, Row } from "sveltestrap";
  import "@material/mwc-icon-button";
  import "@material/mwc-top-app-bar";
  let books = [];
</script>


<link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
<main>
   <DB bind:documents={books} initsrc="./books.json" collection="books"/>
   <mwc-top-app-bar>
    <mwc-icon-button icon="menu" slot="navigationIcon"></mwc-icon-button>
    <div slot="title">Books Storage</div>
    <mwc-icon-button icon="file_download" slot="actionItems"></mwc-icon-button>
    <mwc-icon-button icon="print" slot="actionItems"></mwc-icon-button>
    <mwc-icon-button icon="favorite" slot="actionItems"></mwc-icon-button>
    <div><!-- content --></div>
  </mwc-top-app-bar>
  <Container>
    <Pagination bind:items={books}/>
  </Container>
</main>
