<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-2xl font-bold mb-4">Lista de Socios</h1>

    <!-- drawer init and toggle -->
    <div class="text-center">
      <button
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
        type="button"
        data-drawer-target="drawer-right-example"
        data-drawer-show="drawer-right-example"
        data-drawer-placement="right"
        aria-controls="drawer-right-example"
      >
        Show right drawer
      </button>
    </div>

    <!-- drawer component -->
    <div
      id="drawer-right-example"
      class="fixed top-10 right-0 z-40 h-screen p-4 overflow-y-auto transition-transform translate-x-full bg-white w-80 dark:bg-gray-800"
      tabindex="-1"
      aria-labelledby="drawer-right-label"
    >
      <h5
        id="drawer-right-label"
        class="inline-flex items-center mb-4 text-base font-semibold text-gray-500 dark:text-gray-400"
      >
        <svg
          class="w-5 h-5 mr-2"
          aria-hidden="true"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z"
            clip-rule="evenodd"
          ></path></svg
        >Right drawer
      </h5>
      <button
        type="button"
        data-drawer-hide="drawer-right-example"
        aria-controls="drawer-right-example"
        class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 absolute top-2.5 right-2.5 inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white"
      >
        <svg
          aria-hidden="true"
          class="w-5 h-5"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
            clip-rule="evenodd"
          ></path>
        </svg>
        <span class="sr-only">Close menu</span>
      </button>
      <p class="mb-6 text-sm text-gray-500 dark:text-gray-400">
        Supercharge your hiring by taking advantage of our
        <a
          href="#"
          class="text-blue-600 underline font-medium dark:text-blue-500 hover:no-underline"
          >limited-time sale</a
        >
        for Flowbite Docs + Job Board. Unlimited access to over 190K top-ranked
        candidates and the #1 design job board.
      </p>
      <div class="grid grid-cols-2 gap-4">
        <a
          href="#"
          class="px-4 py-2 text-sm font-medium text-center text-gray-900 bg-white border border-gray-200 rounded-lg focus:outline-none hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700"
          >Learn more</a
        >
        <a
          href="#"
          class="inline-flex items-center px-4 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
          >Get access
          <svg
            class="w-4 h-4 ml-2"
            aria-hidden="true"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z"
              clip-rule="evenodd"
            ></path></svg
        ></a>
      </div>
    </div>

    <!-- Búsqueda de socio por DNI -->
    <div class="mt-8">
      <h2 class="text-lg font-bold mb-2">Buscar socio por DNI:</h2>
      <form @submit.prevent="buscarSocio">
        <div class="flex items-center">
          <input
            type="text"
            v-model="dni"
            class="border border-gray-300 p-2 rounded-l-md focus:outline-none focus:border-blue-500"
            placeholder="Buscar por DNI"
          />
          <button
            type="submit"
            class="bg-blue-500 text-white px-4 py-2 rounded-r-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600"
          >
            Buscar
          </button>
        </div>
      </form>

      <!-- Lista de socios -->
      <div v-if="sociosFiltrados.length > 0" class="mt-4">
        <div class="table-container mt-4 overflow-x-auto">
          <table class="w-full bg-white border border-gray-300">
            <thead class="bg-gray-50">
              <tr>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Nombre
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Apellido
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  DNI
                </th>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  ACCIONES
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
              <tr v-for="(socio, index) in sociosFiltrados" :key="socio.dni">
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm font-medium text-gray-900">
                    {{ socio.nombre }}
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-500">{{ socio.apellido }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-500">{{ socio.dni }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="inline-flex rounded-md shadow-sm" role="group">
                    <button
                      type="button"
                      class="px-4 py-2 text-sm font-medium text-gray-900 bg-transparent border border-gray-900 rounded-l-lg hover:bg-gray-900 hover:text-white focus:z-10 focus:ring-2 focus:ring-gray-500 focus:bg-gray-900 focus:text-white dark:border-white dark:text-white dark:hover:text-white dark:hover:bg-gray-700 dark:focus:bg-gray-700"
                      @click="cargarRecibo(socio.dni)"
                    >
                      Cargar recibo
                    </button>
                    <button
                      type="button"
                      class="px-4 py-2 text-sm font-medium text-gray-900 bg-transparent border border-gray-900 rounded-r-md hover:bg-gray-900 hover:text-white focus:z-10 focus:ring-2 focus:ring-gray-500 focus:bg-gray-900 focus:text-white dark:border-white dark:text-white dark:hover:text-white dark:hover:bg-gray-700 dark:focus:bg-gray-700"
                      @click="editarSocio(socio)"
                    >
                      Editar
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <div v-else class="mt-4">
        <p>No se encontraron socios.</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, watch, onMounted } from "vue"; // Import the `watch` function
import { useRouter } from "vue-router";
import socioService from "../../services/socioService";
import { initFlowbite, initDropdowns } from "flowbite";

export default {
  name: "ListSocio",
  setup() {
    const dni = ref("");
    const socios = ref([]);
    const router = useRouter();

    // Obtener la lista de socios del servicio socioService al montar el componente
    socios.value = socioService.getSocios();

    // Filtrar la lista de socios basado en el valor de dni
    const sociosFiltrados = ref([]);
    const filtrarSocios = () => {
      if (dni.value === "") {
        sociosFiltrados.value = socios.value;
      } else {
        sociosFiltrados.value = socios.value.filter((socio) =>
          socio.dni.includes(dni.value)
        );
      }
    };

    onMounted(() => {
      initFlowbite();
      filtrarSocios();
    });
    // Llamar a la función de búsqueda cada vez que el valor de dni cambie
    watch(dni, filtrarSocios);

    // Función para buscar al socio por DNI
    const buscarSocio = () => {
      console.log("Búsqueda de socio por DNI:", dni.value);
    };

    // Función para cargar el recibo
    const cargarRecibo = (_dni) => {
      router.push({ name: "recibo-socio", query: { dni: _dni } });
      // router.push({ path: "/recibo-socio", params: { dni } });
    };

    const editarSocio = (_socio) => {
      console.log(_socio);
    };

    return {
      socios,
      dni,
      sociosFiltrados,
      buscarSocio,
      cargarRecibo,
      editarSocio,
    };
  },
};
</script>

<style>
/* Puedes agregar estilos de Tailwind CSS aquí si es necesario */
</style>
