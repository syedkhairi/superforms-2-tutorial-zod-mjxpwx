<script lang="ts" context="module">
  type T = Record<string, unknown>;
</script>
  
<script lang="ts" generics="T extends Record<string, unknown>">
  import { formFieldProxy, type SuperForm, type FormPathLeaves, type Infer } from 'sveltekit-superforms';
  
  export let form: SuperForm<T, unknown>;
  export let field: FormPathLeaves<T>;
  export let label: string;
  export let placeholder: string;

  const { value, errors, constraints } = formFieldProxy(form, field);
</script>

<div>
  <label for={field}>{label}</label>
  <input 
    type="text" 
    name={field}
    bind:value={$value} 
    readonly={false}
    placeholder={placeholder} 
    aria-invalid={$errors ? 'true' : undefined}
    {...$constraints}
    {...$$restProps}
  />
</div>
{#if $errors}
  <p>{$errors}</p>
{/if}
  