<template>
  <div>
    <a-card
      class="statistics"
      :bordered="false">
      统计信息
    </a-card>
    <div >
      <a-select default-value="all" style="width: 120px" @change="handleChange">
        <template v-for="(item,index) in selectData">
          <a-select-option :value="item.value" :key="index">
            {{ item.lable }}
          </a-select-option>
        </template>
      </a-select>
      <a-input-search placeholder="输入桥梁名称、编号或者其他属性搜索......" style="width: 350px" @search="onSearch" />
      <a-button type="primary" style="float:right">
        新增桥梁
      </a-button>
    </div>
    <s-table 
      ref="table"
      size="default"
      rowKey="key"
      :columns="columns"
      :data="loadData"
      :alert="false"
      :rowSelection="rowSelection" 
      showPagination="auto">
      <span slot="no" slot-scope="no">
        <span>{{ no[0].bridgeName }}</span><br>
        <span>{{ no[0].number }}</span>
      </span>
      <span slot="action" slot-scope="text, record">
        <template>
          <a @click="handleEdit(record)">详情</a>
          <a-divider type="vertical" />
          <a @click="handleSub(record)">历年检测</a>
          <a-divider type="vertical" />
          <a @click="handleSub(record)">日常巡查</a>
          <a-divider type="vertical" />
          <a @click="handleSub(record)">健康监测</a>
          <a-divider type="vertical" />
          <a @click="handleSub(record)">任务</a>
          <a-divider type="vertical" />
          <a @click="handleSub(record)">应急处理</a>
        </template>
      </span>
      <span slot="tags" slot-scope="tags">
        <a-tag
          v-for="tag in tags"
          :key="tag"
          :color="tag == 'car' ? 'green' : 'blue'">
          <a-icon :type="tag"/>
        </a-tag>
      </span>
      <span slot="callNo" slot-scope="callNo">
        <span>规模：{{ callNo[0].scale }}</span><br>
        <span>用途：{{ callNo[0].use }}</span><br>
        <span>结构形式：{{ callNo[0].structure }}</span><br>
        <span>养护等级：{{ callNo[0].level }}</span>
      </span>
      <span slot="dept" slot-scope="dept">
        <span>{{ dept[0].one }}</span><br>
        <span>{{ dept[0].two }}</span>
      </span>
    </s-table>
  </div>
</template>

<script>
// import { STable, Ellipsis } from '@/components'
// import { getRoleList, getServiceList } from '@/api/manage'
export default {
  name:'BridgeList',
  components: {
    // STable
  },
  data(){
    return{ 
      selectData:[
        {lable:'全部',value:'all'},
        {lable:'桥梁名称',value:'bridgeName'},
        {lable:'桥梁id',value:'bridgeId'},
        {lable:'桥梁编号',value:'bridgeNumber'},
        {lable:'地区',value:'region'},
        {lable:'桥梁类型',value:'bridgeType'},
        {lable:'是否危桥',value:'bridgeDanger'}
      ],
      // 查询参数
      queryParam: {},
      // 加载数据方法 必须为 Promise 对象
      // loadData: parameter => {
      //   const requestParameters = Object.assign({}, parameter, this.queryParam)
      //   console.log('loadData request parameters:', requestParameters)
      //   return getServiceList(requestParameters)
      //     .then(res => {
      //       return res.result
      //     })
      // },
      // selectedRowKeys: [],
      // selectedRows: [],
      // columns : [
      //   {
      //     title: '桥梁名称',
      //     children: [
      //       {
      //         title:'桥梁编号',
      //         dataIndex: 'no',
      //         scopedSlots: { customRender: 'no' }
      //       }
      //     ],
      //   },
      //   {
      //     title: '标签',
      //     dataIndex: 'tags',
      //     scopedSlots: { customRender: 'tags' }
      //   },
      //   {
      //     title: '市/区',
      //     dataIndex: 'description',
      //     scopedSlots: { customRender: 'description' }
      //   },
      //   {
      //     title: '桥梁类型',
      //     dataIndex: 'callNo',
      //     needTotal: false,
      //     scopedSlots:{customRender: 'callNo'}
      //   },
      //   {
      //     title: '状态',
      //     dataIndex: 'status',
      //     customRender: (status)=>status== 1 ? '正常' : '危桥'
      //   },
      //   {
      //     title: '属性',
      //     dataIndex: 'attribute',
      //     scopedSlots:{customRender: 'attribute'}
      //   },
      //   {
      //     title: '档案',
      //     align:'center',
      //     children:[{
      //       align:'center',
      //       dataIndex: 'number',
      //       title: '全国统一编号'
      //     }]
      //   },
      //   {
      //     title: '管理单位/联系人 ',
      //     align:'center',
      //     children:[{
      //       align:'center',
      //       title: '管养单位/联系人',
      //       dataIndex: 'dept',
      //       scopedSlots: { customRender: 'dept' }
      //     }]
      //   },
      //   {
      //     title: '操作',
      //     dataIndex: 'action',
      //     width: '230px',
      //     align:'center',
      //     scopedSlots: { customRender: 'action' }
      //   }
      // ]
    }
  },
  created () {
    // getRoleList({ t: new Date() })
  },
  computed: {
    rowSelection () {
      return {
        selectedRowKeys: this.selectedRowKeys,
        onChange: this.onSelectChange
      }
    }
  },
  methods: {
    onSelectChange (selectedRowKeys, selectedRows) {
      this.selectedRowKeys = selectedRowKeys
      this.selectedRows = selectedRows
    },
    handleChange(value) {
      console.log(`选择： ${value}`)
    },
    onSearch(value) {
      console.log(`搜索关键词：${value}`)
    },
    handleAdd () {
      // this.mdl = null
      // this.visible = true
    },
    handleEdit (record) {
      this.$message.info(`点击第${record.key}行详情`)
      // this.visible = true
      // this.mdl = { ...record }
    },
    handleSub (record) {
      this.$message.info(`点击第${record.key}行`)
      console.log(record)
      // if (record.status !== 0) {
      //   this.$message.info(`${record.no} 订阅成功`)
      // } else {
      //   this.$message.error(`${record.no} 订阅失败，规则已关闭`)
      // }
    },
  }
}
</script>

<style lang="less" scoped>
.statistics{
  height: 100px;
}
</style>