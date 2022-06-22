<template>
  <div class="app">
    <div class="app__section">
      <div class="button">
        <a
          class="waves-effect waves-light btn"
          @click="$refs.modal.openModal()"
        >
          Добавить
        </a>
      </div>
      <user-table
        :users="users"
      />
    </div>
    <div class="app__section">
      <div
        class="modal-element"
      >
        <modal-add-users
          ref="modal"
          @users="saveData"
        />
      </div>
    </div>
  </div>
</template>

<script>
import userTable from './components/userTable'
import modalAddUsers from './components/modalAddUsers'
export default {
  name: 'App',
  components: {
    userTable,
    modalAddUsers
  },
  data () {
    return {
      users: localStorage['users'] ? JSON.parse(localStorage['users']) : []
    }
  },
  methods: {
    saveData: function (data) {
      this.users = data.userData
    }
  }
}
</script>

<style lang="css">
@import "../node_modules/materialize-css/dist/css/materialize.min.css";
.app{
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: flex-start;
}
.app__section{
  padding: 20px;
  width: 50%;
  display: flex;
  flex-direction: column;
}
</style>
