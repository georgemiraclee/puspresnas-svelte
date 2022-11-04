<script>
    import News from '$lib/News.svelte';
    import EventCategory from '$lib/EventCategory.svelte';
    export let journey, category, news, topNews

</script>
<style>
    /* Section Event */

    .bg-orange-grad {
        background-image: url('/assets/images/bg-orange-grad.svg');
        width: 100%;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
    }

    .bg-event {
        /* background-image: url('/assets/images/slider-bg.png'); */
        background-color: #FFFFFF;
        border: solid 2px #E18A29;
        border-radius: 20px;
        height: 250px;
        padding: 0 2%;
    }

    .event-hero {
        position: absolute;
        left: 14%;
        width: 147%;
        z-index: 1;
    }
    .wrapper{
        height: 100%;
    }
    .horizontal-scroll {
        width: 100%;
        height: 100%;
        overflow-x: scroll;
        overflow-y: hidden;        
        white-space:nowrap;        
    }
    .horizontal-scroll > .card-p {  
        margin-top: 10px;     
        margin-right: 20px;
        width: 250px;
        height: 100%;
        cursor: pointer;
        display:inline-block;
        *display:inline;
        *zoom:1;
        vertical-align:top;
        text-align: center;
        background-color: transparent;
    }
    .card-p img{
        display: flex;
        width: 150px;
        height: 150px;
        object-fit: contain;
        margin: 6px auto;
    }
    .card-p a{                
        font-size: 14px;
        font-weight: 500;
        border-radius: 10px;
        color: white;
        padding: 2px 12px;
        background-color: #E78724;        
    }
    ::-webkit-scrollbar {
        height: 10px;
    }    
     /* Extra small devices (portrait phones, less than 576px) */
    @media (max-width: 575.98px) {
        .bg-event {
            background-image: none;
            padding: 10px;
            height: 250px;
        }
        .horizontal-scroll > .card-p {  
            margin-top: 0;   
        }  
    } 
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {     
        .bg-event {
            background-image: none;
            padding: 20px;
        }
    }
    /* Medium devices (tablets, 768px and up) */
    @media (min-width: 768px) and (max-width: 991.98px) {
        .bg-event {
            padding: 0;
        }
    }
</style>

<section id="petualangan" class="bg-orange-grad">
    {#if journey.length > 0}
        <div class="container">
            <div class="row">                
                <div class="col-md-6 col-lg-4 mx-auto">
                    <h4 class="title-section mx-auto">Petualangan Terdekat</h4>
                </div>                                
            </div>
            <div class="row">
                <div class="col-md-2 d-md-block d-none">
                    <img src="assets/images/event-hero-default.svg" class="event-hero" alt="">
                </div>
                <div class="col-md-9">
                    <div class="bg-event">
                        
                        <div class="wrapper">
                            <div class="horizontal-scroll">
                                {#each journey as item}                            
                                    <div class="card-p">                 
                                        <img src="{item.thumbnail}" alt="">
                                        <h6>{item.month.level.nama_jenjang}</h6>
                                        <a href="event/{item.slug}" > Detail</a>    
                                    </div>  
                                {:else}
                                <h4 class="title-section mx-auto">Petualangan Terdekat</h4>
                                {/each}
                            </div>
                        </div>                                                              
                    </div>
                </div>                
            </div>    
                                    
        </div>
    {:else}
    <div class="row">                
        <div class="col-md-6 col-lg-4 mx-auto">
            <h4 class="title-section mx-auto">Tunggu Ajang Prestasi terdekat Kami di {new Date().getFullYear()} ya Sobat</h4>
        </div>                                
    </div>
    {/if}
    <EventCategory {category}/>
    <News {news}{topNews}/>
</section>