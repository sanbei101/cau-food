<template>
  <div class="app">
    <el-select
      v-model="selectedCategory"
      placeholder="选择类别"
      style="width: 200px; margin-right: 10px"
    >
      <el-option
        v-for="category in categories"
        :key="category"
        :value="category"
      ></el-option>
    </el-select>
    <el-button type="primary" @click="fetchFood">获取食物</el-button>

    <el-card v-if="foodData" class="box-card" style="margin-top: 20px">
      <div slot="header" class="clearfix">
        <span>{{ foodData.name }}</span>
      </div>
      <div v-for="canteen in foodData.canteen" :key="canteen">
        {{ canteen }}
      </div>
    </el-card>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { ElMessage } from "element-plus";

const categories = ref(["早餐", "主食", "小吃", "水果", "饮品"]);
const selectedCategory = ref("早餐");
const foodData = ref(null);

const fetchFood = async () => {
  try {
    const response = await fetch(
      `https://food-cau-cekgcmqeyj.cn-beijing.fcapp.run/?category=${selectedCategory.value}`
    );
    const data = await response.json();
    foodData.value = data;
    ElMessage.success("数据获取成功！");
  } catch (error) {
    ElMessage.error("数据获取失败，请稍后再试。");
  }
};
</script>

<style>
.app {
  padding: 20px;
}
.box-card {
  margin-top: 20px;
}
</style>
