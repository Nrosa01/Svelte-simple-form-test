<script>
  import eye from "/eye.svg";
  import eye_slash from "/eye-slash.svg";
  export let title;
  export let value = "";
  export let condition = false;
  let type = "password"
  let isVisible = false;
  let icon = eye;
  let cNode;

  // Como type es estatico, hay que usar este hack
  function typeAction(node) {
        node.type = type;
        cNode = node;
    }

  function togglePasswordVisibility()
  {
      if (isVisible)
      {
          type = "password";
          icon = eye;
          typeAction(cNode);
      }
      else
      {
          type = "text";
          icon = eye_slash;
          typeAction(cNode);
      }

      isVisible = !isVisible;
  }

  let conditionMetClass = "w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600 z-20"
  let conditionNotMetClass = "w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-red-600 z-20"
</script>

<div class="mt-4">
  <div>
    <label class="block" for="{title}"
      >{title}<label>
        <div class="relative">
          
          <input
          use:typeAction
          placeholder="{title}"
          bind:value
          class="{condition ? conditionMetClass : conditionNotMetClass}" /> 
          
          <div class="absolute inset-y-0 right-0 flex items-center text-sm leading-5 py-1 mr-2 mt-2 z-10 scale-95 bg-white">
            <button class="w-full h-full text-gray-500 focus:outline-none focus:text-gray-600 m-1 bg-white hover:bg-gray-200 hover:rounded-md duration-200"
            on:click="{() => togglePasswordVisibility()}">
              <img src="{icon}" alt="eye"/>
            </button>
          </div>
        </div>
  </div>
</div>
