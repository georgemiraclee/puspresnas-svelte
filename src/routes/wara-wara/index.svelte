<script context="module">
    import Nav2 from "$lib/Nav2.svelte"
	import Quotes from "$lib/Quotes.svelte";
	import Footer from "$lib/Footer.svelte";
    import PageTransitions from "$lib/PageTransitions.svelte";

    export async function load({ fetch }) {
      const [quotes] = await Promise.all([
        fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/quote-of-the-day`),
      ]);
      return {
        props: {
            quotes: await quotes.json()
        },
      };
    }
    
</script>
<script>
    import Kategori from "$lib/Kategori.svelte";
    import Overlay from '$lib/Overlay.svelte';
    import RowWara from '$lib/RowWara.svelte';
    import Pagination from '$lib/Pagination.svelte';
    let current_page = 1;
    let from = 1;
    let to = 1;
    let per_page = 1;
    let last_page = 1;
    let total = 0;
    let rows = [];
    let loading = true;
    import axios from 'axios';
    function changePage(params) {
        axios.get('https://data-pusatprestasinasional.kemdikbud.go.id/api/news', {
        params: params
        })
        .then(function (response) {
        current_page = response.data.current_page;
        from = response.data.from;
        to = response.data.to;
        per_page = response.data.per_page;
        last_page = response.data.last_page;
        total = response.data.total;

        rows = response.data.data;
        })
        .catch(error => {
        console.error(error);
        })
        .finally(() => {
        loading = false;
        });
    }

    changePage({ page: 1 });
    
    export let quotes
</script>
<svelte:head>	
	<title>Wara - Wara Prestasi | Puspresnas</title>	
    <!-- <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" on:load={initializeRemarkable}></script>		 -->
</svelte:head>
<style>
    section{
        padding: 0;
    }
</style>
<Nav2/>
<PageTransitions>
<section>
    <div class="container">
        <div class="row">                
            <div class="col-md-6 mx-auto mt-5">
                <h4 class="title-section mx-auto">Wara - Wara Prestasi</h4>
            </div>                                
        </div>           
    </div>
</section>
<section>
    <div class="container py-5 px-5">
        <div class="row">
            <Kategori/>
            <div class="col-md-12 col-lg-9"> 
                <div style="margin-bottom: 10px;">
                    <input class="form-control" placeholder="Cari kata kunci..." on:keyup={e => changePage({cari: e.target.value})}/>
                </div>
                {#if loading}
                <Overlay />
                {/if}
                <div id="data-wrapper">
                    {#each rows as row}
                    <RowWara {row} />
                    
                    {:else}
                    <tr>
                        <td colspan="100%">
                        <h5 class="text-center">Belum ada wara-wara</h5>
                        </td>
                    </tr>
                    {/each}
                </div>     
                {#if total > per_page}
            <Pagination
                {current_page}
                {last_page}
                {per_page}
                {from}
                {to}
                {total}
                on:change="{(ev) => changePage({page: ev.detail})}">
            </Pagination>
            {/if}                                                                                                                             
            </div>
        </div>
        
    </div>
</section>
<Quotes {quotes}/>
</PageTransitions>
<Footer/>