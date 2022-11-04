<script>
    export let topNews
</script>
<style>
    .img-hover-zoom{
        width: 40%;
        margin-right: 30px;
    }
    .img-hover-zoom img{
        width: 100%;
    }
    .img-hover-zoom:hover img {
        transform: scale(1.2);
    }
</style>
<div class="col-md-5 mx-auto">
    <ul class="list-unstyled">
        {#each topNews as item, i}
            {#if i=0}
                <li class="media">
                    <div class="img-hover-zoom">
                        <a href="/wara-wara/{item.slug}" ><img style="object-fit: cover; height: 100px" src="{item.thumbnail}" class="align-self-center rounded mr-3 bg-light" alt=""></a>
                    </div>
                    <div class="media-body">
                            <span class="badge badge-pill badge-orange text-white">{item.kategori}</span>
                            <h6 class="mb-1"><a href="/wara-wara/{item.slug}" class="text-dark">{item.title}</a></h6>                              
                    </div>
                </li>
            {/if}
            <li class="media mt-3">
                <div class="img-hover-zoom">
                    <a href="/wara-wara/{item.slug}" ><img style="object-fit: cover; height: 100px" src="{item.thumbnail}" class="align-self-center rounded mr-3 bg-light" alt="" ></a>
                </div>
                <div class="media-body">
                    <span class="badge badge-pill badge-orange text-white">{item.kategori}</span>
                    <h6 class="mb-1"><a href="/wara-wara/{item.slug}" class="text-dark">{item.title}</a></h6>                              
                </div>
            </li>
        {/each}                
    </ul>                    
</div>