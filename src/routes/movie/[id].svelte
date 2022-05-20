<script context="module">
	export async function load({ params }) {
		console.log(params.id);
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=${
				import.meta.env.VITE_API
			}&language=en-US&page=1`
		);

		const movieDetail = await res.json();
		console.log(movieDetail);

		if (res.ok) {
			return {
				props: { movieDetail }
			};
		}
	}
</script>

<script>
	import { fly } from 'svelte/transition';
	export let movieDetail;
</script>

<div
	class="movie-details"
	in:fly={{ y: 50, duration: 100, delay: 100 }}
	out:fly={{ duration: 100 }}
>
	<div class="img-container">
		<img
			src={'https://image.tmdb.org/t/p/original' + movieDetail.backdrop_path}
			alt={movieDetail.title}
		/>
	</div>
	<div class="txt-container">
		<h1>{movieDetail.title}</h1>
		<p class="overview">{movieDetail.overview}</p>
		<p>
			<span>Release Date </span>
			{movieDetail.release_date}일 <br />
			<span>Budget:</span>
			{movieDetail.budget.toLocaleString()}달러<br />
			<span>Rating:</span>
			{movieDetail.vote_average}점<br />
			<span>Runtime:</span>
			{movieDetail.runtime}분
		</p>
	</div>
</div>

<style>
	h1 {
		padding: 1rem 0rem 2rem;
	}
	p {
		padding: 1rem 0rem;
	}
	.img-container {
		width: 100%;
	}
	img {
		width: 100%;
		border-radius: 1rem;
	}
	.movie-details {
		margin: 2rem 20%;
	}
	span {
		font-weight: bold;
	}
</style>
