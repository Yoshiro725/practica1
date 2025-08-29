<template>
  <div class="container">
    <h2>GENERAR EL RFC DE UNA PERSONA</h2>
    
    <form @submit.prevent="generarRFC" class="formulario">
      <div>
        <label>Nombre(s):</label>
        <input v-model="nombre" type="text" required />
      </div>
      
      <div>
        <label>Apellido Paterno:</label>
        <input v-model="apellidoPaterno" type="text" required />
      </div>
      
      <div>
        <label>Apellido Materno:</label>
        <input v-model="apellidoMaterno" type="text" />
      </div>
      
      <div>
        <label>Fecha Nacimiento:</label>
        <input v-model="fechaNacimiento" type="date" required />
      </div>
      
      <div>
        <label>RFC:</label>
        <input v-model="rfc" type="text" readonly />
      </div>
      
      <button type="submit">GENERAR</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "GenerarRFC",
  data() {
    return {
      nombre: "",
      apellidoPaterno: "",
      apellidoMaterno: "",
      fechaNacimiento: "",
      rfc: ""
    };
  },
  methods: {
    generarRFC() {
      const apPat = this.apellidoPaterno.trim().toUpperCase();
      const apMat = this.apellidoMaterno.trim().toUpperCase();
      const nom = this.nombre.trim().toUpperCase();

      let iniciales = "";
      iniciales += apPat.charAt(0);
      iniciales += apPat.slice(1).match(/[AEIOU]/)?.[0] || "X";
      iniciales += apMat.charAt(0) || "X";
      iniciales += nom.charAt(0);

      const fecha = new Date(this.fechaNacimiento);
      const yy = fecha.getFullYear().toString().slice(-2);
      const mm = String(fecha.getMonth() + 1).padStart(2, "0");
      const dd = String(fecha.getDate()).padStart(2, "0");

      this.rfc = iniciales + yy + mm + dd;
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.formulario div {
  margin-bottom: 10px;
}

input {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
}

button {
  width: 100%;
  padding: 10px;
  background: green;
  color: white;
  border: none;
  border-radius: 5px;
}
</style>
