<template>
  <div>
    <Beverage :isIced="beverageStore.currentTemp === 'Cold'" />
    <ul>
      <li>
        <template v-for="temp in beverageStore.temps" :key="temp">
          <label>
            <input
              type="radio"
              name="temperature"
              :id="`r${temp}`"
              :value="temp"
              v-model="beverageStore.currentTemp"
            />
            {{ temp }}
          </label>
        </template>
      </li>
    </ul>
    <ul>
      <li>
        <template v-for="base in beverageStore.bases" :key="base.id">
          <label>
            <input
              type="radio"
              name="base"
              :id="`b${base.id}`"
              :value="base"
              v-model="beverageStore.currentBase"
            />
            {{ base.name }}
          </label>
        </template>
      </li>
    </ul>
    <ul>
      <li>
        <template v-for="creamer in beverageStore.creamers" :key="creamer.id">
          <label>
            <input
              type="radio"
              name="creamer"
              :id="`c${creamer.id}`"
              :value="creamer"
              v-model="beverageStore.currentCreamer"
            />
            {{ creamer.name }}
          </label>
        </template>
      </li>
    </ul>
    <ul>
      <li>
        <template v-for="syrup in beverageStore.syrups" :key="syrup.id">
          <label>
            <input
              type="radio"
              name="syrup"
              :id="`s${syrup.id}`"
              :value="syrup"
              v-model="beverageStore.currentSyrup"
            />
            {{ syrup.name }}
          </label>
        </template>
      </li>
    </ul>
    <input type="text" placeholder="Beverage Name" v-model="beverageStore.currentName" />
    <button @click="beverageStore.makeBeverage()">🍺 Make Beverage</button>
  </div>
  <div id="beverage-container" style="margin-top: 20px">
    <div class="beverage-list">
      <button
        v-for="bev in beverageStore.savedBeverages"
        :key="bev.id"
        @click="beverageStore.showBeverage(bev)"
        :class="{ selected: isSelected(bev) }"
      >
        {{ bev.name }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import Beverage from "./components/Beverage.vue";
import { useBeverageStore } from "./stores/beverageStore";
import type { BeverageType } from "./types/beverage";
const beverageStore = useBeverageStore();
const isSelected = (bev: BeverageType) =>
  bev.temp === beverageStore.currentTemp &&
  bev.base.id === beverageStore.currentBase.id &&
  bev.creamer.id === beverageStore.currentCreamer.id &&
  bev.syrup.id === beverageStore.currentSyrup.id;
</script>

<style lang="scss">
body,
html {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  background-color: #6e4228;
  background: linear-gradient(to bottom, #6e4228 0%, #956f5a 100%);
}
ul {
  list-style: none;
}
#beverage-container .beverage-list {
  display: flex;
  flex-direction: row;
  gap: 10px;
  flex-wrap: wrap;
}
#beverage-container button {
  padding: 5px 10px;
  border: 1px solid #ccc;
  background: white;
  cursor: pointer;
}
#beverage-container button.selected {
  background: #ffff99;
  border-color: #000;
}
</style>
