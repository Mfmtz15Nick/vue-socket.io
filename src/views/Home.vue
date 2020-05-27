<template>
  <div class="carlos">
    <div>
      <div class="lista">
        <ul
          v-for="componente in componentes.slice().reverse()"
          :key="componente.id"
          id="lista"
          class="list-group"
        >
          <span v-html="componente"></span>
          <!-- <li class="list-group-item">Cras justo odio</li>
          <li class="list-group-item">Dapibus ac facilisis in</li>
          <li class="list-group-item">Morbi leo risus</li>
          <li class="list-group-item">Porta ac consectetur ac</li>-->
        </ul>
      </div>
      <br />
      <div>
        <input autofocus v-on:keyup.13="putElement" v-model="texto" class="form-control" />
        <br />
        <button
          @click="putElement"
          class="btn text-light btn-block bg-success font-weight-bold"
        >Send</button>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
let lista = document.getElementById("lista");

export default {
  name: "Home",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      componentes: [],
      clase: 1,
      texto: ''
    };
  },
  methods: {
    putElement() {
      if (this.texto) {
        console.log("holis");
        if (this.clase % 2) {
          this.componentes.push(
            `<li class="bg-primary text-light list-group-item clase${this.clase}">${this.texto}</li>`
          );
          
        }else{
                this.componentes.push(
            `<li class="bg-success text-light list-group-item clase${this.clase}">${this.texto}</li>`
          );
        }
      this.clase++
      this.texto = ''
        
      }
    },
    scrollToEnd() {
      console.log("Hola perro");

      // scroll to the start of the last message
      const el = this.$el.getElementsByClassName('scroll-to-me')[0];

      if (el) {
        el.scrollIntoView();
      }
    }
  },
  updated() {
    // whenever data changes and the component re-renders, this is called.
    this.$nextTick(() => this.scrollToEnd());
  }
};
</script>
<style scoped>
.carlos {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 90vh;
}
.lista {
  width: 500px;
  height: 400px;
  overflow: auto;
}
</style>
