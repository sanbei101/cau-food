<template>
  <div class="app">
    <h1>🤤农大食堂🫣吃点啥!</h1>
    <el-select
      v-model="selectedCategory"
      placeholder="吃点啥好呢?"
      style="width: 200px; margin-right: 10px"
    >
      <el-option
        v-for="category in categories"
        :key="category"
        :value="category"
      ></el-option>
    </el-select>
    <el-button type="primary" @click="fetchFood">吃点啥🤔</el-button>

    <el-card v-if="foodData" class="box-card" style="margin-top: 20px">
      <h1>🍲菜品名</h1>
      <div>
        <span style="font-size: 18px; font-weight: bold">
          {{ foodData.name }}
        </span>
      </div>
      <h1>👉在哪吃</h1>
      <div v-for="canteen in foodData.canteen" :key="canteen">
        <span style="font-size: 18px; font-weight: bold">
          {{ canteen }}
        </span>
      </div>
    </el-card>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { ElMessage } from "element-plus";

const categories = ref(["早餐", "主食", "小吃", "饮品"]);
const selectedCategory = ref("早餐");
const foodData = ref(null);

const fetchFood = async () => {
  try {
    const response = await fetch(
      `https://api.sanbei101.top/?category=${selectedCategory.value}`
    );
    const data = await response.json();
    foodData.value = data;
    ElMessage.success("我要吃!");
  } catch (error) {
    ElMessage.error("吃的太多了,吃不动了!");
  }
};
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  background-color: #cbf1f5;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.el-card {
  background-color: #a6e3e9;
  border: 1px solid #71c9ce;
  border-radius: 8px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
</style>
