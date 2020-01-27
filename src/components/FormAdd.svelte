<script>
  import { form } from 'svelte-forms'
  import { Row,Container } from 'sveltestrap'
  import ImgEncoder from 'svelte-image-encoder';
  import PouchDB from 'pouchdb-browser'
  export let collection;
  export let books;

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
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Ajout d'un livre</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <form>
                <div class="modal-body">
                    <Container>
                        <Row class='justify-content-md-center'>
                            <label>Auteur :</label>
                            <input type='text' bind:value={authorPut} class:valid={$myForm.author.valid}>
                        </Row>
                        <Row class='justify-content-md-center'>
                            <label>Titre :</label>
                            <input type='text' bind:value={titlePut} class:valid={$myForm.title.valid}>
                        </Row>
                        <Row class='justify-content-md-center'>
                            <label>Prix :</label>
                            <input type='text' bind:value={pricePut} class:valid={$myForm.price.valid}>
                        </Row>
                        <Row class='justify-content-md-center'>
                            <label>Lien d'achat :</label>
                            <input type='url' bind:value={urlBuy} class:valid={$myForm.price.valid}>
                        </Row>
                    </Container>
                    <Container>
                        <Row class='justify-content-md-center'>
                            <ImgEncoder {src} bind:url/>
                        </Row>
                        <Row class='justify-content-md-center'>
                            <input on:change={loadFile} type='file' class:valid={$myForm.image.valid} >
                        </Row>
                    </Container>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Annuler</button>
                    <button on:click={addBook} type='button' class="btn btn-success" disabled={!$myForm.valid}>Ajouter le livre</button>
                </div>
            </form>
        </div>
    </div>
</div>