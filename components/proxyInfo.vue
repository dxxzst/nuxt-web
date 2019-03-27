<template>
  <div>
    <div :class="flagClass" class="country-icon"></div>
    <div>

    </div>
  </div>
</template>

<script>
  import {codes as countryCode} from '~/plugins/countryCode';

  export default {
    props: {
      info: {
        type: Object,
        required: true
      }
    },
    name: "proxyInfo",
    computed: {
      flagClass: function () {
        let detail = countryCode[this.info.country];
        console.log(detail);
        return `${detail.flag} png`;
      }
    }
  }
</script>
