<template>
  <div id="app">
    <!-- 這個每個會面都必須要有 hide-bars-on-scroll往下滾自動隱藏navbar-->
    <f7-page hide-bars-on-scroll="">
      <!-- 這個是往回鍵 -->
      <f7-navbar back-link="Back" title="Page 1" sliding=""></f7-navbar>
    </f7-page>
  </div>
</template>

<script>
export default {
  name: 'page1',
  data() {
    return {
      mydata: 'works'
    }
  }
}
</script>

<style lang="scss">
.red {
  span {
    color: red
  }
}

.cursive {
  span {
    font-style: italic;
  }
}
</style>
