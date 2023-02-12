<script>
	import Repl from '$lib/index.svelte';
	import { onMount, onDestroy } from 'svelte';
	import '@sveltejs/site-kit/styles/index.css';
	import '@sveltejs/site-kit/styles/code.css';

	let repl;
    let components = [
        {
            name: 'App',
            type: 'svelte',
            source: `<h1>Hello world !</h1>`
        }
    ]


    function callback() {
        if (components) localStorage.setItem('components', JSON.stringify(components))
    }

    function onInterval(callback, milliseconds) {
        const interval = setInterval(callback, milliseconds);

        onDestroy(() => {
            clearInterval(interval)
        })
	};

	onInterval(callback, 10000)

	onMount(() => {
        components = JSON.parse(localStorage.getItem('components')) || components
		repl.set({
            components: components
        });
	});
</script>

<main>
	<Repl bind:this={repl} showAst />
</main>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
	}

	main {
		height: 100vh;
	}
</style>
