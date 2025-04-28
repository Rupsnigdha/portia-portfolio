<script lang="ts">
	import Navbar from '$lib/components/Navbar.svelte';
import '../app.css';

	let { children } = $props();
</script>

<div class="relative">
	<Navbar />
	{@render children()}
</div>
<div class="fixed -top-[30%] -right-[10%] w-[600px] h-[600px] rounded-full bg-purple-500/10 blur-[120px]"></div>
<div class="fixed top-[60%] -left-[10%] w-[400px] h-[400px] rounded-full bg-blue-500/10 blur-[100px]"></div>
