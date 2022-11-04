<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/news/${params.level}/${params.slug}`);
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
	export let post;
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
	<title>Detail Wara - Wara | Puspresnas</title>	
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
                  <li class="breadcrumb-item"><a href="/wara-wara">Wara - Wara</a></li>
                  <li class="breadcrumb-item active" aria-current="page">Detail</li>
                </ol>
              </nav>
        </div>
    </div>
    <div class="row">
        <div class="col-md-12">
            <img class="img-fluid rounded rounded-sm" style="width: 100%; object-fit: contain; height: 850px" src="{post.thumbnail}" alt="">
        </div>
    </div>
    <div class="row">
        <div class="col-md-10 mx-auto p-5 rounded-sm bg-berita">
            <h4 class="title-orange-bold mb-3">{post.title}</h4>
            <span class="badge badge-pill badge-orange text-white">{post.kategori}</span>
            <span class="txt-span"> &nbsp; <i class="fas fa-calendar-day"></i> {post.tanggal}</span><span class="txt-span">  &nbsp;  <i class="fas fa-eye"></i>  {post.viewers}</span>
            
            <p class="txt-p text-justify paragrap">{@html post.detail}</p>
            
        </div>
    </div>
    <div class="row mx-auto">
        <div class="col-md-10 ">
            <h4 class="title-orange-bold">Berita Lainnya</h4>
            <hr class="float-left">
        </div>
    </div>
    <div class="row mx-auto mb-5">
        {#each post.user.news as item}
        <div class="col-md-6 col-lg-4 mb-3">
            <a  href="/wara-wara/{item.slug}"><img src="{item.thumbnail}" alt="{item.title}" style=" width: 100%;height: 200px; object-fit: cover;" class="img-fluid rounded-lg"></a>
            <h6 class="mt-3"><a href="/wara-wara/{item.slug}" class="title-black">{item.title}</a></h6>
        </div>
        {/each}    
    </div>
</div>
</PageTransitions>
<Footer/>
