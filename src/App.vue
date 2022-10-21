<!-- every vue component has 3 parts
1. html template :required
2. script to export component :optional
3. style for template :optional 
4. : binding -->

<template>
  <h1>{{ title }}</h1><br>
  <input type="text" ref="name"><br><br>
  <button @click="clickMe">Submit</button>
  <p>Welcome...</p>
  <teleport to=".modals" v-if="showModal">
    <Modal :header="header"
  :subtitle="subtitle" :theme="theme" @close="toggleModal">
   <h1>Store Giveaway!</h1>
   <p>{{subtitle}}</p>  
   
   <template v-slot:links>
    <a href="#">Sign up</a>
    <a href="#">More Info</a>
   </template>
</Modal>
  </teleport>

  <button @click="toggleModal">Show Modal</button><br>
  <teleport to="#modalsId" v-if="showMyModal">
    <Modal :title="myModalTitle" :subtitle="myModalSubtitle" @close="toggleMyModal">
    <h6>{{myModalSubtitle}}</h6>
    <h1>{{myModalTitle}}</h1>
  </Modal>
  </teleport>
  <button @click="toggleMyModal">Show My Modal</button>
</template>

<script>
import Modal from './components/Modal.vue'
// root component
export default {
  name: "App",
  data() {
    return {
      title: "My Vue App!",
      header: "Sign up for the Giveaway!",
      subtitle: "Buy two store-brand products and get 50% off the most expensive one!",
      theme: "sale",
      showModal: false,
      showMyModal: false,
      myModalTitle: "Share our Giveaway!",
      myModalSubtitle: "Share with friends and get 20% off each time they signup and buy for P100 or more."
    };
  },
  methods: {
    clickMe() {
      console.log(this.$refs.name);
      this.$refs.name.classList.add("active");
      this.$refs.name.focus();
    },
    toggleModal() {
      this.showModal = !this.showModal
    },
    toggleMyModal() {
      this.showMyModal = !this.showMyModal
    }
  },
  component: {
    Modal
  },
  components: { Modal }
}
</script>

<style>
#app, .modals, #modalsId {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  border-bottom: 2px solid seagreen;
  display: inline-block;
  padding-bottom: 8px;
}

button {
  margin-bottom: 16px;
}
</style>
