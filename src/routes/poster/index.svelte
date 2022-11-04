<script context="module">
    import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";
</script>
<script>
    import Overlay from '$lib/Overlay.svelte';
    import RowPoster from '$lib/RowPoster.svelte';
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
    axios.get('https://data-pusatprestasinasional.kemdikbud.go.id/api/loadmore/poster', {
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
    
    
</script>
<style>
    
</style>
<svelte:head>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.css" />
    <title>Poster | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<section>
    <div class="container py-2 px-5">
        <div class="row">
            <div class="col-md-12 mt-5">
                <h4 class="title-section ml-0">Poster Prestasi</h4>
            </div>
            
        </div> 
        <div>
                {#if loading}
                <Overlay />
                {/if}
                <div class="row" id="data-wrapper">
                    {#each rows as row}
                    <RowPoster {row} />
                    
                    {:else}
                    <tr>
                        <td colspan="100%">
                        <h5 class="text-center">There are no Users here.</h5>
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
    
</section>
</PageTransitions>
<Footer/>