<script>
	import '../app.css';
</script>

<div class="container">
	<slot />
</div>

<style>
	:global(body, *) {
		font-family: AtlasGrotesk, Helvetica, Arial, sans-serif;
	}

	:global(html, body) {
		/* Height and width fallback for older browsers. */
		height: 100%;
		width: 100%;

		/* Set the height to match that of the viewport. */
		height: 100vh;

		/* Set the width to match that of the viewport. */
		width: 100vw;
		/* Remove any browser-default margins. */
		margin: 0;
	}

	.container {
		position: static;
		height: 100%;
		width: 100%;
		padding: 0px 24px;
	}
</style>
