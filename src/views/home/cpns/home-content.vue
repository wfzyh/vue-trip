<template>
  <div class="content">
    <h2 class="title">热门精选</h2>
    <div class="list">
      <template v-for="(item, index) in houselist" :key="item.data.houseId">
        <home-item-v9 
        v-if="item.discoveryContentType === 9" 
        :item-data="item.data" 
        @click="itemClick(item.data)"
        ></home-item-v9>
        <home-item-v3 
        v-else-if="item.discoveryContentType === 3" 
        :item-data="item.data"
        @click="itemClick(item.data)"
        ></home-item-v3>
      </template>
    </div>
  </div>
</template>

<script setup>
import useHomeStore from '@/stores/modules/home';
import { storeToRefs } from 'pinia';
import HomeItemV9 from "@/components/home-item-v9/home-item-v9.vue"
import HomeItemV3 from "@/components/home-item-v3/home-item-v3.vue"
import { useRouter } from 'vue-router';


const homeStore = useHomeStore()
const { houselist } = storeToRefs(homeStore)

const router = useRouter()
const itemClick = (item)=>{
  router.push("/detail/" + item.houseId)
}
</script>

<style lang="less" scoped>
.content {
  padding: 10px 8px;

  .title {
    font-size: 22px;
    padding: 10px;
  }

  .list {
    display: flex;
    flex-wrap: wrap;
  }
}
</style>