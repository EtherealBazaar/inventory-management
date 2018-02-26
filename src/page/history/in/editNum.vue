<template>
  <Container>
    <div>
      <el-button
        type="primary"
        icon="el-icon-arrow-left"
        @click="handleBack">
        返回入库历史
      </el-button>
    </div>
    <p>你想要修改的记录是：</p>
    <TableIn
      :data="[history]">
    </TableIn>
    <p>新的数量是</p>
    <div>
      <el-input-number v-model="value"></el-input-number>
    </div>
    <br>
    <div>
      <el-button>确定修改</el-button>
    </div>
  </Container>
</template>

<script>
import vuex from '@/mixins/vuex.js'
export default {
  mixins: [
    vuex
  ],
  data () {
    return {
      history: null,
      value: 0
    }
  },
  computed: {
    // 这个页面编辑的数据id 从路由参数中传进来
    id () {
      return this.$route.params.id
    }
  },
  created () {
    // 初始化这个页面
    this.init()
  },
  methods: {
    // 初始化这个页面
    init () {
      if (this.id) {
        const history = this.vuexHistoryIn.find(e => e.id === this.id)
        if (history) {
          this.history = history
          this.value = history.num
        } else {
          this.handleBack()
        }
      } else {
        this.handleBack()
      }
    },
    // 返回
    handleBack () {
      this.$router.push({
        name: 'history-in'
      })
    }
  }
}
</script>
