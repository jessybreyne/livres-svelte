<script>
  import { form } from 'svelte-forms'
  import { Row,Container } from 'sveltestrap'
  import ImgEncoder from 'svelte-image-encoder';
  import PouchDB from 'pouchdb-browser'
  export let collection;
  export let books;

  let src;
  let url;
 
  let titlePut;
  let authorPut;
  let image;
  let pricePut;
  let urlBuy;

function loadFile(e) {
    src = URL.createObjectURL(e.target.files[0]);
}

async function addBook(){
        let db= new PouchDB(collection)
        let image = url.split(':');
        image = image[1].split(';');
        image[1] = image[1].split(',')[1];
        db.post({
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
    }

</script>
<form>
    <Container>
        <Row class='justify-content-md-center'>
            <label>Auteur :</label>
            <input type='text' bind:value={authorPut}>
        </Row>
        <Row class='justify-content-md-center'>
            <label>Titre :</label>
            <input type='text' bind:value={titlePut}>
        </Row>
        <Row class='justify-content-md-center'>
            <label>Prix :</label>
            <input type='text' bind:value={pricePut}>
        </Row>
        <Row class='justify-content-md-center'>
            <label>Lien d'achat :</label>
            <input type='url' bind:value={urlBuy}>
        </Row>
    </Container>
    <Container>
        <Row class='justify-content-md-center'>
            <ImgEncoder {src} bind:url/>
        </Row>
        <Row class='justify-content-md-center'>
            <input on:change={loadFile} type='file' >
            <p>{url}</p>
        </Row>
    </Container>
    <Container>
        <Row class='justify-content-md-center'>
            <button on:click={addBook} type='button' class="btn btn-success">Ajouter le livre</button>
        </Row>
    </Container>
</form> 