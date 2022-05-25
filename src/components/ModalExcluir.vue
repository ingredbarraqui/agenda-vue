<template>
          <div>
            <div><p>Excluir Contato</p></div>
            <div class="form">Deseja realmente excluir o contato?</div>
            <div class="btns-modal">
              <button onClick={props.onClose} className="cancelar" >Cancelar</button>
              <button onClick={handleExcluir} className="delete" >Excluir</button>
            </div>
        <div/>
          </div>
</template>

<script>
export default {

}
</script>

<style>

</style>