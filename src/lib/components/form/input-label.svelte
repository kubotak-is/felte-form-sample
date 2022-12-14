<script lang="ts">
	export let id: string;
	export let label: string;
</script>

<label for={id}>{label}</label>

<style>
	label {
		display: block;
		margin: 0 0 0.5rem;
		font-size: 1rem;
		font-weight: 400;
		color: #666975;
		text-shadow: 1px 1px 1px #ffffff;
	}
</style>
