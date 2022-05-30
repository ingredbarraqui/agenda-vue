<template>
   <div id="app">
      <HeaderVue />
      <Contatos v-if="this.listaContatos.length !== 0" :listaContatos=listaContatos />
      <div  v-else class="contatoNull">
         <img src="./assets/ic-book.svg" />
         <p>Nenhum contato foi criado ainda.</p>
      </div>
   </div>
</template>

<script>
import HeaderVue from './components/HeaderVue.vue';
import Contatos from './components/Contatos.vue';

export default {
  data(){
    return {
      listaContatos: [],
      novoContato: null
    }
  },

  components: {
    HeaderVue,
    Contatos,
  },

  mounted () {
    if (localStorage.getItem('listaContatos')) {
      try {
        this.listaContatos = JSON.parse(localStorage.getItem('listaContatos'));
      } catch (error) {
        localStorage.removeItem('listaContatos');
      }
    }
  },

  methods: {
    salvarContato(contato){

      let data = new Date();
      data.setSeconds(data.getSeconds() + 10);
      contato.destaqueAte = data;

      if (contato.id > 0) {
        let index = this.listaContatos.filter((item, key) => {
          return item.id == key ? key : null;
        });
        this.listaContatos[index] = contato;
      } else {
        contato.id = this.ultimoId()+1
        this.listaContatos.push(contato)
      }
      this.salvarContatos();

      setTimeout(() => {
          this.removerDestaque(contato.id)
      }, "10000")

    },

    salvarContatos(){
      const parsed = JSON.stringify(this.listaContatos);
      localStorage.setItem('listaContatos', parsed);
    },

    excluirContato(id){
      this.listaContatos = this.listaContatos.filter((item) => {
        return item.id != id ? item : null;
      });
      this.salvarContatos()
    },

    ultimoId(){
      if(this.listaContatos.length == 0){
        return 0
      }
      this.listaContatos.sort( compare );
      return this.listaContatos[0].id
    },

    removerDestaque(id){
      this.listaContatos = this.listaContatos.map((item) => {
        if (id === item.id) {
          item.destaqueAte = null;
        }
        return item
      });
      this.salvarContatos();
    }
  }
}

function compare( a, b ) {
  if (a.id > b.id){
    return -1;
  }
  if (a.id < b.id){
    return 1;
  }
  return 0;
}
</script>

<style>
.contatoNull {
    text-align: center;
    padding-top: 6rem;
}
.contatoNull p {
    padding-top: 1.5rem;
}
</style>

