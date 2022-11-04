<script>
    import { onMount } from "svelte";

    const apiURL = "https://data-pusatprestasinasional.kemdikbud.go.id/api/galeri";
    let data = [];
    onMount(async function() {
        const response = await fetch(apiURL);
        data = await response.json();
    });

</script>
<style>
    section{
        /* padding-top: 20px; */
        padding-bottom: 50px;
    }
    /* Galeri */

    .gallery-grid {
        background-color: #f3f4f6;
        padding: 2%;
        border-radius: 3%;
    }

    .image {
        opacity: 1;
        display: block;
        width: 100%;
        height: auto;
        transition: .5s ease;
        backface-visibility: hidden;
    }

    .card-album {
        width: 100%;
        height: 100%;
        transition: .5s ease;
        opacity: 0;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        text-align: center;
    }

    .card-album h3 {
        position: absolute;
        top: 40%;
        color: #272727;
        width: 100%;
    }

    .card-album span {
        margin-top: 10px;
    }

    .card-album span {
        display: block;
        width: 100%;
        color: #535353;
    }

    .card-album a {
        position: absolute;
        bottom: 10px;
        left: 38%;
        background-color: #E18A29;
        border-radius: 20px;
        padding: 10px 20px;
        color: #FFF;
    }

    .card-album a:hover {
        background-color: #29ABE2;
        text-decoration: none;
        transition: .5s ease;
    }

    .gallery-grid:hover .image {
        opacity: 0.3;
    }

    .gallery-grid:hover .card-album {
        opacity: 1;
    }
</style>
<section>
    <div class="container">
        <div class="row">
            <div class="col-md-3 mx-auto mt-5">
                <h4 class="title-section mx-auto">Galeri</h4>
            </div> 
        </div>            
        <div class="row">
            {#each data as item}
                <div class="col-md-12 col-lg-4">
                    <div class="gallery-grid">
                        <div class="row">
                            <div class="col">
                                <img src="{item.thumbnail.foto}" class="image img-fluid rounded rounded-lg mb-3" alt="{item.title}">
                            </div>                        
                        </div>
                        <div class="row">
                            {#each item.photo as items}
                                <div class="col">
                                    <img src="{items.foto}" class="image img-fluid rounded rounded-lg" alt="{item.title}">
                                </div>
                            {/each}
                        </div>  
                        <div class="card-album">
                            <h3>{item.title}</h3>
                            <span><i class="fas fa-calendar-alt"></i> {item.tanggal}</span>
                            <a href="/galeri/{item.slug}">Detail</a>
                        </div>                  
                    </div>
                </div>
            {/each}
            
            <div class="col-md-12">
                <a class="btn-orange2 btn-radius float-right" href="/galeri">Lebih Banyak</a>
            </div>              
        </div>
    </div>
</section>