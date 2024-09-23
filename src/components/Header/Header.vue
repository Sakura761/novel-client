<template>
  <div class="yh-header">
    <div class="yh-header-content">
      <div class="yh-header-logo">
        <a href="/">
          <img src="../../assets/imgs/logo.jpg" height="40" alt="樱花小说网" />
        </a>
      </div>
      <div class="yh-header-nav">
        <nav class="yh-header-nav">
          <router-link class="nav-item" to="/">首页</router-link>
          <router-link class="nav-item" to="/library">书库</router-link>
          <router-link class="nav-item" to="/bookshelf">书架</router-link>
          <router-link class="nav-item" to="/rank">排行榜</router-link>
          <router-link class="nav-item" to="/writer">作家专区</router-link>
          <router-link class="nav-item" to="/help">帮助中心</router-link>
        </nav>
        <div class="yh-header-search">
          <input
            class="yh-header-search-input"
            type="text"
            placeholder="搜索书名、作者"
          />
          <div class="yh-header-search-icon">
            <el-icon><Search /></el-icon>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { Search } from "@element-plus/icons-vue";
</script>

<style scoped lang="less">
.yh-header {
  position: fixed;
  height: 80px;
  background-color: #f6f6f6;
  left: 0;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  min-width: 1240px;
  z-index: 1000;
  transition: background-color 0.2s ease;
  .yh-header-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 100%;
    font-size: 14px;
    color: #000;
    width: 1240px;
    .yh-header-logo {
      display: flex;
      align-items: flex-end;
      cursor: pointer;
    }
    .yh-header-nav {
      display: flex;
      align-items: center;
      height: 14px;
      line-height: 18px;
      .nav-item {
        height: 18px;
        padding-right: 20px;
        padding-left: 20px;
        text-decoration: none; /* 去掉下划线 */
        color: inherit; /* 保持链接颜色与其他文本一致 */
      }
      .nav-item:hover {
        color: #409eff; /* 鼠标悬停时改变颜色 */
        // 鼠标悬停时添加下划线
        text-decoration: underline;
      }
      .router-link-active {
        font-weight: bold; /* 选中的链接加粗 */
      }
      .yh-header-search {
        display: inline-block;
        vertical-align: middle;
        position: relative;
        background: #fff;
        border-radius: 17px;
        padding: 6px 48px 6px 16px;
        margin-right: 24px;
        margin-left: 20px;
        opacity: 0.8;
        .yh-header-search-input {
          border: 0;
          outline: 0;
          font-size: 12px;
          background: transparent;
          opacity: 0.8;
        }
        .yh-header-search-icon {
          font-size: 12px;
          color: #222529;
          position: absolute;
          right: 16px;
          top: 50%;
          transform: translateY(-50%);
          cursor: pointer;
        }
      }
    }
  }
}
</style>
