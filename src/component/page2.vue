<template>
  <f7-views navbar-through="">
    <f7-view main="" url="/" :dynamic-navbar="true">
      <f7-navbar>
        <f7-nav-left></f7-nav-left>
        <f7-nav-center sliding="">Twitter-Vue</f7-nav-center>
        <f7-nav-right></f7-nav-right>
      </f7-navbar>
      <!-- All pages are rendered inside of Pages -->
      <!--以下都是router切頁-->
      <f7-pages id="pages">
        <!-- Initial Page -->
        <f7-page class="navbar-fixed">
          <f7-searchbar cancel-link="Cancel" placeholder="Search in items" :clear-button="true"></f7-searchbar>
        </f7-page>
      </f7-pages>
    </f7-view>
  </f7-views>
</template>

<script>
export default {
  name: 'page2',
  data() {
    return {
      mydata: 'is okili-dokili'
    }
  }
}
</script>

<style lang="scss">

</style>
