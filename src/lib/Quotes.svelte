<script>
    export let quotes

</script>
<style>
    section{
        padding-top: 20px;
        padding-bottom: 50px;
    }
    /* Quotes */
    .quotes {
        background-image: linear-gradient(to right, #E78724, #FBC713);
        border-radius: 16px;
        padding: 40px;
        margin-top: 50px;
    }

    .quotes img {
        position: absolute;
        top: 30px;
        left: -80px;
        width: 25%;
    }

    .quotes .txt-quotes {
        text-align: center;
        color: #FFFFFF;
        margin-top: 0;
        padding: 50px 0 0 20px;
    }

    .txt-quotes h3 {
        font-style: italic;
    }
    /* Extra small devices (portrait phones, less than 576px) */
    @media (max-width: 575.98px) {
        .quotes img {
            left: 30%;
            width: 40%;
        }
        .quotes .txt-quotes {
            padding: 0;
        }
        /* .txt-quotes h1 {
            font-size: 4vh;
        } */
    }
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {
        .quotes img {
            left: 30%;
            width: 40%;
        }
    }
</style>
<section>
    <div class="container">
        <div class="row">
            <div class="col-md-12 p-4 mt-5">
                <div class="quotes">
                    <img src="assets/images/qu-pres.svg" alt="">
                    <div class="txt-quotes">
                        <h3>"{quotes.quote}"</h3>
                        <hr class="w-25" style="border-color: #fff;">
                        <h5>{quotes.speaker}</h5>
                        <p>{quotes.occupation}</p>
                    </div>
                    
                </div>
            </div>
        </div>
    </div>
</section>