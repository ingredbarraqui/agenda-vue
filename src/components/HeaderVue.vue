<template>
   <header>
      <div class="header">
         <div><img src="../assets/ic-logo.svg"></div>
         <div>
            <button type="button" data-toggle="modal" data-target="#ModalContato0"><i class="fa-solid fa-plus"></i>Criar contato</button>
            <ModalForm titulo="Criar novo contato" :contato=contato />
         </div>
         <div class="search">
            <input type="text" placeholder='Buscar...' />
            <i class="fa-solid fa-magnifying-glass"></i>
         </div>
      </div>
   </header>
</template>

<script>
import ModalForm from './ModalForm.vue'

export default {
   data(){
        return{
            contato :{
            nome: null,
            email: null,
            tel: null,
            id: 0
         },
      }
   },
  components: {
    ModalForm,
  }
}
</script>

<style scoped>
.header{
    margin: 1rem 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.header input{
    width: 100%;
    border: none;
    padding: 0.438rem 0.5rem 0.375rem;
    border-radius: 4px;
    background-color: #e4e7f4;
    color: #9198af;
}

.search {
    flex: 1;
}

::placeholder {
    color: #9198af;
    opacity: 1;
  }

.header button{
    border: 1px solid #fa7268;
    color: #fa7268;
    margin: 0 1.5rem 0 3.75rem;
    padding: 0.5rem 1.375rem 0.5rem 1rem;
    border-radius: 20px;
    background-color: #dbff90;
    cursor: pointer;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16), 0 0 0 0.5px rgba(0, 0, 0, 0.08), inset 0 0 0 0.5px rgba(0, 0, 0, 0.08), 0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
}

.search i{
    position: absolute;
    right: 20px;
    margin-top: 11px;
    color: #9198af;
}

.fa-solid, .fas {
    padding-right: 0.5rem;
}

.modal-content p{
    margin: 0 7.75rem 0.781rem 1rem;
    color: #2a2d3b;
}
</style>