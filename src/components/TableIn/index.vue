<template>
  <el-table
    :data="data"
    size="mini"
    :stripe="stripe"
    border>
    <el-table-column v-if="showName" label="物品" width="150px">
      <template slot-scope="scope">{{dictProject(scope.row.project, 'name')}}</template>
    </el-table-column>
    <el-table-column label="数量" width="100">
      <template slot-scope="scope">
        <el-button type="success" size="mini" @click="handleEditNum(scope.row)">{{scope.row.num}}</el-button>
      </template>
    </el-table-column>
    <el-table-column label="价格" width="60">
      <template slot-scope="scope">{{dictProject(scope.row.project, 'price')}}</template>
    </el-table-column>
    <el-table-column label="单位" width="60">
      <template slot-scope="scope">{{dictProject(scope.row.project, 'unit')}}</template>
    </el-table-column>
    <el-table-column label="入库日期">
      <template slot-scope="scope">{{mo(scope.row.date)}}</template>
    </el-table-column>
    <el-table-column label="记录日期">
      <template slot-scope="scope">{{mo(scope.row.creatDate)}}</template>
    </el-table-column>
    <el-table-column label="操作" width="100px">
      <template slot-scope="scope">
        <el-button size="mini" type="danger" @click="handleDelete(scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import vuex from '@/mixins/vuex.js'
import dict from '@/mixins/dict.js'
import mo from '@/mixins/mo.js'
export default {
  mixins: [
    vuex,
    dict,
    mo
  ],
  props: {
    data: {
      type: Array,
      required: false,
      default: () => []
    },
    showName: {
      type: Boolean,
      required: false,
      default: true
    },
    stripe: {
      type: Boolean,
      required: false,
      default: true
    }
  },
  methods: {
    handleEditNum (row) {
      this.$router.push({
        name: 'history-in-editNum',
        params: {
          id: row.id
        }
      })
    },
    handleDelete (row) {
      console.log(row)
      this.$confirm('此操作将会删除这条记录', '确认操作?', {
        confirmButtonText: '我要删除',
        cancelButtonText: '点错了',
        type: 'warning'
      }).then(() => {
        // 更新存量
        this.vuexProjectsUpdateNum({
          id: row.project,
          change: -row.num
        })
        this.vuexProjectsLoad()
        // 删除历史
        this.vuexHistoryInDelete(row.id)
        this.vuexHistoryInLoad()
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消'
        })
      })
    }
  }
}
</script>
