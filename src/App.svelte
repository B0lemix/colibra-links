<script>
  import Logo from "./components/Logo.svelte";
  import AllURLContainer from "./components/AllURLContainer.svelte";
  import SeparateURLContainer from "./components/SeparateURLContainer.svelte";
  export let active =false
  export let URL_List = "";
</script>

<main class="container mx-auto ">

  <Logo />
  <main class=" mx-2 flex items-center justify-center font-medium">
    <AllURLContainer bind:URL_List bind:active />
    <SeparateURLContainer   {URL_List}  />
  </main>
</main>

<style>
/* 	.inactive {
		display: none;
	} */

	.active {
    display: block;
	}
</style>