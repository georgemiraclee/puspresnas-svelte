<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import Footer from "$lib/Footer.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	
    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/event-kategori/${params.slug}`);
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
	.card-img-top{
		padding: 10px;
		box-shadow: 1px;
		height: 180px;
		object-fit: contain;
	}   
	.card-body h5{
		font-family: 'Myriad Pro Semibold';
	}
	
</style>
<svelte:head>	
	<title>Ajang Talenta | Puspresnas</title>	
</svelte:head>
<Nav2/>
<!-- Lomba Jenjang SMA -->
<PageTransitions>
<section>
    <div class="container">
        <div class="row">
            <div class="col-md-4 mx-auto mt-5">
                <h4 class="title-section">Ajang Prestasi {post.title}</h4>                    
            </div>
        </div>
        <div class="justify-content-md-center">
			<div class="row">
                {#each post.event as ev}
							
                    <div class="col-md-3 mb-5">
                        <div class="card border-0">                        
                            <img class="card-img-top shadow-sm p-4 bg-white rounded rounded-lg" src="{ev.thumbnail}" alt="{ev.nama_event}">                        
                            <div class="card-body mt-3 p-0" >
                                
                                <a href="/event/{ev.slug}" class="card-title link-orange"><h5>{ev.nama_event}</h5></a>
                                <span class="badge badge-pill badge-orange text-white">{ev.month.level.nama_jenjang}</span>
                                <br>
                                <span class="badge badge-gray p-0"><i class="fas fa-calendar-day"></i> {ev.tanggal}</span>
                                <br>                          
                                <span class="badge badge-gray p-0"><i class="fas fa-flag"></i> {ev.level.title}</span>       
                                <br>                                               
                                <a href="{ev.link}" class="link-unduh mt-3" target="_blank">Laman</a>
                                <a href="/event/{ev.slug}" class="link-unduh mt-3">Detail</a>
                            </div>
                        </div>
                    </div>
            
                {/each}    
			</div>                   
        </div>            
    </div>
</section>
</PageTransitions>
<Footer/>


