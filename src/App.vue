<script>
import SideBar from "./components/sidebar/SideBar.vue";

export default {
  name: "App",
  components: {
    SideBar,
  },
};
</script>

<template>
  <SideBar></SideBar>

  <div class="p-4 sm:ml-64">
    <div
      class="p-4 border-2 border-gray-200 border-dashed rounded-lg dark:border-gray-700 mt-14"
    >
      <router-view></router-view>
    </div>
  </div>
</template>
