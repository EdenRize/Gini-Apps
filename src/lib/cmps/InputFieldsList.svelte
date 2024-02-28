<script>
  import InputField from './InputField.svelte'

  export let fields = []
  export let onInputChange
</script>

<ul>
  {#each fields as field}
    <li>
      <InputField
        name={field.name}
        label={field.label}
        type={field.type || 'text'}
        placeholder={field.placeholder}
        value={field.value}
        isRequired={field.isRequired}
        prefixOptions={field.prefixOptions}
        isPrefixRequired={field.isPrefixRequired}
        onChange={onInputChange}
      />
    </li>
  {/each}
</ul>

<style>
  ul {
    all: unset;
    width: 100%;
  }
  li {
    all: unset;
  }
</style>
