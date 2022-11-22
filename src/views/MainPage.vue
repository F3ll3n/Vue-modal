<script>
import Modal from '../components/modal.vue'

export default {
  components: {
    Modal
  },
  data() {
    return {
      showModal: false
    }
  }
}
</script>
<!-- Компонент с кнопкой попапа -->
<template>
  <div class="wrapper">
    <h1>POPUP TEST</h1>
    <button id="show-modal" @click="showModal = true">Show Modal</button>
    <Teleport to="body">
      <modal :show="showModal" @close="showModal = false">
        <template #header>
        </template>
      </modal>
    </Teleport>
  </div>
</template>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
  .wrapper{
    font-family: 'Roboto', sans-serif;
    width: 100%;
    min-height: 98vh;
    color: #595E61;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }
  button#show-modal{
    max-width: 200px;
    width: 100%;
    height: 70px;
    font-size: 17px;
    background-color: #C24DFE;
    border: 2px solid #C24DFE;
    border-radius: 35px;
    font-weight: 700;
    cursor: pointer;
    color: #fff;
    transition: .3s;
  }
  button#show-modal:hover{
    background-color: #FFF;
    color: #C24DFE;
    transform: scale(1.05);
    border: 2px solid #C24DFE;
  }
</style>
