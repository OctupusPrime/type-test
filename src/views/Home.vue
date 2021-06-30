<template>
  <div class="home">
    <!-- <Modal title="Test result" :isShow="isShowModal"><p>You pasted test</p></Modal> -->
    <TypeTest :testText="testText" @finished="typeTestFinished"/>
  </div>
</template>

<script>
import TypeTest from '@/components/TypeTest.vue'
// import Modal from '@/components/Modal.vue'

export default {
  name: 'Home',
  components: {
    TypeTest,
    // Modal
  },
  data: () => {
    return {
      testText: 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nostrum quia, ratione laborum voluptates quibusdam est.',
      isShowModal: false
    }
  },
  methods: {
    typeTestFinished() {
      this.isShowModal = true;
    }
  }
}
</script>
