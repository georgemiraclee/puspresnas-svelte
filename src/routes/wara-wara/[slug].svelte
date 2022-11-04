<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
    import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/pengumuman/${params.slug}`);
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
  import RowWara from '$lib/RowWara.svelte';
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
    axios.get(`https://data-pusatprestasinasional.kemdikbud.go.id/api/news/${post.jenjang.slug}`, {
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
	<title>Wara - Wara {post.jenjang.nama_jenjang} | Puspresnas</title>	
    <!-- <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" on:load={initializeRemarkable}></script>		 -->
</svelte:head>
<Nav2/>
<PageTransitions>
<section>
    <div class="container">
        <div class="row">                
            <div class="col-md-6 mx-auto mt-5">
                <h4 class="title-section mx-auto">Wara - Wara Prestasi {post.jenjang.nama_jenjang}</h4>
            </div>                                
        </div>           
    </div>
</section>
<section>
    <div class="container py-5 px-5">
        <div class="row">
            <!-- <Kategori/> -->
            <div class="col-md-12 col-lg-12"> 
                <div style="margin-bottom: 10px;">
                    <input class="form-control" placeholder="Cari kata kunci..." on:keyup={e => changePage({cari: e.target.value})}/>
                </div>
                <div class="row">
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
                    
                    <!-- {#each post.news as item}
                        <div class="col-md-12">
                            <div class="card mb-3 border-0">
                                <div class="row no-gutters">
                                    <div class="col-md-4">
                                        <img style="object-fit: cover; height: 200px" src="{item.thumbnail}" class="rounded rounded-lg" alt="..." width="100%">
                                    </div>
                                    <div class="col-md-8">
                                        <div class="card-body pt-0">                            
                                            <h5 class="card-title">{item.title}</h5>
                                            <span class="badge badge-pill badge-orange text-white">{item.jenjang}</span>
                                            <span class="txt-span">| {item.tanggal}</span>
                                            <p class="card-text txt-p text-justify">{item.detail}
                                                <a href="/wara-wara/{item.slug_jenjang}/{item.slug}" class="txt-orange"> Selengkapnya..</a>
                                            </p>
                                            <p class="card-text"><small class="text-muted">{item.post}</small></p>                                                                
                                        </div>
                                    </div>
                                </div>                        
                            </div> 
                        </div>
                    {/each} -->
                    
                    
                </div>                                                                                                                                
            </div>
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
</section>
</PageTransitions>
<Footer/>


