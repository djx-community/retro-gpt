<script lang="ts">
	// Add any main app logic here
</script>

<div class="h-screen w-screen bg-black flex items-center justify-center">
	<h1 class="text-6xl font-bold text-white animate-glow">RetroGPT</h1>
</div>

<style>
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

	:global(.animate-glow) {
		animation: glow 1s ease-in-out infinite alternate;
	}
</style>
