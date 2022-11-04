<script>
    import { onMount } from "svelte";

    const apiURL = "https://data-pusatprestasinasional.kemdikbud.go.id/api/kategori-video";
    let data = [];
    onMount(async function() {
        const response = await fetch(apiURL);
        data = await response.json();
    });

</script>
<style>
    .nav-link {
        color: #E18A29;
    }
    .nav-link[data-toggle].collapsed:after {
        content: " ▾";
    }
    .nav-link[data-toggle]:not(.collapsed):after {
        content: " ▴";
    }
</style>
<div class="col-lg-3 collapse show d-md-flex mb-5" id="sidebar">
    <div class="card rounded rounded-sm w-100">
        <div class="card-header">
            <h5 class="txt-title-orange">Kategori</h5>
        </div>                    
        <ul class="nav flex-column flex-nowrap overflow-hidden">
            <li class="nav-item">
                <a class="nav-link text-truncate" href="/video"><span class="d-none d-sm-inline">Semua Video</span></a>
            </li>
            {#each data as item}
                <li class="nav-item">
                    <a class="nav-link collapsed text-truncate" href="#submenu{item.id}" data-toggle="collapse" data-target="#submenu{item.id}"> {item.nama_jenjang}</a>
                    <div class="collapse" id="submenu{item.id}" aria-expanded="false">
                        <ul class="flex-column pl-2 nav">
                            <li class="nav-item"><a class="nav-link py-0" href="/video/{item.slug}"><span>Semua Kategori</span></a></li>
                            {#each item.video_category as child}
                                <li class="nav-item"><a class="nav-link py-0" href="/video/kategori/{item.slug}/{child.slug}"><span>{child.title}</span></a></li>
                            {/each}
                        </ul>
                    </div>
                </li>
            {/each}

        </ul>
    </div>   
</div>