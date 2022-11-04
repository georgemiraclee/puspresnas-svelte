<script>
    import { onMount } from "svelte";
    function createChart(){
        var Result = new Array();
        var Labels = new Array();

        fetch('https://data-pusatprestasinasional.kemdikbud.go.id/api/survey_hasil', {
            method: 'GET',
        })

        .then((response) => response.json()).then((result) => {
            result.forEach(function(datas) {
                Result.push(datas.hehe);
                Labels.push(datas.value);
            });

            var config = {
                type: 'pie',
                data: {
                    datasets: [{
                        data: Result,
                        backgroundColor: [
                            '#eeb76b',
                            '#e2703a',
                            '#9c3d54'
                        ],
                        label: 'Dataset 1'
                    }],
                    labels: Labels
                },
                options: {
                    responsive: true,
                    title: {
                        display: true,
                        text: 'Survey Singkat'
                    }
                }
            };

            var ctx = document.getElementById('voteChart').getContext('2d');
            window.myPie = new Chart(ctx, config);


        var formVote = document.getElementById("formVote");
            var hasilVote = document.getElementById("hasilVote");
            if (formVote.style.display == 'none') {
                formVote.style.display = 'block';
                hasilVote.style.display = 'none';
            } else {
                hasilVote.style.display = 'block';
                formVote.style.display = 'none';
            }
        }
        )
        .catch(console.error)            
    }

    function kirim_survey() {
        const value = document.querySelector('input[name="vote"]:checked').value;
        const masukan = document.querySelector('input[name="masukan"]').value;
        let data = new FormData()
        data.append('kuesioner_id', value)
        data.append('masukan', masukan)

        fetch('https://data-pusatprestasinasional.kemdikbud.go.id/api/survey/store', {
            method: 'POST',
            body: data,
        })

            .then((response) => response.json()).then((result) => {
                if (result == 0) {
                        document.getElementById("hasil-teks").innerHTML = 'Terima Kasih Atas Partisipasi Anda <i class="fas fa-check-circle"></i>';
                    } else {
                        document.getElementById("hasil-teks").innerHTML = 'Terima Kasih Atas Partisipasi Anda <i class="fas fa-check-circle"></i>';
                    }
                    createChart();
                    
            })

            .catch(console.error)
            
    }

    
</script>
<style>
    /* Vote */
    .vote {
        margin-top: 200px;
        background-color: #FFFFFF;
        border: 2px #E78724 solid;
        border-radius: 40px;
        /* height: 420px; */
        padding: 50px 29px;
    }

    .vote img {
        position: absolute;
        top: 8%;
        left: 32%;
        z-index: -1;
        width: 35%;
    }

    .vote h2 {
        font-weight: 500;
        color: #E78724;
    }

    .vote h4 {
        color: rgb(138, 137, 137);
        margin: 24px 0;
    }

    .vote label {
        font-weight: 500;
        color: #E78724
    }

    .vote input[type="radio"] {
        /* remove standard background appearance */
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        /* create custom radiobutton appearance */
        display: inline-block;
        width: 20px;
        height: 20px;
        padding: 6px;
        /* background-color only for content */
        background-clip: content-box;
        border: 1px solid #bbbbbb;
        /* background-color: rgb(138, 137, 137); */
        border-radius: 50%;
    }


    /* appearance for checked radiobutton */

    .vote input[type="radio"]:checked {
        background-color: #E78724;
    }
    .hasil-vote {
        text-align: center;
    }

    .hasil-vote canvas {
        width: 90% !important;
        height: 90% !important;
        margin: auto;
    }

    .hasil-vote h3 {
        color: #535353;
        margin-top: 30px;
    }
    /* Extra small devices (portrait phones, less than 576px) */
    @media (max-width: 575.98px) {
        .vote {
            margin-top: 140px;
        }
    }
    /* Small devices (landscape phones, 576px and up) */
    @media (min-width: 576px) and (max-width: 767.98px) {        
        .vote {
            margin-top: 140px;
        }
    }
    /* Medium devices (tablets, 768px and up) */
    @media (min-width: 768px) and (max-width: 991.98px) {
        .vote {
            margin-top: 140px;
        }
    }
</style>
<section>
    <div class="container">
        <div class="row">
            <div class="col-md-8 mx-auto">
                <div class="vote">
                    <div id="formVote">
                        <img src="assets/images/bg-vote.svg" alt="">
                        <h2>Jajak Pendapat #SobatPrestasi</h2>
                        <h4>Bagaimana menurutmu informasi yang ditampilkan di website ini?</h4>
                       
                            
                            <div class="form-check form-check-inline">
                                <input class="form-check-input" type="radio" name="vote" id="vote1" value="1">
                                <label class="form-check-label" for="vote1">Sangat Bermanfaat</label>
                            </div>
                            <div class="form-check form-check-inline">
                                <input class="form-check-input" type="radio" name="vote" id="vote2" value="2">
                                <label class="form-check-label" for="vote2">Bermanfaat</label>
                            </div>
                            <div class="form-check form-check-inline">
                                <input class="form-check-input" type="radio" name="vote" id="vote3" value="3">
                                <label class="form-check-label" for="vote3">Kurang Bermanfaat</label>
                            </div>
                           
                            <div class="form-group" id="masukan">
                                <label for="masukan">Alasan</label>
                                <input class="form-control" type="text" name="masukan"  placeholder="Tulis alasan disini..."/>
                            </div>
                                                        
                            
                            <div class="form-group">
                                <button on:click={kirim_survey} class="btn btn-orange btn-radius">Kirim</button>                            
                            </div>
                       
                    </div>
                    <div class="hasil-vote" id="hasilVote" style="display: none">
                        <img src="assets/images/bg-vote.svg" alt="">
                        <canvas id="voteChart"></canvas>
                        <h3 id="hasil-teks">Survey</h3>
                    </div>
                </div>                                        
            </div>                
        </div>
    </div>
</section>