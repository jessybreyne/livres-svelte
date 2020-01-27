<script>
  import DB from "../components/DB.svelte";
  import Pagination from "./Pagination.svelte";
  import Search from "./Search.svelte";
  import "@polymer/paper-card";
  import PouchDB from 'pouchdb-browser';
  import "@material/mwc-button";
  import { Col, Container, Row } from "sveltestrap";
  import FormAdd from "../components/FormAdd.svelte"
  import "@material/mwc-icon-button";
  import "@material/mwc-top-app-bar";
  let books = [];
  let database= "books";
  let open = false;
  const toggle = () => (open = !open);
</script>


<link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
<main>
   <DB bind:documents={books} initsrc="./books.json" collection={database}/>
   <mwc-top-app-bar>
    <div slot="title">Books Storage</div>
      <div class="collapse" id="collapseSearch">
        <div class="card card-body">
          <Search bind:items={books}/>
        </div>
      </div>
      <mwc-icon-button data-toggle="collapse" data-target="#collapseSearch" aria-expanded="false" aria-controls="collapseSearch" icon="search" slot="actionItems"></mwc-icon-button>
      <mwc-icon-button icon="add" slot="actionItems" on:click={toggle}></mwc-icon-button>
      <mwc-icon-button icon="favorite" slot="actionItems"></mwc-icon-button>
  </mwc-top-app-bar>
  <Container>
    <Pagination bind:items={books} collection={database}/>
  </Container>
  <FormAdd bind:collection={database} bind:books={books} toggle={toggle} bind:open={open}/>
</main>
