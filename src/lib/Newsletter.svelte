<script>
    import { onMount } from "svelte";
    
    const apiURL = "https://data-pusatprestasinasional.kemdikbud.go.id/api/jenjang";
    let data = [];
    onMount(async function() {
        const response = await fetch(apiURL);
        data = await response.json();
       
    });

    function kirim_newsletter() {
        const value = document.getElementById('level_id').value;
        const email = document.querySelector('input[name="email"]').value;

        let data = new FormData()
        data.append('level_id', value)
        data.append('email', email)

        fetch('https://data-pusatprestasinasional.kemdikbud.go.id/api/subscribe', {
            method: 'POST',
            body: data,
        })

            .then((response) => response.json()).then((result) => {
                if (result == 0) {
                    document.getElementById("hasile").innerHTML = 'Maaf Email Anda Sudah Terdaftar Pada Langganan';
                } else {
                    document.getElementById("hasile").innerHTML = 'Langganan Berhasil';
                }
            })

            .catch(console.error)
            
    }
</script>
<style>
    /* Langganan */
    .langganan {
        background-color: #29ABE2;
        color: #fff;
        border-radius: 16px;
        padding: 40px;
        margin-top: 50px;
    }

    .langganan img {
        position: absolute;
        top: 30px;
        left: -80px;
        width: 280px;
    }

    .langganan .txt-langganan {
        color: #FFFFFF;
        margin-top: 0;
        padding: 18px 40px 12px 137px;
    }
    .langganan h1{
        font-family: 'Myriad Pro Semibold';
    }
    .langganan form {
        padding-left: 137px;
    }

    .langganan form .form-control {
        font-weight: 500 !important;
    }
    /* Extra small devices (portrait phones, less than 576px) */
    @media (max-width: 575.98px) {
        .langganan .txt-langganan {
            padding: 0;
            padding-top: 5%;
        }
        .langganan img {
            top: -60px;
            left: 22%;
            width: 200px;
        }
        .langganan form {
            padding: 0;
        }
    }
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {
        .langganan img {
            top: -60px;
            left: 26%;
            width: 200px;
        }
        .langganan .txt-langganan {
            padding: 0;
            padding-top: 5%;
        }
    }
</style>
<section>
    <div class="container">
        <div class="row">
            <div class="col-md-12 p-4 mx-auto mt-5">
                <div class="langganan">
                    <img src="assets/images/langganan2.svg" alt="">
                    <div class="txt-langganan">
                        <h1>Jangan lewatkan informasi terbaru kami!</h1>                            
                        <p>Dapatkan beragam informasi, pengumuman dan berita terbaru seputar dunia pendidikan dan prestasi nasional langsung melalui email Anda. Berlangganan sekarang!</p> 
                        <p id="hasile"></p>                           
                    </div>
                    <form action="">
                        <div class="form-row">
                            <div class="col">
                                <select id="level_id" name="level_id" class="form-control">
                                    <option>Pilih Jenjang</option>
                                    <option value="">Umum</option>
                                    {#each data as item}
                                        <option value="{item.id}">{item.nama_jenjang}</option>
                                    {/each}
                                </select>
                            </div>
                            <div class="col">
                                <input type="email" name="email" id="email" class="form-control" placeholder="Email">
                            </div>                                
                        </div>
                        <button type="button" on:click={kirim_newsletter} class="btn btn-orange btn-radius float-right">Langganan</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</section>