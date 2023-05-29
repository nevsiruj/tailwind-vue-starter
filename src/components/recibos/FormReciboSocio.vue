<template>
  <div class="p-4">
    <h2 class="text-2xl font-bold mb-4">Cargar Recibo</h2>

    <div class="mb-4">
      <label for="socio" class="font-bold">Seleccione un socio:</label>
      <select
        v-model="selectedSocio"
        class="w-full py-2 px-4 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-400"
      >
        <option v-for="socio in socios" :key="socio.dni" :value="socio">
          {{ socio.nombre }}
        </option>
      </select>
      <label class="ml-4">
        <strong>DNI :</strong>
        {{ selectedSocio ? selectedSocio.dni : "" }}</label
      >
    </div>

    <div class="mb-4">
      <label for="numero" class="font-bold">Número de Recibo:</label>
      <input
        type="text"
        v-model="numeroRecibo"
        class="w-full py-2 px-4 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-400"
      />
    </div>

    <div class="mb-4">
      <label for="monto" class="font-bold">Monto:</label>
      <input
        type="number"
        v-model="monto"
        class="w-full py-2 px-4 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-400"
      />
    </div>

    <div class="mb-4">
      <label for="fecha" class="font-bold">Fecha:</label>
      <input
        type="text"
        v-model="fecha"
        class="w-full py-2 px-4 rounded-lg border border-gray-300 bg-gray-100"
        disabled
      />
    </div>

    <button
      @click="cargarRecibo"
      class="bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-400"
    >
      Cargar Recibo
    </button>
  </div>
</template>

<script>
import { ref, computed, onMounted } from "vue";
import { useRouter } from "vue-router";
import socioService from "../../services/socioService";
import { initFlowbite } from "flowbite";

export default {
  name: "CargarRecibo",
  setup() {
    const selectedSocio = ref(null);
    const numeroRecibo = ref("");
    const monto = ref(null);
    const fecha = ref("");
    const recibo = ref({
      socioDni: "",
      nombre: "",
    });

    const router = useRouter();

    const socios = computed(() => {
      return socioService.getSocios();
    });

    onMounted(() => {
      initFlowbite();
      const data = router.currentRoute.value.query.dni;
      // alert(data);
      if (data) {
        const socioEncontrado = socios.value.find(
          (socio) => socio.dni === data
        );
        if (socioEncontrado) {
          // Realiza acciones con el socio encontrado, por ejemplo, asignarlo a una referencia

          selectedSocio.value = socioEncontrado;
        }
      }
    });

    const cargarRecibo = () => {
      // Lógica para cargar el recibo al socio seleccionado
      // mediante una llamada a la API o la actualización del almacenamiento
    };

    return {
      selectedSocio,
      numeroRecibo,
      monto,
      fecha,
      socios,
      cargarRecibo,
      recibo,
    };
  },
};
</script>

<style scoped>
/* Estilos específicos del componente */
</style>
