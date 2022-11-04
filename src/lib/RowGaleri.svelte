<script>
    export let row;
</script>
<div class="col-md-4">
    <div class="pb-2">
        <a data-fancybox="video-gallery" href="/galeri/{row.slug}">
            <img src="{row.thumbnail.foto}" alt="{row.title}" class="img-thumbnail" />
        </a>
    </div>
    <span class="badge badge-pill badge-orange text-white">{row.kategori} </span> <br>                   
    <h6 class="mt-2 ml-1 txt-title-black">{row.title}</h6>
    <span class="badge badge-gray"><i class="fas fa-calendar-alt"></i> {row.tanggal}</span>
</div>