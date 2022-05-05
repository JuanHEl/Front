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
        <p>Filtros</p>
      </div>
      <div id="formsIput">
        <b-form-input
          id="input-1"
          type="text"
          placeholder="Id"
          required
        ></b-form-input>
        <b-form-select v-model="selected" :options="opciones"></b-form-select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: null,
      opciones:[{ value: null, text: 'Selecciona una opción' },],
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
  color: white;
  width: 70%;
}

#formLogs {
  width: 30%;
  background-color: white;
}

#formsInput{
  margin-bottom: 55px;
  background-color: aqua;
}
</style>
