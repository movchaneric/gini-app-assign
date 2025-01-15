<script>
  export let label = '';
  export let type = 'text';
  export let value = '';
  export let placeholder = '';
  export let error = '';
  export let onChange = (evnet) => {};

  function handleInput(event) {
    onChange(event.target.value); 
  }
</script>


<div class="form-input">
    <label>{label}</label>
    <input
      type={type}
      bind:value
      placeholder={placeholder}
      on:input={handleInput}
    />

    {#if error}
      <span class="error">{error}</span>
    {/if}
</div>
  

<style>
    .input-container {
      margin-bottom: 16px;
    }
    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
    }
    input {
      width: 100%;
      padding: 6px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    .error {
      color: red;
      font-size: 12px;
      margin-top: 4px;
    }
  </style>