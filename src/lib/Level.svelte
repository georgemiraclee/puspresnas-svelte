<script>
    export let jenjang

</script>
<style>
    section{
        /* padding-top: 10px; */
        padding-bottom: 50px;
    }
</style>
<section id="ajang-talenta" class="bg-blue-grad">
    <div class="container">
        <div class="row">                
            <div class="col-md-5 col-lg-4 mx-auto">
                <h4 class="title-section mx-auto">Ajang Talenta</h4>
            </div>                                
        </div>
        <div class="row">
            {#each jenjang as item}
                <div class="col-lg-2 col-md-4 col-sm-6 ">
                    <a style="background-color: {item.color}" class="menu-jenjang" href="jenjang/{item.slug}">
                        <img src="{item.icon}" alt="">                        
                        <h3>{item.nama_jenjang}</h3>
                    </a>
                </div>
            {/each}      
        </div>
    </div>
</section>