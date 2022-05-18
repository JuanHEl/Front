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
import axios from "axios";
export default {
    name: "FormStatus",
    data: function () {
        return {
            listservicios:[],
        };
    },
    components: {
    },
    methods: {
    },
    watch: {
    },
    mounted: function () {
        let catservicios = "http://127.0.0.1:8000/api/muestracatservicio";
        axios.get(catservicios).then((data) => {
            // console.log(data);
            this.catservicios = data.data;
            for (let index = 0; index < this.catservicios.length; index++) {
                this.listservicios.push({name:this.catservicios[index].Nom_Cat_Servicios,item:this.catservicios[index].Id_Cat_Servicios});
            }
            console.log(this.listservicios);
        });
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