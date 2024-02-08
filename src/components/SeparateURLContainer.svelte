<script>
// @ts-nocheck

  import { fly } from "svelte/transition";
  import LogoMin from "/logo-min.svg";
  export let URL_List;
  export let active;
  let separateURLS;

  function corregirUrls(url) {
    // Eliminar el texto antes de "https://"
    url = url.replace(/.*?https:\/\//, "https://");
    url = url.replace(/.*?http:\/\//, "http://");
    url = url.replace(/.*?ftp:\/\//, "ftp://");

    // Si hay dos URLs en la misma línea, quedarse solo con la primera
    url = url.split("https://")[1] || url;
    url = url.split("http://")[1] || url;

    // Eliminar "\" al inicio de la URL
    url = url.replace(/^\//, "");

    // Agregar "http://" si la URL no tiene un prefijo
    if (!url.startsWith("http://") && !url.startsWith("https://")) {
      url = "http://" + url;
    }
    return url;
  }

  function separarURLs(inputText) {
    // Limpiar el array antes de cada separación
    separateURLS = [];

    // Dividir el texto en líneas
    /* const lineas = inputText.split(/(https?:\/\/(www\.)?[-a-zA-Z0-9@:%._+~#=]{1,256}\.[\da-zA-Z]{2,}\b([-a-zA-Z0-9@:%_+.~#?&//=,]*))/gi).filter(Boolean); */
    const lineas = inputText
      .split(
        /(https?:\/\/(www\.)?[-a-zA-Z0-9@:%._+~#=]{1,256}\.[\da-zA-Z]{2,}\b([-a-zA-Z0-9@:%_+.~#?&/=,]*))/gi
      )
      .filter(Boolean);

    console.log(lineas, "lineas");
    let urlsCorregidas = lineas.map(corregirUrls);

    console.log(urlsCorregidas, "lineaurlsCorregidass");
    // Filtrar las líneas para obtener solo las URL válidas
    const urlsValidas = urlsCorregidas.filter((linea) => isValidURL(linea));

    // Agregar las URL válidas al array
    separateURLS = [...separateURLS, ...urlsValidas];
  }

  function isValidURL(url) {
    // Validar la URL utilizando una expresión regular simple
    /* const urlRegex = /(https?:\/\/(www\.)?[-a-zA-Z0-9@:%._+~#=]{1,256}\.[\da-zA-Z]{2,}\b([-a-zA-Z0-9@:%_+.~#?&//=,]*))/gi; */
    const urlRegex =
      /(https?:\/\/(www\.)?[-a-zA-Z0-9@:%._+~#=]{1,256}\.[\da-zA-Z]{2,}\b([-a-zA-Z0-9@:%_+.~#?&//=,]*))/gi;
    return urlRegex.test(url);
  }

  function checkCheckbox(i) {
    // Obtén el elemento de input correspondiente al índice
    const checkbox = document.getElementById("checkbox" + i);
    if (checkbox) {
      // Marca el checkbox como checked
      checkbox.checked = true;
    }
  }

  $: {
    separarURLs(URL_List);
    console.log("the component has mounted", separateURLS);
  }
</script>

{#if active}
  <div
    class="flex flex-grow items-center justify-center h-full text-gray-600 dark:text-gray-300 bg-gray-100 dark:bg-slate-900"
    in:fly={{ x: 200, duration: 2000 }}
  >
    <div
      class="max-w-full p-8 bg-white dark:bg-zinc-800 rounded-lg shadow-lg w-96 dark:border-2 dark:border-orange-900"
    >
      <div class="flex items-center mb-6">
        <img src={LogoMin} class="size-12" alt="Vite Logo" />
        <h4 class="font-semibold ml-3 text-lg">Lista URLs</h4>
      </div>
      {#if separateURLS.length == 0}
        No hay URLs válidas para mostrar.
      {/if}
      {#each separateURLS as URL, i}
        <div>
          <input class="hidden" id={"checkbox" + i} type="checkbox" />
          <label
            class="flex items-center h-10 px-2 rounded cursor-pointer hover:bg-gray-100 dark:hover:dark:bg-zinc-600"
            for={"checkbox" + i}
          >
            <span
              class="flex items-center justify-center w-5 h-5 text-transparent border-2 border-gray-300 rounded-full"
            >
              <svg
                class="w-4 h-4 fill-current"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                  clip-rule="evenodd"
                />
              </svg>
            </span>
            <span class="ml-4 text-sm">
              <button on:click={() => checkCheckbox(i)}>
                <a target="_blank" href={URL} id={i}>{URL}</a>
              </button>
            </span>
          </label>
        </div>
      {/each}
    </div>
  </div>
{/if}

<style>
  input[type="checkbox"]:checked + label span:first-of-type {
    background-color: #10b981;
    border-color: #10b981;
    color: #fff;
  }
  input[type="checkbox"]:checked + label a {
    text-decoration: line-through;
    color: #9ca3af;
  }

  /*   input[type="checkbox"]:checked + label span:nth-of-type(2) {
    text-decoration: line-through;
    color: #9ca3af;
  } */
</style>
