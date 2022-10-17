<script>
  import Button from "./lib/Button.svelte";
  import FormLabel from "./lib/FormLabel.svelte";
  import LargeButton from "./lib/LargeButton.svelte";
  import Icon from "./lib/Icon.svelte";
</script>

<main>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
      <div class="px-8 py-6 mx-4 mt-4 mb-4 text-left bg-white shadow-lg md:w-1/2 lg:w-1/3 sm:w-1/3">
          <div class="flex justify-center">
            <Icon></Icon>
          </div>
          <h3 class="text-2xl font-bold text-center">Join us</h3>
          <form action="">
                 <FormLabel title={"Nombre"}></FormLabel>
                 <FormLabel title={"Email"}></FormLabel>
                 <FormLabel title={"Contraseña"}></FormLabel>
                 <FormLabel title={"Confirmar Contraseña"}></FormLabel>
                  <span class="text-xs text-red-400">Password must be same!</span>
                  <LargeButton>Crear Cuenta</LargeButton>
                  <div class="mt-6 text-grey-dark">
                      Already have an account?
                      <a class="text-blue-600 hover:underline" href="#">
                          Log in
                      </a>
              </div>
          </form>
      </div>
  </div>
</main>
