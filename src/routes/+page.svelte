<script>
    import {Button, Container, Input, Row} from "sveltestrap";
    let vejnavn =""
    let husnr =""

    let fetchData = async ()=>{
        await new Promise(r => setTimeout(r, 1000)); //Some delay for testing - just remove
        const res = await fetch("https://api.dataforsyningen.dk/adresser?vejnavn=" + vejnavn +"&husnr="+ husnr +"&struktur=mini");
        return await res.json();
    };
    let promise = [];
</script>
<!-- Some sveltestrap rows to align stuff: -->
<Container>
<Row>
    <!-- Input bound to variables -->
<Input type="text" bind:value={vejnavn} placeholder="Search for vejnavn"/>
</Row>
<Row>
<Input type="text" bind:value={husnr} placeholder="Search for nr"/>
</Row>
<Row>
    <!-- Button that starts async fetching -->
<Button on:click={()=>promise=fetchData()}>Test</Button>
</Row>
</Container>
<!-- Svelte syntax to show Loading until async promise is resolved -->
{#await promise}
    Loading...
{:then json}
    <div>
        Got Adresses:
    </div>
    <!-- Svelte templating to map address array to multiple lines -->
    {#each json as address }
    <ol>
        {address.betegnelse}
    </ol>
    {/each}
{/await}

