<script>
  import { Row,Container,Button,Modal,ModalBody,ModalFooter,ModalHeader } from 'sveltestrap'
  import Graphique from "./Graphique.svelte";
  export let toggleChart;
  export let openChart;
  export let sizeChart;

</script>
<Modal isOpen={openChart} {toggleChart} {sizeChart}>
    <ModalHeader {toggleChart}>Les prix des livres</ModalHeader>
    <ModalBody>
        <Graphique/>
     </ModalBody>
    <ModalFooter>
        <Button type="button" on:click={toggleChart}>Fermer</Button>
    </ModalFooter>
</Modal>