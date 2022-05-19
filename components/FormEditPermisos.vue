<template>
    <div id="contenedor">
        <div id="tabla">
            <div class="container form-group col-sm-10">
                <b-form-group>
                    <template #label>
                        <label for="" class="control-label text-white">Selecciona los servicios:</label>
                        <!-- <b class="control-label col-sm-2 text-white">Selecciona los servicios:</b> --><br>
                        <b-form-checkbox
                        size="lg"
                        v-model="allSelected"
                        :indeterminate="indeterminate"
                        @change="toggleAll"
                        class="control-label text-white"
                        stacked
                        >
                        {{ allSelected ? 'Quitar todos' : 'Selecciona todos' }}
                        </b-form-checkbox>
                    </template>
                    <template v-slot="{ ariaDescribedby }">
                        <b-form-checkbox-group
                        size="lg"
                        v-model="selected"
                        :options="listservicios"
                        :aria-describedby="ariaDescribedby"
                        class="ml-4 control-label text-white"
                        value-field="item"
                        text-field="name"
                        stacked
                        ></b-form-checkbox-group>
                    </template>
                </b-form-group>
            </div>
        </div>
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
</template>
<script>
import axios from "axios";
export default {
    name: "FormStatus",
    data: function () {
        return {
            selected: [],
            allSelected: false,
            indeterminate: false,
            listservicios:[],
        };
    },
    components: {
    },
    methods: {
    toggleAll(checked) {
        let listavariable = [];
        let variable;
        for (let index = 0; index < this.listservicios.length; index++) {
            variable = this.listservicios[index].item;
            listavariable.push(variable)
        }
        this.selected = checked ? listavariable : []
    },
    },
    watch: {
        selected(newValue, oldValue) {
            // Handle changes in individual flavour checkboxes
            if (newValue.length === 0) {
                this.indeterminate = false
                this.allSelected = false
            } else if (newValue.length === this.listservicios.length) {
                this.indeterminate = false
                this.allSelected = true
            } else {
                this.indeterminate = true
                this.allSelected = false
            }
        }
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