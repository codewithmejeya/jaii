<script>
	import { fade, blur, slide } from 'svelte/transition';
	import { quadInOut } from 'svelte/easing';
	import { onMount } from 'svelte';
	import CircularButton from '$lib/components/atoms/CircularButton.svelte';
	import { user } from '../data/Data';

	let animate = false;
	const helloInDifferentLanguages = [
		'Hi',
		'வணக்கம்',
		'ഹലോ',
		'ನಮಸ್ಕಾರ',
		'హలో',
		'नमस्ते',
		'પધારો',
		'سَلَام',
		'Hola',
		'Cześć',
		'God dag',
		'Bonjour',
		'Merhaba',
		'こんにちは',
		'Guten Tag'
	];
	let currentHello = helloInDifferentLanguages[0];
	let currentIndex = 0;

	function updateHelloText() {
		currentIndex = (currentIndex + 1) % helloInDifferentLanguages.length;
		currentHello = helloInDifferentLanguages[currentIndex];
	}

	onMount(() => {
		animate = true;
		setInterval(updateHelloText, 3000);
	});
</script>

<style>
	.hello-text {
		font-size: 1.5rem;
	}
	
	@media (min-width: 640px) {
		.hello-text {
			font-size: 2rem;
		}
	}
	@media (min-width: 768px) {
		.hello-text {
			font-size: 2.5rem;
		}
	}
	@media (min-width: 1024px) {
		.hello-text {
			font-size: 3rem;
		}
	}
	@media (min-width: 1280px) {
		.hello-text {
			font-size: 3.5rem;
		}
	}

	.button-container {
		display: flex;
		justify-content: center;
		gap: 1rem;
		flex-wrap: wrap;
		padding: 1rem;
	}
</style>

<section class="pt-28 dark:bg-gray-900 mocha">
	{#if animate}
		<div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:py-16" transition:blur|local={{ duration: 500 }}>
			<div class="flex justify-center">
				<h1 class="mb-4 text-4xl p-0 font-bold md:text-6xl lg:text-8xl dark:text-white flex flex-col-reverse">
					{#key currentHello}
						{#if currentHello}
							<span class="py-2 text-latte-blue dark:text-ctp-mauve text-center hello-text" transition:slide={{ duration: 1000, easing: quadInOut }}>
								{currentHello}! &nbsp
							</span>
						{/if}
					{/key}
				</h1>
				<h1 class="mb-4 text-4xl py-2 font-bold md:text-6xl lg:text-8xl dark:text-white sticky">
					I'm {user.name}
				</h1>
			</div>
			<p class="mb-8 text-2xl font-normal md:text-3xl lg:text-4xl sm:px-16 lg:px-48 dark:text-gray-200">
				{user.role}
			</p>
		</div>
		<div class="button-container" transition:fade|local={{ duration: 700 }}>
			<CircularButton size="md" href="/about">About Me!&nbsp;🪴</CircularButton>
			<CircularButton size="md" href="/contact">👋 &nbsp;Connect with me</CircularButton>
		</div>
	{/if}
	<br>

</section>
