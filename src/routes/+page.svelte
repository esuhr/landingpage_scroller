<script>
	import lottie from "lottie-web";
	import { onMount } from "svelte";
	import { gsap } from "gsap/dist/gsap";
	import MorphSVGPlugin from "gsap/dist/MorphSVGPlugin";
	import ScrollTrigger from "gsap/dist/ScrollTrigger";
	import ScrambleTextPlugin from "gsap/dist/ScrambleTextPlugin";

	let logoContainer, contentContainer, pageContainer, aniContainer, emailContainer, touchContainer, imageContainer, videoContainer, textContainer, arrowContainer;
	let emailInput, emailButton, form;
	let inputText, buttonText;
	let innerHeight, innerWidth;
	let y = 0;
	let logo;
	let LottiePlayhead = { frame: 0 };
	let LottieVideohead = { frame: 0 };
	let LottieTexthead = { frame: 0 };
	let s1,s2,s3,s4, s5;
	let video, totalScroll;
	let thankyou;
	let team, teamphoto;
	let text;
	let imageCaption;
	let arrow;
	let vis = "visible";

	const colors = {
		black: "#272727",
		yellow: "#FFC82C",
		white: "#F4F3EE"
	}

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, ScrambleTextPlugin, MorphSVGPlugin);
		ScrollTrigger.normalizeScroll(true);

		logo = lottie.loadAnimation({
			container: logoContainer,
			path: "/OCHRE_logo.json",
			autoplay: false,
			loop: false,
			renderer: "svg",
		});

		arrow = lottie.loadAnimation({
			container: arrowContainer,
			path: "/arrow.json",
			autoplay: true,
			loop: true,
			renderer: "svg",
		});

		video = lottie.loadAnimation({
			container: videoContainer,
			path: "/video.json",
			autoplay: false,
			loop: false,
			renderer: "canvas",
		});

		var tl = gsap.timeline({
			scrollTrigger: {
				trigger: s1,
				scrub: 1,
				start: "top top",
				end: "bottom top",
				// markers: true,
			},
			onUpdate: () => {
				logo.goToAndStop(LottiePlayhead.frame, true)
			}
		});

			tl.to(LottiePlayhead, {
				frame: 341,
				ease: "none",
			});


		var tl1 = gsap.timeline({
			scrollTrigger: {
				trigger: s1,
				scrub: 1,
				start: "top top",
				end: "+=1000",
				// markers: true,
			},
		});
			tl1.add("start");
			tl1.to(pageContainer, {
				backgroundColor: colors.white,
				duration: 1,
			},"start");
			tl1.to(aniContainer, {
				autoAlpha: 1,
				duration: 3,
			},);
			tl1.to(logoContainer, {
				duration: 1,
				height: "15vh",
			}, "start");


		var tlvid = gsap.timeline({
			scrollTrigger: {
				trigger: s2,
				scrub: true,
				start: "top 50%",
				end: "+=280%",
				// markers: true,
			},
			onUpdate: () => {
				video.goToAndStop(LottieVideohead.frame, true)
			}
		});

			tlvid.to(LottieVideohead, {
				frame: 341,
				ease: "none",
			});

		text = lottie.loadAnimation({
			container: textContainer,
			path: "/text.json",
			autoplay: false,
			loop: false,
			renderer: "svg",
		});

		var tltext = gsap.timeline({
			scrollTrigger: {
				trigger: s2,
				scrub: true,
				start: "top 50%",
				end: "+=280%",
				// markers: true,
			},
			onUpdate: () => {
				text.goToAndStop(LottieTexthead.frame, true)
			}
		});

			tltext.to(LottieTexthead, {
				frame: 341,
				ease: "none",
			});


		var tl3 = gsap.timeline({
			scrollTrigger: {
				trigger: s3,
				scrub: 1,
				start: "top top",
				end: "+=500%",
				// markers: true,
			},
		});
			tl3.add("start", 5);
			tl3.add("end", 5);
			tl3.to(touchContainer, {
				duration: 2,
				top: "30%",
			}, "start");
			tl3.to(videoContainer, {
				duration: 2,
				top: "40%",
			}, "start");
			tl3.to(aniContainer, {
				duration: 5,
				autoAlpha: 0,
			}, "end");

		var tl4 = gsap.timeline({
			scrollTrigger: {
				trigger: s4,
				// scrub: 1,
				toggleActions: "play none none reverse",
				start: "top top",
				end: "bottom bottom",
				// markers: true, 
			},
		});
			tl4.add("start", 1);
			tl4.add("end", 1);

			tl4.to(imageContainer, {
				duration: 0.8,
				autoAlpha: 1,
				top: "55%",
			},"start");
			tl4.to(form, {
				duration: 2,
				bottom: "8%",
			}, "start");
			tl4.to(emailInput, {
				duration: 2,
				autoAlpha: 1,
			}, "start");
			tl4.to(emailButton, {
				duration: 2,
				autoAlpha: 1,
			}, "start");
			tl4.to(imageCaption, {
				duration: 5,
				autoAlpha: 1,
			}, "start");

		totalScroll = document.documentElement.scrollHeight - innerHeight;
	});
	buttonText = "SUBSCRIBE"
	const emailFunc = () => {
		if(inputText.length == 1 ) {
			gsap.to(emailButton, {
				duration:.5,
				scrambleText: {
					text: "SUBSCRIBE",
					chars: "upperCase"
				}
			})
		} 
	}
	const submitFunc = () => {
		if(inputText && inputText.length > 3) {
			gsap.to(emailButton, {
				duration:1,
				scrambleText: {
					text: "THANK YOU",
					chars: "upperCase"
				}
			});
			gsap.to(emailButton, {
				duration: 0.2,
				backgroundColor: colors.black,
				color: colors.white,
			});
			gsap.to(thankyou, {
				duration: 1,
				autoAlpha: 1,
			});
			gsap.to(team, {
				delay: 1.0,
				duration: 1,
				autoAlpha: 1,
			});
			gsap.to(teamphoto, {
				delay: 2.0,
				duration: 5,
				autoAlpha: 1,
			})
			gsap.to(contentContainer, {
				duration: 1,
				autoAlpha: 0,
			});
			gsap.to(emailInput, {
				duration: 1,
				autoAlpha: 0,
			});
		}
	}
	$: if(y == totalScroll) { emailInput.focus() }
	$: if(y > 10) {vis = "hidden"}
</script>

<svelte:window on:beforeunload={scrollTo(0,0)} bind:innerHeight={innerHeight} bind:innerWidth={innerWidth} bind:scrollY={y}/>

<div class="pageContainer" bind:this={pageContainer}>
	<div class="arrowContainer" bind:this={arrowContainer} style="visibility:{vis};"></div>
	<div class="textContainer" bind:this={textContainer}></div>
	<div class="logoContainer" bind:this={logoContainer}></div>
	<div class="contentContainer" bind:this={contentContainer}>

		<div class="touchContainer" bind:this={touchContainer}>
			<div class="touch touch-top">
				<div class="touchpoints touchpoints-left"/>
				<div class="touchpoints touchpoints-middle"/>
				<div class="touchpoints touchpoints-right"/>
			</div>
			<div class="touch touch-bottom"></div>
		</div>
		<div class="aniContainer" bind:this={aniContainer}>
			<div class="videoContainer" bind:this={videoContainer}></div>
		</div>
		<div class="imageContainer" bind:this={imageContainer}>
			<img src="/Products.png" alt=""/>
		</div>
		<div class="imageCaption" bind:this={imageCaption} style="visibility:hidden;">
			<p>We are creating a microbiome balancing haircare system for sensitive skin.</p>
		</div>
	</div>
	<div class="thankyou" bind:this={thankyou} style="visibility: hidden;">
		<p>Your support means a lot to us.</p>
		<p>We'll keep you updated.</p>
		<br><br>
		<p style="visibility: hidden;" bind:this={team}>from the team:</p>
		<img src="/sig.png" alt="" bind:this={teamphoto} style="visibility: hidden;">
	</div>
	<div class="emailContainer" bind:this={emailContainer}>
		<form bind:this={form} method="POST" on:submit={submitFunc} data-netlify="true">
			<input type="hidden" name="form-name" value="netlify-form-example" />
			<input type="email" class="email" placeholder="EMAIL" bind:value={inputText} bind:this={emailInput} on:input={emailFunc}>
			<button type="submit" class="emailbutton" bind:this={emailButton} contenteditable="true" >{buttonText}</button>
		</form>
	</div>
</div>

<div class="scrollContainer">
	<div class="scroll s1" bind:this={s1}></div>
	<div class="scroll s2" bind:this={s2}></div>
	<div class="scroll s3" bind:this={s3}></div>
	<div class="scroll s4" bind:this={s4}></div>
	<div class="scroll s5" bind:this={s5}></div>
</div>


<style>
	@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,200;0,300;0,400;1,300&family=IBM+Plex+Sans:wght@200;300;400&display=swap');
	:root {
		--black: #272727;
		--yellow: #FFC82C;
		--white: #F4F3EE;
		--font1: 'IBM Plex Mono', monospace;
		--font2: 'IBM Plex Sans', sans-serif;
	}

	:html {
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		overflow-x: hidden;
	}

	.pageContainer {
		width: 100vw;
		height: 500vh;
		background-color: var(--yellow);
		z-index: -1;
		/* visibility: hidden; */
	}

	.scrollContainer {
		z-index: 5;
		display: flex;
		flex-direction: column;
		position: absolute;
		top: 0;
	}

	.scroll {
		width: 100vw;
		height: 100vh;
		z-index:5;
		/* border: .5px red solid; */
	}
	.email:focus {
		outline: none;
		transition: .5s;
	}
	.emailbutton:hover {
		color: var(--white);
		background-color: var(--black);
		border: .1px var(--black) solid;
		transition-duration: 0.5s;
	}
	.touchContainer {
		display: flex;
		flex-direction: column;
	}
	.touch-top {
		width: 100%;
		height: 75%;
		/* border: .5px red solid; */
		display: flex;
		flex-direction: row;
	}
	.touch-bottom {
		width: 100%;
		height: 25%;
		/* border: .5px red solid; */
	}
	.touchpoints {
		width: 33%;
		height: 100%;
		/* border: .5px blue solid; */
	}
	.thankyou {
		position: fixed;
		text-align: center;
		top: 40%;
		width: 100vw;
		height: 100vh;
		z-index: 12;
		font-family: var(--font1);
		font-weight: 300;
		color: var(--black);
		font-size: 1rem;
	}

	.thankyou img {
		height: 7vh;
	}

	.textContainer {
		position: fixed;
		z-index: 9;
		top: 80%;
		left: 50%;
		transform: translate(-50%, -20%);
		max-width: 200px; 
	}

	@media screen and (min-width: 480px) {

		.arrowContainer {
			position: fixed;
			height: 80vh;
			top: 60%;
			left: 50%;
			transform: translate(-50%, -40%);
			z-index: 15;
			/* border: 1px red solid; */
		}


		.aniContainer {
			position: fixed;
			top: 60%;
			left: 50%;
			transform: translate(-50%, -40%);
			opacity: 0;
		}

		.imageContainer {
			opacity: 0;
			visibility: hidden;
			position: fixed;
			top: 60%;
			left: 50%;
			transform: translate(-50%, -40%);
			width: 100%;
			max-width: 380px;
			z-index: 10;
		}
		.imageContainer img {
			width: 100%;
			max-width: 700px;
		}

		.textContainer {
			position: fixed;
			z-index: 9;
			top: 80%;
			left: 50%;
			transform: translate(-50%, -20%);
			max-width: 200px; 
		}

		.imageCaption {
			position: fixed;
			z-index: 10;
			top: 78%;
			left: 50%;
			transform: translate(-50%, -22%);
			font-family: var(--font2);
			font-weight: 200;
			font-size: 0.8rem;
			max-width: 700px;
		}

		.logoContainer {
			position: fixed;
			z-index: 10;
			width: 50vw;
			top: 30%;
			left: 50%;
			transform: translate(-50%, -70%);
			/* border: .5px blue solid; */
		}

		.touchContainer {
			position: fixed;
			z-index: 10;
			width: 70vw;
			max-height: 30vh;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			/* border: .5px blue solid; */
		}

		.videoContainer {
			position: fixed;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			width: 80vw;
			max-width: 800px;
			z-index: -1;
		}

		form {
			left: 50%;
			width: 95vw;
			transform: translate(-50%, 0);
			z-index: 10;
			position: fixed;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			bottom: 0rem;
		}

		.email {
			border-top: none;
			border-left: none;
			border-right: none;
			border-bottom: .5px var(--black) solid;
			font-size: 1rem	;
			font-family: var(--font1);
			font-weight: 300;
			margin: .8rem;
			padding: .5rem;
			opacity: 0;
			background-color: rgba(27,27,27,0);
			width: 400px;
			text-align: center;
		}

		.emailbutton {
			font-family: var(--font2);
			font-size: .8rem;
			width: 400px;
			color: var(--black);
			border: .1px var(--black) solid;
			border-radius: .3rem;
			height: 2.2rem;
			padding: .2rem;
			padding-left: .5rem;
			padding-right: .5rem;
			opacity: 0;
			background-color: rgba(27,27,27,0);
		}
	}
/* mobile sizing */
	@media screen and (max-width: 480px) {
		.arrowContainer {
			position: fixed;
			height: 800px;
			top: 60%;
			left: 50%;
			transform: translate(-50%, -40%);
			z-index: 15;
			/* border: 1px red solid; */
		}

		.thankyou {
			font-size: 0.7rem;
		}
		.aniContainer {
			position: fixed;
			top: 70%;
			left: 50%;
			transform: translate(-50%, -30%);
			width: 100vw;
			height: 60vw;
			opacity: 0;
			visibility: hidden;
			/* border: .5px red solid; */
		}

		.imageContainer {
			opacity: 0;
			visibility: hidden;
			position: fixed;
			top: 60%;
			left: 50%;
			transform: translate(-50%, -40%);
			width: 55vw;
			z-index: 10;
		}
		.imageContainer img {
			width: 100%;
		}

		.textContainer {
			position: fixed;
			z-index: 9;
			top: 80%;
			left: 50%;
			transform: translate(-50%, -20%);
			max-width: 150px; 
		}

		.imageCaption {
			position: fixed;
			z-index: 10;
			top: 75%;
			left: 50%;
			transform: translate(-50%, -25%);
			font-family: var(--font2);
			font-weight: 200;
			font-size: 0.6rem;
			max-width: 55vw;
			text-align: center;
		}

		.logoContainer {
			position: fixed;
			z-index: 10;
			width: 70vw;
			max-height: 30vh;
			top: 30%;
			left: 50%;
			transform: translate(-50%, -70%);
			/* border: .5px blue solid; */
		}

		.touchContainer {
			position: fixed;
			z-index: 10;
			width: 70vw;
			max-height: 30vh;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			/* border: .5px blue solid; */
		}

		.videoContainer {
			position: fixed;
			top: 30%;
			left: 50%;
			transform: translate(-50%, -70%);
			width: 120vw;
			z-index: -1;
		}

		form {
			left: 50%;
			width: 95vw;
			transform: translate(-50%, 0);
			z-index: 10;
			position: fixed;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			bottom: 0rem;

		}

		.email {
			border-top: none;
			border-left: none;
			border-right: none;
			border-bottom: .5px var(--black) solid;
			font-size: 0.8rem	;
			font-family: var(--font1);
			font-weight: 300;
			margin: .8rem;
			padding: .5rem;
			opacity: 0;
			visibility: hidden;
			background-color: rgba(27,27,27,0);
			width: 50vw;
			text-align: center;
		}

		.emailbutton {
			font-family: var(--font2);
			font-size: .5rem;
			width: 50vw;
			color: var(--black);
			border: .1px var(--black) solid;
			border-radius: .3rem;
			height: 2rem;
			padding: .2rem;
			padding-left: .5rem;
			padding-right: .5rem;
			visibility: hidden;
			opacity: 0;
			background-color: rgba(27,27,27,0);
		}
	}
</style>