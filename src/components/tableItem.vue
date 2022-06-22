<template>
  <div>
    <table>
      <tbody>
      <tr>
        <td class="tableName">{{userItem.name}}</td>
        <td>+ {{userItem.phoneNumber}}</td>
      </tr>
      </tbody>
    </table>
    <table-item
      :childUser="JSON.stringify(userItem.chief) !== '{}'"
      v-if="JSON.stringify(userItem.chief) !== '{}'"
      :class="{childElement: childUser}"
      :userItem="userItem.chief"
    />
  </div>
</template>

<script>
export default {
  name: 'tableItem',
  props: ['userItem', 'childUser']
}
</script>

<style scoped>
.childElement{
  margin-left: 25px;
}
.tableName{
  width: 45%;
}
</style>
