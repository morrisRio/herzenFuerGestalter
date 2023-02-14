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
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
