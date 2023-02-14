<script>
	import { browser } from '$app/environment';
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
		});
	};

	if (browser) {
		connectWebSocket();
	}

	const handleClick = (e) => {
		console.log('clicked');
		socket.send('Clicked');
	};
</script>

<div class="container">
	<img src="HfG-Logo-White.svg" alt="Logo der HfG Schwäbisch Gmünd" class="logo" />

	<button class="button" on:click={handleClick}>
		<p>Click me</p>
		<img src="heart.svg" alt="Logo der HfG Schwäbisch Gmünd" class="heart" />
	</button>
	<h1 class="hashtag">#valentinstag</h1>
</div>

<style>
	:global(body) {
		background-color: black;
		color: white;
		/* position: fixed; */
		overflow: hidden;
	}

	.container {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 100%;
		width: 100%;
		padding-left: 12px;
		padding-right: 12px;
		top: 0;
		left: 0;
	}

	.logo {
		width: 240px;
		height: 200px;
		align-self: flex-start;
	}

	.button {
		max-width: 50%;
		width: 100%;
		min-height: 200px;
		background: white;
		align-self: center;
		border: none;
		background: none;
		position: relative;
	}

	.button p {
		position: absolute;
		z-index: 200;
		top: 42%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-size: 36px;
		color: white;
	}

	.heart {
		width: 100%;
		height: 100%;
	}

	.hashtag {
		align-self: center;
	}
</style>
