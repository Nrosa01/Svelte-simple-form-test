<script>
  let count = 0;
  export let text;
  const increment = () => {
    count += 1;
  };
</script>

<button
  on:click={increment}
  type="button"
  data-mdb-ripple="true"
  data-mdb-ripple-color="light"
  class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out"
  >{text} {count}</button
>
