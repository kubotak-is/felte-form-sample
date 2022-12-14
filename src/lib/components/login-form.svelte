<script lang="ts">
	import InputLabel from '$lib/components//form/input-label.svelte';
	import InputText from '$lib/components/form/input-text.svelte';
	import SubmitButton from '$lib/components//form/submit-button.svelte';
	import { createForm } from 'felte';
	import { validator } from '@felte/validator-yup';
	import * as yup from 'yup';
	import { descriptive } from 'yup-locale-ja';
	import YupPassword from 'yup-password';

	yup.setLocale(descriptive);
	YupPassword(yup);
	const schema = yup.object({
		email: yup.string().email().required(),
		password: yup
			.string()
			.min(6)
			.max(255)
			.minLowercase(1, 'パスワードには少なくとも1つの小文字が含まれている必要があります')
			.minUppercase(1, 'パスワードには少なくとも1つの大文字が含まれている必要があります')
			.minNumbers(1, 'パスワードには少なくとも1つの数字が含まれている必要があります')
			.minSymbols(1, 'パスワードには少なくとも1つの記号が含まれている必要があります')
			.required()
	});
	const { form, errors, isValid, touched } = createForm<yup.InferType<typeof schema>>({
		extend: validator({ schema })
	});
	$: submitDisabled = $isValid === false && Object.entries($touched).some((result) => result[1]);
</script>

<div class="form-group">
	<h2>Login</h2>
	<form use:form>
		<div class="input-group">
			<InputLabel id="email" label="email" />
			<InputText type="email" name="email" id="email" errorMessages={$errors.email ?? []} />
		</div>
		<div class="input-group">
			<InputLabel id="password" label="password" />
			<InputText
				type="password"
				name="password"
				id="password"
				errorMessages={$errors.password ?? []}
			/>
		</div>
		<div class="button-group">
			<SubmitButton disabled={submitDisabled}>Login</SubmitButton>
		</div>
	</form>
</div>

<style>
	h2 {
		font-size: 2rem;
		font-weight: 700;
		text-align: center;
		color: #babecc;
		text-shadow: 1px 1px 1px #ffffff;
		margin-bottom: 1rem;
	}
	.form-group {
		width: 300px;
		padding: 20px;
	}
	.input-group {
		margin-top: 0.5rem;
	}
	.button-group {
		margin-top: 1.5rem;
	}
</style>
