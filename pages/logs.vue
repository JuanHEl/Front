<template>
  <div id="logs">
    <b-table
      responsive
      id="tablalogs"
      striped
      hover
      :items="items"
      :fields="fields"
    ></b-table>
    <div id="formLogs">
      <div>
        <p style="color:white;">Filtros</p>
      </div>
      <div id="formsInput">
        <b-form-input
          id="input-1"
          type="text"
          placeholder="Id"
          required
          class="mb-2"
        ></b-form-input>
        <b-form-select
          v-model="form.servicio"
          :options="opciones"
          class="mb-2"
        ></b-form-select>
        <b-form-datepicker
          v-model="form.fechaI"
          class="mb-2"
        ></b-form-datepicker>
        <b-form-datepicker
          v-model="form.fechaF"
          class="mb-2"
        ></b-form-datepicker>
        <b-form-select
          v-model="form.servicio"
          :options="opcionesEstatus"
        ></b-form-select>
      </div>
      <b-button class="btn btn-primary" variant="primary">Buscar</b-button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      selected: null,
      opciones: [
        { value: null, text: "Selecciona un servicio" },
        { value: 1, text: "Servicio 1" },
      ],
      opcionesEstatus: [
        { value: null, text: "Selecciona un estatus" },
        { value: 1, text: "Estatus 1" },
      ],
      form: {
        id: null,
        servicio: null,
        fechaI: null,
        fechaF: null,
        estatus: null,
      },
      fields: [
        {
          key: "Id_Administradores_Servicios_Log",
          label: "Id",
          sortable: true,
        },
        {
          key: "Id_Administradores",
          label: "Administrador",
          sortable: false,
        },
        {
          key: "Id_Cat_Servicios",
          label: "Servicio",
          sortable: true,
        },
        {
          key: "Ip_Dispositivo_Orig",
          label: "Ip Origen",
          sortable: true,
        },
        {
          key: "MAC_Dispositivo_Orig",
          label: "MAC Origen",
          sortable: true,
        },
        {
          key: "Ip_Dispositivo_Ant",
          label: "Ip inicial",
          sortable: true,
        },
        {
          key: "Ip_Dispositivo_Desp",
          label: "Ip final",
          sortable: true,
        },
        // {
        //   key: "ipFinal",
        //   label: "Ip final",
        //   sortable: true,
        // },
        {
          key: "Dir_MAC_Disp_Fin",
          label: "MAC final",
          sortable: true,
        },
        {
          key: "Fecha_Init_Serv",
          label: "Fecha inicio",
          sortable: true,
        },
        {
          key: "Fecha_Fin_Serv",
          label: "Fecha fin",
          sortable: true,
        },
        {
          key: "Id_Status_Log",
          label: "Estatus",
          sortable: true,
        },
      ],
      items: [],
    };
  },
  mounted: function (){
    let logservicioadmin = "http://127.0.0.1:8000/api/muestraadminserviciolog";
    axios.get(logservicioadmin).then((data) => {
        console.log(data);
        this.items = data.data;
    });
  }
};
</script>

<style>
#logs {
  display: flex;
}
#tablalogs {
  color: black;
  width: 70%;
  margin: 2px;
  background-color: whitesmoke;
}

#formLogs {
  width: 30%;
  /* background-color: rgb(255, 255, 255); */
  margin: 2px;
  padding: 5px;
  border-radius: 10px;
  min-height: 400px;
}

#formsInput {
  margin-bottom: 10px;
  min-height: 70%;
}
</style>
