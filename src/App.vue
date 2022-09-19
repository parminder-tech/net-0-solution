<template>
  <div id="topNav">
    <top-nav></top-nav>
    <div class="d-flex">
      <side-nav id="sideBar"></side-nav>
      <main id="main">
        <Org />
      </main>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import TopNav from "@/components/layout/TopNav.vue";
import SideNav from "@/components/layout/SideNav.vue";
import Org from "@/components/Org.vue";
export default defineComponent({
  name: "Home",
  components: {
    TopNav,
    SideNav,
    Org,
  },
});
</script>
<style lang="scss">
#app {
  font-family: Poppins;
  box-sizing: border-box;
}
#main {
  width: calc(100vw - 45px);
  min-height: calc(100vh - 64px);
  background: #f8fcfc;
  margin-left: auto;
  border-top: 1px solid hsla(0, 0%, 44%, 0.12);
}
#sideBar {
  position: fixed;
  top: 63px;
  left: 0;
  height: 100%;
  border-right: 1px solid hsla(0, 0%, 44%, 0.12);
  padding-top: 1.5625rem;
  z-index: 1;
  &:hover{
    z-index: 2;
  }
}
::placeholder {
  color: hsla(0, 0%, 44%, 0.3);
  font-weight: 300;
  font-size: 16px;
  opacity: 1; /* Firefox */
}

:-ms-input-placeholder {
  color: hsla(0, 0%, 44%, 0.3);
  font-size: 16px;
  font-weight: 300;
}

::-ms-input-placeholder {
  color: hsla(0, 0%, 44%, 0.3);
  font-size: 16px;
  font-weight: 300;
}
.form-control {
  color: #232426;
  width: 100%;
}
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-thumb {
  background-color: #c4ffcf;
  border-radius: 8px;
}
::-webkit-scrollbar-track {
  background-color: #ededed;
  border-radius: 8px;
}
</style>
<style scoped>
#main {
  position: relative;
  z-index: 1;
}
</style>
