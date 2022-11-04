<script>
    export let kabar
</script>

<section>
    <div class="container">
        <div class="row">
            <div class="col-md-5 col-lg-3 mx-auto mt-5">
                <h4 class="title-section">Kabar Prestasi</h4>
            </div>
        </div>
        <div class="row">
            {#each kabar as item}
                <div class="col-md-12 col-lg-6">                                        
                    <a href="pengumuman/{item.slug}" class="pengumuman-card">        
                        <div>
                            <strong>{@html item.created_at}</strong>
                            
                        </div>                                                                                                
                        <h4>{item.sub}</h4>                            
                    </a>                    
                </div>
            {/each}
        </div>
        <div class="row">
            <div class="col-md-4 text-center mx-auto mt-3 mb-5">
                <a href="/pengumuman" class="btn btn-orange2 btn-radius">Pengumuman Lainya <i class="fas fa-chevron-right"></i></a>
            </div>
        </div>
    </div>
</section>