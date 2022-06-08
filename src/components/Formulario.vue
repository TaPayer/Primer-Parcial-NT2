<template>

  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2>Ingreso de Notas</h2>
      <hr>
      <br>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            v-model="formData.nombre" 
            required name="nombre" 
            autocomplete="off" 
            class="form-control"
            :minlength="stringMinLength"
            :maxlength="stringMaxLength"
          />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">
                Este campo requiere como mínimo {{stringMinLength}} caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
                Este campo requiere como máximo {{stringMaxLength}} caracteres.
            </div>
          </field-messages>
        </validate>
        <br>

        <!-- Campo apellido -->
        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input 
            type="text" 
            id="apellido" 
            v-model="formData.apellido" 
            required name="apellido" 
            autocomplete="off" 
            class="form-control"
            :minlength="stringMinLength"
            :maxlength="stringMaxLength"
          />
    
          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">
                Este campo requiere como mínimo {{stringMinLength}} caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
                Este campo requiere como máximo {{stringMaxLength}} caracteres.
            </div>
          </field-messages>
        </validate>
        <br>
        
        <!-- Campo nota -->
        <validate tag="div">
          <label for="nota">Nota</label>
          
          <input 
            type="number" 
            id="nota" 
            v-model.number="formData.nota" 
            required name="nota" 
            autocomplete="off" 
            class="form-control"
            :min="notaMin"
            :max="notaMax"
          />
    
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="min" class="alert alert-danger mt-1">
                El valor mínimo de la nota debe ser {{notaMin}}.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
                El valor máximo de la nota debe ser {{notaMax}}.
            </div>
          </field-messages>
        
        </validate>

        <br>

        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>

      <!-- Tabla para mostrar las notas -->
      <h2>Detalle de Notas</h2>
      <br>

      <div v-if="alumnos.length" class="table-dark">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Nota</th>
          </tr>
          
          <tr v-for="(alumno,index) in alumnos" :key="index">
            <td>{{ alumno.nombre }} {{ alumno.apellido }}</td>
            <td :style="{color: colorearNota(alumno.nota).color }">{{ colorearNota(alumno.nota).notaColoreada }}</td>
          </tr>

          <tr>
            <td>Promedio de notas</td>
            <td :style="{color: colorearNota(calcularPromedio()).color }">{{ calcularPromedio() }}</td>
          </tr>
        
        </table>
     
      </div>
      <h3 v-else class="alert alert-info">No hay alumnos ingresados</h3>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        alumnos : [],
        stringMinLength: 3,
        stringMaxLength: 15,
        notaMin: 0,
        notaMax: 10,
        promedio: 0
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : null,
          apellido: null,
          nota: null
        }
      },
      enviar() {
        let alumno = {
          nombre: this.formData.nombre,
          apellido: this.formData.apellido,
          nota: this.formData.nota
        }
        this.alumnos.push(alumno)
        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      
      calcularPromedio() {
        let acum = 0
        this.alumnos.forEach(alumno => {
            acum = acum + alumno.nota
        });
        this.promedio = acum / this.alumnos.length

        return this.promedio
      
     },
      colorearNota(nota){
        let notaColor = nota
        let color = '#e8d41c'
        if (notaColor < 4) color = '#e81c1c'
        if (notaColor >= 4 && notaColor < 7) color = '#e8d41c'
        if (notaColor >= 7) color = '#1ce823'
        return {
          notaColoreada : notaColor,
          color
        }
      }
    },
    computed: {
    }
}


</script>

<style scoped lang="css">
  .src-componentes-formulario {

  }
  .jumbotron {
    background-color: #bfbfbf;
    color: rgb(22, 22, 22);
    border: 2px inset rgb(0,0,0,0.5);
  }

  .table-dark{
    color: rgb(22, 22, 22);
  }

  th{
    color: rgb(187, 186, 186);
  }

  td{
    color: rgb(187, 186, 186);
  }

  h2{
    font: bold;
  }
</style>
