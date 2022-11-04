<script>
    export let row;
</script>
<div class="col-md-12">                                        
    <a href="/pengumuman/{row.slug}" class="pengumuman-card">                                                                                                                            
        <div>
            <strong>{@html row.created_at}</strong>
            
        </div>                                                                                                
        <h5>{row.title}</h5>                             
    </a>                    
</div>