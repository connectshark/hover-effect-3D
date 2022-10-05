<template>
<main>
  <div class="card" ref="card">
    <h1>BS Meeting Notes</h1>
    <div class="author">
      <img src="../assets/main.png" alt="main">
      <p>@mattmaribojoc</p>
    </div>
    <p class="content">{{ content }}</p>
  </div>
</main>
</template>

<script setup>
import { useMouseInElement } from '@vueuse/core'
import { ref, computed } from 'vue'

const card = ref(null)

const { elementX, elementY, isOutside, elementWidth, elementHeight } =
  useMouseInElement(card)

const cardTransform = computed(() => {
  const MAX_ROTATION = 6
  const rX = (
    MAX_ROTATION / 2 - (elementY.value / elementHeight.value) * MAX_ROTATION
  ).toFixed(2)

  const rY = (
    (elementX.value / elementWidth.value) * MAX_ROTATION - MAX_ROTATION / 2
  ).toFixed(2)

  return isOutside.value
    ? ''
    : `rotateX(${rX}deg) rotateY(${rY}deg)`
})

const content = `Organic growth beef up, and shotgun approach note for the previous submit: Can you ballpark the cost per unit for me. Conversational content reach out, what's the status on the deliverables for eow?`

</script>

<style lang="scss" scoped>
main {
  height: 100vh;
  background-image: linear-gradient(135deg, #C2BEFF 0%, #657BB3 100%);
  text-align: center;
  perspective: 200px;
  &::before{
    content: '';
    width: 0;
    height: 100%;
    display: inline-block;
    vertical-align: middle;
  }
  .card {
    color: #fff;
    display: inline-block;
    vertical-align: middle;
    box-sizing: border-box;
    width: 80%;
    max-width: 500px;
    padding: 2rem;
    background-color: #22222299;
    border-radius: 20px;
    transition: transform .25s ease;
    transform: v-bind(cardTransform);
    text-align: left;
    backdrop-filter: blur(10px);
    h1 {
      font-size: 2rem;
      line-height: 2;
      font-weight: bold;
    }
    .author {
      display: flex;
      align-items: center;
      margin-bottom: 1rem;
      img{
        width: 30px;
        border-radius: 5px;
      }
      p{
        margin-left: 10px;
      }
    }
    .content {
      font-size: 1rem;
      line-height: 1.5;
    }
  }
}
</style>