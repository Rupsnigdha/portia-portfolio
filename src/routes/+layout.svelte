<script lang="ts">
	import Navbar from '$lib/components/Navbar.svelte';
import '../app.css';

	let { children } = $props();
</script>

<div class="relative">
	<Navbar />
	{@render children()}
</div>