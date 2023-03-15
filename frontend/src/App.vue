<script>
export default {

}
</script>
<template>
  <div class="d-flex flex-column body" style="flex: 1;">
    <router-view class="d-flex flex-column" style="flex: 1;" />
  </div>
</template>
<style scoped>
.body {
  background: rgb(155, 198, 251);
  background: linear-gradient(90deg, rgba(155, 198, 251, 1) 0%, rgba(213, 197, 252, 1) 100%);
}
</style>