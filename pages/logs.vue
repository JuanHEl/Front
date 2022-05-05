<template>
  <div id="logs">
    <b-table
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
      <b-button block pill variant="primary">Buscar</b-button>
    </div>
  </div>
</template>

<script>
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
          key: "idLogs",
          label: "Id",
          sortable: true,
        },
        {
          key: "idAdministrador",
          label: "Administrador",
          sortable: false,
        },
        {
          key: "servicios",
          label: "Servicio",
          sortable: true,
        },
        {
          key: "idOrigen",
          label: "Ip Origen",
          sortable: true,
        },
        {
          key: "macOrigen",
          label: "MAC Origen",
          sortable: true,
        },
        {
          key: "ipInicial",
          label: "Ip inicial",
          sortable: true,
        },
        {
          key: "ipFinal",
          label: "Ip final",
          sortable: true,
        },
        {
          key: "ipFinal",
          label: "Ip final",
          sortable: true,
        },
        {
          key: "macTarget",
          label: "MAC target",
          sortable: true,
        },
        {
          key: "fechaInicio",
          label: "Fecha inicio",
          sortable: true,
        },
        {
          key: "fechaFin",
          label: "Fecha fin",
          sortable: true,
        },
        {
          key: "estatus",
          label: "Estatus",
          sortable: true,
        },
      ],
      items: [],
    };
  },
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
