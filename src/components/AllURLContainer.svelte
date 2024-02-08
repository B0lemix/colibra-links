<script>
  export let URL_List;

  function handleOnSubmit(e) {
    e.preventDefault();
    const textarea = document.querySelector("textarea");
    URL_List = textarea.value;
    alert("Generando URLs...");
  }
</script>

<div
  class="flex flex-grow items-center justify-center h-full text-gray-600 bg-gray-100"
>
  <!-- Component Start -->
  <div class="max-w-full p-8 bg-white rounded-lg shadow-lg w-96">
    <div class="flex items-center mb-6">
      <svg
        class="h-8 w-8 text-indigo-500 stroke-current"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4"
        />
      </svg>
      <h4 class="font-semibold ml-3 text-lg">Pega todas las URLs</h4>
    </div>

    <div>
      <form
        class="overflow-hidden rounded-lg border border-gray-200 shadow-sm focus-within:border-blue-600 focus-within:ring-2 focus-within:ring-blue-600"
        on:submit={handleOnSubmit}
      >
        <textarea
          class="w-full p-4 h-full resize-none border-none align-top focus:ring-0 sm:text-sm"
          rows="10"
          placeholder="Pega todas las URLs en formato texto"
        ></textarea>

        <div class="flex items-center justify-end gap-3 bg-white p-3">
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
  <!-- Component End  -->
</div>

<style>
  textarea {
    border: none;
    outline: none;
  }
</style>
