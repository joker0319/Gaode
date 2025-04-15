<script setup>
</script>

<template>
  <div class="basicLayout">
    <div class="layout-demo">
    <a-layout style="height: 400px;">
      <a-layout-header>
        <a-row class="grid-demo" style="margin-bottom: 16px;" :wrap="false">
    <a-col flex="auto">
      <div class="menu-demo">
     <a-menu mode="horizontal" :default-selected-keys="['1']">
       <a-menu-item key="0" :style="{ padding: 0, marginRight: '80px' }" disabled>
         <div
           :style="{
             width: '80px',
             height: '30px',
             borderRadius: '2px',
             background: 'var(--color-fill-3)',
             cursor: 'text',
           }"
         />
       </a-menu-item>
       <a-menu-item key="1">主页</a-menu-item>
       <a-menu-item key="2">地图</a-menu-item>
       <a-menu-item key="3">提问</a-menu-item>
       <a-menu-item key="4">解决</a-menu-item>
     </a-menu>
    </div>
    </a-col>
    <a-col flex="100px">
      <div class="button">
        <a-button type="primary">登录</a-button>
      </div>
    </a-col>
  </a-row>
      </a-layout-header>
      <a-layout-content>
        <div class="content">
          <img src="https://restapi.amap.com/v3/staticmap?location=104.065831,30.657338&zoom=12&size=750*300&markers=mid&key=02014705b4019e68cd65764c99ad3211" alt="" srcset="">
        </div>
      </a-layout-content>
      <a-layout-footer>
        <div class="footer">footer</div>
      </a-layout-footer>
    </a-layout>
  </div>
  </div>

</template>

<style scoped>
.basicLayout{
  width: 100%;
  height: 700px;
}
.menu-demo {
  box-sizing: border-box;
  width: 100%;
  /* padding: 5px; */
  /* background-color: #ddd; */
}
.layout-demo{
  height: 700px;
  width: 100%;
}
.content{
  height: 600px;
  text-align: center;
}
.footer{
  height:50px;
  text-align: center;
}
.grid-demo{
  align-items: center;
  justify-content: center;
}
</style>