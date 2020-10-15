<template>
  <div class="header">
    <!-- <div class="header__count"><b>Count</b>: 1/4</div> -->
    <div class="header__title"><b>Vue QUIZ</b></div>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  display: flex;
  flex-direction: row;
  background-color: cadetblue;
  color: white;
  height: 50px;
  justify-content: center;
}
.header__count {
  margin-left: 10px;
  display: flex;
  align-items: center;
  flex: 0.5;
}
.header__title {
  font-size: 20px;
  display: flex;
  align-items: center;
}
</style>