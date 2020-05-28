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
import HelloWorld from "@/components/HelloWorld.vue";
import io from "socket.io-client";
var socket = io.connect("https://kango.ngrok.io/");

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
