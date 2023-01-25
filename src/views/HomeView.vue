<template>
  <HeaderView />
  <div class="home container">
    <div class="logo">
      <img src="/img/Github.png" alt="Github Users" />
      <h1>GitHub Users</h1>
    </div>
    <div class="table-heading">
      <div class="id">ID</div>
      <div class="avatar">AVATAR</div>
      <div class="login">LOGIN</div>
      <div class="actions">ACTIONS</div>
    </div>
    <div class="table-rows">
      <div class="table-row" v-for="user in users" :key="user.id">
        <div class="id">{{ user.id }}</div>
        <div class="avatar">
          <img :src="user.avatar_url" />
        </div>
        <div class="login">{{ user.login }}</div>
        <div class="actions"> 
         <router-link :to="'/details/' + user.login"><button>Details</button></router-link>  
        </div>
      </div>
    </div>
    <div class="pagination">
      <div class="prev" @click="prev()">Prev</div>
      <div class="next" @click="next()">Next</div>
    </div>
  </div>
  <FooterView />
</template>

<script>
import HeaderView from '@/components/HeaderView.vue';
import FooterView from '@/components/FooterView.vue';

export default {
    name: "HomeView",
    data() {
        return {
            users: null,
            user_id: null,
            user_avatar: null,
            user_login: null,
            offset:null
        };
    },
    methods: {
        async getUsers() {

            const req = await fetch(`http://localhost:8080/api_github/users?per_page=5`);
            const data = await req.json();
            this.users = data;

        },
        prev() {


        },
        next() {

        }
    },
  mounted() {
      this.getUsers();
  },
  components: { HeaderView, FooterView }
}
</script>
<style scoped>
.logo {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
}

.logo img {
  width: 60px;
}

.logo h1 {
  font-family: inherit;
  font-weight: 400;
  font-size:40px;
}

.table-heading, 
.table-rows, 
.table-row{
  display: flex;
  flex-wrap: wrap;
}

.table-heading {
  background-color:#343a40;
  height:50px;
  align-items: center;
}


.table-heading div {
  color:#fff;
  width: 22%;
}

.table-row {
  margin-bottom: 30px;
}

.table-row {
  color:#333;
  padding: 10px;
  width: 100%;
  border-top: 1px solid #dee2e6;
}

.table-row .id, 
.table-row .avatar, 
.table-row .login, 
.table-row .actions {
  color:#333;
  width: 22%;
}

.table-row .id {
  font-weight: bold;
}

.avatar img {
  max-width: 80px;
  max-height: 80px;
  padding: 5px;
  border: 1px solid #dee2e6;
}

.login {
  width: 200px;
  padding: 15px;
}

.actions button{
  background-color:#343a40;
  padding: 10px 15px;
  color:#fff;
  border-radius:5px;
  cursor: pointer;
}

.pagination {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 15px;
}

.prev, .next{
  border:1px solid #dee2e6;
  border-radius:2px;
  padding: 10px 15px;
  cursor: pointer;
}
</style>
