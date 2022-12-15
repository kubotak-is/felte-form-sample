<script lang="ts">
	import InputRadio from './form/input-radio.svelte';
	import InputLabel from '$lib/components/form/input-label.svelte';
	import InputText from '$lib/components/form/input-text.svelte';
	import SubmitButton from '$lib/components/form/submit-button.svelte';
	import { createForm } from 'felte';
	import { validator } from '@felte/validator-yup';
	import * as yup from 'yup';
	import { descriptive } from 'yup-locale-ja';

	yup.setLocale(descriptive);
	const schema = yup.object({
		has_secret: yup.string().required(),
		secret: yup
			.string()
			.max(20)
			.when('has_secret', {
				is: '1',
				then: (schema) => schema.required()
			})
	});
	const { form, data, errors, isValid, touched } = createForm<yup.InferType<typeof schema>>({
		extend: validator({ schema })
	});
	$: submitDisabled = $isValid === false && Object.entries($touched).some((result) => result[1]);
</script>

<div class="form-group">
	<h2>Required If</h2>
	<form use:form>
		<div class="input-group">
			<p>秘密の質問を設定する</p>
			<InputRadio
				name="has_secret"
				radioList={[
					{ value: '1', label: 'Yes', id: 'yes' },
					{ value: '0', label: 'No', id: 'no' }
				]}
				errorMessages={$errors.has_secret ?? []}
			/>
		</div>
		<div class="input-group">
			<InputLabel id="secret" label="ペットの名前は？" />
			<InputText
				type="text"
				name="secret"
				id="secret"
				errorMessages={$errors.secret ?? []}
				disabled={$data.has_secret !== '1'}
			/>
		</div>
		<div class="button-group">
			<SubmitButton disabled={submitDisabled}>Submit</SubmitButton>
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
	p {
		font-size: 1rem;
		font-weight: 400;
		margin: 0 0 0.5rem;
		color: #666975;
		text-shadow: 1px 1px 1px #ffffff;
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
