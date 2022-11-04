<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";
	import Footer from "$lib/Footer.svelte";

    export function load({ error, status }) {
        return {
            props: {
                message: error.message,
                status // same as status: status
            }
        };
    }
</script>
<script>
  
    export let message;
    export let status;
  </script>
<svelte:head>	
	<title>Maaf.. {status} {message}</title>	
    <!-- <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" on:load={initializeRemarkable}></script>		 -->
</svelte:head>
<Nav2/>
<PageTransitions>
<div class="container mt-5 mb-2 ">
    <div class="row">
        <div class="col-md-4 mx-auto mt-5">
            <h4 class="title-section">{status} {message}</h4>                    
        </div>
    </div>
    <div class="row">
        <div class="col-md-4 text-center mx-auto mt-5">
            <a href="/" class="btn btn-orange2 btn-radius">Kembali ke Beranda</a>
        </div>
    </div>
</div>
</PageTransitions>
<Footer/>
