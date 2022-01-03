<script>
	let initial_sum = 10000;
	let interest_rate = 7;
	let number_of_years = 1;
	
	let total_sum = 0;

	function CalculateTotal() {
		let running_total = initial_sum;

		for(let i = 0; i < number_of_years; i++) {
			running_total = running_total * (interest_rate / 100 + 1);
		}

		total_sum = Math.round((running_total + Number.EPSILON) * 100) / 100
	}

</script>

<main>
	<h1>Interest Calculator</h1>

	<form>
		<label for="initialInvestment">Initial investment</label>
		<input type="number" name="initialInvestment" bind:value={initial_sum}>

		<label for="interestRate">Interest rate</label>
		<input type="number" name="interestRate" bind:value={interest_rate}>

		<label for="noOfYears">Number of years</label>
		<input type="number" name="noOfYears" bind:value={number_of_years}>

		<input type="button" on:click={CalculateTotal} value="Calculate">
	</form>

	{#if total_sum}
		<p>Total value after {number_of_years} years: {total_sum}</p>
	{/if}
</main>

<style>
</style>