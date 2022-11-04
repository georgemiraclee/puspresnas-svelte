<script>
    export let row;
</script>
<div class="col-md-4">
    <div class="card-p">
        <a href="/poster/{row.slug}"><img style="width: 100%; margin-bottom: 12px;" src="{row.image}" alt=""></a>
        <a style="color: rgb(46, 46, 46);" href="/poster/{row.slug}">
            <h4>{row.title}</h4>
            <p>{row.user.name}</p>
        </a>    
    </div>
</div>