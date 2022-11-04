<script>
    import { onMount } from "svelte";
    const apiURL = "https://data-pusatprestasinasional.kemdikbud.go.id/api/service";
    let data = [];
    onMount(async function() {
        const response = await fetch(apiURL);
        data = await response.json();        
    });

</script>
<nav class="navbar navbar-expand-lg navbar-custom navbar-dark" id="custom-nav">
	<div class="container">
		<div class="d-flex flex-grow-1">
			<!-- <span class="w-100 d-lg-none d-block">
				 hidden spacer to center brand on mobile 
			</span> -->
			<a class="navbar-brand" href="/">                        
				<img src="/assets/images/logo.svg" alt="" width="220px">
			</a>
			<div class="w-100 text-right">
				<button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#myNavbar7">
					<span class="navbar-toggler-icon"></span>
				</button>
			</div>
		</div>
		<div class="collapse navbar-collapse flex-grow-1 text-right" id="myNavbar7">
			<ul class="navbar-nav ml-auto flex-nowrap">
				<li class="nav-item">
					<a href="/" class="nav-link">Beranda</a>
				</li>
				<li class="nav-item dropdown">
					<a class="nav-link dropdown-toggle" data-toggle="dropdown" href="/" role="button" aria-haspopup="true" aria-expanded="false">Profil</a>
					<div class="dropdown-menu">
					  <a class="dropdown-item" href="/profil/wawasan-umum-dan-misi">Wawasan Umum dan Misi </a>	
					  <a class="dropdown-item" href="/profil/filosofi-organisasi">Filosofi Organisasi </a>
					  <a class="dropdown-item" href="/profil/struktur-organisasi">Struktur Organisasi </a>	
					  <a class="dropdown-item" target="_blank" href="https://data-pusatprestasinasional.kemdikbud.go.id/uploads/dokumen/lakip-puspresnas-2020.pdf">LAKIP</a>				  	  
					  <a class="dropdown-item" target="_blank" href="https://data-pusatprestasinasional.kemdikbud.go.id/uploads/dokumen/renstra-puspresnas-2020.pdf">Rencana Strategis</a>			  	  
					</div>
				</li>
				<li class="nav-item">
					<a href="/#ajang-talenta" class="nav-link">Ajang Talenta</a>
				</li>
				<!-- <li class="nav-item">
					<a href="/#mtn" class="nav-link">MTN</a>
				</li> -->
				<li class="nav-item dropdown">
					<a class="nav-link dropdown-toggle" data-toggle="dropdown" href="/" role="button" aria-haspopup="true" aria-expanded="false">MTN</a>
					<div class="dropdown-menu">
						{#each data as item}       
						<a class="dropdown-item" href="/mtn/{item.slug}">{item.name}</a>                                                                                                                          
                        {/each}					  
					</div>
				</li>				
				<li class="nav-item dropdown">
					<a class="nav-link dropdown-toggle" data-toggle="dropdown" href="/" role="button" aria-haspopup="true" aria-expanded="false">Media</a>
					<div class="dropdown-menu">
						<a class="dropdown-item" href="/wara-wara">Wara - Wara</a>
					  	<a class="dropdown-item" href="/galeri">Galeri</a>
					 	<a class="dropdown-item" href="/video">Video</a>
					  	<a class="dropdown-item" href="/poster">Poster</a>					  
					</div>
				</li>
				<!-- <li class="nav-item">
					<a href="/" class="nav-link">ZIWBK</a>
				</li> -->
				<li class="nav-item">
					<a href="/kontak" class="nav-link">Kontak Kami</a>
				</li>
				
				
			</ul>
		</div>
	</div>
</nav>
