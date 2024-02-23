<template>
    <div  class="container" >
      <h1 >Formulário</h1>
      <input v-model="nome" type="text" placeholder="Nome">
      <input v-model="email" type="text" placeholder="E-mail">
      <input v-model="tel" type="text" placeholder="Telefone">
      <input v-model="menssagem" type="text" placeholder="Mensagem">
      <button v-if="!modoEdicao" @click="enviarDados" >Enviar</button>
      <button v-else @click="editarDados">Editar</button>
    
    </div>

    
    
  </template>
  
  <script>
  export default {
    props: ['addEdit', 'modoEdicao'],
    data() {
      return {
        id: 0,
        nome: '',
        email: '',
        tel: '',
        menssagem: '',
      }
    },
    methods: {
      enviarDados() {
        if(this.nome !== '' && this.email !== ''){
          this.$emit("enviar", {
          id: this.id++,
          nome: this.nome,
          email: this.email,
          tel: this.tel,
          menssagem: this.menssagem
        })

        this.nome = ''
        this.email = ''
        this.tel = ''
        this.menssagem = ''
        }        
      },
      editarDados(){
        this.$emit("editar", {
          id: this.id,
          nome: this.nome,
          email: this.email,
          tel: this.tel,
          menssagem: this.menssagem
        })

        this.nome = ''
        this.email = ''
        this.tel = ''
        this.menssagem = ''
      }
    },
    watch:{
      modoEdicao() {
        for(var key in this.addEdit){
          if(key == 'id'){
            this.id = this.addEdit[key]

          }else if(key == 'nome'){
            this.nome = this.addEdit[key]
          }else if(key == 'email'){
            this.email = this.addEdit[key]
          }else if(key == 'tel'){
            this.tel = this.addEdit[key]
          }else if(key == 'menssagem'){
            this.menssagem = this.addEdit[key]
          }
        
        }
      }
    }
  }
  </script>

  
<style scoped>
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: orangered;
  padding: 1rem;
  width: 100%;
}

input, button{
  width: 80%;
  padding: .2rem;
  margin: .1rem;
  border: none;
}

h1{
  color: white;
  font-size: 1.3rem;
  margin-bottom: .3rem;
}

button{
  border: none;
  background-color: burlywood;
  color: chocolate;
  border-radius: 3px;
  font-weight: 500;
  font-size: .8rem;
}

@media screen and (min-width: 700px) {
  input,button {
    width: 500px;
  }
}
</style>