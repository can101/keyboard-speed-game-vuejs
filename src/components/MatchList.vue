<template>
  <div class="container">
    <table>
      <thead>
      <tr>
        <th class="table-header">#</th>
        <th class="table-header">İstenilen</th>
        <th class="table-header">Girilen</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item,index) in list" :key="index" class="wrapper">
        <td :class="['correct-box', item.isStatus&&'bg-succes',!item.isStatus&&'bg-danger']">{{ index }}</td>
        <td :class="['correct-box', item.isStatus&&'bg-succes',!item.isStatus&&'bg-danger']">{{ item.value }}</td>
        <td :class="['incorrect-box', item.isStatus&&'bg-succes',!item.isStatus&&'bg-danger']">{{ item.gusess }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "MatchList",
  props: ["list"],
}
</script>

<style scoped>
.container {
  user-select: none;
}

.container table {
  width: 100%;
}

.wrapper {
  width: 100%;
}

.correct-box {

}

.incorrect-box {

}

.correct-box, .incorrect-box, .table-header {
  text-align: center;
  border-radius: 3px;
  padding: 5px;
  box-shadow: inset 0 0 7px #fff;
}

.id-box {
  text-align: center;
  /*background-color: rgb(185 185 185 / 29%);*/
  font-weight: 600;
  color: #F79B2D;
  padding: 5px;
}

.table-header {
  color: #F79B2D;
  padding: 10px;
}

.bg-succes {
  color: #568D73;
  background-color: #baecd2;
}

.bg-danger {
  color: #cc454d;
  background-color: #ffcacd;
}
</style>