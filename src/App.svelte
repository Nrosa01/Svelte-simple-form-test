<script>
  import FormLabel from "./lib/FormLabel.svelte";
  import PasswordLabel from "./lib/PasswordLabel.svelte";
  import LargeButton from "./lib/LargeButton.svelte";
  import Icon from "./lib/Icon.svelte";
  import Texts from "./assets/data/en.json";

  let name = "";
  let email = "";
  let password = "";
  let confirmPassword = "";

  function isEmpty(str) {
    return !str || 0 === str.length;
  }

  function validateEmail(email) {
    var emailRegEx = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;  
    return emailRegEx.test(String(email).toLowerCase());
  }

  function isPassword(password) {
    return /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$/.test(password);
  }

  function isPasswordMatch(password, confirmPassword) {
    return password === confirmPassword;
  }

  function handleSubmission()
  {
    let fieldsNotEmpty = !isEmpty(name) && !isEmpty(email) && !isEmpty(password) && !isEmpty(confirmPassword);
    if(isValidName && isValidEmail && isValidPassword && isValidConfirmPassword && fieldsNotEmpty)
    {
      alert("Cuenta creada")
    }
  }

  function containsSpecialCharacters(str) {
    var format = /[!@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?]+/;
    return format.test(str);
  }

  $: isValidName = name.length >= 4 || isEmpty(name);
  $: isValidEmail = validateEmail(email) || isEmpty(email);
  $: isValidPassword = isPassword(password) || isEmpty(password);
  $: isValidConfirmPassword = isPasswordMatch(password, confirmPassword) || isEmpty(confirmPassword);
</script>

<main>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
      <div class="px-8 py-6 mx-4 mt-4 mb-4 text-left bg-white shadow-lg md:w-1/2 lg:w-1/3 sm:w-1/3">
          <div class="flex justify-center">
            <Icon></Icon>
          </div>
          <h3 class="text-2xl font-bold text-center">LTS</h3>
          <h6 class="text-s text-gray-500 font-semibold text-center">Long Term Suffering</h6>
          <form action="">
                 <FormLabel title={Texts["Name"]} bind:value={name} bind:condition={isValidName}></FormLabel>
                  {#if !isValidName}
                 <span class="text-xs text-red-400 font-medium">{Texts["NameErrorLabel"]}</span>
                  {/if}
                 <FormLabel title={Texts["Email"]} bind:value={email} bind:condition={isValidEmail}>
                </FormLabel>
                  {#if !isValidEmail}
                 <span class="text-xs text-red-400 font-medium">{Texts["EmailErrorLabel"]}</span>
                  {/if}
                 <PasswordLabel title={Texts["Password"]} bind:value={password} bind:condition={isValidPassword}></PasswordLabel>
                 {#if !isValidPassword || containsSpecialCharacters(password)}
                 <div class="inline-flex flex-col">
                  {#if !isValidPassword}
                  <span class="text-xs text-red-400 font-medium">{Texts["PasswordErrorLabel"]}</span>
                    {/if}
                  {#if containsSpecialCharacters(password)}
                    <span class="text-xs text-red-400 font-medium">{Texts["NoSpecialCharacters"]}</span>
                   {/if}
                  </div>
                  {/if}
                 <PasswordLabel title={"Confirmar Contraseña"} bind:value={confirmPassword} bind:condition={isValidConfirmPassword}></PasswordLabel>
                  {#if !isValidConfirmPassword}
                  <span class="text-xs text-red-400 font-medium">{Texts["ConfirmPasswordErrorLabel"]}</span>
                  {/if}
                  <LargeButton on:click={handleSubmission}>{Texts["CreateAccount"]}</LargeButton>
                  <div class="mt-6 text-grey-dark">
                      {Texts["Already have an account?"]}
                      <a class="text-blue-600 hover:underline" href="#">
                          {Texts["Login"]}
                      </a>
              </div>
          </form>
      </div>
  </div>
</main>
