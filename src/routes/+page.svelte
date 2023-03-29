<script>
    import {Button} from "sveltestrap";

    let fetchData = async ()=>{
        const res = await fetch("https://api.dataforsyningen.dk/adresser?vejnavn=Rødkildevej&husnr=46&struktur=mini");
        const data = await res.json();
        const text = JSON.stringify(data)
        return text;
    };


</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<Button on:click={fetchData}>Test</Button>
{#await fetchData}
    {:then}

{/await}

