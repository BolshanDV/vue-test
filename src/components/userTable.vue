<template>
  <div
    v-if="users.length"
    class="table"
  >
    <div class="table__section">
      <table>
        <thead>
        <tr>
          <th @click="sortByName">Имя</th>
          <th @click="sortByNumber">Телефон</th>
        </tr>
        </thead>
      </table>
      <table-item
        v-for="(userItem, index) of users"
        :childUser="JSON.stringify(userItem.chief) !== '{}'"
        :userItem="userItem"
        :key="index"
      />
    </div>
  </div>

</template>

<script>
import tableItem from './tableItem'
export default {
  name: 'userTable',
  props: ['users'],
  components: {
    tableItem
  },
  methods: {
    sortByName: function () {
      this.users.sort((sortElementA, sortElementB) => {
        let nameA = sortElementA.name.toLowerCase()
        let nameB = sortElementB.name.toLowerCase()
        if (nameA < nameB) {
          return -1
        }
        if (nameA > nameB) {
          return 1
        }
        return 0
      })
    },
    sortByNumber: function () {
      this.users.sort((sortElementA, sortElementB) => {
        return sortElementA.phoneNumber - sortElementB.phoneNumber
      })
    }
  }
}
</script>

<style scoped>
.table{
  width: 90%;
}
</style>
