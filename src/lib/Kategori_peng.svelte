<script>
    import { onMount } from "svelte";

    const apiURL = "https://data-pusatprestasinasional.kemdikbud.go.id/api/jenjang";
    let data = [];
    onMount(async function() {
        const response = await fetch(apiURL);
        data = await response.json();
    });

</script>
<div class="col-md-12 col-lg-3 mb-5">
    <div class="card rounded rounded-sm">
        <div class="card-header">
          <h5 class="txt-title-orange">Kategori</h5>
        </div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item"><a href="/pengumuman" class="txt-orange">Umum</a></li>
          {#each data as item}
            <li class="list-group-item"><a href="/pengumuman/{item.slug}" class="txt-orange">{item.nama_jenjang}</a></li>
          {/each}                       
        </ul>
    </div>
</div>