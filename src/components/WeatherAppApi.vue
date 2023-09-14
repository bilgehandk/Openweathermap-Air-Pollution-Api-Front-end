<template>
  <div class="container mx-auto p-4 grid gap-x-8 gap-y-4">
    <h1 class="text-3xl font-bold mb-4">Air Pollution Data</h1>
    <div class="flex flex-col items-center space-y-4">
      <a-select v-model:value="selectedCity" placeholder="Select City" class="w-64">
        <a-select-option v-for="city in cities" :key="city" :value="city">{{ city }}</a-select-option>
      </a-select>
      <a-range-picker
          v-model:value="startDate"
          format="DD-MM-YYYY"
          class="w-64"
          :disabledDate="disabledDate"
      />
      <a-range-picker
          v-model:value="endDate"
          format="DD-MM-YYYY"
          class="w-64"
          :disabledDate="disabledDate"
      />
      <a-button type="primary" @click="getAirPollutionData">Get Data</a-button>
    </div>
    <div v-if="airPollutionData">
      <h2 class="text-2xl mt-4">Air Pollution Results for {{ selectedCity }}</h2>
      <table class="mt-2">
        <thead>
        <tr>
          <th>Date</th>
          <th>CO</th>
          <th>SO2</th>
          <th>O3</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="result in airPollutionData.results" :key="result.dt">
          <td>{{ result.dt }}</td>
          <td>{{ result.categories.CO }}</td>
          <td>{{ result.categories.SO2 }}</td>
          <td>{{ result.categories.O3 }}</td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue';
import axios from 'axios';

import {Button as AButton, DatePicker as ARangePicker, Select as ASelect,} from 'ant-design-vue';

const cities = ['London', 'Barcelona', 'Ankara', 'Tokyo', 'Mumbai'];
const selectedCity = ref();
const startDate = ref();
const endDate = ref();
const airPollutionData = ref(null);


const getAirPollutionData = async () => {
  try {
    const response = await axios.get(`http://localhost:8080/api/pollution?city=${selectedCity.value}&startDate=${startDate.value.format('DD-MM-YYYY')}&endDate=${endDate.value.format('DD-MM-YYYY')}`);
    airPollutionData.value = response.data;
  } catch (error) {
    console.error(error);
  }
};
</script>

