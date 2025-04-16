<script setup>
import { onMounted, ref } from 'vue'
import AMapLoader from '@amap/amap-jsapi-loader'
import { useRouter } from 'vue-router'

const map = ref(null)
const router = useRouter()

onMounted(() => {
  initMap()
})

const initMap = async () => {
  try {
    const AMap = await AMapLoader.load({
      key: '02014705b4019e68cd65764c99ad3211',
      version: '2.0',
      plugins: ['AMap.Scale', 'AMap.ToolBar', 'AMap.CircleEditor'],
    })

    // 创建地图实例
    map.value = new AMap.Map('container', {
      zoom: 13,
      center: [104.065831, 30.657338],
      viewMode: '2D',
      mapStyle: 'amap://styles/normal',
      layers: [new AMap.TileLayer()], // 添加图层
    })

    // 等待地图加载完成
    map.value.on('complete', () => {
      // 创建圆形范围
      const circle = new AMap.Circle({
        center: [104.065831, 30.657338],
        radius: 20000,
        strokeColor: '#3366FF',
        strokeWeight: 2,
        strokeOpacity: 0.3,
        fillColor: '#FFA500',
        fillOpacity: 0.1,
      })

      // 将圆形添加到地图
      circle.setMap(map.value)

      // 自适应圆形范围
      map.value.setFitView([circle])
    })

    // 添加控件
    map.value.addControl(new AMap.Scale())
    map.value.addControl(new AMap.ToolBar())

  } catch (error) {
    console.error('地图加载失败：', error)
  }
}

const handleMenuClick = (key) => {
  switch (key) {
    case '1':
      router.push('/')
      break
    case '2':
      router.push('/map')
      break
  }
}

const goToLogin = () => {
  router.push('/login')
}
</script>

<template>
  <div class="app-container">
    <a-layout class="layout">
      <a-layout-header class="header">
        <div class="header-content">
          <div class="left-section">
            <div class="nav-group">
              <span class="logo">户外徒步导航</span>
              <a 
                :class="['nav-link', $route.path === '/' ? 'active' : '']" 
                @click="handleMenuClick('1')"
              >
                主页
              </a>
              <a 
                :class="['nav-link', $route.path === '/map' ? 'active' : '']" 
                @click="handleMenuClick('2')"
              >
                地图
              </a>
            </div>
          </div>
          <div class="right-section">
            <a-button type="primary" @click="goToLogin" class="login-button">登录</a-button>
          </div>
        </div>
      </a-layout-header>
      <a-layout-content class="content">
        <router-view></router-view>
      </a-layout-content>
      <a-layout-footer class="footer">
        &copy; 2024
      </a-layout-footer>
    </a-layout>
  </div>
</template>

<style scoped>
.app-container {
  width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.layout {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  background-color: var(--color-bg-2);
  border-bottom: 1px solid var(--color-border);
  padding: 0;
  height: 50px;
}

.header-content {
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 24px;
  width: 100%;
}

.left-section {
  flex: 1;
  min-width: 0;
  display: flex;
  align-items: center;
  padding-left: 24px;
}

.nav-group {
  display: flex;
  align-items: center;
  gap: 24px;
  white-space: nowrap;
}

.logo {
  font-size: 18px;
  font-weight: bold;
  color: var(--color-text-1);
  margin-right: 12px;
}

.nav-link {
  font-size: 15px;
  color: var(--color-text-2);
  cursor: pointer;
  text-decoration: none;
  padding: 0 4px;
  position: relative;
  transition: color 0.3s;
}

.nav-link:hover {
  color: rgb(var(--primary-6));
}

.nav-link.active {
  color: rgb(var(--primary-6));
  font-weight: 500;
}

.nav-link.active::after {
  content: '';
  position: absolute;
  bottom: -14px;
  left: 0;
  width: 100%;
  height: 2px;
  background-color: rgb(var(--primary-6));
}

.right-section {
  flex-shrink: 0;
  margin-left: 16px;
  position: absolute;
  right: 48px;
}

.login-button {
  padding: 0 20px;
}

.content {
  flex: 1;
  margin-top: 50px;
  padding-bottom: 30px;
  background: var(--color-fill-2);
  position: relative;
  height: calc(100vh - 80px);
}

.footer {
  height: 30px;
  line-height: 30px;
  text-align: center;
  background: var(--color-bg-2);
  flex-shrink: 0;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

:deep(.arco-layout-header) {
  height: 50px;
  line-height: 50px;
  padding: 0;
}

:deep(.arco-layout-content) {
  padding: 0;
  height: 100%;
}

:deep(.router-view-container) {
  height: 100%;
}
</style>