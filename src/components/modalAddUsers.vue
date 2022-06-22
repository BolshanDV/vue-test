<template>
  <div
    class="modal-section"
    v-if="show"
  >
    <div class="modal-section__header">
      Добавление пользователя
    </div>
    <div class="modal-section__content">
      <div class="modal-content">
        <div class="modal-content__name">
          <p>Имя</p>
        </div>
        <div class="modal-content__input">
          <div class="input-field">
            <input
              v-model="user.name"
              class="validate"
              type="text"
            >
          </div>
        </div>
      </div>
      <div class="modal-content">
        <div class="modal-content__name">
          <p>Телефон</p>
        </div>
        <div class="modal-content__input">
          <div class="input-field">
            <input
              v-model="user.phoneNumber"
              id="icon_telephone"
              class="validate"
              type="tel"
            >
          </div>
        </div>
      </div>
      <div class="modal-content">
        <div class="modal-content__name">
          <p>Начальник</p>
        </div>
        <div class="modal-content__select">
          <select
            class="browser-default"
            v-model="user.chief"
          >
            <option value="" disabled selected>Choose your chief</option>
            <option
              v-for="(userItem, index) of users"
              :key="index"
              :value="userItem"
            >{{userItem.name}}
            </option>
          </select>
        </div>
      </div>
    </div>
    <div
      class="modal-section__footer"
    >
      <div class="modal-footer__button">
        <a
          class="waves-effect waves-light btn"
          @click="saveUser"
        >
          Сохранить
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'modalAddUsers',
  data () {
    return {
      show: false,
      selectedChief: '',
      users: localStorage['users'] ? JSON.parse(localStorage['users']) : [],
      user: {
        name: '',
        phoneNumber: '',
        chief: {}
      }
    }
  },
  methods: {
    openModal: function () {
      this.show = true
    },
    closeModal: function () {
      this.show = false
    },
    saveUser: function () {
      if (this.user.name !== '' && this.user.phoneNumber !== '') {
        const users = JSON.stringify(this.user)
        this.users.push(JSON.parse(users))
        this.$emit('users', {userData: this.users})
        localStorage['users'] = JSON.stringify(this.users)
        this.closeModal()
      }
      this.user = {
        name: '',
        phoneNumber: '',
        chief: {}
      }
    }
  }
}
</script>

<style scoped>
.modal-section{
  width: 90%;
  padding: 4% 2%;
  border: 2px solid gray;
  border-radius: 5px ;
}
.modal-content{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 100%;
}
.modal-content__name{
  width: 20%;
}
.modal-content__input{
  width: 60%;
}
.modal-content__select{
  width: 60%;
}
.modal-section__footer{
  margin-top: 5%;
}
.input-field{
  margin: 0;
}
</style>
