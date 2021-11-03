<script context="module">
	export const prerender = true;
</script>

<script>
	import { onMount, tick } from "svelte";

	if (!Array.at) {
		Object.defineProperty(Array.prototype, "at", {
			value: function at(n) {
				// ToInteger() abstract op
				n = Math.trunc(n) || 0;
				// Allow negative indexing from the end
				if (n < 0) n += this.length;
				// OOB access is guaranteed to return undefined
				if (n < 0 || n >= this.length) return undefined;
				// Otherwise, this is just normal property access
				return this[n];
			},
			writable: true,
			enumerable: false,
			configurable: true,
		});
	}

	onMount(() => {
		let frame = 0;
		const bg1 = document.getElementById("bg1");
		const bg2 = document.getElementById("bg2");
		const bg3 = document.getElementById("bg3");
		const framelist = [bg1, bg2, bg3, bg2];
		const changebg = async () => {
			await tick();
			framelist[frame].style.display = "block";
			framelist.at(frame - 1).style.display = "none";
			setTimeout(changebg, frame === 0 ? 3000 : 80);
			frame === framelist.length - 1 ? (frame = 0) : frame++;
		};
		changebg();
	});
</script>

<div class="shutter1" />
<main>
	<div class="flex full videowarp">
		<img id="bg1" class="blur" src="/bg1.png" style="display: block;" alt />
		<img id="bg2" class="blur" src="/bg2.png" style="display: none;" alt />
		<img id="bg3" class="blur" src="/bg3.png" style="display: none;" alt />
		<div class="blurbar" />
		<h1>NotRealPaz</h1>
	</div>
	<div class="flex full" />
	<p>
		© {new Date().getFullYear()} by NotRealPaz
	</p>
</main>

<style>
	.videowarp {
		position: relative;
		overflow: hidden;
		width: 100%;
		height: 100vh;
	}

	img.blur {
		position: absolute;
		width: 150%;
		/* min-height: 100vh; */
		z-index: 1;
		filter: blur(4px) brightness(0.25);
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
