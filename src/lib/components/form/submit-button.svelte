<script lang="ts">
	export let disabled: boolean = false;
</script>

<button type="submit" {disabled}>
	<slot />
</button>

<style>
	button {
		width: 100%;
		text-align: center;
		border: 0;
		outline: 0;
		font-size: 16px;
		border-radius: 16px;
		padding: 8px 16px;
		background-color: #ededed;
		text-shadow: 1px 1px 0 #ffffff;
		margin-right: 16px/2;
		color: #61677c;
		font-weight: bold;
		box-shadow: -3px -3px 10px #ffffff, 3px 3px 10px #babecc;
		transition: all 0.2s ease-in-out;
		cursor: pointer;
		font-weight: 600;
	}
	button:disabled {
		background-color: #dedede;
	}
	button:not(:disabled):hover {
		box-shadow: -2px -2px 5px #ffffff, 2px 2px 5px #babecc;
	}
	button:not(:disabled):active {
		box-shadow: inset 1px 1px 2px #babecc, inset -1px -1px 2px #ffffff;
	}
</style>
