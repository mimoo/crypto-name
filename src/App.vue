<script setup lang="ts">
import { ref } from 'vue'
import words from './assets/words.json'

const count = ref(0)

const keywords = ["zk", "chain", "block", "coin", "token", "protocol", "network", "DAO"]

function randInt(max: number): number {
  return Math.floor(Math.random() * max);
}

function randBool(): boolean {
  return randInt(2) === 0;
}

function pickRandom(arr: string[]): string {
  return arr[randInt(arr.length)];
}


function create(): string {
  let res = "";

  // pick keyword
  const keyword = pickRandom(keywords);

  // pick word
  const word = pickRandom(words);

  // attach keyword
  switch (randInt(5)) {
    case 0:
      res = word + keyword;
      break;
    case 1:
      res = keyword + word;
      break;
    case 2:
      res = keyword + " " + word;
      break;
    case 3:
      res = word + " " + keyword;
      break;
    case 4:
      res = word + "-" + keyword;
      break;
  }

  // uppercase
  if (randBool()) {
    res = res.toUpperCase();
  }

  // second word
  if (randBool()) {
    let word = pickRandom(words);

    if (randBool()) {
      word = word.toUpperCase();
    }

    switch (randInt(5)) {
      case 0:
        res = word + keyword;
        break;
      case 1:
        res = keyword + word;
        break;
      case 2:
        res = keyword + " " + word;
        break;
      case 3:
        res = word + " " + keyword;
        break;
      case 4:
        res = word + "-" + keyword;
        break;
    }
  }

  return res;
}

const name = ref("What's your crypto name?");

function generate() {
  name.value = create();
}

</script>

<template>
  <div class="flex h-screen">
    <div class="m-auto">
      <!-- main content -->
      <div class="bg-white dark:bg-gray-800">
        <div class="sm:px-6 lg:py-16 lg:px-8 z-20">
          <h2 class="text-3xl font-extrabold text-black dark:text-white sm:text-4xl">
            <span class="block">{{ name }}</span>
          </h2>
          <div class="lg:mt-0 lg:flex-shrink-0">
            <div class="mt-12 inline-flex rounded-md shadow">
              <button
                @click="generate"
                type="button"
                class="py-4 px-6 bg-indigo-600 hover:bg-indigo-700 focus:ring-indigo-500 focus:ring-offset-indigo-200 text-white w-full transition ease-in duration-200 text-center text-base font-semibold shadow-md focus:outline-none focus:ring-2 focus:ring-offset-2 rounded-lg"
              >Generate</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
