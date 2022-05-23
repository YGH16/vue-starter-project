<template>
  <h1>{{title}}</h1>
  <!-- ref used to reference a component -->
  <input type="text" ref="name">
  <button @click="handleclick"></button>
  <p>welcome</p>
  <!-- teleport allows this piece of code to render outise of app in a different custom div -->
  <teleport to=".modals" v-if="showModal">
    <!-- passing props to component -->
    <Modal :header="header" :text="text" @close="toggleModal" >
      <!-- .slots used to pass templates into components  -->
      <h1>lol</h1>
      <p>bye man</p>
      <!-- named slots -->
      <template v-slot:links>
        <a href="#">signup</a>
        <a href="#">login</a>
        <a href="#">more info</a>
      </template>
    </Modal>

  </teleport>
  <!-- event click modifiers -->
  <button @click.shift="toggleModal">open (shift)</button>
  <hr>
  <button @click="toggleModal2">Click me to open modal 2</button>
  <div v-if="showModal2">
    <Modal @close="toggleModal2">
      <h1>yolo(You Only Live Once)</h1>
    </Modal>
  </div>
</template>

<script>
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Modal
  },
  data() {
    return {
      title: "my first app",
      text: "hello",
      header: "hey world",
      showModal: false,
      showModal2 : false

    }
  },
  methods: {
    handleclick() {
      console.log(this.$refs.name)
      // $this.ref used to pick up reference components
      this.$refs.name.classList.add('active')
    },
    toggleModal(){
      this.showModal = !this.showModal
    },
    toggleModal2() {
      this.showModal2 = !this.showModal2
    }
  }
}
</script>

<style>
#app, .modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  color: aqua;
}
</style>
