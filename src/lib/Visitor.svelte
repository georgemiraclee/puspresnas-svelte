<script>
    export let visitor
</script>
<style>
    /* Counter Pengunjung */
    .pengunjung {
        display: flex;
        width: 80%;
        margin: auto;
    }

    .pengunjung h1 {
        color: #29ABE2;
    }

    .pengunjung p {
        color: #E18A29;
        padding: 4px 80px 4px 10px;
        font-size: 13px;
        font-weight: 500;
    }    
    /* Extra small devices (portrait phones, less than 576px) */
    @media (max-width: 575.98px) {
        .pengunjung {
            width: fit-content;
        }        
        .pengunjung{
            flex-direction: column;
        }
        .pengunjung p{
            padding: 0;
        }
    }
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {
        .pengunjung {
            width: fit-content;
        }        
    }
    /* Medium devices (tablets, 768px and up) */
    @media (min-width: 768px) and (max-width: 991.98px) {
        .pengunjung {
            width: fit-content;
        }
    }
</style>
<section>
    <div class="container">
        <div class="row mt-5">
            <div class="col-4 col-md-3 mx-auto">
                <div class="pengunjung">
                    <h1>{visitor.hari}</h1>
                    <p>Pengunjung hari ini</p>
                </div>                    
            </div>
            <div class="col-4 col-md-3 mx-auto">
                <div class="pengunjung">
                    <h1>{visitor.minggu}</h1>
                    <p>Pengunjung minggu ini</p>
                </div> 
            </div>
            <div class="col-4 col-md-3 mx-auto">
                <div class="pengunjung">
                    <h1>{visitor.bulan}</h1>
                    <p>Pengunjung bulan ini</p>
                </div> 
            </div>
        </div>
    </div>
</section>
{#if visitor.bulan==undefined}
    <div class="loading-bar">
        <div>            
            <img src="assets/images/logo.png" class="puspresnas"alt="">
            <p>Loading..</p>
            <img class="loading" src="loading-bar.svg" alt="">
        </div>        
    </div>
{/if}
