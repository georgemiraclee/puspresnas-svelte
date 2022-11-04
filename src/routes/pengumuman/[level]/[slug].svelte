<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte"
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/pengumuman/${params.level}/${params.slug}`);
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
<svelte:head>
    <title>Kabar Prestasi | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<div class="container mt-5 mb-2">
	<div class="row">
        <div class="col-md-6 mx-auto">
            <nav aria-label="breadcrumb" class="">
                <ol class="breadcrumb bg-transparent txt-link-orange2 p-0">
                  <li class="breadcrumb-item "><a href="/">Beranda</a></li>
                  <li class="breadcrumb-item"><a href="/pengumuman">Pengumuman</a></li>
                  <li class="breadcrumb-item active" aria-current="page">Detail</li>
                </ol>
              </nav>
        </div>
    </div>
    <div class="row">
        <div class="col-md-6 mx-auto ">
            <h4 class="title-orange-bold">{post.title}</h4>
            <span class="badge badge-pill badge-orange text-white">Jenjang {post.user.level.nama_jenjang}</span>
            <span class="txt-span"> | &nbsp;<i class="fas fa-calendar-day"></i> {post.tanggal}</span>
            
            <p class="txt-p text-justify mt-3">{@html post.detail}</p>
            <br>
            <h6 class="title-orange-bold">Berkas Tambahan</h6>
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
