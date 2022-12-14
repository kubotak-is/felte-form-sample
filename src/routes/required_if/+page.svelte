<script lang="ts">
	import RequiredIfForm from '$lib/components/required-if-form.svelte';
</script>

<div class="container">
	<div class="card">
		<RequiredIfForm />
	</div>
</div>

<style>
	.container {
		display: grid;
		place-content: center;
		height: 100%;
	}
	.card {
		border-radius: 20px;
		background: #ededed;
		box-shadow: 20px 20px 35px #c9c9c9, -20px -20px 35px #ffffff;
		padding: 1rem;
	}
</style>
