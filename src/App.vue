<template>
  <div id="app">
    <HeaderVue />
    <Contatos :listaContatos=listaContatos />
  </div>
</template>

<script>
import HeaderVue from './components/HeaderVue.vue'
import Contatos from './components/Contatos.vue'

export default {
  data(){
      return {
         listaContatos: this.listarContatos()
      }
   },
  components: {
    HeaderVue,
    Contatos,
  },
  methods:{
    listarContatos(){
      return useLocalStorage("listaContatos", [])
    },
    salvarContatos (key, valueToStore){
      try {
        if (typeof window !== "undefined") {
          window.localStorage.setItem( key, JSON.stringify(valueToStore));
        }
      } catch (error) {
        console.log(error);
      }
    },
    salvarContato(contato, destaque = false){
        let listaContatos = this.listarContatos()

        if (listaContatos == null) {
            listaContatos = []
        }
        console.log(contato.id)
        if (contato.id > 0) {
            contato.destaque = destaque;
            let index = listaContatos.filter((key, item,) => {
          return item.id == contato.id ? item : null;
        });
            listaContatos[index] = contato;
        } else {
            contato.id = this.ultimoId()+1
            contato.destaque = true;
            listaContatos.push(contato)
            // setTimeout(() => {
            //     editarDestaque((listaContatos.length - 1), false)
            // }, "10000")
        }
        this.salvarContatos("listaContatos", listaContatos)
    },
    excluirContato(id){
      let listaContatos = this.listarContatos()
      listaContatos = listaContatos.filter((item) => {
        return item.id != id ? item : null;
      });
      this.salvarContatos("listaContatos", listaContatos)
    },

    ultimoId(){
      let listaContatos = this.listarContatos()
      if(listaContatos.length == 0){
        return 0
      }
      listaContatos.sort( compare );
      return listaContatos[0].id
    }
  }
}
  function compare( a, b ) {
  if ( a.id > b.id ){
    return -1;
  }
  if ( a.id < b.id ){
    return 1;
  }
  return 0;
}
  const useLocalStorage = (key, initialValue) => {

    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.log(error);
      return initialValue;
    }
  };

</script>

<style>
body, ul, li, dt, dd, dl {
    margin: 16px !important;
    font-family: 'Roboto', sans-serif !important;
    background: #f8f9fd !important;
}
</style>

