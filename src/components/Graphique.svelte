<script>
    import Chart from 'svelte-frappe-charts';
    export let books;

    let valeurs = [];
    let count;
    let tableauCountVal = [];
 
    console.log(books);


    books.forEach(book => {
        console.log(book.price);
        valeurs.push(Math.round(book.price));

    });

    function cleanArray(array) {
    var i, j, len = array.length, out = [], obj = {};
    for (i = 0; i < len; i++) {
        obj[array[i]] = 0;
    }
    for (j in obj) {
        out.push(j);
    }
    return out;
    }

    let labelsVal = cleanArray(valeurs);

    labelsVal.forEach(val => {
        count = 0;
        for(var i = 0; i < valeurs.length; ++i){
            if(valeurs[i] == val)
                count++;
        }
        tableauCountVal.push(count);

    });

    


    let data = {
        labels: labelsVal,
        datasets: [
        {
            name: "Livres",
            values: tableauCountVal
        }
        ]
    };
</script>
 
<Chart data={data} type="line"/>