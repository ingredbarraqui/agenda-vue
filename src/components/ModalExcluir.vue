<template>
<div class="modal fade" :id="'ModalExcluir' + index" aria-hidden="true">
   <div class="modal-dialog">
      <p>Excluir contato</p>
         <div>
          <div>
            <div class="excluir">
              <p>Deseja realmente excluir o contato?</p>
            </div>
            <div class="btns-modal">
              <button data-dismiss="modal" class="cancelar" >Cancelar</button>
              <button data-dismiss="modal" @click="handleExcluir" class="delete" >Excluir</button>
            </div>
          <div/>
        </div>
      </div>
   </div>
</div>
</template>





<script>
export default {
  props:["index"],
  methods:{
    handleExcluir(){
      this.$root.$children[0].excluirContato(this.index)
    }
  },
}
</script>

<style scoped>
.excluir{
    display: block;
    border-top: 1px solid #c0c3d2;
    border-bottom: 1px solid #c0c3d2;
    padding: 1.2rem 0;
}

</style>