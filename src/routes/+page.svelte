<script>
	import { browser } from '$app/environment';

	let windowHeight, windowWidth;

	let hearts = [];

	const duration = 5000;
	const speed = 1.5;

	function generateHeart(x, y, xBound, xStart, scale) {
		console.log('generate heart');

		let newHeart = {};

		newHeart.time = duration;
		newHeart.startX = x;
		newHeart.x = x;
		newHeart.y = y;
		newHeart.bound = xBound;
		newHeart.direction = xStart;
		newHeart.scale = scale;
		//if (hearts == null) hearts = [];
		hearts.push(newHeart);
		hearts = hearts;
		console.log(hearts);
		return newHeart;
	}

	var before = Date.now();
	var id = setInterval(frame, 5);
	function frame() {
		var current = Date.now();
		var deltaTime = current - before;
		before = current;
		hearts.forEach((heart, index) => {
			heart.time -= deltaTime;
			if (heart.time > 0) {
				heart.y -= speed;
				heart.x =
					heart.startX + heart.direction * heart.bound * Math.sin(heart.y / heart.scale / 20);
			} else {
				console.log('remove heart');
				hearts.splice(index, 1);
			}
			hearts = hearts;
		});
	}

	if (browser) {
		//socket.on('message');
	}
</script>

<svelte:window bind:innerHeight={windowHeight} bind:innerWidth={windowWidth} />

{#if browser}
	<button
		on:click={() => {
			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 100, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			);
			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 100, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			);
			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 100, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			);
		}}>ADD</button
	>
{/if}

<h1>Herzen für Gestaltung</h1>

{#each hearts as heart}
	<div style={`opacity: ${heart.time / duration}`}>
		<img
			src="./openmoji-heart.svg"
			alt="herzFuerGestalter"
			class="heart-img"
			style={`position: absolute; top: ${heart.y}px; left: ${heart.x}px; scale: ${heart.scale}`}
		/>
	</div>
{/each}

<style>
	.heart-img {
		z-index: 999;
		height: 50px;
		width: 50px;
		position: absolute;
	}
	:global(body) {
		background: black;
		color: white;
		overflow: hidden;
	}
</style>
