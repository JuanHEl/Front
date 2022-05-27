<template>
    <div id="admins">
        <div>
        </div>
        <div id="botones">
            <div>
                <b-button block class="buttons" pill variant="primary" to="/nuevoadmin" font-scale="3">Configurar Servidores</b-button>
                <b-button block class="buttons" pill variant="primary" to="/cambiastatus" font-scale="3">Configurar Switches</b-button>
                <b-button block class="buttons" pill variant="primary" to="/editaradmin" font-scale="3">Configurar Routers</b-button>
                <br>
                <b-button block class="buttons" pill variant="primary" to="/editarpermisos" font-scale="3">Monitorizar</b-button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'configuracion',
    component: {},

}
</script>

<style scoped>
#admins {
    display: flex;
}
#botones {
    width: 30%;
    margin: 2px;
    padding: 5px;
    border-radius: 10px;
    min-height: 400px;
    color: white;
}
</style>
