<script context="module">
	import Nav2 from "$lib/Nav2.svelte";
	import Footer from "$lib/Footer.svelte";
	import PageTransitions from "$lib/PageTransitions.svelte";


    export async function load({ fetch, params }) {
        let post;

        try {
        // here we are gonna fetch the single article by id
            post = await fetch(`https://data-pusatprestasinasional.kemdikbud.go.id/api/level/${params.slug}`);
            post = await post.json();
        } catch (e) {
            console.log(e);
        }
        return {
            props: {
                post
            }
        };
    }
</script>
<script>
	export let post;
	const initializeRemarkable = () => {
		(function() {
			// VARIABLES
			const timeline = document.querySelector(".timeline ol"),
				elH = document.querySelectorAll(".timeline li > div"),
				arrows = document.querySelectorAll(".timeline .arrows .arrow"),
				arrowPrev = document.querySelector(".timeline .arrows .arrow__prev"),
				arrowNext = document.querySelector(".timeline .arrows .arrow__next"),
				firstItem = document.querySelector(".timeline li:first-child"),
				lastItem = document.querySelector(".timeline li:last-child"),
				xScrolling = 280,
				disabledClass = "disabled";

			// START
			init();

			function init() {
				setEqualHeights(elH);
				animateTl(xScrolling, arrows, timeline);
				setSwipeFn(timeline, arrowPrev, arrowNext);
				setKeyboardFn(arrowPrev, arrowNext);
			}

			// SET EQUAL HEIGHTS
			function setEqualHeights(el) {
				let counter = 0;
				for (let i = 0; i < el.length; i++) {
					const singleHeight = el[i].offsetHeight;

					if (counter < singleHeight) {
						counter = singleHeight;
					}
				}

				for (let i = 0; i < el.length; i++) {
					el[i].style.height = `${counter}px`;
				}
			}

			// CHECK IF AN ELEMENT IS IN VIEWPORT
			// http://stackoverflow.com/questions/123999/how-to-tell-if-a-dom-element-is-visible-in-the-current-viewport
			function isElementInViewport(el) {
				const rect = el.getBoundingClientRect();
				return (
					rect.top >= 0 &&
					rect.left >= 0 &&
					rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
					rect.right <= (window.innerWidth || document.documentElement.clientWidth)
				);
			}

			// SET STATE OF PREV/NEXT ARROWS
			function setBtnState(el, flag = true) {
				if (flag) {
					el.classList.add(disabledClass);
				} else {
					if (el.classList.contains(disabledClass)) {
						el.classList.remove(disabledClass);
					}
					el.disabled = false;
				}
			}

			// ANIMATE TIMELINE
			function animateTl(scrolling, el, tl) {
				let counter = 0;
				for (let i = 0; i < el.length; i++) {
					el[i].addEventListener("click", function() {
						if (!arrowPrev.disabled) {
							arrowPrev.disabled = true;
						}
						if (!arrowNext.disabled) {
							arrowNext.disabled = true;
						}
						const sign = (this.classList.contains("arrow__prev")) ? "" : "-";
						if (counter === 0) {
							tl.style.transform = `translateX(-${scrolling}px)`;
						} else {
							const tlStyle = getComputedStyle(tl);
							// add more browser prefixes if needed here
							const tlTransform = tlStyle.getPropertyValue("-webkit-transform") || tlStyle.getPropertyValue("transform");
							const values = parseInt(tlTransform.split(",")[4]) + parseInt(`${sign}${scrolling}`);
							tl.style.transform = `translateX(${values}px)`;
						}

						setTimeout(() => {
							isElementInViewport(firstItem) ? setBtnState(arrowPrev) : setBtnState(arrowPrev, false);
							isElementInViewport(lastItem) ? setBtnState(arrowNext) : setBtnState(arrowNext, false);
						}, 1100);

						counter++;
					});
				}
			}

			// ADD SWIPE SUPPORT FOR TOUCH DEVICES
			function setSwipeFn(tl, prev, next) {
				const hammer = new Hammer(tl);
				hammer.on("swipeleft", () => next.click());
				hammer.on("swiperight", () => prev.click());
			}

			// ADD BASIC KEYBOARD FUNCTIONALITY
			function setKeyboardFn(prev, next) {
				document.addEventListener("keydown", (e) => {
					if ((e.which === 37) || (e.which === 39)) {
						const timelineOfTop = timeline.offsetTop;
						const y = window.pageYOffset;
						if (timelineOfTop !== y) {
							window.scrollTo(0, timelineOfTop);
						}
						if (e.which === 37) {
							prev.click();
						} else if (e.which === 39) {
							next.click();
						}
					}
				});
			}
		})();
	}
	
</script>

<style>
	.panel-pengumuman { 
		margin:4px, 4px; 
		padding:4px;                 
		height: 500px; 
		width: 100%;
		overflow-x: hidden; 
		overflow-y: auto; 
		text-align:justify; 
	}

	/*
	*  style scroll
	*/
	#style-2::-webkit-scrollbar-track {
		box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
		border-radius: 10px;
		background-color: #F5F5F5;
	}

	#style-2::-webkit-scrollbar {
		width: 8px;
		background-color: #F5F5F5;
	}

	#style-2::-webkit-scrollbar-thumb {
		border-radius: 10px;
		box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
		background-color: #E78724;
	}
	.card-img-top{
		padding: 10px;
		box-shadow: 1px;
		height: 180px;
		object-fit: contain;
	}   
	.btn-timeline {
		background: transparent;
		border: none;
		cursor: pointer;
		outline: none;
	}
	.media {
        background-color: #fff;
        min-height: 140px;
        padding: 14px;
        border-radius: 20px;
    }
	.media-body h6{
		color: #464646;
		margin: 15px 0;
	}
	.pengumuman-card {
		padding: 1% !important;
	}	
	.card-body h5{
		font-family: 'Myriad Pro Semibold';
	}
	
</style>
<svelte:head>	
	<title>Ajang Talenta | Puspresnas</title>	
	<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" on:load={initializeRemarkable}></script>		
</svelte:head>
<Nav2/>
<!-- Lomba Jenjang SMA -->
<PageTransitions>
<section>
    <div class="container">
        <div class="row">
            <div class="col-md-4 mx-auto mt-5">
                <h4 class="title-section">Ajang Talenta {post.nama_jenjang}</h4>                    
            </div>
        </div>
        <div class="justify-content-md-center">
			<div class="row">
				{#each post.month as item}
					
						{#each item.event as ev}
							
								<div class="col-md-3 mb-5">
									<div class="card border-0">                        
										<img class="card-img-top shadow-sm p-4 bg-white rounded rounded-lg" src="{ev.thumbnail}" alt="{ev.nama_event}">                        
										<div class="card-body mt-3 p-0" >
											
											<a href="/event/{ev.slug}" class="card-title link-orange"><h5>{ev.nama_event}</h5></a>
											<span class="badge badge-pill badge-orange text-white">{ev.category.title}</span>
											<br>
											<span class="badge badge-gray p-0"><i class="fas fa-calendar-day"></i> {ev.tanggal}</span>
											<br>                          
											<span class="badge badge-gray p-0"><i class="fas fa-flag"></i> {ev.level.title}</span>       
											<br>                                               
											<a href="{ev.link}" class="link-unduh mt-3" target="_blank">Laman</a>
											<a href="/event/{ev.slug}" class="link-unduh mt-3">Detail</a>
										</div>
									</div>
								</div>
							
						{/each}
					
				{/each}    
			</div>                   
        </div>            
    </div>
</section>
<!-- Timeline -->
<section class="pt-5" style="background-color: antiquewhite;">
	<div class="container timeline" >
		<div class="row">
			<div class="col-md-4 mx-auto">
				<h4 class="title-section">Timeline Lomba</h4>                                                            
			</div>
		</div>
		<div class="row">
			<ol>
				{#each post.month as item}
					<li class="wh">
						<div>
							<time>{item.alias}</time>
							
							{#each item.event as items}
							<span>- {items.tanggal} | {items.nama_singkat}</span> <br>
							{/each} 
																			
						</div>  					  						         
						<h5 class="bulan">{item.bulan}</h5>           
					</li>
				{/each}
				<li></li>
			</ol>
		</div>
		
		
		<div class="arrows">
			<button class="btn-timeline arrow  arrow__prev disabled" disabled>
			<img src="/assets/images/arrow_prev.svg" alt="prev timeline arrow">
			</button>
			<button class="btn-timeline arrow arrow__next">
			<img src="/assets/images/arrow_next.svg" alt="next timeline arrow">
			</button>
		</div>
	</div>
</section>

<!-- Berita & Pengumuman -->
<section>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-6">                                                       
                <div class="row" >
                    <div class="col-md-12">
                        <h4 class="title-section ml-0">Kabar Prestasi</h4>
                    </div>                        
                </div>    
                <div class="row" >
                    <div class="panel-pengumuman" id="style-2">
						{#each post.user.announcement as items}
							<div class="col-md-12">                                        
								<a href="/pengumuman/{items.slug}" class="pengumuman-card">                                                                                                                            
									<div>
										<strong>{@html items.created_at}</strong>
									</div>                                                                                                
									<h5>{items.sub}</h5>                             
								</a>                    
							</div>
						{/each}
                        <a href="/pengumuman/{post.slug}" class="btn btn-orange2 btn-radius float-right">Pengumuman lainya</a>
                    </div>
                </div>           
            </div>
            <div class="col-md-5 offset-1">
                <div class="row">
                    <div class="col">
                        <h4 class="title-section ml-0">Berita Terbaru</h4>                            
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-12">
                        <ul class="list-unstyled">
							{#each post.user.news as items}
								<li class="media mb-2">
									<img src="{items.thumbnail}" class="rounded mr-3 bg-light" alt="" width="40%" >
									<div class="media-body">
											<span class="badge badge-pill badge-orange text-white">Jenjang {items.user.level.nama_jenjang}</span>										
											<a href="/wara-wara/{items.slug}"><h6>{items.title}</h6> </a> 										
											<span class="badge badge-gray p-0 my-2"><i class="fas fa-calendar-day"></i> {items.tanggal} | <i class="fas fa-eye"></i> {items.viewers}</span>  
											<br>										                    
									</div>
								</li>
							{/each}
                            
                        </ul>
                        <a href="/wara-wara/{post.slug}" class="btn btn-orange2 btn-radius float-right">Berita lainya</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>
</PageTransitions>
<Footer/>


