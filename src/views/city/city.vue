<template>
  <div class="city top-page">
    <div class="top">
      <!-- 1.搜索框 -->
      <van-search v-model="searchValue" placeholder="城市/区域/位置" shape="round" show-action @cancel="cacnelClick" />

      <!-- 2.tab切换 -->
      <van-tabs v-model:active="tabActive" color="#ff9854" line-height="3">
        <template v-for="(value, key, index) in allCities" :key="key">
          <van-tab :title="value.title" :name="key"></van-tab>
        </template>
      </van-tabs>
    </div>
    <div class="content">
      <template v-for="(value, key, index) in allCities">
        <city-group v-show="tabActive === key" :group-data="value"></city-group>
      </template>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import { useRouter } from 'vue-router';
import { storeToRefs } from 'pinia';
import useCityStore from '@/stores/modules/city';
import CityGroup from './cpns/city-group.vue'


const searchValue = ref("")

// 搜索取消点击事件
const router = useRouter()
const cacnelClick = () => {
  router.back()
}

// v-model绑定
const tabActive = ref()

// 从store中获取数据
const cityStore = useCityStore()
cityStore.fetchAllCitiesData()
const { allCities } = storeToRefs(cityStore)

// 获取选中标签后的数据
const currentGroup = computed(() => allCities.value[tabActive.value])


</script>

<style lang="less" scoped>
.city {

  .top {
    position: relative;
    z-index: 9;
  }

  .content {
    height: calc(100vh - 98px);
    overflow-y: auto;
  }
}
</style>