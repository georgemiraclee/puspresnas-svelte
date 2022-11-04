<script>
    export let row;
</script>
<div class="col-md-12">
    <div class="card mb-3 border-0">
        <div class="row no-gutters">
            <div class="col-md-4">
            <a href="/wara-wara/{row.slug}">
                <img style="object-fit: cover; height: 200px" src="{row.thumbnail}" class="img-hover-zoom rounded rounded-lg" alt="..." width="100%">
            </a>
            </div>
            <div class="col-md-8">
                <div class="card-body pt-0">     
                    <a href="/wara-wara/{row.slug}">                       
                        <h5 class="card-title">{row.title}</h5>
                    </a>
                    <span class="badge badge-pill badge-orange text-white">{row.kategori}</span>
                    <span class="txt-span">| {row.tanggal}</span><span class="txt-span"> | {row.viewers}x dikunjungi</span>
                    
                    <p style="margin-top: 10px" class="card-text txt-p text-justify">{row.sub}
                        <a href="/wara-wara/{row.slug}" class="txt-orange"> Selengkapnya..</a>
                    </p>
                    <p class="card-text"><small class="text-muted">{row.time}</small></p>                                                                
                </div>
            </div>
        </div>                        
    </div> 
</div>
