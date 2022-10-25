<script>
  import { scale } from 'svelte/transition';
</script>

<img
  transition:scale="{{delay: 250, duration:500}}"
  class="w-20 h-20 text-blue-600"
  alt="Unity Logo"
  src="unity.svg"
/>

