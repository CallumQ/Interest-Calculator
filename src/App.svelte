<script>
	let initial_sum = 10000;
	let interest_rate = 7;
	let number_of_years = 1;
	let currency_symbol = "$";
	let total_sum = 0;

	function CalculateTotal() {
		let running_total = initial_sum;

		for(let i = 0; i < number_of_years; i++) {
			running_total = running_total * (interest_rate / 100 + 1);
		}

		total_sum = Math.round((running_total + Number.EPSILON) * 100) / 100
	}

	function setActiveCurrency(element) {
		currency_symbol = element.target.innerText;
	}

</script>

<main>
	<div class="container">
		<div class="row">
		  <div class="col-8 offset-md-2">
			<h1>Interest Calculator</h1>
			
			<form>
				<div class="mb-2 row">
					<label for="currency" class="col-sm-4 col-form-label">Currency</label>
					<div class="col-sm-8">
						<div class="btn-group" role="group" aria-label="Basic example" on:click={setActiveCurrency}>
							<button type="button" class="btn btn-primary">$</button>
							<button type="button" class="btn btn-outline-primary">£</button>
							<button type="button" class="btn btn-outline-primary">€</button>
							<button type="button" class="btn btn-outline-primary">¥</button>
							<button type="button" class="btn btn-outline-primary">₹</button>	
						</div>
					</div>
				</div>
				<div class="mb-2 row">
					<label for="initialInvestment" class="col-sm-4 col-form-label">Initial investment</label>
					<div class="col-sm-8">
						<input type="number" name="initialInvestment" bind:value={initial_sum}>
					</div>
				</div>
				<div class="mb-2 row">
					<label for="interestRate" class="col-sm-4 col-form-label">Interest rate</label>
					<div class="col-sm-8">
						<input type="number" name="interestRate" bind:value={interest_rate}>
					</div>
				</div>
				<div class="mb-2 row">
					<label for="noOfYears" class="col-sm-4 col-form-label">Number of years</label>
					<div class="col-sm-8">
						<input type="number" name="noOfYears" bind:value={number_of_years}>
					</div>
				</div>
				<input type="button" on:click={CalculateTotal} value="Calculate" class="btn btn-primary">
			</form>

			{#if total_sum}
				<h2> Result:</h2>
				<p>Total value after {number_of_years} years: {currency_symbol + total_sum}</p>
			{/if}
		  </div>
		</div>
	  </div>
</main>

<style>
</style>