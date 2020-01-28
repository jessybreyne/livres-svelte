<script>
  import { Row,Container,Button,Modal,ModalBody,ModalFooter,ModalHeader } from 'sveltestrap'
  import Graphique from "./Graphique.svelte";
  export let toggleChart;
  export let openChart;
  export let books;

</script>
<Modal isOpen={openChart} {toggleChart}  class="modal-xl">
    <ModalHeader {toggleChart}>Les prix des livres</ModalHeader>
    <ModalBody>
        <Graphique bind:books={books}/>
     </ModalBody>
    <ModalFooter>
        <Button type="button" on:click={toggleChart}>Fermer</Button>
    </ModalFooter>
</Modal>