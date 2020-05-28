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
        <input autofocus v-on:keyup.13="sendEmit" v-model="texto" class="form-control" />
        <br />
        <button
          @click="sendEmit"
          class="btn text-light btn-block bg-success font-weight-bold"
        >Send</button>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import HelloWorld from "@/components/HelloWorld.vue";
import io from "socket.io-client";
var socket = io.connect("http://localhost:3001/");

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
      texto: ""
    };
  },
  methods: {
    sendEmit(){
      socket.emit("hello", this.texto);

    },
    putElement() {
      if (this.texto) {
        if (this.clase % 2) {
          this.componentes.push(
            `<li class="bg-primary text-light list-group-item clase${this.clase}">${this.texto}</li>`
          );
        } else {
          this.componentes.push(
            `<li class="bg-success text-light list-group-item clase${this.clase}">${this.texto}</li>`
          );
        }
        this.clase++;
        this.texto = "";
      }
    },
    conectarse(){
        socket.on("hello", message => {
          this.texto = message
          this.putElement()
    })
    }
  },
  mounted() {
    this.conectarse()
    

  },
  updated() {
    // whenever data changes and the component re-renders, this is called.
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
