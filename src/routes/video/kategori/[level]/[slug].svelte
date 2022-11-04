<script context="module">
    import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/video-kategori/${params.slug}`);
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
    import Overlay from '$lib/Overlay.svelte';
    import Row from '$lib/Row.svelte';
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
        axios.get(`https://data-pusatprestasinasional.kemdikbud.go.id/api/video/${post.level.slug}/${post.slug}`, {
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
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.css" />
    <title>Video Sinema | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<section>
    <div class="container py-5 px-5">
        <div class="row">
            <div class="col-md-12">
                <h4 class="title-section ml-0">Sinema Prestasi {post.title} - {post.level.nama_jenjang}</h4>
            </div>
            
        </div>         
        <div class="row"> 
            <div class="col-lg-12">
                {#if loading}
                <Overlay />
                {/if}
                <div class="row" id="data-wrapper">
                    {#each rows as row}
                    <Row {row} />
                    
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