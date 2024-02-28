<script>
  export let name = ''
  export let label = ''
  export let type = 'text'
  export let value = ''
  export let placeholder = ''
  export let onChange
  export let isRequired
  export let prefixOptions = []
  export let isPrefixRequired
</script>

<label>
  <p>{label}:</p>
  <div class="inputs-container">
    {#if prefixOptions.length > 0}
      <select
        required={isPrefixRequired}
        name={name + 'Prefix'}
        on:change={onChange}
      >
        <option value="">--</option>
        {#each prefixOptions as option}
          <option value={option}>{option}</option>
        {/each}
      </select>
    {/if}
    <input
      required={isRequired}
      {type}
      {name}
      {value}
      {placeholder}
      on:input={onChange}
      autocomplete={type === 'password' ? 'current-password' : 'off'}
    />
  </div>
</label>

<style>
  label {
    display: block;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-block-end: 20px;
  }

  .inputs-container {
    display: flex;
    align-items: center;
    width: 200px;
  }

  p {
    margin: 0;
  }

  select {
    width: 80px;
    margin-inline-end: 10px;
  }

  input,
  select {
    width: calc(50% - 5px);
    padding: 8px;
    margin-top: 4px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }

  input {
    width: 100%;
  }

  select {
    width: calc(50% - 5px);
  }
</style>
