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
                  :class="{
                    'condition-item': true,
                    active: state.bookStatusOn == null,
                  }"
                  @click="selectStatus(null)"
                >
                  全部
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.bookStatusOn == 0,
                  }"
                  @click="selectStatus(0)"
                >
                  连载中
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.bookStatusOn == 1,
                  }"
                  @click="selectStatus(1)"
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
                  :class="{
                    'condition-item': true,
                    active: state.wordCounton == null,
                  }"
                  @click="selectWords(null, null)"
                >
                  全部
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.wordCounton == 0,
                  }"
                  @click="selectWords(0, 300000)"
                >
                  30万以下
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.wordCounton == 300000,
                  }"
                  @click="selectWords(300000, 500000)"
                >
                  30-50万
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.wordCounton == 500000,
                  }"
                  @click="selectWords(500000, 1000000)"
                >
                  50-100万
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.wordCounton == 1000000,
                  }"
                  @click="selectWords(1000000, 2000000)"
                >
                  100万-200万
                </div>
                <div
                  :class="{
                    'condition-item': true,
                    active: state.wordCounton == 2000000,
                  }"
                  @click="selectWords(2000000, null)"
                >
                  200万以上
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="yh-stack-filter">
          <div
            class="byte-tabs byte-tabs-horizontal byte-tabs-line byte-tabs-size-default stack-order-tab"
          >
            <div
              class="byte-tabs-header-nav byte-tabs-header-nav-horizontal byte-tabs-header-size-default byte-tabs-header-nav-line"
            >
              <div class="byte-tabs-header-scroll is-dropdown">
                <div class="byte-tabs-header-wrapper">
                  <div
                    class="byte-tabs-header"
                    style="transform: translateX(0px)"
                  >
                    <div
                      :class="{
                        'byte-tabs-header-title': true,
                        active: state.sort == 0,
                      }"
                      @click="selectSort(0)"
                    >
                      最热
                    </div>
                    <div
                      :class="{
                        'byte-tabs-header-title': true,
                        active: state.sort == 1,
                      }"
                      @click="selectSort(1)"
                    >
                      最新
                    </div>
                    <div
                      :class="{
                        'byte-tabs-header-title': true,
                        active: state.sort == 2,
                      }"
                      @click="selectSort(2)"
                    >
                      完结
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="yh-stack-book-list">
          <div
            class="yh-stack-book-item"
            v-for="book in state.books"
            :key="book.id"
          >
            <div class="book-cover">
              <img
                class="cover"
                src="https://p9-reading-sign.fqnovelpic.com/novel-pic/c5397e4a514736bb1c6754663dbee3db~tplv-resize:200:260.image?lk3s=8c91f0b0&x-expires=1729999040&x-signature=mXKZYemFfgaueAnoV1fj80kP4w0%3D"
                width="100"
                height="130"
              />
            </div>
            <div class="book-info">
              <div>
                <router-link
                  class="book-item-title font-fKts9tCXDjS49UhH"
                  to="/book-detail/${book.id}"
                >
                  {{ book.name }}
                </router-link>
              </div>
              <div class="book-item-desc">
                <span>
                  作者：
                  <span class="font-fKts9tCXDjS49UhH">{{ book.author }}</span>
                </span>
              </div>
              <div class="book-item-desc">
                <span>
                  {{ book.status == 0 ? "连载中" : "已完结" }}
                  <span class="font-fKts9tCXDjS49UhH">{{
                    book.wordCount
                  }}</span>
                </span>
              </div>
              <div
                class="book-item-desc book-item-abstract font-fKts9tCXDjS49UhH"
              >
                {{ book.desc }}
              </div>
              <div class="book-item-footer">
                <span>{{ book.updateTime }}</span>
              </div>
            </div>
          </div>
        </div>
        <div class="yh-stack-pagination">
          <el-pagination background layout="prev, pager, next" :total="1000" />
        </div>
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
    status: null,
    wordCountMin: null,
    wordCountMax: null,
    sort: 0, // Added sort property here
  },
  books: [
    {
      id: 1,
      name: "遮天",
      author: "辰东",
      category: "玄幻",
      status: 0,
      wordCount: 3000000,
      desc: "一个平凡的少年，一个卑微的村子，一个无奈的命运，一段不平凡的传奇。",
      updateTime: "2021-09-01",
    },
  ],
  bookCategory: [],
  audience: 0,
  bookStatusOn: null,
  wordCounton: null,
  sort: 0,
});
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
const selectedCategory = ref("全部");
onMounted(() => {
  state.bookStatusOn = null;
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
});
const selectStatus = (item: any) => {
  state.bookStatusOn = item;
  state.searchCondition.status = item;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectAudience = (index: number) => {
  state.audience = index;
  state.searchCondition.audience = index;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectCategory = (item: string) => {
  selectedCategory.value = item;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectWords = (wordCountMin: any, wordCountMax: any) => {
  state.wordCounton = wordCountMin;
  state.searchCondition.wordCountMin = wordCountMin;
  state.searchCondition.wordCountMax = wordCountMax;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const selectSort = (index: number) => {
  state.sort = index;
  state.searchCondition.sort = index;
  search();
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};
const search = () => {
  console.log(state.searchCondition);
  // 这里可以添加其他逻辑，比如发送请求或更新其他组件的状态
};

const goToDetail = (bookId: number) => {
  // Implement the logic to navigate to the book detail page
  console.log(`Navigating to book detail page with id: ${bookId}`);
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
              font-weight: 500;
              color: #fa6725;
              background-color: rgba(250, 103, 37, 0.1);
            }
          }
        }
      }
      .byte-tabs {
        position: relative;
        overflow: hidden;
      }
    }
    .byte-tabs-header-nav {
      position: relative;
      background: #fff;
    }
    .byte-tabs-header-nav:before {
      content: "";
      clear: both;
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      height: 1px;
      background-color: #e6e8eb;
      display: block;
    }
    .byte-tabs-header-nav-horizontal .byte-tabs-header-scroll.is-dropdown {
      padding-right: 20px;
    }
    .byte-tabs-header-nav-horizontal .byte-tabs-header-scroll {
      overflow: hidden;
      position: relative;
    }
    .byte-tabs-header-wrapper {
      overflow: hidden;
    }
    .byte-tabs-header {
      position: relative;
      display: inline-block;
      transition: transform 0.3s ease;
      white-space: nowrap;
      height: 44px;
      .byte-tabs-header-title {
        box-sizing: border-box;
        height: 44px;
        line-height: 44px;
        margin: 0 20px;
        cursor: pointer;
        font-size: 14px;
        color: var(--font-color);
        display: inline-block;
        transition: color 0.3s;
      }
      .byte-tabs-header-title.active {
        color: #fa6725;
        font-weight: 500;
      }
    }
    .yh-stack-book-list {
      display: flex;
      flex-wrap: wrap;
    }
    .yh-stack-book-item {
      position: relative;
      margin-top: 42px;
      width: 328px;
    }
    .book-cover {
      float: left;
      flex: 0 0 auto;
      width: 100px;
      height: 130px;
      cursor: pointer;
    }
    .book-info {
      position: relative;
      margin-left: 120px;
      height: 130px;
      font-size: 12px;
      line-height: 17px;
      .font-fKts9tCXDjS49UhH {
        font-family: fKts9tCXDjS49UhH, -apple-system, "PingFang SC",
          "Microsoft YaHei", "Helvetica Neue", Helvetica, Arial, sans-serif;
      }
      .book-item-title {
        display: inline-block;
        font-size: 18px;
        line-height: 25px;
        font-weight: 500;
        cursor: pointer;
        width: 100%;
        word-wrap: normal;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        text-decoration: none; /* 去掉下划线 */
        color: inherit; /* 保持链接颜色与其他文本一致 */
      }
      .book-item-title:hover {
        color: #fa6725; /* 鼠标悬停时改变颜色 */
      }
      .book-item-desc {
        line-height: 17px;
        color: rgba(0, 0, 0, 0.4);
        margin-top: 5px;
      }
      .book-item-abstract {
        line-height: 16px;
        word-break: break-word;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
      }
      .book-item-footer {
        color: rgba(0, 0, 0, 0.4);
        position: absolute;
        bottom: 0;
      }
    }
    .yh-stack-pagination {
      display: flex;
      align-items: center;
      padding-top: 62px;
      justify-content: center;
    }
  }
}
</style>
