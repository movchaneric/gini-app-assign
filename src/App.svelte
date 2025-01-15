<script>
  import FormLayout from './components/shared/FormLayout.svelte';
  import FormInput from './components/form/FormInput.svelte';
  import FormPhoneInput from './components/form/FormPhoneInput.svelte';
  import Button from './components/shared/Button.svelte';
  
  let formData = {
    firstName: '',
    lastName: '',
    email: '',
    phone: { prefix: '', number: '' },
    password: ""
  }

  let errors = {
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    password: '',
  };

  function resetData() {
    formData.firstName = '';
    formData.lastName = '';
    formData.email = '';
    formData.phone.prefix = '';
    formData.phone.number = '';
    formData.password = '';
  }

  function resetErros(){
      errors.firstName= '';
      errors.lastName= '';
      errors.email= '';
      errors.phone= '';
      errors.password= '';
  };
  

  function validate() {
    resetErros()

    let isValid = true;
    const passwordRegex  = /^(?=.*[!@#$%^&*])[a-zA-Z0-9!@#$%^&*]{8,16}$/

    //first name = no digits and up to 12 chars
    if(!/^[A-Za-z]{1,12}$/.test(formData.firstName)){
      errors.firstName = 'First name must contain only letters and be up to 12 characters.';
      isValid = false
    }else {
      errors.firstName = ""
    }

    //Last name = no digits and up to 15 chars
    if (!/^[A-Za-z]{1,15}$/.test(formData.lastName)) {
      errors.lastName = 'Last name must contain only letters and be up to 15 characters.';
      isValid = false;
    } else {
      errors.lastName = '';
    }

    //Email regex
    const emailRegex = /^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$/;
    if (!emailRegex.test(formData.email)) {
      errors.email = 'Enter a valid email address.';
      isValid = false;
    } else {
      errors.email = '';
    }

    // Phone Number Validation
    if (!/^\d{7}$/.test(formData.phone.number)) {
      console.log("phone-number: ", formData.phone.number)
      errors.phone = 'Phone number must be exactly 7 digits.';
      isValid = false;
    } else {
      errors.phone = '';
    }

     // Password Validation
    if (!passwordRegex.test(formData.password)) {
      errors.password = 'Password must contain a special character and be 8-16 characters long.';
      isValid = false;
    } else {
      errors.password = '';
    }

    return isValid
  }

  function handleSubmit(event) {
    event.preventDefault();
    if (validate()) {
      console.log('Form data:', formData);
      
      //rest
      resetData()
      resetErros()

    } else {
      console.log("form-data:" , formData)
      console.log('Validation errors:', errors);
      
    }
    // resetData()
  }
</script>

<main>
  <FormLayout>
      <form on:submit={handleSubmit}>
        <FormInput 
          label="First name"
          placeholder="Sima"
          type="text"
          value={formData.firstName}
          error={errors.firstName}
          onChange={(val) => {
            formData.firstName = val
            errors.firstName = '';
          }}
        />
        <FormInput 
          label="Last name"
          placeholder="Cohen"
          type="text"
          value={formData.lastName}
          error={errors.lastName}
          onChange={(val) => {
            formData.lastName = val
            errors.lastName = '';
            }}
        />
        <FormInput 
          label="Email"
          type="email"
          placeholder="name@example.com"
          value={formData.email}
          error={errors.email}
          onChange={(val) => {
            formData.email = val
            errors.email = '';
            }}
        />
        <FormPhoneInput 
          label="Phone"
          bind:prefix={formData.phone.prefix}
          bind:number={formData.phone.number}
          onChange={(val) => {
            formData.phone.prefix = val.prefix;
            formData.phone.number = val.number;
            errors.phone = '';
          }}
/>
        {#if errors.phone}
          <span class="error">{errors.phone}</span>
        {/if}

        <FormInput label="password"
                    type="password"
                    placeholder="*******"
                    value={formData.password} 
                    error={errors.password}
                    onChange={(val) => {
                      formData.password = val
                      errors.password = '';
                    }}/> 

        <Button text="Submit"/>
      </form>
  </FormLayout>
</main>

<style>
  .error {
    color: red;
    font-size: 12px;
    margin-top: 4px;
    display: block;
  }
</style>
