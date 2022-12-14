<script lang="ts">
	export let name: string;
	export let radioList: { value: string; label: string; id: string }[];
	export let errorMessages: string[] = [];
	$: hasError = errorMessages.length > 0;
</script>

<div class="radio-group">
	{#each radioList as radio}
		<div class="radio">
			<input type="radio" {name} value={radio.value} id={radio.id} />
			<label for={radio.id}>{radio.label}</label>
		</div>
	{/each}
</div>
{#if hasError}
	{#each errorMessages as message}
		<p class="error">{message}</p>
	{/each}
{/if}

<style>
	.radio-group {
		display: flex;
		gap: 1rem;
	}
	.radio {
		display: flex;
		gap: 0.5rem;
		align-items: center;
	}
	input {
		width: 20px;
		height: 20px;
		background-color: #ededed;
		text-shadow: 1px 1px 0 #ffffff;
		font-weight: bold;
		box-shadow: -3px -3px 10px #ffffff, 3px 3px 10px #babecc;
		border-radius: 100%;
	}
	input,
	label {
		cursor: pointer;
	}
	input:checked {
		background-color: #cfcfcf;
		box-shadow: inset 1px 1px 2px #babecc, inset -1px -1px 2px #ffffff;
	}
	label {
		font-size: 1rem;
		font-weight: 400;
		color: #666975;
		text-shadow: 1px 1px 1px #ffffff;
	}
	.error {
		color: #ff1313;
	}
	p.error {
		padding: 0.2rem 0;
	}
</style>
