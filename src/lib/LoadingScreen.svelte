<script lang="ts">
	// Previous script code remains exactly the same
	import { onMount, onDestroy } from 'svelte';

	let isLoading = true;
	let revealProgress = 0;
	let scaleProgress = 0;
	let glitchState = {
		isGlitching: false,
		offsetX: 0,
		offsetY: 0,
		scale: 1,
		rotation: 0
	};

	let animationFrame: number;
	let startTime: number | null = null;
	const duration = 5000;
	const firstPhaseThreshold = 0.3;
	const firstPhaseDuration = duration * firstPhaseThreshold;
	const secondPhaseDuration = (duration * (1 - firstPhaseThreshold)) / 2;

	function animate(timestamp: number) {
		if (!startTime) startTime = timestamp;
		const progress = timestamp - startTime;

		if (progress <= firstPhaseDuration) {
			revealProgress = (progress / firstPhaseDuration) * firstPhaseThreshold;
		} else {
			const secondPhaseProgress = progress - firstPhaseDuration;
			revealProgress =
				firstPhaseThreshold +
				(secondPhaseProgress / secondPhaseDuration) * (1 - firstPhaseThreshold);
		}

		revealProgress = Math.min(revealProgress, 1);

		const scaleAmount = 0.1;
		if (revealProgress < 1) {
			scaleProgress = 1 + scaleAmount * revealProgress;
		} else {
			const scaleDownDuration = 200;
			const scaleDownProgress = Math.min(
				(progress - (firstPhaseDuration + secondPhaseDuration)) / scaleDownDuration,
				1
			);
			scaleProgress = 1 + scaleAmount * (1 - scaleDownProgress);
		}

		if (revealProgress < 1 || scaleProgress > 1) {
			animationFrame = requestAnimationFrame(animate);
		}
	}

	onMount(() => {
		const loadingTimer = setTimeout(() => {
			isLoading = false;
		}, 5000);

		animationFrame = requestAnimationFrame(animate);

		const glitchTime = Math.random() * 3000 + 1000;
		const glitchTimer = setTimeout(() => {
			let step = 0;
			const totalSteps = 8;
			const stepInterval = setInterval(() => {
				if (step < totalSteps) {
					glitchState = {
						isGlitching: true,
						offsetX: (Math.random() - 0.5) * 20,
						offsetY: (Math.random() - 0.5) * 20,
						scale: step === totalSteps - 1 ? 20 : 1 + Math.random() * 0.5,
						rotation: (Math.random() - 0.5) * 10
					};
					step++;
				} else {
					glitchState = {
						isGlitching: false,
						offsetX: 0,
						offsetY: 0,
						scale: 1,
						rotation: 0
					};
					clearInterval(stepInterval);
				}
			}, 50);
		}, glitchTime);

		return () => {
			clearTimeout(loadingTimer);
			clearTimeout(glitchTimer);
			cancelAnimationFrame(animationFrame);
		};
	});
</script>

<div class="relative h-screen w-screen bg-black overflow-hidden">
	<!-- Modified CRT scan lines with increased gap -->
	<div
		class="absolute inset-0 pointer-events-none animate-scanline"
		style="
		background: repeating-linear-gradient(
		  0deg,
		  rgba(255, 255, 255, 0.1) 0px,
		  rgba(255, 255, 255, 0.1) 2px,
		  transparent 2px,
		  transparent 40px
		);
		background-size: 100% 40px;
	  "
	/>

	<!-- Screen flicker effect -->
	<div
		class="absolute inset-0 mix-blend-overlay animate-crt-flicker pointer-events-none bg-white/10"
	/>

	<!-- Main content container -->
	<div class="relative flex items-center justify-center h-full w-full">
		<!-- Chromatic aberration layers -->
		<div
			class="relative w-64 h-64 overflow-visible animate-crt-displacement"
			style="transform: scale({scaleProgress}); transition: transform 0.2s ease-out;"
		>
			<!-- Red channel -->
			<div
				class="absolute w-full h-full"
				style:clip-path="inset(0 0 0 {100 - revealProgress * 100}%)"
				style="
			transform: 
			  translate(
				{glitchState.offsetX - (glitchState.isGlitching ? 2 : 0)}px,
				{glitchState.offsetY}px
			  )
			  rotate({glitchState.rotation}deg)
			  scale({glitchState.scale});
			opacity: {glitchState.isGlitching ? 0.5 : 1};
			transition: all 0.05s linear;
			mix-blend-mode: screen;
		  "
			>
				<div class="w-full h-full bg-red-500 rounded-lg" />
			</div>

			<!-- Green channel -->
			<div
				class="absolute w-full h-full"
				style:clip-path="inset(0 0 0 {100 - revealProgress * 100}%)"
				style="
			transform: 
			  translate(
				{glitchState.offsetX}px,
				{glitchState.offsetY + (glitchState.isGlitching ? 2 : 0)}px
			  )
			  rotate({glitchState.rotation}deg)
			  scale({glitchState.scale});
			opacity: {glitchState.isGlitching ? 0.5 : 1};
			transition: all 0.05s linear;
			mix-blend-mode: screen;
		  "
			>
				<div class="w-full h-full bg-green-500 rounded-lg" />
			</div>

			<!-- Blue channel -->
			<div
				class="absolute w-full h-full"
				style:clip-path="inset(0 0 0 {100 - revealProgress * 100}%)"
				style="
			transform: 
			  translate(
				{glitchState.offsetX + (glitchState.isGlitching ? 2 : 0)}px,
				{glitchState.offsetY - (glitchState.isGlitching ? 2 : 0)}px
			  )
			  rotate({glitchState.rotation}deg)
			  scale({glitchState.scale});
			opacity: {glitchState.isGlitching ? 0.5 : 1};
			transition: all 0.05s linear;
			mix-blend-mode: screen;
		  "
			>
				<div class="w-full h-full bg-blue-500 rounded-lg">
					<div class="absolute inset-0 flex items-center justify-center">
						<span class="text-white text-2xl font-bold animate-glow"> RETRO GPT </span>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	@keyframes scanline {
		0% {
			transform: translateY(0);
		}
		100% {
			transform: translateY(40px);
		}
	}

	@keyframes crt-flicker {
		0% {
			opacity: 0.7;
		}
		2% {
			opacity: 1;
		}
		4% {
			opacity: 0.7;
		}
		6% {
			opacity: 0.3;
		}
		8% {
			opacity: 1;
		}
		10% {
			opacity: 0.7;
		}
		12% {
			opacity: 1;
		}
		14% {
			opacity: 0.3;
		}
		16% {
			opacity: 1;
		}
		18% {
			opacity: 0.7;
		}
		20% {
			opacity: 1;
		}
		22% {
			opacity: 0.3;
		}
		24% {
			opacity: 1;
		}
		26% {
			opacity: 0.7;
		}
		28% {
			opacity: 1;
		}
		30% {
			opacity: 0.3;
		}
		32% {
			opacity: 1;
		}
		34% {
			opacity: 0.7;
		}
		36% {
			opacity: 0.3;
		}
		38% {
			opacity: 1;
		}
		40% {
			opacity: 0.7;
		}
	}

	@keyframes crt-displacement {
		0% {
			transform: translateY(0) scale(1);
		}
		20% {
			transform: translateY(-1px) scale(1.001);
		}
		40% {
			transform: translateY(1px) scale(0.999);
		}
		60% {
			transform: translateY(-0.5px) scale(1.001);
		}
		80% {
			transform: translateY(0.5px) scale(0.999);
		}
		100% {
			transform: translateY(0) scale(1);
		}
	}

	@keyframes glow {
		0% {
			text-shadow:
				0 0 5px #fff,
				0 0 10px #fff,
				0 0 15px #e60073,
				0 0 20px #e60073;
		}
		100% {
			text-shadow:
				0 0 10px #fff,
				0 0 20px #ff4da6,
				0 0 30px #ff4da6,
				0 0 40px #ff4da6;
		}
	}

	:global(.animate-scanline) {
		animation: scanline 0.75s linear infinite;
	}

	:global(.animate-crt-flicker) {
		animation: crt-flicker 0.1s infinite;
	}

	:global(.animate-crt-displacement) {
		animation: crt-displacement 0.05s infinite;
	}

	:global(.animate-glow) {
		animation: glow 1s ease-in-out infinite alternate;
	}
</style>
