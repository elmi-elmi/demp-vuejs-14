<template>
  <router-view v-slot="slotProp">
    <transition name="fade-button" mode="out-in">
      <component :is="slotProp.Component"></component>
    </transition>
  </router-view>
  <!-- <div class="container">
    <user-list></user-list>
  </div>
  <div class="container">
    <div class="block" :class="{ animate: animatedBlock }"></div>
    <button @click="animateBlock">
      Animate
    </button>
  </div>
  <div class="container"> -->
  <!-- <transition enter-to-class="some-class" enter-active-class="some-other-class"> -->
  <!-- <transition
      name="para" -->
  <!-- <transition
      :css="false"
      @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
      @leave="leave"
      @after-leave="afterLeave"
      @enter-cancelled="enterCancelled"
      @leave-cancelled="leaveCancelled"
    >
      <p v-if="paraIsAppere">something appeare and disappere....</p>
    </transition>
    <button @click="togglePara">toggle</button>
  </div> -->
  <!-- <base-modal @close="hideDialog" v-if="dialogIsVisible"> -->
  <!-- <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>

  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>

  <div class="container">
    <transition name="fade-button" mode="out-in">
      <button @click="showButton" v-if="buttonsAreVisible">show</button>
      <button @click="hideButton" v-else>hidden</button>
    </transition>
  </div> -->
</template>

<script>
// import UserList from './components/UserList.vue';
export default {
  // components: { UserList },
  data() {
    return {
      dialogIsVisible: false,
      animatedBlock: false,
      paraIsAppere: true,
      buttonsAreVisible: true,
      intervalEnter: null,
      intervalLeave: null
    };
  },
  methods: {
    enterCancelled(el) {
      console.log(el);
      clearInterval(this.intervalEnter);
    },
    leaveCancelled(el) {
      console.log(el);
      clearInterval(this.intervalLeave);
    },
    beforeEnter(el) {
      console.log('beforeEnter');
      console.log(el);
      el.style.opacity = 0;
    },
    enter(el, done) {
      console.log('enter');
      console.log(el);
      let round = 1;
      this.intervalEnter = setInterval(() => {
        el.style.opacity = 0.01 * round;
        round++;
        if (round > 100) {
          clearInterval(this.intervalEnter);
          done();
        }
      }, 20);
    },
    afterEnter(el) {
      console.log('afterEnter');
      console.log(el);
    },
    beforeLeave(el) {
      console.log('beforeLeave');
      console.log(el);
      el.style.opacity = 1;
    },
    leave(el, done) {
      console.log('leave');
      console.log(el);
      let round = 1;
      this.intervalLeave = setInterval(() => {
        el.style.opacity = 1 - 0.01 * round;
        round++;
        if (round > 100) {
          clearInterval(this.intervalLeave);
          done();
        }
      }, 20);
    },
    afterLeave(el) {
      console.log('afterLeave');
      console.log(el);
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateBlock() {
      this.animatedBlock = true;
    },
    togglePara() {
      this.paraIsAppere = !this.paraIsAppere;
    },
    showButton() {
      this.buttonsAreVisible = false;
    },
    hideButton() {
      this.buttonsAreVisible = true;
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  transition: transform 0.27s ease-in;
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.animate {
  transform: translateX(-100px);
  animation: slide-scale 0.5s ease-out forwards;
}
/* 
.para-enter-from {
   opacity: 0;
  transform: translateY(-50px);
}
.para-enter-active {
  transition: all 0.3s ease-out;
}
.para-enter-to {
  opacity: 1;
  transform: translateY(0px);
  animation: slide-scale 0.3s ease-in;
}
.para-leave-from {
  opacity: 1;
  transform: translateY(0px);
}

.para-leave-active {
  transition: all 0.3s ease-in;
  animation: slide-scale 0.3s ease-out;
}
.para-leave-to {
  opacity: 0;
  transform: translateY(-50px);
} */

.fade-button-enter-from,
.fade-button-leave-to {
  opacity: 0;
}
.fade-button-enter-active {
  transition: opacity 0.3s ease-out;
}
.fade-button-leave-active {
  transition: opacity 0.3s ease-in;
}
.fade-button-enter-to,
.fade-button-leave-from {
  opacity: 1;
}

@keyframes slide-scale {
  0% {
    transform: translateX(0) scale(1);
  }
  70% {
    transform: translateX(-120px) scale(1.27);
  }
  100% {
    transform: translateX(-150px) scale(1);
  }
}
</style>
