<script>
	import { onMount } from 'svelte';
	import 'bootstrap/dist/css/bootstrap.min.css';
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	let countriesData;
  
	onMount(async () => {
	  const response = await fetch('https://restcountries.com/v3.1/lang/spanish');
	  const data = await response.json();
	  countriesData = data;
	});
  </script>

  	<Header title="Paises" />
  	<main>
		{#if countriesData}
			{#each countriesData as country, index}
			<div class="container border-bottom">
				<div class="accordion w-75 float-start">
					<div>
						<input type="checkbox" id={`section${index}`} class="accordion__input">
						<label for={`section${index}`} class="accordion__label">{country.name.common}</label>
						<div class="accordion__content">
							<div class="row">
								<div class="col">
									<strong>Capital: </strong><span class="badge text-bg-success"> {country.capital}</span>
								</div>
								<div class="col">
									<strong>Poblacion: </strong><span class="badge text-bg-primary">{country.population}</span>
								</div>
								<div class="col">
									<strong>Subregion: </strong><span class="badge text-bg-warning">{country.subregion}</span>
								</div>
							</div>
						</div>
					</div>
				</div>					
				<img class="float-end rounded-circle shadow border" src={country.flags.svg} alt="Flag">
			</div>
			{/each}
		{/if}
  	</main>
  	<Footer />

  <style>
	main {
	  display: flex;
	  flex-wrap: wrap;
	  gap: 1rem;
	  padding: 1rem;
	  margin-top: 5rem;
	  margin-bottom: 5rem;
	}
  
	img{
		width: 75px;
		height: 75px;
		margin-bottom: 1rem;
	}

	.accordion{
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
		border-radius: 15px;
		overflow: hidden;
		background: linear-gradient(to right, rgb(252, 74, 26), rgb(247, 183, 51));
		margin-bottom: 1rem;
	}

	.accordion__label, .accordion__content{
		padding: 14px 20px;
	}

	.accordion__label{
		display: block;
		color: white;
		font-weight: bold;
		cursor: pointer;
		position: relative;
		transition: background-color 0.1s;
	}
	.accordion__label:hover{
		background-color: rgba(0, 0, 0, 0.1);
	}
	.accordion__content{
		background: white;
		line-height: 1.6;
		font-size: 0.85em;
		display: none;
	}
	.accordion__input{
    display: none;
	}
	.accordion__input:checked ~ .accordion__content{
		display: block;
	}
  </style>
  