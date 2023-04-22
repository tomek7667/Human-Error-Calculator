<script lang="ts">
	enum K1 {
		SimpleRoutine = 0.001,
		RequiringAttention = 0.01,
		NotRoutine = 0.1
	}

	enum K2Routine {
		TwoSeconds = 10,
		TenSeconds = 1,
		TwentySeconds = 0.5
	}

	enum K2NonRoutine {
		ThreeSeconds = 10,
		ThirtySeconds = 1,
		FortyFiveSeconds = 0.3,
		SixtySeconds = 0.1
	}

	enum K3 {
		Expert = 0.5,
		Average = 1,
		PoorlyTrained = 3
	}

	enum K4 {
		GraveEmergency = 3,
		PotentialEmergency = 2,
		NormalSituation = 1
	}

	enum K5 {
		Excellent = 0.7,
		Good = 1,
		DiscreteDiscrete = 3,
		DiscretePoor = 7,
		VerryPoor = 10
	}

	interface Parameters {
		K1: number;
		K2: number;
		K3: number;
		K4: number;
		K5: number;
		isRoutine: boolean;
		calculateResult: () => number;
	}

	const parameters: Parameters = {
		K1: K1.SimpleRoutine,
		K2: K2Routine.TenSeconds,
		K3: K3.Average,
		K4: K4.NormalSituation,
		K5: K5.Good,
		isRoutine: true,
		calculateResult: () => {
			return (
				Math.round(
					parameters.K1 * parameters.K2 * parameters.K3 * parameters.K4 * parameters.K5 * 1000000
				) / 1000000
			);
		}
	};
</script>

<section class="section">
	<div class="container">
		<img class="image is-center" src="favicon.png" alt="Logo" />
		<h1 class="title">Human error calculator</h1>
		<p class="subtitle">
			This is a calculator for human error. It is based on the TESEO method provided in Data Quality
			Assurance lectures.
		</p>
		<h1 class="subtitle">
			Result - There is probability of {parameters.calculateResult() * 100}% of human error
			happening.
		</h1>
		<hr />
		<div class="control">
			<p>
				1. Is the action a routine? <input type="checkbox" bind:checked={parameters.isRoutine} />
			</p>
		</div>
		<hr />
		<div class="control">
			<p>2. What's the type of the activity?</p>
			<label class="radio">
				<input type="radio" name="K1" bind:group={parameters.K1} value={K1.SimpleRoutine} />
				Simple, a routine for the operator
			</label>
			<label class="radio">
				<input type="radio" name="K1" bind:group={parameters.K1} value={K1.RequiringAttention} />
				Requiring attention
			</label>
			<label class="radio">
				<input type="radio" name="K1" bind:group={parameters.K1} value={K1.NotRoutine} />
				Complex, pretty new to the operator
			</label>
		</div>
		<hr />
		<div class="control">
			<p>3. What's the time available for completion of task?</p>
			{#if parameters.isRoutine}
				<label class="radio">
					<input type="radio" name="K2" bind:group={parameters.K2} value={K2Routine.TwoSeconds} />
					&lt;= 2 seconds
				</label>
				<label class="radio">
					<input type="radio" name="K2" bind:group={parameters.K2} value={K2Routine.TenSeconds} />
					10 seconds
				</label>
				<label class="radio">
					<input
						type="radio"
						name="K2"
						bind:group={parameters.K2}
						value={K2Routine.TwentySeconds}
					/>
					&gt;= 20 seconds
				</label>
			{:else}
				<label class="radio">
					<input
						type="radio"
						name="K2"
						bind:group={parameters.K2}
						value={K2NonRoutine.ThreeSeconds}
					/>
					&lt;= 3 seconds
				</label>
				<label class="radio">
					<input
						type="radio"
						name="K2"
						bind:group={parameters.K2}
						value={K2NonRoutine.ThirtySeconds}
					/>
					30 seconds
				</label>
				<label class="radio">
					<input
						type="radio"
						name="K2"
						bind:group={parameters.K2}
						value={K2NonRoutine.FortyFiveSeconds}
					/>
					&gt;= 45 seconds
				</label>
			{/if}
		</div>
		<hr />
		<div class="control">
			<p>4. What are the operator qualities?</p>
			<label class="radio">
				<input type="radio" name="K3" bind:group={parameters.K3} value={K3.Expert} />
				Carefully selected, expert, well trained
			</label>
			<label class="radio">
				<input type="radio" name="K3" bind:group={parameters.K3} value={K3.Average} />
				Average knowledge and training
			</label>
			<label class="radio">
				<input type="radio" name="K3" bind:group={parameters.K3} value={K3.PoorlyTrained} />
				Little knowledge, poorly trained
			</label>
		</div>
		<hr />
		<div class="control">
			<p>5. What's the emergency of the situation?</p>
			<label class="radio">
				<input type="radio" name="K4" bind:group={parameters.K4} value={K4.GraveEmergency} />
				Situation of grave emergency
			</label>
			<label class="radio">
				<input type="radio" name="K4" bind:group={parameters.K4} value={K4.PotentialEmergency} />
				Situation of potential emergency
			</label>
			<label class="radio">
				<input type="radio" name="K4" bind:group={parameters.K4} value={K4.NormalSituation} />
				Normal situation
			</label>
		</div>
		<hr />
		<div class="control">
			<p>6. What's the familiarity of the UI? Wha'ts the activity ergonomic factor?</p>
			<label class="radio">
				<input type="radio" name="K5" bind:group={parameters.K5} value={K5.Excellent} />
				Excellent model, good interface with plant
			</label>
			<label class="radio">
				<input type="radio" name="K5" bind:group={parameters.K5} value={K5.Good} />
				Good model, good interface with plant
			</label>
			<label class="radio">
				<input type="radio" name="K5" bind:group={parameters.K5} value={K5.DiscreteDiscrete} />
				Discrete model, discrete interface with plant
			</label>
			<label class="radio">
				<input type="radio" name="K5" bind:group={parameters.K5} value={K5.DiscretePoor} />
				Discrete model, poor interface with plant
			</label>
			<label class="radio">
				<input type="radio" name="K5" bind:group={parameters.K5} value={K5.VerryPoor} />
				Very poor model, poor interface with plant
			</label>
		</div>
		<hr />
		<h1 class="subtitle">
			Result - There is probability of {parameters.calculateResult() * 100}% of human error
			happening.
		</h1>
	</div>
</section>
