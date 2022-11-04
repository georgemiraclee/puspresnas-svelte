<script>
    export let service

</script>
<style>
    section{
        padding: 0;
    }
    .wrapper{
        height: 300px;
        
    }
    .horizontal-scroll {
        width: 100%;
        padding-bottom: 24px;
        overflow-x: auto;
        overflow-y: hidden;        
        white-space:nowrap;    
        
    }
    .horizontal-scroll  .card {  
        padding-top: 15px; 
        padding-left: 60px;   
        padding-right: 24px;                
        width: 300px;
        height: 100%;
        cursor: pointer;
        display:inline-block;
        *display:inline;
        *zoom:1;
        vertical-align:top;        
        border-radius: 1.25rem;
        background-color: #29ABE2;
        border: none;
        margin-left: 60px;
        height: 200px;
        white-space: normal;
        color: #fff;
    }
    .card h3{
        font-family: 'Myriad Pro Bold';
    }
    .card p{        
        font-family: 'Myriad Pro Light';
    }
    .icon-layanan {
        position: absolute;
        top: 25%;
        left: -15%;
        width: 35%;
        z-index: 0;
    }
    .card-link {
        display: block;
        width: fit-content;
        font-size: 14px;
        font-family: 'Myriad Pro Semibold';
        margin-top: auto;
        margin-bottom: 0;
        border-radius: 10px;
        color: white;
        padding: 2px 12px;
        background-color: #E78724;
        position: absolute;
        bottom: 10px;
    }
    ::-webkit-scrollbar {
        height: 10px;
    }
</style>
<section id="mtn">
    <div class="container">
        <div class="row pt-5">                
            <div class="col-md-6 col-lg-5 mx-auto">
                <h4 class="title-section mx-auto">Manajemen Talenta Nasional</h4>
            </div>                                
        </div>
        <div class="row">
            <div class="col-md-12">
                <div class="wrapper">
                    <div class="horizontal-scroll">    
                        {#each service as item}                                            
                        <div class="card shadow-sm">
                            <img class="icon-layanan" src="{item.icon}" alt="{service.name}"/>
                            <h3>{item.name}</h3>
                            <p>{item.detail_singkat}</p>
                            <a href="/mtn/{item.slug}" class="card-link">Kunjungi</a>                                                                               
                        </div>                                                                                          
                        {/each}                             
                    </div>  
                </div> 
            </div>
                                     
        </div>
    </div>
</section>