<script>
  import Logo from "./components/Logo.svelte";
  import AllURLContainer from "./components/AllURLContainer.svelte";
  import SeparateURLContainer from "./components/SeparateURLContainer.svelte";
  export let active = false;
  export let URL_List = "";
</script>

<main class="container p-6 mx-auto dark:text-red-500 ">
  <Logo />
  <main
    class=" mx-2 flex md:flex-row flex-col items-baseline justify-center font-medium md:gap-4 gap-12"
  >
    <AllURLContainer bind:URL_List bind:active />
    <SeparateURLContainer {URL_List} bind:active />
  </main>
</main>

<style>
</style>
