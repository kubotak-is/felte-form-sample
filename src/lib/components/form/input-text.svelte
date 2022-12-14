<script lang="ts">
	export let name: string;
	export let id: string;
	export let type: 'text' | 'email' | 'password' | 'tel' | 'url';
	export let placeholder: string = '';
	export let disabled: boolean = false;
	export let errorMessages: string[] = [];
	$: hasError = errorMessages.length > 0;
</script>

<input {type} {placeholder} {name} {id} class:error={hasError} {disabled} />
{#if hasError}
	{#each errorMessages as message}
		<p class="error">{message}</p>
	{/each}
{/if}

<style>
	input {
		border: 0;
		outline: 0;
		font-size: 16px;
		border-radius: 16px;
		padding: 8px 16px;
		background-color: #ededed;
		text-shadow: 1px 1px 0 #ffffff;
		margin-right: 16px/2;
		box-shadow: inset 2px 2px 5px #babecc, inset -5px -5px 10px #ffffff;
		width: 100%;
		box-sizing: border-box;
		transition: all 0.2s ease-in-out;
		appearance: none;
		-webkit-appearance: none;
	}
	input:focus {
		box-shadow: inset 1px 1px 2px #babecc, inset -1px -1px 2px #ffffff;
	}
	input:disabled {
		background-color: #d1d1d1;
		box-shadow: inset 2px 2px 5px #babecc, inset -5px -5px 10px #e6e6e6;
	}
	.error {
		color: #ff1313;
	}
	input.error {
		background-color: #ffe4e4;
		box-shadow: inset 2px 2px 5px #ccbabf, inset -5px -5px 10px #fff1f1;
	}
	input.error:focus {
		box-shadow: inset 1px 1px 2px #ccbabf, inset -1px -1px 2px #fff1f1;
	}
	p.error {
		padding: 0.2rem 0;
	}
</style>
