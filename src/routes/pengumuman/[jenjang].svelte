<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
    import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/pengumuman/${params.jenjang}`);
            post = await post.json();
        } catch (e) {
            console.log(e);
        }
        return {
            props: {
                post
            }
        };
    }

</script>
<script>
    import Overlay from '$lib/Overlay.svelte';
      import RowPengumuman from '$lib/RowPengumuman.svelte';
      import Pagination from '$lib/Pagination.svelte';
      export let post; 
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
        axios.get(`https://data-pusatprestasinasional.kemdikbud.go.id/api/loadmore/load_data/${post.jenjang.slug}`, {
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
            <div class="col-md-12">
                <h4 class="title-section ml-0">Kabar Prestasi {post.jenjang.nama_jenjang}</h4>
            </div>
            
        </div>  
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
        
            
            <!-- {#each post.pengumuman as item}
                <div class="col-md-12">                                        
                    <a href="pengumuman/{post.jenjang.slug}/{item.slug}" class="pengumuman-card">                                                                                                                            
                        <div>
                            <h5>{@html item.tgl}</h5>
                        </div>                                                                                                
                        <h5>{item.title}</h5>                             
                    </a>                    
                </div>
            {/each} -->
        
    </div>
</section>
</PageTransitions>
<Footer/>