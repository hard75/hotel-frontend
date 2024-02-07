<template>
  <div>
    <h1>Consulta de Disponibilidad</h1>
    <input v-model="sitio" type="text" />
    <br>
    <button @click="consultarDisponibilidad">Consultar Disponibilidad</button>
    <div v-if="disponibilidad">
      <h2>Resultado:</h2>
      <pre>{{ disponibilidad }}</pre>
    </div>

    <h1>Consulta de Tarifas</h1>
    <button @click="consultarTarifas">Consultar Tarifas</button>
    <div v-if="tarifas">
      <h2>Resultado:</h2>
      <pre>{{ tarifas }}</pre>
    </div>

    <h1>Calcular Tarifa a Cancelar</h1>
    <button @click="calcularTarifaCancelar">Calcular Tarifa</button>
    <div v-if="tarifaCancelar">
      <h2>Resultado:</h2>
      <pre>{{ tarifaCancelar }}</pre>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      sitio: '',
      disponibilidad: null,
      tarifas: null,
      tarifaCancelar: null,
    };
  },
  methods: {
    async consultarDisponibilidad() {
      try {
        const respuesta = await axios.get(
          "http://localhost:3000/api/disponibilidad/" + this.sitio
        );
        this.disponibilidad = respuesta.data.disponibilidad;
      } catch (error) {
        console.error("Error al consultar disponibilidad:", error);
      }
    },
    async consultarTarifas() {
      try {
        const respuesta = await axios.get(
          "http://localhost:3000/api/tarifas"
        );
        this.tarifas = respuesta.data.tarifas;
      } catch (error) {
        console.error("Error al consultar tarifas:", error);
      }
    },
    async calcularTarifaCancelar() {
      try {
        const respuesta = await axios.get(
           "http://localhost:3000/api/calcular-tarifa"
        );
        this.tarifaCancelar = respuesta.data.tarifa;
      } catch (error) {
        console.error("Error al calcular tarifa a cancelar:", error);
      }
    },
  },
};
</script>

<style>
</style>
