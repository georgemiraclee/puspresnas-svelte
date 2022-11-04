<script>
    export let video
</script>
<style>
    section{
        padding-top: 20px;
        padding-bottom: 50px;
    }
    .slider-vid{
        width: 100%;
        display: flex;
        align-items: center;
        align-content: center;
        
    }
    .slider-vid .card-slider{
        width: 30%;
        margin: 10px;
    }
    .card-slider.tengah{
        width: 40%;
    }   
    .link-yt {
        position: relative;
        display: block;
    }

    .icon-play {
        position: absolute;
        top: 35%;
        left: 40%;
        display: block;
        font-size: 85px;
        color: #ffffff;
    }

    .link-yt:hover .icon-play {
        color: #bbbbbb;
    }

    .link-yt img {
        margin: auto;
    }

    .card-slider .caption {
        display: block;
        width: 90%;
        text-align: center;
        margin: auto;
        margin-top: 20px;
        margin-bottom: 20px;
        padding: 12px;
        background-color: #F7FAFC;
        color: #E78724;
        border-radius: 18px;
        font-weight: 500;
        -webkit-box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        -moz-box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
    }
     /* Extra small devices (portrait phones, less than 576px) */
    @media (max-width: 575.98px) {
        .card-slider a {
            padding: 20px;
        }        
    }
    @media (max-width: 767.98px) {
        .slider-vid{
            flex-direction: column;
        }
        .slider-vid .card-slider{
            width: 100%;
            margin: 10px;
        }
        .card-slider.tengah{
            width: 100%;
        }
    }
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {
        .card-slider a {
            padding: 20px;
        }        
    }
</style>
<section id="sinema">
    <div class="container">
        <div class="row">
            <div class="col-md-4 mx-auto mt-5">
                <h4 class="title-section mx-auto">Sinema Prestasi</h4>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <div class="slider-vid">
                    {#each video as item, index}
                        {#if index==1}
                            <div class="card-slider tengah">                                                      
                                <a href="/video/{item.slug}" class="link-yt">
                                    <img src="{item.thumbnail}" class="img-fluid" alt=""> 
                                    <i class="far fa-play-circle icon-play"></i>
                                </a>                           
                                <a href="/video/{item.slug}" class="caption">{item.title}</a>
                            </div>
                        {:else}
                            <div class="card-slider">                                                      
                                <a href="/video/{item.slug}" class="link-yt">
                                    <img src="{item.thumbnail}" class="img-fluid" alt=""> 
                                    <i class="far fa-play-circle icon-play"></i>
                                </a>                           
                                <a href="/video/{item.slug}" class="caption">{item.title}</a>
                            </div>
                        {/if}
                    {/each}
                     
                </div>
            </div>
        </div>	
        <div class="row">
            <div class="col-md-12">
                <a class="btn-orange2 btn-radius float-right" href="/video">Lebih Banyak</a>
            </div>
        </div>
    </div>
</section>