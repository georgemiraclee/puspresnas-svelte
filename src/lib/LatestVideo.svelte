<script>
    export let latestVideo

</script>
<style>
    .videoterkini{
        background-color: #EAF5FB;
    }
    .videoterkini .title{
        color: #E18A29;
        font-family: 'Myriad Pro Semibold';
    }
</style>
<section class="videoterkini">
    <div class="container">
        <div class="row">
            <div class="col-md-4 mx-auto mt-5">
                <h4 class="title-section mx-auto">Video Terkini</h4>
            </div>
        </div>
        <div class="row pb-5">
            <div class="col-md-6 mb-5">
                <div class="embed-responsive embed-responsive-16by9">
                    <iframe class="embed-responsive-item" src="https://youtube.com/embed/{latestVideo.link}" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                </div>                
            </div>
            <div class="col-md-6 pl-5 mb-5">
                <h4 class="title">{latestVideo.title} </h4>
                <p class="txt-p">{latestVideo.description}</p>
            </div>
        </div>
    </div>
</section>