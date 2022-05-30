<template>
<div class="modal fade" :id="'ModalContato' + contato.id" aria-hidden="true" >
   <div class="modal-dialog">
      <p>{{titulo}}</p>
            <form  :id="'formEditar' + contato.id" @submit="handleSubmit">
               <div class="form">
                  <label>Nome
                  <input
                     :value="contato.nome"
                     type="text"
                     name='nome'
                     placeholder='Nome'
                     @keyup="habilitado()"
                     required
                     />
                  </label>

                  <label>E-mail
                  <input
                     :value="contato.email"
                     type="email"
                     name='email'
                     placeholder='Email'
                     @keyup="habilitado()"
                     required
                     />
                  </label>

                  <label>Telefone
                  <the-mask
                     :value="contato.tel"
                     name='tel'
                     placeholder='Telefone'
                     @keyup.native="habilitado()"
                     :mask="['(##) ####-####', '(##) #####-####']"
                     required
                     />
                  </label>
               </div>

               <div class="btns-modal">
                  <button data-dismiss="modal" type="button" class="cancelar">Cancelar</button>
                  <button data-dismiss="modal" :disabled=disabled @click="handleSubmit" class="salvar">Salvar</button>
               </div>
            </form>
         </div>
   </div>
</template>

<script>
import {TheMask} from 'vue-the-mask'
export default {
   props: [
      "contato",
      "titulo"
      ],

   components: {
      TheMask
      },

   data(){
      return{
         nome: null,
         email: null,
         tel: null,
         disabled: true
      }
   },

   methods:{
      handleSubmit(e){
         e.preventDefault();
         let contatoSalvar = {}

         if(this.contato.id !== 0){
            contatoSalvar = this.contato
         }

         let form = document.querySelector("#formEditar" + this.contato.id).elements
         contatoSalvar.nome = form.nome.value
         contatoSalvar.email = form.email.value
         contatoSalvar.tel = form.tel.value
         form.nome.value = ""
         form.email.value = ""
         form.tel.value = ""

         this.$root.$children[0].salvarContato(contatoSalvar)
      },

      habilitado(){
         let form = document.querySelector("#formEditar" + this.contato.id).elements
         this.contato.nome = form.nome.value
         this.contato.email = form.email.value
         this.contato.tel = form.tel.value

         if(form.nome.value !== "" && form.email.value !== "" && form.tel.value !== "" ){
            this.disabled = false
         } else {
           this.disabled = true
         }
      }
    },
}
</script>

<style>
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

.btns-modal button:disabled {
    background-color: #fa7268;
    opacity: 0.32;
  }
</style>
