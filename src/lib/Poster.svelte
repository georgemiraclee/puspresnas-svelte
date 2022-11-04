<script>
    export let poster
</script>

<style>
    .wrapper{
        height: 460px;
    }
    .horizontal-scroll {
        width: 100%;
        height: 450px;
        overflow-x: scroll;
        overflow-y: hidden;        
        white-space:nowrap;        
    }
    .horizontal-scroll > .card-p {       
        margin-right: 20px;
        width: 300px;
        height: 100%;
        cursor: pointer;
        display:inline-block;
        *display:inline;
        *zoom:1;
        vertical-align:top;
        text-align: center;
        background-color: transparent;
    }
    
    .card-poster {
        margin-bottom: 40px;
    }

    .card-poster h3 {
        color: #E18A29;
        font-family: 'Myriad Pro Bold';
    }

    .card-poster p {
        color: #696969;
        font-family: 'Myriad Pro Regular';
        margin-bottom: 40px; 
    }

    .card-poster a {
        color: #C8B32D;
    }
    .card-p img{
        width: 100% ;
        margin-bottom: 12px;
    }
    .card-p a{        
        color: rgb(46, 46, 46);
    }
    .card-p a h4{
        font-family: 'Myriad Pro Semibold';        
        margin-top: 12px;
        color: #696969;
        white-space: normal;
    }
    .card-p a p{
        font-family: 'Myriad Pro Light';
        font-size: 14px;
        color: #999999;
    }
    .card-p a:hover{
        text-decoration: none;
        color: #3f3f3f;
    }
    ::-webkit-scrollbar {
        height: 10px;
    }
    
</style>
<section class="overflow-hidden position-relative">
    <div class="container">
        <div class="bg__grub--slider p-3">
            <div class="row pt-5 pb-5 pl-4">
                <div class="col-md-5 col-lg-4 pb-5 text-center text-md-left pb-md-0 my-auto">
                    <div class="card-poster">
                        <h3 class="mb-3">Poster Prestasi</h3>
                        <p>Visualisasi ide dalam bentuk gambar oleh #sobatprestasi</p>
                        <a href="/poster">Lihat lebih banyak</a>
                    </div>
                </div>
                <div class="col-md-7 col-lg-8 my-auto">
                    <div class="wrapper">
                        <div class="horizontal-scroll">
                            {#each poster as item}   
                                <div class="card-p">      
                                    <a href="/poster/{item.slug}">
                                        <img src="{item.image}" alt="">
                                    </a>           
                                    <a href="/poster/{item.slug}">
                                        <h4>{item.title}</h4>
                                        <p>{item.user.name}</p>
                                    </a>    
                                </div>                                
                            {/each}
                        </div>
                    </div>
                    
                </div>
            </div>
        </div>
    </div>
</section>