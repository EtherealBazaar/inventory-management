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
    handleEditNum (row) {
      console.log(row)
    }
  }
}
</script>
