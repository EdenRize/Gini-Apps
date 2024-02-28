<script>
  import InputFieldsList from './InputFieldsList.svelte'

  const userInfo = {
    username: '',
    lastName: '',
    email: '',
    phone: { prefix: '', number: '' },
    password: '',
  }
  var formError = ''

  const fields = [
    {
      name: 'username',
      label: 'Username',
      value: userInfo.username,
      placeholder: 'Enter your username',
      isRequired: true,
      regex: /^[a-zA-Z]{2,12}$/,
      errorMsg: 'Username must be between 2 and 12 alphabetical characters.',
    },
    {
      name: 'lastName',
      label: 'Last Name',
      value: userInfo.lastName,
      placeholder: 'Enter your last Name',
      regex: /^[a-zA-Z]{2,15}$/,
      errorMsg: 'Last name must be between 2 and 15 alphabetical characters.',
      isRequired: true,
    },
    {
      name: 'email',
      label: 'Email',
      value: userInfo.email,
      placeholder: 'Enter your email',
      type: 'email',
      regex: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
      errorMsg: 'Invalid email address.',
      isRequired: true,
    },
    {
      name: 'phone',
      label: 'Phone',
      value: userInfo.phone.number,
      placeholder: 'Enter your phone',
      prefixOptions: [
        '050',
        '051',
        '052',
        '053',
        '054',
        '055',
        '056',
        '057',
        '058',
        '059',
      ],
      isPrefixRequired: true,
      regex: /^\d{7}$/,
      errorMsg: 'Phone number must be exactly 7 digits.',
      isRequired: true,
    },
    {
      name: 'password',
      label: 'Password',
      value: userInfo.password,
      placeholder: 'Enter your password',
      type: 'password',
      regex: /^[a-zA-Z0-9!@#$%^&*()_+{}\[\]:;<>,.?\/\\-]+$/,
      errorMsg:
        'Password must ccontain letters, numbers and special characters',
      isRequired: true,
    },
  ]

  const handleSubmit = () => {
    const isDataValid = getIsDataValid()
    if (!isDataValid) return

    console.log('userInfo', userInfo)
    formError = ''
  }

  function getIsDataValid() {
    return fields.every((field) => {
      var fieldToTest
      var isFieldValid

      if (field.name === 'phone') {
        fieldToTest = userInfo.phone.number
        isFieldValid = field.regex.test(fieldToTest) && userInfo.phone.prefix
      } else {
        fieldToTest = userInfo[field.name]
        isFieldValid = field.regex.test(fieldToTest)
      }

      if (!isFieldValid) formError = field.errorMsg

      return isFieldValid
    })
  }

  function onInputChange({ target }) {
    const { name, value } = target

    switch (name) {
      case 'phonePrefix':
        userInfo.phone.prefix = value
        return
      case 'phone':
        userInfo.phone.number = value
        return

      default:
        break
    }

    userInfo[name] = value
  }
</script>

<div class="form-container">
  <form on:submit|preventDefault={handleSubmit}>
    <InputFieldsList {fields} {onInputChange} />

    <button type="submit">Submit</button>
  </form>

  {#if formError}
    <p class="error">{formError}</p>
  {/if}
</div>

<style>
  .form-container {
    position: fixed;
    top: 50%;
    left: 50%;
    translate: -50% -50%;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 400px;
    font-size: 1.5rem;
    font-family: 'Courier New', Courier, monospace;
  }

  .error {
    position: absolute;
    color: red;
    top: 330px;
  }

  button {
    background-color: #4caf50;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    margin-top: 30px;
    font-size: 1.5rem;
    font-family: 'Courier New', Courier, monospace;
  }

  button:hover {
    background-color: #45a049;
  }
</style>
