<script>
    export let category

</script>
<section id="petualangan" style="margin-top: 100px">
    <div class="container">
        <div class="row">                
            <div class="col-md-6 col-lg-4 mx-auto">
                <h4 class="title-section mx-auto">Kategori Ajang Prestasi</h4>
            </div>                                
        </div>
        <div class="container">
            <div class="row text-center">
        
                <!-- Team item -->
                {#each category as item}
                
                    <div class="col-xl-3 col-sm-6 mb-5">
                        <a href="/event/{item.slug}">
                            <div class="bg-white rounded shadow-sm py-5 px-4"><img src="{item.icon}" alt="" style="object-fit: cover;  height: 100px; width: 100px;" class="img-fluid rounded-circle mb-3 img-thumbnail shadow-sm">
                                <h6 class="mb-0" style="color: #E78724;">{item.title}</h6>
                            </div>
                        </a>
                    </div> 
                                            
                {/each}
                <!-- End -->
        
            </div>
        </div>    
                                
    </div>
</section>