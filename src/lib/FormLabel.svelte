<script>
  export let title;
  export let value = "";
  export let condition = false;
  export let type = "text"
  export let ref = null;

  // Como type es estatico, hay que usar este hack
  function typeAction(node) {
        node.type = type;
    }

    let conditionMetClass = "focus:ring-blue-600"
    let conditionNotMetClass = "border-red-600 focus:ring-transparent"
    $: classes = `w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 ${condition ? conditionMetClass :conditionNotMetClass}`
</script>

<div class="mt-4">
  <div>
    <label class="block" for="{title}"
      >{title}<label>
        <input
          bind:this="{ref}"
          use:typeAction
          placeholder="{title}"
          bind:value
          class="{classes}" />
  </div>
</div>
