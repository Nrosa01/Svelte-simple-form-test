<script>
  import FormLabel from "./lib/FormLabel.svelte";
  import PasswordLabel from "./lib/PasswordLabel.svelte";
  import LargeButton from "./lib/LargeButton.svelte";
  import Icon from "./lib/Icon.svelte";
  import Texts from "./assets/data/en.json";
  import { slide } from 'svelte/transition';
  import { scale } from 'svelte/transition';
  
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
  $: fieldsNotEmpty = !isEmpty(name) && !isEmpty(email) && !isEmpty(password) && !isEmpty(confirmPassword);
  $: isFormValid = isValidName && isValidEmail && isValidPassword && isValidConfirmPassword && fieldsNotEmpty;
</script>

<main>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
      <div transition:scale="{{duration: 500, delay: 50}}" class="px-8 py-6 mx-4 mt-4 mb-4 text-left bg-white shadow-lg md:w-1/2 lg:w-1/3 sm:w-1/3">
          <div class="flex justify-center">
            <Icon></Icon>
          </div>
          <h3 transition:scale="{{delay: 350, duration:500}}" class="text-2xl font-bold text-center">LTS</h3>
          <h6 transition:scale="{{delay: 450, duration:500}}" class="text-s text-gray-500 font-semibold text-center">Long Term Suffering</h6>
          <form action="">
                 <FormLabel focused title={Texts["Name"]} bind:value={name} bind:condition={isValidName}></FormLabel>
                  {#if !isValidName}
                 <div transition:slide class="text-xs text-red-400 font-medium">{Texts["NameErrorLabel"]}</div>
                  {/if}
                 <FormLabel title={Texts["Email"]} bind:value={email} bind:condition={isValidEmail}>
                </FormLabel>
                  {#if !isValidEmail}
                 <div transition:slide class="text-xs text-red-400 font-medium">{Texts["EmailErrorLabel"]}</div>
                  {/if}
                 <PasswordLabel title={Texts["Password"]} bind:value={password} bind:condition={isValidPassword}></PasswordLabel>
                 {#if !isValidPassword || containsSpecialCharacters(password)}
                 <div class="inline-flex flex-col">
                  {#if !isValidPassword}
                  <div transition:slide class="text-xs text-red-400 font-medium">{Texts["PasswordErrorLabel"]}</div>
                    {/if}
                  {#if containsSpecialCharacters(password)}
                    <div transition:slide class="text-xs text-red-400 font-medium">{Texts["NoSpecialCharacters"]}</div>
                   {/if}
                  </div>
                  {/if}
                 <PasswordLabel title={"Confirmar Contraseña"} bind:value={confirmPassword} bind:condition={isValidConfirmPassword}></PasswordLabel>
                  {#if !isValidConfirmPassword}
                  <div transition:slide class="text-xs text-red-400 font-medium">{Texts["ConfirmPasswordErrorLabel"]}</div>
                  {/if}
                    <LargeButton bind:canBeClicked={isFormValid} on:click={handleSubmission}>{Texts["CreateAccount"]}</LargeButton>
                  <div class="mt-6 text-grey-dark">
                      {Texts["Already have an account?"]}
                      <a class="text-blue-600 hover:underline" href="#/">
                          {Texts["Login"]}
                      </a>
              </div>
          </form>
      </div>
  </div>
</main>
