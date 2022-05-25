<template>
<div class="modal fade" id="ModalContato" aria-hidden="true">
   <div class="modal-dialog">
      <div class="modal-content">
         <div>
            <p>Modal title</p>
         </div>
         <div class="modal-body">
            <form  id="formEditar" @submit="handleSubmit">
               <div class="form">
                  <label>{{contato}} Nome
                  <input
                     value=""
                     type="text"
                     name='nome'
                     placeholder='nome'
                     required
                     />
                  </label>
                  <label>E-mail
                  <input
                     :value="email"
                     type="email"
                     name='email'
                     placeholder='email'
                     required
                     />
                  </label>
                  <label>Telefone
                  <input
                     :value="tel"
                     type="tel"
                     name='tel'
                     mask="(99) 99999-9999"
                     placeholder='Telefone'
                     required
                     />
                  </label>
               </div>
               <div class="btns-modal">
                  <button type="button" class="cancelar">Cancelar</button>
                  <button class="salvar">Salvar</button>
               </div>
            </form>
         </div>
      </div>
   </div>
</div>
</template>

<script>

export default {
    props: ["contato"],
    data(){
      return{
          nome: null,
          email: null,
          tel: null,
        }
    },
    methods:{
    handleSubmit  (e, index) {
        e.preventDefault();
        const nome = e.target.elements.nome.value;
        const email = e.target.elements.email.value;
        const tel = e.target.elements.tel.value;
        console.log(nome, email, tel)
      }
    },
    created(){
      console.log(this.contato)
      $('#ModalContato').on('show.bs.modal', function (e) {
   // let button = $(e.relatedTarget)
   // let contato = button.data('contato')
   // let modal = $(this)

//   modal.find('.modal-title').text('New message to ' + recipient)
//   modal.find('.modal-body input').val(recipient)
      })
    }
}




</script>

<style scoped>
.form{
    display: table-caption;
    border-top: 1px solid #c0c3d2;
    border-bottom: 1px solid #c0c3d2;
}

.form input{
    width: 24rem;
    height: 2rem;
    margin: 0.25rem 0 1rem;
    border-radius: 4px;
    border: solid 1px #c0c3d2;
    padding-left: 4px;
}

.modal {
    width: 440px;
    background: #ffffff;
    margin: 225px auto;
    padding: 1rem 0;
    border-radius: 16px;
    box-shadow: 0 16px 10px 0 rgba(0, 0, 0, 0.16);
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