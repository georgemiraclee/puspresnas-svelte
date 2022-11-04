<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
    import Footer from "$lib/Footer.svelte";
    import PageTransitions from "$lib/PageTransitions.svelte";
</script>
<svelte:head>
    <title>Kontak Kami | Puspresnas</title>
</svelte:head>
<style>
    .card-kontak{
        display: block;
        width: 100%;
    }
    .hero-kontak{
        position: absolute;
        left: 14%;
        width: 147%;
        z-index: 1;
    }    
    .card-kontak {
        /* background-image: url('/assets/images/slider-bg.png'); */
        background-color: #FFFFFF;
        border: solid 2px #E18A29;
        border-radius: 20px;
        height: 250px;
        padding: 5% 10%;
    }
    
    .card-kontak small{
        color: #C6A22F;
        font-weight: bold;        
    }
    .card-kontak a{
        display: block;
        width: fit-content;
        margin-top: 20px;
        border-radius: 10px;
        padding: 10px 40px;
        background-color: #E18A29;
        color: #fff;
        font-weight: bold;
    }
    .card-kontak a:hover{
        text-decoration: none;
        background-color: #d17914;
    }
    .wa {
        display: flex;
        flex-direction: row;
    }
    .wa a{
        margin-top: 20px;
        width: 15%;
        margin: auto;
        font-size: 1.5rem;
        font-weight: bold;
        color: #414141;
    }
    .wa a:hover{
        color: #1EBEA5;
        text-decoration: none;
    }
     /* Extra small devices (portrait phones, less than 576px) */
     @media (max-width: 575.98px) {
        .card-kontak {            
            padding: 24px;            
        }   
        .wa {
            flex-direction: column;
        } 
        .wa a{
            width: 100%;
        }     
    } 
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {     
        .card-kontak {            
            padding: 20px;
        }
        .wa {
            flex-direction: column;
        } 
        .wa a{
            width: 100%;
        } 
    }
    /* Medium devices (tablets, 768px and up) */
    @media (min-width: 768px) and (max-width: 991.98px) {
        .card-kontak {
            padding: 20px;
        }
    }
</style>
<PageTransitions>
    <section>
        <Nav2 />
        <div class="container mt-5">
            <div class="row">
                <div class="col-md-2 d-md-block d-none">
                    <img src="/assets/images/event-hero-default.svg" alt="" class="hero-kontak" />
                </div>
                <div class="col-md-9">                                    
                    <div class="card-kontak">
                        <h3 class="title-orange-bold">Layanan Aspirasi dan Masukan Berharga</h3>
                        <small>Sampaikan aspirasi Anda langsung kepada instansi pemerintah berwenang</small>
                        <a href="https://www.lapor.go.id" target="_blank">LAMAR</a>
                    </div>                                    
                </div>
            </div>
            <div class="row">
                <div class="col-md-4 mt-5">
                    <h3 class="title-orange-bold mt-5">Nomor Kontak</h3>
                </div>
            </div>
<!--             <div class="row">
                <div class="col-md-12">
                    <div class="wa">
                        <a href="https://wa.me/6281230876151" target="_blank"><i class="fab fa-whatsapp"></i> SD</a>
                        <a href="https://wa.me/6281230876151" target="_blank"><i class="fab fa-whatsapp"></i> SMP</a>
                        <a href="https://wa.me/6281230876151" target="_blank"><i class="fab fa-whatsapp"></i> SMA</a>
                        <a href="https://wa.me/6281230876151" target="_blank"><i class="fab fa-whatsapp"></i> SMK</a>
                        <a href="https://wa.me/6281230876151" target="_blank"><i class="fab fa-whatsapp"></i> DIKSUS</a>
                        <a href="https://wa.me/6281230876151" target="_blank"><i class="fab fa-whatsapp"></i> DIKTI</a>
                    </div>
                </div>
            </div> -->
        </div>
    </section>
</PageTransitions>
<Footer/>
