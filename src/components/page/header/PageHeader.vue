<template>
  <div :class="['page-header', layout, pageWidth]">
    <div class="page-header-wide">
      <div class="breadcrumb">
        <a-breadcrumb>
          <a-breadcrumb-item :key="index" v-for="(item, index) in breadcrumb">
            <span>{{item}}</span>
          </a-breadcrumb-item>
        </a-breadcrumb>
        <div class="breadcrumb-select">
          <a-select default-value="jack" style="width: 120px" @change="handleChange">
            <a-select-option value="jack">
              市级
            </a-select-option>
          </a-select>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
  name: 'PageHeader',
  props: {
    title: {
      type: [String, Boolean],
      required: false
    },
    breadcrumb: {
      type: Array,
      required: false
    },
    logo: {
      type: String,
      required: false
    },
    avatar: {
      type: String,
      required: false
    },
  },
  methods:{
    handleChange(e){
      console.log(e)
    }
  },
  computed: {
    ...mapState('setting', ['layout', 'showPageTitle', 'pageWidth'])
  }
}
</script>

<style lang="less" scoped>
  @import "index";
</style>
