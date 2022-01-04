<script>
	let initial_sum = 10000;
	let interest_rate = 7;
	let number_of_years = 10;
	let annual_deposit = 5000;

	let currency_symbol = "$";

	let total_sum = 0;
	let computed_years_array;

	function CalculateTotal() {
		let deposit_total = initial_sum;

		computed_years_array = [];
		computed_years_array.push({
				deposit: initial_sum,
				deposit_total: initial_sum,
				interest: 0,
				interest_total: 0,
				cumulative_total: 0
		});

		let running_total = initial_sum;
		let running_interest = 0;
		for(let i = 0; i < number_of_years; i++) {
			let annual_interest = running_total * (interest_rate / 100);
			running_interest += annual_interest;

			running_total += annual_interest + annual_deposit;
			deposit_total += annual_deposit;

			computed_years_array.push({
				deposit: Math.round((annual_deposit + Number.EPSILON) * 100) / 100,
				deposit_total: Math.round((deposit_total + Number.EPSILON) * 100) / 100,
				interest: Math.round((annual_interest + Number.EPSILON) * 100) / 100,
				interest_total: Math.round((running_interest + Number.EPSILON) * 100) / 100,
				cumulative_total: Math.round((running_interest + deposit_total + Number.EPSILON) * 100) / 100
			});
		}
		console.log(computed_years_array);
		total_sum = Math.round((running_total + Number.EPSILON) * 100) / 100
	}

	function setActiveCurrency(element) {
		currency_symbol = element.target.innerText;
	}

</script>

<main>
	<div class="container">
		<div class="row">
		  <div class="col-6 offset-md-3">
			<h1>Interest Calculator</h1>
			
			<form>
				<div class="mb-2 row">
					<label for="currency" class="col-sm-4 col-form-label">Currency</label>
					<div class="col-sm-6">
						<div class="btn-group" role="group" aria-label="Basic example">
							<button type="button" class="btn btn-primary" on:click={setActiveCurrency}>$</button>
							<button type="button" class="btn btn-outline-primary" on:click={setActiveCurrency}>£</button>
							<button type="button" class="btn btn-outline-primary" on:click={setActiveCurrency}>€</button>
							<button type="button" class="btn btn-outline-primary" on:click={setActiveCurrency}>¥</button>
							<button type="button" class="btn btn-outline-primary" on:click={setActiveCurrency}>₹</button>

							<!-- <button id="otherCurrencyDropdown" type="button" class="btn btn-outline-primary dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false">Other</button>
							<ul class="dropdown-menu" aria-labelledby="otherCurrencyDropdown">
								<li>
									<div class="row">
										<label for="otherCurrencySymbol" class="col-sm-6 col-form-label">Custom symbol</label>
										<div class="col-sm-6">
											<div class="input-group">
												<input type="string" id="otherCurrencySymbol" name="otherCurrencySymbol" bind:value={currency_symbol} class="form-control">
											</div>
										</div>
									</div>
								</li>
							</ul>	 -->
						</div>
					</div>
				</div>
				<div class="mb-2 row">
					<label for="initialInvestment" class="col-sm-4 col-form-label">Initial investment</label>
					<div class="col-sm-6">
						<div class="input-group">
							<div class="input-group-prepend">
								<span class="input-group-text">{currency_symbol}</span>
							  </div>
							<input type="number" id="initialInvestment" name="initialInvestment" bind:value={initial_sum} class="form-control">
						</div>
					</div>
				</div>
				<div class="mb-2 row">
					<label for="interestRate" class="col-sm-4 col-form-label">Interest rate</label>
					<div class="col-sm-6">
						<div class="input-group">
							<input type="number" id="interestRate" name="interestRate" bind:value={interest_rate} class="form-control">
							<span class="input-group-text">%</span>
						</div>

					</div>
				</div>
				<div class="mb-2 row">
					<label for="noOfYears" class="col-sm-4 col-form-label">Number of years</label>
					<div class="col-sm-6">
						<input type="number" id="noOfYears" name="noOfYears" bind:value={number_of_years} class="form-control">
					</div>
				</div>
				<div class="mb-2 row">
					<label for="annualDeposit" class="col-sm-4 col-form-label">Annual deposit</label>
					<div class="col-sm-6">
						<input type="number" id="annualDeposit" name="annualDeposit" bind:value={annual_deposit} class="form-control">
					</div>
				</div>
				<input type="button" on:click={CalculateTotal} value="Calculate" class="btn btn-primary">
			</form>

			{#if total_sum}
				<h2> Result</h2>
				<p>Total value after {number_of_years} years: {currency_symbol + total_sum}</p>


				<table class="table">
					<thead>
					  <tr>
						<th scope="col">Year</th>
						<th scope="col">Deposits</th>
						<th scope="col">Interest</th>
						<th scope="col">Cumulative Deposits</th>
						<th scope="col">Cumulative Interest</th>
						<th scope="col">Cumulative Total</th>

					  </tr>
					</thead>
					<tbody>
						{#each computed_years_array as year, i}
						<tr>
							<td >{i}</td>
							<td>{currency_symbol + year.deposit}</td>
							<td>{currency_symbol + year.interest}</td>
							<td>{currency_symbol + year.deposit_total}</td>
							<td>{currency_symbol + year.interest_total}</td>
							<td>{currency_symbol + year.cumulative_total}</td>
						  </tr>
						{/each}

					</tbody>
				  </table>

			{/if}
		  </div>
		</div>
	  </div>
</main>

<style>
</style>