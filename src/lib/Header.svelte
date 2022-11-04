<script>
    import NavHeader from '$lib/NavHeader.svelte';
    export let slider

</script>
<header class="bg-header">
    <NavHeader/>
    <div class="container">            
        <div class="row">
            <div class="col p-4 mb-5">
                <div id="slider-header" class="carousel slide carousel-fade" data-ride="carousel">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <div class="mask flex-center">
                                <div class="container">
                                    <div class="row align-items-center">
                                        <div class="col-md-6 col-12 order-md-1 order-2 pl-5">                                            
                                            <h3>"Selamat datang para pejuang juara, Petualangan, Talenta, dan Masa Depan Indonesia"</h3>                                               
                                        </div>
                                        <div class="col-md-6 col-12 order-md-2 order-1">
                                            <img src="assets/images/slider.png" alt="slide" style="width: 100%;">
                                        </div>                                            
                                    </div>
                                    
                                </div>
                            </div>
                        </div>
                        {#each slider as item}
                            <div class="carousel-item">
                                <div class="mask flex-center">
                                    <div class="container">
                                        <div class="row align-items-center">
                                            <div class="col-md-6 col-12 order-md-1 order-2 pl-5">
                                                <h4>Pusat Prestasi Nasional</h4>
                                                <h5>Melejitkan Talenta Emas Indonesia</h5>
                                                <h3>"{item.title}"</h3>                                                
                                            </div>
                                            <div class="col-md-6 col-12 order-md-2 order-1">
                                                <img src="{item.image}" alt="slide">
                                            </div>                                            
                                        </div>
                                        
                                    </div>
                                </div>
                            </div>  
                        {/each}                                                                      
                    </div>
                    <ol class="carousel-indicators">
                        <li data-target="#slider-header" data-slide-to="0" class="active"></li>                        
                        {#each slider as item,index}                                                                                                                        
                            <li data-target="#slider-header" data-slide-to={index+1} id={item.id}></li>                            
                        {/each}  
                    </ol>  
                </div>
            </div>
        </div>
    </div>
</header>
