<template>
    <div id="contenedor">
        <div id="tabla">
            <div id="botones">
                <div>
                    <br>
                    <b-button block class="buttons" pill variant="primary" to="/nuevoadmin" font-scale="3"> Agregar Nuevo Administrador</b-button>
                    <b-button block class="buttons" pill variant="primary" to="cambiastatus" font-scale="3"> Cambiar Status </b-button>
                    <b-button block class="buttons" pill variant="primary" to="/editaradmin" font-scale="3"> Editar Administrador</b-button>
                    <br>
                    <b-button block class="buttons" pill variant="primary" to="/editarpermisos" font-scale="3"> Editar Permisos</b-button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "FormStatus",
    data: function () {
        return {
        };
    },
    components: {
    },
    methods: {
    },
    watch: {
    },
    mounted: function () {
    },
};
</script>
<style scoped>
#contenedor {
    display: flex;
}
.left {
    text-align: left;
}
#botones {
    width: 35%;
    margin: 2px;
    padding: 5px;
    border-radius: 10px;
    min-height: 400px;
    color: white;
}
#tabla {
    width: 100%;
    /* background-color: rgb(255, 255, 255); */
    /* margin: 2px;
    padding: 5px;
    border-radius: 10px;
    min-height: 400px; */
}
</style>