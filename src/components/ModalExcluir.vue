<template>
<div class="modal fade" :id="'ModalExcluir' + index" aria-hidden="true">
   <div class="modal-dialog">
      <div class="modal-content">
         <div>
            <p>Excluir contato</p>
         </div>
         <div class="modal-body">
          <div>
            <div><p>Excluir Contato</p></div>
            <div class="form">Deseja realmente excluir o contato?</div>
            <div class="btns-modal">
              <button data-dismiss="modal" class="cancelar" >Cancelar</button>
              <button  @click="handleExcluir" class="delete" >Excluir</button>
            </div>
        <div/>
          </div>
                   </div>
      </div>
   </div>
</div>
</template>

<script>
import AppVue from '../App.vue';
export default {
  props:["index"],
  methods:{
    handleExcluir(){
      AppVue.methods.excluirContato(this.index)
      window.location.reload(true)
    }
  },
}
</script>

<style>

</style>