<template>
  <a-config-provider :locale="appLocale">
    <div id="app">
      <!-- 路由出口：所有页面通过这里渲染 -->
      <BasicLayout />
      <!-- 全局的返回上一级按钮 -->
      <div class="back-btn-container">
        <a-tooltip title="返回上一级">
          <a-button
            type="primary"
            shape="round"
            :icon="h(ArrowLeftOutlined)"
            class="back-btn"
            @click="handleBack"
          />
        </a-tooltip>
      </div>
    </div>
  </a-config-provider>
</template>

<script setup lang="ts">
import BasicLayout from '@/layout/BasicLayout.vue'
// import { healthCheck } from '@/api/healthController.ts'
import router from '@/router'
import { ArrowLeftOutlined } from '@ant-design/icons-vue'
import { h } from 'vue'
import dayjs from 'dayjs'
import zhCN from 'ant-design-vue/es/locale/zh_CN' // 引入 ant-design-vue 的中文语言包

// // 获取健康检查信息
// healthCheck().then((res) => {
//   console.log(res.data)
// })

dayjs.locale('zh-cn')
// 使用 Composition API 和 setup 函数定义响应式数据
const appLocale = zhCN // 设置当前应用的语言环境

// 添加返回上一级逻辑
const handleBack = () => {
  router.back()
}
</script>

<style>
/* 全局样式优化 */
#app {

}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family:
    -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell',
    'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  overflow-x: hidden;
}

html {
  overflow-x: hidden;
}

/* 返回按钮容器：固定在右下角 */
.back-btn-container {
  position: fixed; /* 固定定位，不随滚动变化 */
  right: 30px; /* 距离右侧30px */
  bottom: 90px; /* 距离底部90px（避开footer） */
  z-index: 8; /* 确保在内容上方，低于header和footer */
}

/* 返回按钮样式 - 圆形设置 */
.back-btn {
  opacity: 0.5;
  width: 56px;
  height: 56px;
  font-size: 20px;
  background-color: #5e4caf; /* 主色调 */
  border-color: #6777b4;
  border-radius: 50% !important; /* 关键：设置为50%实现圆形 */
  box-shadow: 0 4px 12px rgba(53, 7, 148, 0.3); /* 阴影增强立体感 */
  transition: all 0.3s ease;
}

/* 按钮悬停效果 - 保持圆形 */
.back-btn:hover {
  background-color: #5e4caf;
  border-color: #6777b4;
  transform: translateY(-3px); /* 上移效果 */
  box-shadow: 0 6px 16px rgba(53, 7, 148, 0.3);
  /* 移除hover状态的border-radius修改，保持圆形 */
}
</style>
