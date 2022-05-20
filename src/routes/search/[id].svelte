<script context="module">
	import SearchMovies from './../../components/SearchMovies.svelte';
	export async function load({ params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=${
				import.meta.env.VITE_MOVIE_API
			}&language=en-US&query=${params.id}&page=1&include_adult=false`
		);

		const data = await res.json();

		if (res.ok) {
			return {
				props: { searchedMovie: data.results }
			};
		}
	}
</script>

<script>
	import MovieCard from './../../components/MovieCard.svelte';

	export let searchedMovie;
</script>

<div class="searched-movies">
	{#if searchedMovie == ''}
		<div style="margin:0 auto">
			<h2 style="color:red">관련 영화가 없습니다.</h2>
		</div>
	{:else}
		{#each searchedMovie as movie}
			{#if movie.poster_path}
				<MovieCard {movie} />
			{:else}{/if}
		{/each}
	{/if}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
		height: 20vh;
	}
</style>
