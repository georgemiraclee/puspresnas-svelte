<script>
    export let row;
  </script>
  
  <div class="col-md-4 mb-5">
    <div class="pb-2">
        <a data-fancybox="video-gallery" href="/video/{row.slug}">
            <img src="{row.thumbnail}" alt="{row.title}" class="img-thumbnail" />
        </a>
    </div>
    <span class="badge badge-pill badge-orange text-white">{row.kategori}</span> <br>                   
    <h6 class="mt-2 txt-title-black">{row.title}</h6>
</div>