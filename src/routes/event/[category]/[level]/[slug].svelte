<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";
    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/event/${params.category}/${params.level}/${params.slug}`);
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
    .img-event{
        width: 300px;
        height: 300px;
        object-fit: contain;
        margin-top: 30px;
    }
</style>
<svelte:head>
    <title>{post.nama_event} | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<div class="container mt-5 mb-2">
	<div class="row">
        <div class="col-md-6 mx-auto">
            <nav aria-label="breadcrumb" class="">
                <ol class="breadcrumb bg-transparent txt-link-orange2 p-0">
                  <li class="breadcrumb-item "><a href="/">Beranda</a></li>
                  <li class="breadcrumb-item"><a href="/event">Event</a></li>
                  <li class="breadcrumb-item active" aria-current="page">Detail</li>
                </ol>
              </nav>
        </div>
    </div>
    <div class="row">
        <div class="col-md-6 mx-auto ">
            <h4 class="title-orange-bold">{post.nama_event}</h4>
            <span class="badge badge-pill badge-orange text-white">{post.month.level.nama_jenjang} | {post.category.title}</span>
            <span class="txt-span"> | &nbsp;<i class="fas fa-calendar-day"></i> {post.tanggal}</span>
            <br>
            <img src="{post.thumbnail}" class="img-event" alt="{post.nama_event}" />
            
            <p class="txt-p text-justify mt-3">{@html post.detail}</p>
            <br>
            <h6 class="title-orange-bold">Lampiran</h6>
            <a href="{post.link}" style="margin-right: 5px;" class="btn btn-orange3 btn-radius">Portal {post.nama_singkat}</a>
            {#each post.attachment as item}
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
