<template>
    <FormsInput 
        @enviar="addComentarios"
        @editar="editarDados"
        :addEdit="editar ? dadosEditar: null"
        :modoEdicao="editar"
        ></FormsInput>

    
        <div v-for="comment in coments" :key="comment.id" class="containerComentarios">
            <div class="comentarios">
            <div class="nome">{{ comment.nome }}</div>
            <div>{{ comment.email }}</div>
            <div>{{ comment.tel }}</div>
            <div>{{ comment.menssagem }}</div>
            <div class="button">
            <button @click="removerComentarios(comment.id)">Excluir</button>
            <button @click="editarComentarios(comment.id)">Editar</button>
            </div>    
            </div>
        </div>


    
</template>


<script>
import FormsInput from './FormsInput.vue';
export default{
    components:{FormsInput},
    data(){
        return{
            coments: [],
            editar: false,
            dadosEditar: []
        }
    },
    methods:{
        addComentarios(coment){
            this.coments.push(coment)
        },
        removerComentarios(id){
            const index = this.coments.findIndex(comment => comment.id === id)
            this.coments.splice(index, 1)
        },
        editarComentarios(id){
            this.editar = true

            const index = this.coments.findIndex(comment => comment.id === id )
            this.dadosEditar = { ...this.coments[index] };
            
        },
        editarDados(coment){
            const index = this.coments.findIndex(comment => comment.id === coment.id )
            this.coments[index] = coment
            this.editar = false
        }
    },
    
}
</script>


<style scoped>
.containerComentarios{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 1rem;
    width: 100%;

}

.comentarios{
    margin: .1rem;
    background-color: white;
    width: 80%;
    padding: .3rem;
    font-size: 14px;
}
button{
    font-size: 10px;
    padding: .3rem;
    margin:.2rem;
    font-weight: 700;
    border: none;
    background-color: burlywood;
    color: chocolate;
}
.nome{
    font-weight: 700;
}

@media screen and (min-width: 700px) {
  .comentarios {
    width: 500px;
  }
}
</style>

