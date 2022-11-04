<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/galeri/${params.level}/${params.slug}`);
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
	.breadcrumb-item a{
		color: #D78428;
		margin: 0;
		padding: 0;
		font-family: 'Myriad Pro Semibold';
	}
	/* Style to change separator  */
    .breadcrumb-item + .breadcrumb-item::before {
        content: ">";
		font-family: 'Myriad Pro Semibold';
    }
</style>
<svelte:head>
    <title>Detail Galeri | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<section>
    <div style="margin-top: 20px" class="container">
		<div class="row">
			<div class="col-md-10 mx-auto">
                <nav aria-label="breadcrumb" class="">
                    <ol class="breadcrumb bg-transparent txt-link-orange2 p-0">
                      <li class="breadcrumb-item "><a href="/">Beranda</a></li>
                      <li class="breadcrumb-item"><a href="/galeri">Galeri</a></li>
                      <li class="breadcrumb-item active" aria-current="page">Detail Galeri </li>
                    </ol>
                </nav>
            </div>
			<div class="col-md-10 mx-auto">
                <h4 class="title-orange-bold mb-3">{post.title}</h4>
                <span class="badge badge-pill badge-orange text-white">{post.kategori}</span>
                <span class="txt-span">| <i class="fas fa-calendar-alt"></i> {post.tanggal}</span>				
				<div class="row mt-2" >
					{#each post.photo as item}
						<div class="col-md-4">
							<div class="pb-2">
								<a target="_blank" data-fancybox="video-gallery" href="{item.foto}">
									<img src="{item.foto}" alt="{item.id}" class="img-thumbnail" />
								</a>
							</div>                
							
						</div>
					{/each}
				</div>
							
		</div>
	</div>
</section>
</PageTransitions>
<Footer/>
