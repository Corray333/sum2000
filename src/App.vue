

<template>
  <div class="main">
    <div class="input-section">
      <div class="input-block">
        <div class="input-block__placeholder">
          <p>Введите первое число: </p>
          <div class="input-block__placeholder__indicator positive" id="ind1"></div>
        </div>
        <input type="text" class="input-block__input" v-model="num1">
      </div>
      <div class="input-block">
        <div class="input-block__placeholder">
          <p>Введите второе число: </p>
          <div class="input-block__placeholder__indicator positive" id="ind2"></div>
        </div>
        <input type="text" class="input-block__input" v-model="num2">
      </div>
    </div>
    <div class="sum-section">
      <button class="sum-section__button" @click="sum()"></button>
      <div class="printer-block">
        <div class="printer-block__hole"></div>
        <div class="printer-block__result">
          <div class="printer-block__result__img">
            <div class="printer-block__result__img__text">
              <div class="printer-block__result__img__text__char" v-for="(dig, i) in row2">
                <p>{{ row1[i] }}</p>
                <p>{{ row2[i] }}</p>
              </div>
            </div>
            <img src="../src/components/images/listik.png" alt="">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">

import { ref, watch } from 'vue'

const num1 = ref('0')
const num2 = ref('0')
const row2 = ref(['знак', 512, 256, 128, 64, 32, 16, 8, 4, 2, 1])
const row1 = ref([]);




watch(num1, (num: string) => {
  const re = /^-?\d+$/
  const ind1: any = document.querySelector('#ind1')
  if (re.test(num) && Math.abs(parseInt(num)) < 512) {
    if (ind1.classList.value.includes('negative')) {
      ind1.classList.toggle('negative')
      ind1.classList.toggle('positive')
    }
  }
  else {
    if (ind1.classList.value.includes('positive')) {
      ind1.classList.toggle('negative')
      ind1.classList.toggle('positive')
    }
  }
})
watch(num2, (num: string) => {
  const re = /^-?\d+$/
  const ind2: any = document.querySelector('#ind2')
  if (re.test(num) && Math.abs(parseInt(num)) < 512) {
    if (ind2.classList.value.includes('negative')) {
      ind2.classList.toggle('negative')
      ind2.classList.toggle('positive')
    }
  }
  else {
    if (ind2.classList.value.includes('positive')) {
      ind2.classList.toggle('negative')
      ind2.classList.toggle('positive')
    }
  }
})

function sum() {
  const ind1: any = document.querySelector('#ind1')
  const ind2: any = document.querySelector('#ind2')
  const res: any = document.querySelector('.printer-block__result__img')
  const resWrap: any = document.querySelector('.printer-block__result')
  if (ind1.classList.value.includes('positive') && ind2.classList.value.includes('positive')) {
    if (row1.value.length != 0) {
      resWrap.style.transition = '1s'
      resWrap.style.transform = 'translateY(50vh)'
      setTimeout(() => {
        resWrap.style.transition = '0s'
        resWrap.style.transform = 'translateY(0) translateX(-5px)'
        res.style.transition = 'all 0s'
        res.style.transform = 'translateX(-110%)'
        let num: any = parseInt(num1.value) + parseInt(num2.value)
        let f: any = num < 0 ? 0 : 1
        num = num.toString(2)
        console.log(num)
        if (!f) num = num.slice(1)
        console.log(num)
        while (num.length < row2.value.length) {
          num = '0' + num
        }
        row1.value = num.split('')
        row1.value.splice(0, 1, f)
        setTimeout(() => {
          res.style.transition = '3s linear'
          res.style.transform = 'translateX(0)'
        }, 20)
      }, 1000)

    }
    else {
      let num: any = parseInt(num1.value) + parseInt(num2.value)
      let f: any = num < 0 ? 0 : 1
      num = num.toString(2)
      console.log(num)
      if (!f) num = num.slice(1)
      console.log(num)
      while (num.length < row2.value.length) {
        num = '0' + num
      }
      row1.value = num.split('')
      row1.value.splice(0, 1, f)
      res.style.transform = 'translateX(0)'
    }
  }

}


</script>

<style>
#app {
  background-color: var(--bg-main);
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  margin: 0;

}

.main {
  width: 50%;
  padding: 40px;
  background: #E8F6FF;
  border: 1px solid #C7D0C0;
  box-shadow: 2px 4px 5px rgba(0, 0, 0, 0.25), -2px -4px 5px rgba(255, 255, 255, 0.25), inset 4px 5px 5px rgba(142, 142, 142, 0.23);
  border-radius: 20px;
  width: fit-content;
}

@media (max-width: 750px) {
  #app{
    padding: 15px;
  }
  .input-section {
    flex-direction: column;
  }
  .input-block{
    width: 100% !important;
  }
  
  .input-block:first-child{
    margin-bottom: 15px;
  }

  .main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 15px;
  }

  .sum-section__button{
    margin-right: 15px !important;
    min-width: 50px !important;
    min-height: 50px !important;
    width: 50px !important;
    height: 50px !important;
  }

  .printer-block__result__img>img {
    width: 100%;
    height: auto;
  }
}

.input-section {
  display: flex;
  width: 100%;
}

.input-block {
  padding: 25px;
  width: fit-content;
  background: #C8D2C1;
  border: 1px solid #C7D0C0;
  box-shadow: 2px 4px 2px rgba(0, 0, 0, 0.25), -2px -4px 2px rgba(255, 255, 255, 0.25), inset 4px 5px 5px rgba(142, 142, 142, 0.23);
  border-radius: 20px;
}

.input-block:first-child {
  margin-right: 40px;
}

.input-block__input {
  background-color: transparent;
  width: 250px;
  border: none;
  caret-color: var(--text-color);
  bottom: 0;
  font-size: 24px;
  margin-top: 25px;
}

.input-block__input:focus {
  outline: none;
}

.input-block__placeholder {
  border-bottom: 2px solid var(--text-color);
  padding: 10px 0;
  display: flex;
  justify-content: space-between;
}

.input-block__placeholder__indicator {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  border: 1px solid #5CC44C;
  box-shadow: 1px 2px 1px rgba(0, 0, 0, 0.25), -1px -2px 1px rgba(255, 255, 255, 0.25), inset 4px 5px 5px rgba(142, 142, 142, 0.23);
}

.negative {
  background-color: var(--btn-yellow);
}

.positive {
  background-color: var(--btn-green);
}


.sum-section {
  display: flex;
  margin-top: 40px;
  align-items: center;
}

.sum-section__button {
  width: 70px;
  height: 70px;
  margin-right: 40px;
  background: #E8F6FF;
  box-shadow: 0px 4px 5px rgba(17, 47, 64, 0.3), inset -1px -4px 2px rgba(17, 56, 73, 0.25), inset 2px 4px 2px #FFFFFF;
  border-radius: 34px;
  border: none;
  transition: 0.1s;
}

.sum-section__button:active {
  box-shadow: 0px 2px 2px rgba(17, 47, 64, 0.3), inset -1px -2px 1px rgba(17, 56, 73, 0.25), inset 0px 2px 1px #FFFFFF;
  transition: 0.1s;
}

.printer-block {
  display: flex;
  align-items: center;
}

.printer-block__result {
  transform: translateX(-5px);
  overflow: hidden;
  height: fit-content;
  padding: 10px;
}


.printer-block__hole {
  background: #2D2D2D;
  border: 2px solid #C1C1C1;
  box-shadow: inset 4px 4px 5px rgba(0, 0, 0, 0.23);
  border-radius: 20px;
  width: 10px;
  height: 70px;
}


.printer-block__result__img {
  display: flex;
  align-items: center;
  transform: translateX(-110%);
  transition: 3s linear;
  box-shadow: 2px 2px 1px rgba(0, 0, 0, 0.25);
}

.printer-block__result__img>img {
  height: 65px;
}

.printer-block__result__img__text__char {
  text-align: center;
  display: block;
}

.printer-block__result__img__text {
  display: flex;
  justify-content: space-around;
  position: absolute;
  width: 100%;
}
</style>
