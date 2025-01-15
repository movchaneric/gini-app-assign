<script>
  import FormInput from "./FormInput.svelte";

  export let label = '';
  export let prefix = '';
  export let number = '';
  export let onChange = () => {};

  const prefixes = ['050', '052', '054', '058'];

  function handlePrefixChange(event) {
    prefix = event.target.value;
    updateChanges();
  }

  function handleNumberChange(event) {
    number = event.target.value;
    updateChanges();
  }

  function updateChanges() {
    onChange({ prefix, number });
  }
</script>

<div class="phone-input">
  <label>{label}</label>
  <div class="flex items-center gap-2">
    <select bind:value={prefix} on:change={handlePrefixChange}>
      <option value="" disabled hidden>050</option>
      {#each prefixes as p}
        <option value={p}>{p}</option>
      {/each}
    </select>
    <FormInput
      type="number"
      placeholder="1234567"
      value={number}
      onChange={(val) => handleNumberChange({ target: { value: val } })}
    />
  </div>
</div>

<style>
  .phone-input {
    display: flex;
    flex-direction: column;
    
  }
  select, input {
    margin-top: 5px;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  label {
    display: block;
    margin-bottom: 8px;
    font-weight: bold;
  }
</style>
