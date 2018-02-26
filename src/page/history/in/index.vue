<template>
  <Container>
    <TableIn
      :data="vuexHistoryIn"
      @editNum="handleEditNum">
    </TableIn>
  </Container>
</template>

<script>
import vuex from '@/mixins/vuex.js'
export default {
  mixins: [
    vuex
  ],
  methods: {
    // 用户点击了编辑数量
    handleEditNum (row) {
      this.$router.push({
        name: 'history-in-editNum',
        params: {
          id: row.id
        }
      })
    }
  }
}
</script>
