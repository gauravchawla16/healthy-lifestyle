<template>
  <div>
    <div class="row mt-4">
      <div class="d-flex product">
        <div><img width="300" height="200" src="https://static.boydgaming.net/samstownlv10/assets/body_image/ST-Subway-KeyFeatures-640x356.jpg"></div>
        <div class="details ml-3 d-flex flex-column">
          <div class="name">{{item.value}}</div>
          <div class="calories">Calories- {{item.calories}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ComponentDetail',
  props: {
    item: Object,
    default: {}
  }
}
</script>
<style scoped>
.product >.details {
  text-align: left;
    justify-content: center;
}
</style>
