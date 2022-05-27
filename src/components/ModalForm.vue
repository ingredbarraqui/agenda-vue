<template>
<div class="modal fade" :id="'ModalContato' + contato.id" aria-hidden="true" >
   <div class="modal-dialog">
      <p>{{titulo}}</p>
            <form  id="formEditar" @submit="handleSubmit">
               <div class="form">
                  <label>Nome
                  <input
                     :value="contato.nome"
                     type="text"
                     name='nome'
                     placeholder='nome'
                     required
                     />
                  </label>
                  <label>E-mail
                  <input
                     :value="contato.email"
                     type="email"
                     name='email'
                     placeholder='email'
                     required
                     />
                  </label>
                  <label>Telefone
                  <input
                     :value="contato.tel"
                     type="tel"
                     name='tel'
                     v-mask="'(##) #####-####'"
                     placeholder='Telefone'
                     required
                     />
                  </label>
               </div>
               <div class="btns-modal">
                  <button data-dismiss="modal" type="button" class="cancelar">Cancelar</button>
                  <button class="salvar">Salvar</button>
               </div>
            </form>
         </div>
   </div>
</template>

<script>
import AppVue from '../App.vue';

export default {
    props: ["contato", "titulo"],
    data(){
      return{
          nome: null,
          email: null,
          tel: null,
        }
    },
    methods:{
    handleSubmit  (e) {
        e.preventDefault();
        let contatoSalvar = {

        }

         if(this.contato.id !== 0){
            contatoSalvar = this.contato
         }

         contatoSalvar.nome = e.target.elements.nome.value
         contatoSalvar.email = e.target.elements.email.value
         contatoSalvar.tel = e.target.elements.tel.value


         AppVue.methods.salvarContato(contatoSalvar)
        console.log(AppVue)

      }
    },
}




</script>

<style scoped>
.form{
    display: table-caption;
    border-top: 1px solid #c0c3d2;
    border-bottom: 1px solid #c0c3d2;
    padding: 1.2rem 0;
}

.form input{
    width: 24rem;
    height: 2rem;
    margin: 0.25rem 0 1rem;
    border-radius: 4px;
    border: solid 1px #c0c3d2;
    padding-left: 4px;
}

.form label{
   margin-bottom: none;
}

.modal-dialog {
    width: 420px;
    background: #ffffff;
    margin: 165px auto;
    padding: 1rem;
    border-radius: 16px;
    box-shadow: 0 16px 10px 0 rgba(0, 0, 0, 0.16);
    pointer-events: auto;
}

.btns-modal{
    padding: 16px 16px 0;
    display: flex;
    justify-content: flex-end;
}

.cancelar{
    color: #fa7268;
    background: none;
    border: none;
    font-weight: 500;
    font-size: 0.875rem;
    padding: 8px;
    cursor: pointer;
}

.salvar, .delete{
  padding: 0.5rem 1rem;
  border-radius: 16px;
  color: #fff;
  border: none;
  cursor: pointer;
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16), 0 0 0 0.5px rgba(0, 0, 0, 0.08), inset 0 0 0 0.5px rgba(0, 0, 0, 0.08), 0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
  background-color: #fa7268;
}

.btns-modal input:disabled {
    background-color: #fa7268;
    opacity: 0.32;
  }


</style>