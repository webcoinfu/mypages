<script context="module">
	export const prerender = true;
</script>

<svelte:head>
	<link rel="preload" as="image" href="/bg1.png">
	<link rel="preload" as="image" href="/bg2.png">
	<link rel="preload" as="image" href="/bg3.png">
</svelte:head>

<div class="shutter1" />
<main>
	<div class="flex full videowarp">
		<div class="bg" />
		<div class="blurbar" />
		<h1>NotRealPaz</h1>
	</div>
	<div class="flex full" />
	<p>
		© {new Date().getFullYear()} by NotRealPaz
	</p>
</main>

<style>
	@keyframes bgchange {
		from {
			content: url("/bg1.png");
		}

		96% {
			content: url("/bg1.png");
		}

		98% {
			content: url("/bg2.png");
		}

		to {
			content: url("/bg3.png");
		}
	}

	.videowarp {
		position: relative;
		overflow: hidden;
		width: 100%;
		height: 100vh;
	}

	div.bg {
		position: absolute;
		width: 150%;
		/* min-height: 100vh; */
		z-index: 1;
		filter: blur(4px) brightness(0.25);
		content: url("/bg1.png");
		animation: bgchange 2s forwards infinite alternate;
	}

	.blurbar {
		position: absolute;
		width: 100%;
		height: 100vh;
		background-image: linear-gradient(
			rgba(0, 0, 0, 0) 70%,
			var(--bg-color) 100%
		);
		z-index: 2;
	}

	main {
		text-align: center;
		margin: 0 auto;
		max-width: 1024px;
	}

	.flex {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.full {
		width: 100%;
		height: 100vh;
	}

	h1 {
		position: absolute;
		color: #0084ff;
		font-size: 10vw;
		font-weight: 200;
		z-index: 3;
	}

	p {
		font-size: 1em;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	.shutter1 {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: #000;
		z-index: 10000;
		animation: byeShutter 2s forwards;
	}

	.shutter1:before {
		content: "";
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		margin: auto;
		width: 0;
		height: 1px;
		animation: shutterOpen 2s forwards;
	}

	@keyframes byeShutter {
		80% {
			opacity: 1;
		}

		to {
			opacity: 0;
			display: none;
			z-index: -1;
		}
	}

	@keyframes shutterOpen {
		0% {
			width: 0;
			height: 2px;
			background-color: rgb(0, 132, 255);
		}

		50% {
			width: 100%;
			height: 5%;
		}

		90% {
			width: 100%;
			height: 100%;
		}

		to {
			width: 100%;
			height: 100%;
			background-color: var(--bg-color);
		}
	}
</style>
