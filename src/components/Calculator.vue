<script setup>
import { ref, computed } from "vue";

const userInput = ref("0");
const inputDynamicClass = ref("");
const arithmaticSigns = ref(["/", "*", "-", "+"]);
const focusOnError = ref(null);
const errorClass = ref("");

// const handleClick = (e) => {
//   userInput.value = userInput.value.concat(e.target.innerText);
// };

const handleClick = (event) => {
  if (userInput.value === "0" && userInput.value !== ".") {
    userInput.value = event;
  } else {
    userInput.value += event;
  }
};

const clearInputHandler = () => {
  userInput.value = "";
};

const calculateResult = () => {
  try {
    userInput.value = eval(userInput.value).toString();
  } catch (error) {
    userInput.value = "Invalid Input";
    focusOnError.value.focus();
    errorClass.value = "input-error";
    setTimeout(() => {
      userInput.value = "";
      errorClass.value = "";
    }, 2000);
  }
};
</script>

<template>
  <div class="main-wrapper">
    <h1>Calculator</h1>
    <div class="cal-wrapper">
      <input
        v-model="userInput"
        :class="['user-input', errorClass]"
        type="text"
        ref="focusOnError"
      />
      <div class="btns">
        <button @click="handleClick('7')">7</button>
        <button @click="handleClick('8')">8</button>
        <button @click="handleClick('9')">9</button>
        <button class="signs" @click="handleClick('/')">
          {{ arithmaticSigns[0] }}
        </button>
        <button @click="handleClick('4')">4</button>
        <button @click="handleClick('5')">5</button>
        <button @click="handleClick('6')">6</button>
        <button class="signs" @click="handleClick('*')">
          {{ arithmaticSigns[1] }}
        </button>
        <button @click="handleClick('1')">1</button>
        <button @click="handleClick('2')">2</button>
        <button @click="handleClick('3')">3</button>
        <button class="signs" @click="handleClick('-')">
          {{ arithmaticSigns[2] }}
        </button>
        <button @click="handleClick('0')">0</button>
        <button class="signs" @click="handleClick('.')">.</button>
        <button class="equal" @click="calculateResult">=</button>
        <button class="signs" @click="handleClick('+')">
          {{ arithmaticSigns[3] }}
        </button>
      </div>
      <button class="clear" @click="clearInputHandler">Clear</button>
    </div>
  </div>
</template>

<style scoped>
.main-wrapper {
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  h1 {
    font-family: times, Times New Roman, times-roman, georgia, serif;
    font-size: 50px;
    margin: 20px;
  }
  .cal-wrapper {
    display: flex;
    flex-direction: column;

    .user-input {
      font-size: 25px;
      height: 55px;
      padding: 0px 10px;
      font-family: sans-serif;
      font-weight: bolder;
      letter-spacing: 2px;
    }
    .special-character-class {
      color: rgb(151, 27, 27);
      margin: 0 5px;
    }
    .input-error {
      border: 2px solid red;
      color: red;
    }
  }
  .btns {
    display: grid;
    grid-template-columns: auto auto auto auto;
    padding: 15px 0px;
    gap: 15px;
    button {
      font-size: 18px;
      font-size: 20px;
      padding: 10px 15px;
      font-weight: bolder;
    }
    .signs {
      font-weight: bolder;
      color: red;
      font-size: 35px;
      padding: 10px;
    }
    .equal {
      color: green;
      font-size: 45px;
      padding: 0;
    }
  }
  .clear {
    font-size: 22px;
    font-weight: bold;
    padding: 10px 130px;
    background-color: rgb(59, 148, 148);
  }
}
input,
button {
  border-radius: 10px !important;
}
</style>
