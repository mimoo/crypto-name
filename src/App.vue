<script setup lang="ts">
import { ref, onUpdated } from 'vue'
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

const names = ref(Array<string>(0));

function generate(event: any) {
  const new_name = create();
  names.value.push(new_name);
}

// scroll when new names appear
onUpdated(() => {
  const chat = document.querySelector("#chat");
  if (chat && chat.lastElementChild) {
    console.log(chat.lastElementChild);
    chat.lastElementChild.scrollIntoView();
  }
})
</script>

<template>
  <div
    class="flex flex-col items-center justify-center w-screen min-h-screen bg-gray-100 text-gray-800 p-10"
  >
    <!-- Component Start -->
    <div
      class="flex flex-col flex-grow w-full max-w-xl bg-white shadow-xl rounded-lg overflow-hidden"
    >
      <div class="flex flex-col flex-grow h-0 p-4 overflow-auto" id="chat">
        <!-- him -->
        <div class="flex w-full mt-2 space-x-3 max-w-xs">
          <img src="./assets/david.jpg" class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300" />
          <div>
            <div class="bg-gray-300 p-3 rounded-r-lg rounded-bl-lg">
              <p class="text-sm">Do you have a crypto name?</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">2 min ago</span>
          </div>
        </div>
        <!-- me -->
        <div class="flex w-full mt-2 space-x-3 max-w-xs ml-auto justify-end">
          <div>
            <div class="bg-blue-600 text-white p-3 rounded-l-lg rounded-br-lg">
              <p class="text-sm">What's that?</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">2 min ago</span>
          </div>
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
        </div>
        <!-- him -->
        <div class="flex w-full mt-2 space-x-3 max-w-xs">
          <img src="./assets/david.jpg" class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300" />
          <div>
            <div class="bg-gray-300 p-3 rounded-r-lg rounded-bl-lg">
              <p class="text-sm">Dude you gotta have a crypto name!</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">2 min ago</span>
          </div>
        </div>
        <!-- me -->
        <div class="flex w-full mt-2 space-x-3 max-w-xs ml-auto justify-end">
          <div>
            <div class="bg-blue-600 text-white p-3 rounded-l-lg rounded-br-lg">
              <p class="text-sm">Alright alright, here's my crypto name.</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">2 min ago</span>
          </div>
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
        </div>

        <!-- me -->
        <div class="flex w-full mt-2 space-x-3 max-w-xs ml-auto justify-end" v-for="name in names">
          <div>
            <div class="bg-blue-600 text-white p-3 rounded-l-lg rounded-br-lg">
              <p class="text-sm">{{ name }}</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">2 min ago</span>
          </div>
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
        </div>

        <!-- end -->
      </div>

      <div class="bg-gray-300 p-4">
        <button
          @click="generate"
          class="flex items-center h-10 w-full rounded px-3 text-sm"
        >Generate your crypto name…</button>
      </div>
    </div>
    <!-- Component End  -->
  </div>
</template>
