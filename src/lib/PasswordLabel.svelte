<script>
  import eye from "/eye.svg";
  import eye_slash from "/eye-slash.svg";
  export let title;
  export let value = "";
  export let condition = false;
  let type = "password"
  let isVisible = false;
  let inputField;
  $: icon = `${isVisible ? eye : eye_slash}`

  function togglePasswordVisibility()
  {
      type = `${isVisible ? "password" : "text"}`;
      inputField.type = type;
      isVisible = !isVisible;
  }

  let conditionMetClass = "focus:ring-blue-600"
  let conditionNotMetClass = "border-red-600 focus:ring-transparent"
  $: classes = `w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 ${condition ? conditionMetClass :conditionNotMetClass}`
</script>

<div class="mt-4">
  <div>
    <label class="block" for="{title}"
      >{title}<label>
        <div class="relative">
          
          <input
          bind:this="{inputField}"
          type="password"
          placeholder="{title}"
          bind:value
          class="{classes}" /> 
          
          <div class="absolute inset-y-0 right-0 flex items-center text-sm leading-5 py-1 mr-2 mt-2 z-10 scale-95 bg-white">
            <button tabindex="-1" type="button" class="w-full h-full text-gray-500 focus:outline-none focus:text-gray-600 m-1 bg-white hover:bg-gray-200 hover:rounded-md duration-200"
            on:click="{() => togglePasswordVisibility()}" href="#">
              <img src="{icon}" alt="eye"/>
            </button>
          </div>
        </div>
  </div>
</div>
