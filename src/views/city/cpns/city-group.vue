<template>
  <div class="city-group">

    <van-index-bar :sticky="false" :index-list="indexList">
      <!-- 热门城市 -->
      <van-index-anchor index="热门" />
      <div class="list">
        <template v-for="(city, index) in groupData.hotCities">
          <div class="city" @click="cityClick(city)">{{ city.cityName }}</div>
        </template>
      </div>
      <!-- 城市列表 -->
      <template v-for="(group, index) in groupData.cities" :key="index">
        <van-index-anchor :index="group.group" />
        <template v-for="(city, indey) in group.cities" :key="indey">
          <van-cell :title="city.cityName" @click="cityClick(city)" />
        </template>
      </template>
    </van-index-bar>

  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useRouter } from 'vue-router';
import useCityStore from '@/stores/modules/city'

// 定义props
const props = defineProps({
  groupData: {
    type: Object,
    default: () => ({})
  }
})

// 动态的索引
const indexList = computed(() => {
  const list = props.groupData.cities.map(item => item.group)
  list.unshift("#")
  return list
})

// 监听城市的点击
const router = useRouter()
const cityStore = useCityStore()
const cityClick = (city) => {
  // 选中当前城市
  cityStore.currentCity = city

  // 返回上一级
  router.back()
}

</script>

<style lang="less" scoped>
.list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 10px;
  padding-right: 25px;

  .city {
    width: 70px;
    height: 28px;
    border-radius: 14px;
    font-size: 12px;
    color: #000;
    line-height: 28px;
    text-align: center;
    background-color: #fff4ec;
    margin: 6px 0;
  }
}
</style>