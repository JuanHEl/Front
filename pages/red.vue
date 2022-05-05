<template>
  <div id="red">
    <div class="tablared">
      <div class="lineared" v-for="(elem,index) in red " :key="index">
        <div class="lineadis" v-for="(dis,index) in elem" :key="index+1" :style="'background-color:'+colorClase(dis)">{{nombreClase(dis)}}</div>
      </div>
    </div>
    <div id="formred">

      <div id="formsInput">

      <b-button block class="" pill variant="primary">Buscar</b-button>
      <b-button block pill variant="primary">Buscar</b-button>
      <b-button block pill variant="primary">Buscar</b-button>
      <b-button block pill variant="primary">Buscar</b-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      red:[
        [0,0,1,2,4,0,1,0,0,0,0],[0,0,2,0,0,0,2,0,0,0,0],[0,0,1,0,0,0,0,0,0,0,0],[0,0,2,0,0,0,0,0,0,0,0],[0,0,3,0,0,0,0,0,0,0,0],
        [0,0,2,0,0,0,0,0,0,0,0],[0,0,0,0,0,0,0,0,0,0,0]
      ],
      form: {
        id: null,
        servicio: null,
        fechaI: null,
        fechaF: null,
        estatus: null,
      },

    };
  },
  methods:{
    colorClase(valor){
      return valor==1?'red':valor==2?'black':valor==3?'yellow':valor==4?'orange':'white'
    },
    nombreClase(valor){
      return valor==1?'SWI':valor==2?'CON':valor==3?'ROU':valor==4?'SER':'  '
    }
  }
};
</script>

<style>
#red {
  display: flex;
}
#tablared {
  color: white;
  width: 10em !important;
  max-height: 10%;
  overflow: auto;
  background-color: red;
  margin: 2px;
  padding: 10px;
}

#formred {
  width: 15%;
  margin: 2px;
  padding: 5px;
  border-radius: 10px;
  min-height: 400px;
}

.lineared{
  display: flex;
  min-width: 100%;
}

.lineadis{
  min-width:70px;
  min-height: 70px;
  max-width: 70px;
  border-color: black;
  border-style:solid;
  color:white;
  padding: 15px;
}

#formsInput {
  margin-bottom: 10px;
  min-height: 70%;
}
</style>
