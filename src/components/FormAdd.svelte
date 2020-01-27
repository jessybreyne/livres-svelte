<script>
  import { form } from 'svelte-forms'
  import { Row,Container,Button,Modal,ModalBody,ModalFooter,ModalHeader,InputGroup,Label,FormGroup } from 'sveltestrap'
  import ImgEncoder from 'svelte-image-encoder';
  import PouchDB from 'pouchdb-browser'
  import "@material/mwc-icon-button";
  export let collection;
  export let books;
  export let open;
  export let toggle;
  let src;
  let url;
 
  let titlePut='';
  let authorPut='';
  let image='';
  let pricePut='';
  let urlBuy='';

function loadFile(e) {
    src = URL.createObjectURL(e.target.files[0]);
}

async function addBook(){
        let db= new PouchDB(collection)
        let image = url.split(':');
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
    }

const myForm = form(() => ({ 
    author: { value: authorPut, validators: ['required']},
    title: { value: titlePut, validators: ['required']},
    price: { value: pricePut, validators: ['required']},
    url: { value: urlBuy, validators: ['required','url']},
    image: {value: url, validators:['required']}
    }));
</script>
<Modal isOpen={open} {toggle}>
    <ModalHeader {toggle}>Ajout d'un livre</ModalHeader>
    <ModalBody>
        <Container>
        <form>
            <FormGroup>
                <Label for="auteur">Auteur</Label>
                <input id="auteur" type="text" class="form-control" bind:value={authorPut} class:valid={$myForm.author.valid} aria-describedby="auteur du livre"/>
            </FormGroup>
            <FormGroup>
                <Label for="titre">Titre</Label>
                <input id="titre" type="text" class="form-control" bind:value={titlePut} class:valid={$myForm.title.valid} aria-describedby="auteur du livre"/>
            </FormGroup>
            <FormGroup>
                <Label for="prix">Prix</Label>
                <InputGroup>
                    <input id="prix" class="form-control" bind:value={pricePut} class:valid={$myForm.price.valid} aria-describedby="le prix du livre"/>
                    <span class="input-group-text" id="basic-addon2">€</span>
                </InputGroup>
            </FormGroup>
            <FormGroup>
                <Label for="url">Lien d'achat</Label>
                <input id="url" type="text" class="form-control" bind:value={urlBuy} class:valid={$myForm.price.valid} aria-describedby="url d'achat du livre"/>
            </FormGroup>
            <Row class='justify-content-md-center'>
                <ImgEncoder {src} bind:url/>
            </Row>
            <Row class='justify-content-md-center'>
                <input on:change={loadFile} type='file' class:valid={$myForm.image.valid}/>
            </Row>
            </form>
        </Container>
     </ModalBody>
    <ModalFooter>
        <Button type="button" on:click={toggle}>Annuler</Button>
        <Button on:click={addBook} type='button' class="btn btn-success" disabled={!$myForm.valid}>Ajouter le livre</Button>
    </ModalFooter>
</Modal>