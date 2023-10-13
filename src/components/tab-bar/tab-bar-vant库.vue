<template>
  <div class="tab-bar">
    <van-tabbar v-model="currentIndex" active-color="#ff9854">
      <template v-for="(item, index) in tarbarData">
        <van-tabbar-item :to="item.path" icon="home-o">
          <span>{{ item.text }}</span>
          <!-- <template #icon>
            <img v-if="currentIndex !== index" :src="getAssetURL(item.image)" alt="">
            <img v-else :src="getAssetURL(item.imageActive)" alt="">
          </template> -->
        </van-tabbar-item>
      </template>
    </van-tabbar>
  </div>
</template>

<script setup>

import tarbarData from "@/assets/data/tabbar.js"
import { getAssetURL } from "@/utils/load-assets.js"
import { ref } from "vue";

const currentIndex = ref(0)

</script>

<style lang="less" scoped>
.tab-bar {
  // 局部变量：只修改.tab-bar子元素的--van-tabbar-item-icon-size
  --van-tabbar-item-icon-size: 30px;

  // 找到类，对类中的css属性重写
  // :deep(.class)找到子组件的类，让子组件也可以生效
  // :deep(.van-tabbar-item__icon) {
  //   font-size: 40px;
  // }

  img {
    height: 28px;
  }
}
</style>