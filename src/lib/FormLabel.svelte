<script>
  export let title;
  export let value = "";
  export let condition = false;
  export let type = "text"

  // Como type es estatico, hay que usar este hack
  function typeAction(node) {
        node.type = type;
    }

  let conditionMetClass = "w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
  let conditionNotMetClass = "w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-red-600"
</script>

<div class="mt-4">
  <div>
    <label class="block" for="{title}"
      >{title}<label>
        <input
          use:typeAction
          placeholder="{title}"
          bind:value
          class="{condition ? conditionMetClass : conditionNotMetClass}" />
  </div>
</div>
