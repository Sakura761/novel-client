<template>
  <Header />
  <div class="yh-library">
    <div class="yh-stack">
      <div class="yh-stack-wrap">
        <div class="yh-stack-filter-panel">
          <div class="filter">
            <div class="filter-condition">
              <div class="condition-title">读者：</div>
              <div class="condition-items">
                <div
                  :class="{
                    'condition-item': true,
                    active: state.audience == 0,
                  }"
                  @click="selectAudience(0)"
                >
                  男生
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.audience == 1,
                  }"
                  @click="selectAudience(1)"
                >
                  女生
                </div>
              </div>
            </div>
          </div>
          <div class="filter">
            <div class="filter-condition">
              <div class="condition-title">分类：</div>
              <div class="condition-items">
                <div
                  v-for="item in categories[state.audience]"
                  :key="item"
                  class="condition-item"
                  :class="{ active: selectedCategory === item }"
                  @click="selectCategory(item)"
                >
                  {{ item }}
                </div>
              </div>
            </div>
          </div>
          <div class="filter">
            <div class="filter-condition">
              <div class="condition-title">状态：</div>
              <div class="condition-items">
                <div
                :class="
                {
                  'condition-item': true,
                  active: state.bookStatusOn == 0,
                }"
                @click="selectStatus(0)"
                >
                  全部
                </div>
                <div
                :class="{
                  'condition-item': true,
                  active: state.bookStatusOn == 1,
                }"
                @click="selectStatus(1)"
                >
                  连载中
                </div>
                <div
                :class="{
                  'condition-item': true,
                  active: state.bookStatusOn == 2,
                }"
                @click="selectStatus(2)"
                >
                  已完结
                </div>
              </div>
            </div>
          </div>
          <div class="filter">
            <div class="filter-condition">
              <div class="condition-title">字数：</div>
              <div class="condition-items">
                <div
                  v-for="item in words"
                  :key="item"
                  class="condition-item"
                  :class="{ active: selectedWords === item }"
                  @click="selectWords(item)"
                >
                  {{ item }}
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="yh-stack-filter"></div>
        <div class="yh-stack-book-list"></div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { onMounted, reactive, ref } from "vue";
import Header from "@/components/Header/Header.vue";
const state = reactive({
  searchCondition: {
    audience: 0,
    category: "全部",
    status: 0,
    words: "全部",
  },
  bookCategory: [],
  bookStatus: ["全部", "连载中", "已完结"],
  bookWords: [],
  audiences: ["男生", "女生"],
  audience: 0,
  bookStatusOn: 0,
});
const audiences = reactive(["男生", "女生"]);
const selectedAudience = ref("男生");
const categories = reactive([
  [
    "全部",
    "玄幻",
    "奇幻",
    "武侠",
    "仙侠",
    "都市",
    "历史",
    "军事",
    "游戏",
    "体育",
    "科幻",
    "灵异",
  ],
  [
    "全部",
    "古代言情",
    "现代言情",
    "青春校园",
    "玄幻言情",
    "仙侠奇缘",
    "科幻",
    "游戏竞技",
    "悬疑推理",
  ],
]);
const stautes = reactive(["全部", "连载中", "已完结"]);
const words = reactive([
  "全部",
  "30万以下",
  "30-50万",
  "50-100万",
  "100万以上",
]);
const selectedCategory = ref("全部");
const selectedStatus = ref("全部");
const selectedWords = ref("全部");
const searchCondition = ref(
  reactive({
    audience: "男生",
    category: "全部",
    status: "全部",
    words: "全部",
  })
);
onMounted(() => {
  state.bookStatusOn = 0;
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
});
const selectStatus = (item: number) => {
  state.bookStatusOn = item;
  state.searchCondition.status = item;
  // selectedStatus.value = item;
  // searchCondition.value.status = item;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectAudience = (index:number) => {
  state.audience = index;
  state.searchCondition.audience = index;
  // searchCondition.value.audience = item;
  // selectedCategory.value = "全部";
  // searchCondition.value.category = "全部";
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectCategory = (item: string) => {
  selectedCategory.value = item;
  searchCondition.value.category = item;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectWords = (item: string) => {
  selectedWords.value = item;
  searchCondition.value.words = item;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const search = () => {
  console.log(state.searchCondition);
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
</script>
<style scoped lang="less">
.yh-library {
  background-color: #fff;
  color: #222;
  min-width: 1220px;
  .yh-stack {
    width: 1260px;
    margin: 80px auto 0;
    padding: 0 20px 20px;
    font-size: 14px;
    color: #333;
    .yh-stack-wrap {
      background-color: #fff;
      padding: 30px 30px 84px;
      border-radius: 3px;
      min-height: 920px;
      .yh-stack-filter-panel {
        padding: 12px 0 60px;
        position: relative;
        .filter:not(:last-child) {
          margin-bottom: 17px;
        }
        .filter-condition {
          display: flex;
          align-items: center;
          // flex-wrap: wrap;
          .condition-title {
            margin-right: 32px;
            color: rgba(0, 0, 0, 0.4);
            white-space: nowrap;
          }
          .condition-items {
            display: flex;
            flex-wrap: wrap;
            .condition-item {
              margin-right: 20px;
              padding: 0 10px;
              line-height: 24px;
              border-radius: 12px;
              &:hover {
                background-color: #f5f5f5;
              }
            }
            .condition-item.active {
              background-color: #add8e6;
              border-color: #007bff;
            }
          }
        }
      }
    }
  }
}
</style>
