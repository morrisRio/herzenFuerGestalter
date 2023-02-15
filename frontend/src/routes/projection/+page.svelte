<script>
	import { browser } from '$app/environment';

	let windowHeight, windowWidth;

	let hearts = [];

	const duration = 3500;
	const speed = 1.4;

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

	let socket;
	const connectWebSocket = () => {
		socket = new WebSocket('wss://hearts-backend.fly.dev');

		socket.addEventListener('open', (event) => {
			socket.send('Hello Server!');
			console.log('server connected');
		});

		socket.addEventListener('message', (event) => {
			const data = event.data;
			console.log(data);
			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 20, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			);

			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 20, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			);
			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 20, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			);
		});
	};
	if (browser) {
		connectWebSocket();
	}
</script>

<svelte:window bind:innerHeight={windowHeight} bind:innerWidth={windowWidth} />

<!-- {#if browser}
	<button
		on:click={() =>
			generateHeart(
				windowWidth * Math.random(), //x-start
				windowHeight - 200 + Math.random() * 20, //y-start
				20, //left-right swiggle
				Math.random() * 2, //start direction
				1 + Math.random() * 2 //scale
			)}>ADD</button
	>
{/if} -->

<!-- <h1>Herzen für Gestaltung</h1> -->
<img src="HfG-Logo-White.svg" alt="Logo der HfG Schwäbisch Gmünd" class="logo" />

<div class="qrcode">
	<img src="qrcode.svg" alt="QR Code" />

	<p>Scanne den QR-Code,<br /> um Liebe zu verteilen.</p>
</div>

<p class="spreadlove">#valentinstag</p>

{#each hearts as heart}
	<div style={`opacity: ${heart.time / duration}`}>
		<img
			src="./heart.svg"
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

	.logo {
		width: 20%;
		padding-top: 3%;
		padding-left: 2%;
	}

	.qrcode {
		float: right;
		padding-top: 3%;
		padding-right: 4%;
		font-size: 24px;
	}

	.spreadlove {
		position: absolute;
		bottom: 0;
		left: 50%;
		transform: translateX(-50%);
		font-size: 120px;
		font-weight: bold;
	}
</style>
