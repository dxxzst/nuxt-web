<template>
  <el-container>
    <el-row>
      <el-menu :default-active="activeIndex2"
               @select="handleSelect"
               active-text-color="#ffd04b" background-color="#545c64" class="el-menu-demo" mode="horizontal" text-color="#fff">
        <el-menu-item index="1">首页</el-menu-item>
        <el-menu-item index="3">测试</el-menu-item>
      </el-menu>
    </el-row>
    <el-main>
      <Logo></Logo>
    </el-main>
    <el-footer>Footer</el-footer>
  </el-container>
</template>

<script>
  import Logo from '~/components/Logo.vue'

  export default {
    components: {
      Logo
    },
    data() {
      return {
        activeIndex: '1',
        activeIndex2: '1'
      };
    },
    methods: {
      handleSelect(key, keyPath) {
        console.log(key, keyPath);
      }
    }
  }
</script>

<style>
  .el-header, .el-footer {
    text-align: center;
  }

  .el-main {
    text-align: center;
  }
</style>
