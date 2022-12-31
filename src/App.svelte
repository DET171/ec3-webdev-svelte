<script>
	import axios from 'axios';

	let products = [];

	axios.get('https://dummyjson.com/products')
		.then(response => {
			products = response.data.products;
		}).catch(error => {
			console.log(error);
		});

	let searchTerm = '';
</script>

<div class="p-10">
	<h1 class="text-4xl font-bold text-center">Products</h1>

	<div class="flex justify-center mt-10">
		<input
			type="text"
			class="w-1/2 px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-600 focus:border-transparent"
			placeholder="Search for a product"
			bind:value={searchTerm}
		/>
	</div>

	<div class="grid grid-cols-1 gap-4 mt-10 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
		{#each products.filter((product) => {
			return product.title.toLowerCase().includes(searchTerm.toLowerCase());
		}) as product}
			<div class="p-4 bg-white rounded shadow">
				<img src={product.thumbnail} alt={product.title} class="w-full h-64 object-cover rounded-t" />
				<div class="p-4">
					<h2 class="text-xl font-bold">{product.title}</h2>
					<p class="mt-2 text-gray-600">{product.description}</p>
					<div class="flex items-center justify-between mt-4">
						<span class="text-2xl font-bold">${product.price}</span>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div>
