<script>
  import { Row,Container,Button,Modal,ModalBody,ModalFooter,ModalHeader,InputGroup,Label,FormGroup,Alert } from 'sveltestrap'
  import ImgEncoder from 'svelte-image-encoder';
  import PouchDB from 'pouchdb-browser'
  import "@material/mwc-icon-button";
  export let collection;
  export let books;
  export let open;
  export let toggle;
  let src;
  let url;
 
  let isEdit=false;
  let titlePut;
  let authorPut;
  let image;
  let pricePut;
  let urlBuy;
  let visible=false;

function loadFile(e) {
    src = URL.createObjectURL(e.target.files[0]);
}
async function addBook(){
    if (url && titlePut && authorPut && pricePut && urlBuy){
        let db= new PouchDB(collection)
        image = url.split(':');
        image = image[1].split(';');
        image[1] = image[1].split(',')[1];
        await db.post({
            author: authorPut,
            url: urlBuy,
            _id: titlePut,
            price: pricePut,
            title: titlePut,
            img:{
                content_type: image[0],
                filename: image[1].substring(2,10)+".jpg",
                data: image[1],
                path: "images/"+ image[1].substring(2,10) +".jpg"  
            }     
        });
        const zdocs = await db.allDocs({include_docs: true});
        books = zdocs.rows.map(d => d.doc)
        titlePut= '';
        urlBuy = '';
        authorPut = '';
        image = '';
        url = '';
        src = '';
        pricePut = '';
        open=false;
    }
    else{
        visible=true;
    }
}

</script>
<Modal isOpen={open} {toggle}>
    <ModalHeader {toggle}>Ajout d'un livre</ModalHeader>
    <ModalBody>
        <Container>
        <Alert color="danger" isOpen={visible} toggle={() => (visible = false)}>
            Une information est invalide !
        </Alert>
        <form>
            <FormGroup>
                <Label for="auteur">Auteur</Label>
                <input id="auteur" type="text" class="form-control" bind:value={authorPut} aria-describedby="auteur du livre" required/>
            </FormGroup>
            <FormGroup>
                <Label for="titre">Titre</Label>
                <input id="titre" type="text" class="form-control" bind:value={titlePut} aria-describedby="auteur du livre" required/>
            </FormGroup>
            <FormGroup>
                <Label for="prix">Prix</Label>
                <InputGroup>
                    <input id="prix" class="form-control" bind:value={pricePut} aria-describedby="le prix du livre" required/>
                    <span class="input-group-text" id="basic-addon2">€</span>
                </InputGroup>
            </FormGroup>
            <FormGroup>
                <Label for="url">Lien d'achat</Label>
                <input id="url" type="text" class="form-control" bind:value={urlBuy} aria-describedby="url d'achat du livre"/>
            </FormGroup>
            <Row class='justify-content-md-center'>
                <ImgEncoder {src} bind:url/>
            </Row>
            <Row class='justify-content-md-center'>
                <input on:change={loadFile} type='file'/>
            </Row>
            </form>
        </Container>
     </ModalBody>
    <ModalFooter>
        <Button type="button" on:click={toggle}>Annuler</Button>
        <button on:click|preventDefault={addBook} type='submit' class='btn btn-success'>Ajouter le livre</button>
    </ModalFooter>
</Modal>