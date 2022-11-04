<script context="module">
    import Nav2 from "$lib/Nav2.svelte";	
	import Footer from "$lib/Footer.svelte";
    import PageTransitions from "$lib/PageTransitions.svelte";
</script>
<script>
    import Kategori from "$lib/Kategori_peng.svelte";
    import Overlay from '$lib/Overlay.svelte';
    import RowPengumuman from '$lib/RowPengumuman.svelte';
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
    axios.get('https://data-pusatprestasinasional.kemdikbud.go.id/api/loadmore/load_data', {
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
<svelte:head>
    <title>Kabar Prestasi | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<section>
    <div class="container py-5 px-5">
        <div class="row">
            <div class="col-md-6 mx-auto mt-5">
                <h4 class="title-section mx-auto">Kabar Prestasi</h4>
            </div>
            
        </div> 
        <div class="row">
            <Kategori />
            <div class="col-md-12 col-lg-9"> 
                <div style="margin-bottom: 10px;">
                    <input class="form-control" placeholder="Cari kata kunci..." on:keyup={e => changePage({cari: e.target.value})}/>
                </div>
                {#if loading}
                <Overlay />
                {/if}
                <div id="data-wrapper">
                    {#each rows as row}
                    <RowPengumuman {row} />
                    
                    {:else}
                    <tr>
                        <td colspan="100%">
                        <h5 class="text-center">There are no Users here.</h5>
                        </td>
                    </tr>
                    {/each}
                </div>     
                                                                                                                                        
            </div>
        </div>     
        <div class="d-flex align-items-end flex-column">
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