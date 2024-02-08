<script>
  export let URL_List;
  export let active;
  import LogoMin from "/logo-min.svg";
  import { flip } from "svelte/animate";
  function handleOnSubmit(e) {
    e.preventDefault();
    const textarea = document.querySelector("textarea");
    URL_List = textarea.value;
    /*    alert("Generando URLs..."); */
    active = true;
  }
</script>

<div
  class="flex flex-grow items-center justify-center h-full text-gray-600 dark:text-gray-300 bg-gray-100 dark:bg-slate-900"
>
  <div
    class="max-w-full p-8 bg-white dark:bg-slate-700 dark:border-2 dark:border-orange-900 rounded-lg shadow-lg w-96"
  >
    <div class="flex items-center mb-6">
      <img src={LogoMin} class="size-12" alt="Vite Logo" />
      <h4 class="font-semibold ml-3 text-lg">Pega todas las URLs</h4>
    </div>

    <div>
      <form
        class="overflow-hidden rounded-lg border border-gray-200 shadow-sm focus-within:border-blue-600 focus-within:ring-2 focus-within:ring-blue-600"
        on:submit={handleOnSubmit}
      >
        <textarea
          class="w-full p-4 h-full resize-none border-none align-top focus:ring-0 sm:text-sm dark:bg-zinc-800"
          rows="15"
          placeholder="Pega todas las URLs en formato texto"
        ></textarea>

        <div
          class="flex items-center justify-end gap-3 bg-white dark:bg-zinc-800 p-3"
        >
          <button
            type="reset"
            class="rounded bg-gray-200 px-3 py-1.5 text-sm font-medium text-gray-700 hover:bg-gray-300"
          >
            Borrar
          </button>

          <button
            type="submit"
            class="rounded bg-indigo-600 px-3 py-1.5 text-sm font-medium text-white hover:bg-indigo-700"
          >
            Anadir
          </button>
        </div>
      </form>
    </div>
  </div>
</div>

<style>
  textarea {
    border: none;
    outline: none;
  }
</style>
