<template>
  <div>
    <template v-for="item in proxyList">
      <proxy-info :info="item"></proxy-info>
    </template>
    <el-button :loading="loadingData" @click="showMore" plain style="width: 150px;" type="success">more...</el-button>
  </div>
</template>

<script>
  import axios from 'axios';
  import ProxyInfo from "@/components/proxyInfo";

  export default {
    name: "proxyList",
    components: {ProxyInfo},
    data() {
      return {
        loadingData: false,
        params: {
          page: 1,
          skip: 0,
          pageSize: 30
        }
      }
    },
    async asyncData() {
      const timeStamp = new Date().getTime();
      const url = `https://api.openproxy.space/short?skip=0&ts=${timeStamp}&limit=20`;
      let response = await axios.get(url);
      return {
        proxyList: response.data,
        timeStamp
      };
    },
    methods: {
      async toGetList() {
        this.loadingData = true;
        const url = `https://api.openproxy.space/short?skip=${this.params.skip}&ts=${this.timeStamp}&limit=${this.params.pageSize}`;
        let response = await axios.get(url);
        let data = response.data;
        if (data.status && data.status === 'error') {
          this.$message.error(data.message);
        } else {
          this.proxyList.push(...data);
        }
        this.loadingData = false;
      },
      showMore() {
        this.params.page++;
        this.params.skip = (this.params.page - 1) * this.params.pageSize;
        this.toGetList();
      }
    }
  }
</script>
