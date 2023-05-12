<script>
	import lottie from "lottie-web";
	import { onMount } from "svelte";
	import { gsap } from "gsap/dist/gsap";
	import MorphSVGPlugin from "gsap/dist/MorphSVGPlugin";
	import DrawSVGPlugin from "gsap/dist/DrawSVGPlugin";
	import ScrollTrigger from "gsap/dist/ScrollTrigger";
	import ScrambleTextPlugin from "gsap/dist/ScrambleTextPlugin";
	import videoSrc from "/video.mp4"

	let logoContainer, pageContainer, aniContainer, emailContainer, touchContainer, imageContainer, emailInput, emailButton, form;
	let inputText, buttonText;
	let innerHeight, innerWidth;
	let y = 0;
	let logo;
	let LottiePlayhead = { frame: 0 };
	let s1,s2,s3,s4;
	let mask;
	let video, time, duration, totalScroll;
	let vis = "visible";

	const colors = {
		black: "#272727",
		yellow: "#FFC82C",
		white: "#F7F4EE"
	}

	const paths = {
		first:  "M2073.79,1148.14H153.79V68.14h1920V1148.14Z",
		second: "M153.79,68.14V1148.14h1920V68.14H153.79Zm958.59,961.13c-220.91,0-400-179.09-400-400s179.09-400,400-400,400,179.09,400,400-179.09,400-400,400Z",
		third: "M153.79,68.14V1148.14h1920V68.14H153.79ZM1634.1,621.74l-4.24,31.34-38.96,372.71-45.74,27.11,.85,5.93,5.93,4.24v16.09l10.16,5.93,.85,16.09-17.79,6.78-33.88,.85-37.27-.85-16.94-5.93v-17.79l11.86-4.24-.85-19.48,5.93-3.39-.85-5.93-31.51-15.42-.02,40.17s3.01-1.88-6.78,16.19c-9.79,18.07-56.47,16.56-56.47,16.56l-73.79,1.51s-54.78,.28-112.38,.56c-57.6,.28-67.2-9.04-75.67-14.4-.22-.14-.43-.28-.63-.43-10.67,17.26-56.03,15.8-56.03,15.8l-73.79,1.51s-54.78,.28-112.38,.56c-57.6,.28-67.2-9.04-75.67-14.4-5.31-3.37-8.18-10.4-9.58-15.17-24.22,14.58-52.59,22.96-82.92,22.96-88.96,0-161.08-72.12-161.08-161.08s72.12-161.08,161.08-161.08c29.85,0,57.8,8.13,81.78,22.29V305.72c-2.26-6.78,6.02-15.44,6.02-15.44l100.52-98.26,.38-7.53-11.67,.38-3.39-1.88-2.64-1.13-2.64-3.39,1.88-5.27,4.89-1.51,.75-3.76,1.13-3.01v-6.4l-1.51-5.27,.75-5.65,2.64-5.65-.75-6.02-1.88-3.39s-.75-25.22,0-27.11c.75-1.88,2.64-3.39,6.4-6.78s129.88-1.88,132.89,0c3.01,1.88,7.53,6.78,7.53,6.78l-.38,19.58-1.88,4.89v4.89l2.64,3.01-.38,7.53-6.02,5.65,.38,4.52,5.27,6.4,.38,8.66s4.14,1.88,6.4,3.39c2.26,1.51,1.51,3.39,1.13,6.02-.38,2.64-6.78,3.76-6.78,3.76h-13.18l.75,9.04s81.9,82.24,95.63,93.72l99.75-97.51,.38-7.53-11.67,.38-3.39-1.88-2.64-1.13-2.64-3.39,1.88-5.27,4.89-1.51,.75-3.76,1.13-3.01v-6.4l-1.51-5.27,.75-5.65,2.64-5.65-.75-6.02-1.88-3.39s-.75-25.22,0-27.11c.75-1.88,2.64-3.39,6.4-6.78s129.88-1.88,132.89,0c3.01,1.88,7.53,6.78,7.53,6.78l-.38,19.58-1.88,4.89v4.89l2.64,3.01-.38,7.53-6.02,5.65,.38,4.52,5.27,6.4,.38,8.66s4.14,1.88,6.4,3.39c2.26,1.51,1.51,3.39,1.13,6.02-.38,2.64-6.78,3.76-6.78,3.76h-13.18l.75,9.04s89.98,90.35,97.13,94.87c7.15,4.52,9.41,14.68,9.41,14.68l-.14,279.05,195.62-.65,.85,26.26-4.24,17.79Z",
	}

	onMount(() => {

		gsap.registerPlugin(ScrollTrigger, ScrambleTextPlugin, MorphSVGPlugin, DrawSVGPlugin);
		ScrollTrigger.normalizeScroll(true);
		

		logo = lottie.loadAnimation({
			container: logoContainer,
			path: "/OCHRE_logo.json",
			autoplay: false,
			loop: false,
			renderer: "svg",
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
			frame: 500,
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
			tl1.to(mask, {
				fill: colors.white,
				duration: 1,
			}, "start");
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
				width: "48%",
			}, "start");

		var tlvid = gsap.timeline({
			scrollTrigger: {
				trigger: s2,
				scrub: true,
				start: "top 50%",
				end: "+=280%",
				// markers: true,
			}
		});


		tlvid.to(video, {currentTime: duration});

		var tl2 = gsap.timeline({
			scrollTrigger: {
				trigger: s2,
				scrub: 1,
				start: "top 90%",
				end: "+=300%",
				// markers: true,
			},
		});
			tl2.to(mask, {
				duration: 5,
				morphSVG: {
					shape: paths.second,
				},
			});

			tl2.to(mask, {
				// ease: "slow (0.7, 0.7, false", 
				duration: 3,
				morphSVG: paths.third,
			});


		var tl3 = gsap.timeline({
			scrollTrigger: {
				trigger: s3,
				scrub: 1,
				start: "top top",
				end: "+=100%",
				// markers: true,
			},
		});
			tl3.add("start", 5);
			tl3.add("end", 5);
			tl3.to(logoContainer, {
				duration: 1,
				top: "30%",
			}, "start");
			tl3.to(touchContainer, {
				duration: 1,
				top: "30%",
			}, "start");
			tl3.to(aniContainer, {
				duration: 1,
				top: "55%",
			}, "start");
			tl3.to(form, {
				duration: 1,
				bottom: "8%",
			}, "start");
			tl3.to(emailInput, {
				duration: 1,
				alpha: 1,
			}, "start");
			tl3.to(emailButton, {
				duration: 1,
				alpha: 1,
			}, "start");
			tl3.to(aniContainer, {
				duration: 1,
				alpha: 0,
			}, "start");
			tl3.to(imageContainer, {
				duration: 1,
				alpha: 1,
				top: "55%",
			},"start");

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
			})
			gsap.to(emailButton, {
				duration: 0.2,
				backgroundColor:colors.black,
				color: colors.white,
			})
		}


	}
	$: if(y == totalScroll) { emailInput.focus() }


</script>

<svelte:window on:beforeunload={scrollTo(0,0)} bind:innerHeight={innerHeight} bind:innerWidth={innerWidth} bind:scrollY={y}/>

<div class="pageContainer" bind:this={pageContainer}>
	<div class="contentContainer">
		<div class="logoContainer" bind:this={logoContainer}></div>
		<div class="touchContainer" bind:this={touchContainer}>
			<div class="touch touch-top">
				<div class="touchpoints touchpoints-left"/>
				<div class="touchpoints touchpoints-middle"/>
				<div class="touchpoints touchpoints-right"/>
			</div>
			<div class="touch touch-bottom"></div>
		</div>
		<div class="emailContainer" bind:this={emailContainer} style="visibility: {vis};">
			<form bind:this={form} on:submit|preventDefault={submitFunc}>
				<input type="email" class="email" bind:value={inputText} bind:this={emailInput} on:input={emailFunc}>
				<button type="submit" class="emailbutton" bind:this={emailButton} contenteditable="true" >{buttonText}</button>
			</form>
		</div>
		<div class="aniContainer" bind:this={aniContainer}>
			<svg class="mask" width="100%" height="100%" viewbox="0 0 2100 1280">
				<path id="mask" bind:this={mask} fill={colors.yellow} d={paths.first}/>
			</svg>
			<video
				class="video"
				bind:this={video}
				bind:duration={duration}
				bind:currentTime={time}
				preload="auto"
				muted
				data-sveltekit-preload-data
				>
				<!-- <source src="/video.webm" type="video/webm"> -->
				<source src="{videoSrc}" type="video/mp4">
			</video>
		</div>
		<div class="imageContainer" bind:this={imageContainer}>
			<img src="/Products.png" alt=""/>
		</div>
	</div>
</div>

<div class="scrollContainer">
	<div class="scroll s1" bind:this={s1}></div>
	<div class="scroll s2" bind:this={s2}></div>
	<div class="scroll s3" bind:this={s3}></div>
	<div class="scroll s4" bind:this={s4}></div>
</div>


<style>
	:root {
		--black: #272727;
		--yellow: #FFC82C;
		--white: #F7F4EE;
	}

	:html {
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		overflow-x: hidden;
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
		border-bottom: .5px var(--yellow) solid;
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

	@media screen and (min-width: 480px) {
		.pageContainer {
			width: 100vw;
			height: 400vh;
			background-color: var(--yellow);
			z-index: -1;
		}
		.aniContainer {
			position: fixed;
			top: 70%;
			left: 50%;
			transform: translate(-50%, -30%);
			width: 30vw;
			opacity: 0;
			/* border: .5px red solid; */
		}
		.logoContainer {
			position: fixed;
			z-index: 10;
			max-width: 30vw;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			/* border: .5px blue solid; */
		}

		.touchContainer {
			position: fixed;
			z-index: 11;
			height: 10vw;
			width: 20vw;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			/* border: .5px blue solid; */
		}

		.mask {
			width: 100%;
			height: 100%;
			left: 50%;
			top: 50%;
			transform: translate(-50, -50);
			z-index: 10;
		}

		.video {
			position: fixed;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			width: 95%;
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
			font-size: 1.2rem	;
			font-family: 'Courier New', Courier, monospace;
			margin: .8rem;
			padding: .5rem;
			opacity: 0;
			background-color: rgba(0,0,0,0);
			width: 25vw;
			text-align: center;
		}

		.emailbutton {
			font-family: 'Courier New', Courier, monospace;
			font-size: 0.8rem;
			width: 25vw;
			color: var(--black);
			border: .1px var(--black) solid;
			border-radius: .3rem;
			height: 2rem;
			padding: .2rem;
			padding-left: .5rem;
			padding-right: .5rem;
			opacity: 0;
			background-color: rgba(0,0,0,0);
		}
	}
/* mobile sizing */
	@media screen and (max-width: 480px) {
		.aniContainer {
			position: fixed;
			top: 70%;
			left: 50%;
			transform: translate(-50%, -30%);
			width: 100vw;
			height: 60vw;
			opacity: 0;
			/* border: .5px red solid; */
		}

		.imageContainer {
			opacity: 0;
			position: fixed;
			top: 70%;
			left: 49%;
			transform: translate(-51%, -30%);
			width: 100%;
			z-index: 10;
		}
		.imageContainer img {
			width: 100%;

		}

		.pageContainer {
			width: 100vw;
			height: 400vh;
			background-color: var(--yellow);
			z-index: -1;
		}

		.logoContainer {
			position: fixed;
			z-index: 10;
			width: 70vw;
			max-height: 30vh;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
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
		
		.mask {
			position: fixed;
			width: 100%;
			height: 100%;
			left: 49%;
			top: 51%;
			transform: translate(-51%, -49%);
			z-index: 10;
		}

		.video {
			position: fixed;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			width: 80%;
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
			font-size: .8rem	;
			font-family: 'Courier New', Courier, monospace;
			margin: .8rem;
			padding: .5rem;
			opacity: 0;
			background-color: rgba(0,0,0,0);
			width: 50vw;
			text-align: center;
		}

		.emailbutton {
			font-family: 'Courier New', Courier, monospace;
			font-size: .5rem;
			width: 50vw;
			color: var(--black);
			border: .1px var(--black) solid;
			border-radius: .3rem;
			height: 1.8rem;
			padding: .2rem;
			padding-left: .5rem;
			padding-right: .5rem;
			opacity: 0;
			background-color: rgba(0,0,0,0);
		}
	}
</style>