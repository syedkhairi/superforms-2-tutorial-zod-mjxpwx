<script lang="ts">
  import { superForm } from 'sveltekit-superforms';
  import SuperDebug from 'sveltekit-superforms';
	import Input from '$lib/Input.svelte';

  export let data;

  const supForm = superForm(data.form);
	const { form, enhance, delayed, tainted, errors } = supForm;
</script>

<SuperDebug data={$form} />

<form method="POST" use:enhance>
	<Form form={supForm} />
	<label for="name">Name</label>
	<input
		type="text"
		name="name"
		aria-invalid={$errors.name ? 'true' : undefined}
		bind:value={$form.name}
		{...$constraints.name}
	/>
	{#if $errors.name}<span class="invalid">{$errors.name}</span>{/if}

	<label for="email">E-mail</label>
	<input
		type="email"
		name="email"
		aria-invalid={$errors.email ? 'true' : undefined}
		bind:value={$form.email}
		{...$constraints.email}
	/>
	{#if $errors.email}<span class="invalid">{$errors.email}</span>{/if}

	<div><button>Submit</button></div>
</form>

<div style="margin-top:2rem;">
	<a target="_blank" href="https://superforms.rocks/get-started">Tutorial for this example here</a>
</div>

<style>
	.invalid {
		color: red;
	}
</style>
