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
      let nombres = this.nombre.trim().toUpperCase().split(" ");

      // Nombres comunes que se omiten si hay más de uno
      const comunes = ["JOSE", "J", "MARIA", "MA"];
      if (nombres.length > 1 && comunes.includes(nombres[0])) {
        nombres.shift();
      }
      const nom = nombres[0] || "";

      // Iniciales según reglas SAT
      let iniciales = "";
      iniciales += apPat.charAt(0) || "X"; 
      iniciales += apPat.slice(1).match(/[AEIOU]/)?.[0] || "X"; 
      iniciales += apMat.charAt(0) || "X"; 
      iniciales += nom.charAt(0) || "X";   

      // Palabras inconvenientes
      const prohibidas = [
        "BUEI","BUEY","CACA","CAKA","KAKA","COGE","COJE","COJO",
        "FETO","JOTO","KULO","MAME","MAMO","MEAR","MEON","MION",
        "PENE","PUTA","PUTO","QULO","RATA","RUIN"
      ];
      if (prohibidas.includes(iniciales)) {
        iniciales = iniciales[0] + "X" + iniciales.slice(2);
      }

      // Fecha de nacimiento en formato AAMMDD
      const fecha = new Date(this.fechaNacimiento);
      const yy = fecha.getFullYear().toString().slice(-2);
      const mm = String(fecha.getMonth() + 1).padStart(2, "0");
      const dd = String(fecha.getDate()).padStart(2, "0");

      // Homoclave simulada
      const homoclave = "XXX";

      this.rfc = iniciales + yy + mm + dd + homoclave;
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 420px;
  margin: auto;
  padding: 24px;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f9f9f9;
  font-family: Arial, Helvetica, sans-serif;
}

h2 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 20px;
}

.formulario div {
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  color: #34495e;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border: 1px solid #bbb;
  border-radius: 6px;
  box-sizing: border-box;
  font-size: 14px;
}

input[readonly] {
  background-color: #eaeaea;
}

button {
  width: 100%;
  padding: 12px;
  background: #2c3e50;
  color: #fff;
  border: none;
  border-radius: 6px;
  font-size: 15px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease;
}

button:hover {
  background: #1a252f;
}
</style>
