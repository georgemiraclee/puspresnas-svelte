<script>
    import TopNews from '$lib/TopNews.svelte';
    export let news, topNews

</script>
<style>
    section{
        padding-top: 100px;
        padding-bottom: 100px;
    }
    /* Section Berita */
    .berita-terbaru {
        background-color: #fff;
        padding: 18px;
        border-radius: 20px;
    }    
    .berita-terbaru img{
        width: 100%;
        height: 250px;
        object-fit: cover;
    }
    .berita-terbaru p{
        font-family: 'Myriad Pro Reguler';
        color: rgb(115 115 115);
    }
    .img-hover-zoom:hover img {
        transform: scale(1.05);
    }
        
</style>
<section>
    <div class="container">
        <div class="row">                
            <div class="col-md-5 col-lg-4 mx-auto mt-5">
                <h4 class="title-section">Wara - Wara Prestasi</h4>
            </div>                                
        </div>
        <div class="row">
            <div class="col-md-7 ">
                <div class="berita-terbaru">
                    <div class="img-hover-zoom">
                        <a href="/wara-wara/{news.slug}"><img src="{news.thumbnail}" alt="" class="align-self-center rounded mb-3" width="100%"></a>
                    </div>
                    <span class="badge badge-pill badge-orange text-white">{news.kategori}</span> <br>                   
                    <h3 class="mt-2 txt-title-black">{news.title}</h3>
                    <span class="badge badge-gray p-0"><i class="fas fa-calendar-day"></i> {news.tanggal} &nbsp;</span><span class="badge badge-gray p-0"> | <i class="fas fa-eye"></i> {news.viewers}</span>
                    <p style="word-wrap: break-word;" class="text-justify mt-3">{news.sub}</p>
                    <a href="/wara-wara/{news.slug}" class="btn btn-orange btn-radius">Selengkapnya <i class="fas fa-chevron-right"></i></a>
                </div>                    
            </div>
            <TopNews {topNews}/>
        </div>
        <div class="row">
            <div class="col-md-4 text-center mx-auto mt-5">
                <a href="/wara-wara" class="btn btn-orange2 btn-radius">Berita Lainya <i class="fas fa-chevron-right"></i></a>
            </div>
        </div>
    </div>
</section>