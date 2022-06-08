<template>

  <section class="src-components-respuestas">
    
    <div class="jumbotron">
      
      <h2>Respuestas</h2>

      <div class="table-responsive">
        
        <table class="table table-dark">
          
          <tr>
            <th>Numero de Pregunta</th>
            <th>Respuesta</th>
          </tr>
          
          <tr v-for="(respuesta,index) in respuestas" :key="index" :style="{color: white}">
            <td>{{ respuesta.pregunta }}</td>
            <td>{{ respuesta.respuesta }}</td>
          </tr>
        
        </table>
      
      
      </div>      
    
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
        respuestas: [
          {pregunta: '1', respuesta: 'C'},
          {pregunta: '2', respuesta: 'C'},
          {pregunta: '3', respuesta: 'B'}
        ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-respuestas {

  }
</style>
