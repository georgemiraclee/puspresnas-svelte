<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let article;

        try {
        // here we are gonna fetch the single article by id
            article = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/mtn/${params.slug}`);
            article = await article.json();
        } catch (e) {
            console.log(e);
        }
        return {
            props: {
                article
            }
        };
    }
</script>
<script>
	export let article;
</script>
<style>
    .bg-berita{
        position: relative;
        top: -150px;
        background-color: #fff;            
    }    
    .paragrap{
        margin-top: 60px;
    }
</style>
<svelte:head>	
	<title>MTN | Pusat Prestasi Nasional</title>	
    <!-- <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" on:load={initializeRemarkable}></script>		 -->
</svelte:head>
<Nav2/>
<PageTransitions>
<div class="container mt-5 mb-2 ">
    <div class="row">
        <div class="col">
            <nav aria-label="breadcrumb" class="">
                <ol class="breadcrumb bg-transparent txt-link-orange2">
                  <li class="breadcrumb-item "><a href="/">Beranda</a></li>
                  <li class="breadcrumb-item"><a href="#">MTN</a></li>
                  <li class="breadcrumb-item active" aria-current="page">Detail</li>
                </ol>
              </nav>
        </div>
    </div>
    <div class="row">
        <div class="col-md-12">
            <img class="img-fluid rounded rounded-sm" style="width: 100%; object-fit: contain; height: 850px" src="{article.thumbnail}" alt="">
        </div>
    </div>
    <div class="row">
        <div class="col-md-10 mx-auto p-5 rounded-sm bg-berita">
            <h4 class="title-orange-bold mb-3">{article.name}</h4>
            
            <p class="txt-p text-justify paragrap">{@html article.description}</p>
            <br>
            <h6 class="title-orange-bold">Lampiran</h6>
            {#each article.attachment as item}
                {#if item.type == 0}
                    <a href="{item.berkas}" target="_blank" style="margin-right: 5px;" class="btn btn-orange3 btn-radius">{item.judul}</a>
                {:else if item.type == 1}
                    <a href="{item.url}" target="_blank" style="margin-right: 5px;" class="btn btn-orange3 btn-radius">{item.judul}</a>
                {/if}
            {/each}
        </div>
    </div>
</div>
</PageTransitions>
<Footer/>
