<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/video/${params.level}/${params.category}/${params.slug}`);
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
    <title>Video Sinema | Puspresnas</title>
</svelte:head>
<Nav2/>
<PageTransitions>
<section>
    <div style="margin-top: 20px" class="container">
		<div>
			<h4 class="title-orange-bold">{post.title}</h4>
			<span class="badge badge-pill badge-orange text-white">{post.kategori}</span> <span class="badge badge-pill badge-orange text-white">{post.category.title}</span>
			<div style="margin-top: 20px" class="embed-responsive embed-responsive-16by9">
				<iframe style="width: 100%" class="embed-responsive-item" src="https://youtube.com/embed/{post.link}" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
			</div>
			
		</div>
	</div>
</section>
</PageTransitions>
<Footer/>