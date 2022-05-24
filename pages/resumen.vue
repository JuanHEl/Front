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
    </div>
</template>

<script>
export default {
    data() {
        return {
        fields: [
            {
            key: "idSolicitud",
            label: "Id",
            sortable: true,
            },
            {
            key: "NombreDispo",
            label: "Nombre del Dispositivo",
            sortable: false,
            },
            {
            key: "Memoria",
            label: "Memoria",
            sortable: true,
            },
            {
            key: "CPU",
            label: "CPU",
            sortable: true,
            },
            {
            key: "AnchoB ",
            label: "Ancho de Banda",
            sortable: true,
            },
            {
            key: "Storage",
            label: "Almacenamiento obtenido",
            sortable: true,
            },
            {
            key: "SegData",
            label: "Segmento de datos",
            sortable: true,
            }
        ],
        items: [],
        }
    },
    methods: {},
    mounted: function () {}
}
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
</style>
