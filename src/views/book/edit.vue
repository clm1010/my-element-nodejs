<template>
  <detail :is-edit="true" />
</template>

<script>
import Detail from './components/Detail.vue'
export default {
  name: 'Edit',
  components: { Detail }
}
</script>

<style lang="scss" scoped></style>
