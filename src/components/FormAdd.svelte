<script>
  import { Row,Container } from 'sveltestrap'
  import ImgEncoder from 'svelte-image-encoder';
  let src='some-image.jpg';
  let url;
 
  let title = "";
  let author = "";
  let image = "";
  let price = 0;
  let urlBuy = '';

function loadFile(e) {
    src = URL.createObjectURL(e.target.files[0]);
}

function addBook(){
    let imageJson = url.substring(5)
    console.log(imageJson)
    let data = JSON.stringify(
    {
        "author": author,
        "url": urlBuy,
        "_id": title,
        "price": price,
        "title": title,
        "img": {
            "content_type": "image/jpeg",
            "filename": "51l6jdkdagL._SL160_SL150_.jpg",
            "data": "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",
            "path": "images/51l6jdkdagL._SL160_SL150_.jpg"
        }
    }
    )
}

</script>
<form>
    <Container>
        <Row class='justify-content-md-center'>
            <label>Auteur :</label>
            <input type='text' bind:value={author}>
        </Row>
        <Row class='justify-content-md-center'>
            <label>Titre :</label>
            <input type='text' bind:value={title}>
        </Row>
        <Row class='justify-content-md-center'>
            <label>Prix :</label>
            <input type='text' bind:value={price}>
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