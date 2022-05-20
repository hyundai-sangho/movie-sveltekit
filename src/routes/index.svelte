<script context="module">
	export async function load() {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=${
				import.meta.env.VITE_MOVIE_API
			}&language=en-US&page=1`
		);
		const data = await res.json();
		console.log(data);
		if (res.ok) {
			return {
				props: { popular: data.results }
			};
		}
	}
</script>

<script>
	import PopularMovies from './../components/PopularMovies.svelte';
	export let popular;

	import SearchMovies from '../components/SearchMovies.svelte';

	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 50, duration: 100, delay: 100 }} out:fly={{ duration: 100 }}>
	<SearchMovies />
	<PopularMovies {popular} />
</section>
