<template>
  <HeaderView />
  <div class="details">
    <div class="member">
      <div class="avatar">
        <img :src="user_avatar" :alt="user_login">
      </div>
      <div class="info">
        <p><span> #</span> {{ user_id }} - {{ user_login }}</p>
        <p><span>Profile URL:</span> {{ profileUrl }}</p>
        <p><span>Created at:</span> {{created}}</p>
      </div>
      <div class="button">
        <router-link to="/"><button>Go Back</button></router-link>
      </div>
    </div>

    <div class="repos">
      <div class="table-heading-repos">
        <div class="id">ID</div>
        <div class="repo">Repository</div>
        <div class="url">URL</div>
      </div>
      <div class="table-rows-repos">
        <div class="table-row-repos" v-for="repo in repos" :key="repo.id">
          <div class="id">{{repo.id}}</div>
          <div class="repo">{{repo.name}}</div>
          <div class="url"><a :href="repo.html_url" :alt="repo.name">{{repo.html_url}}</a></div>
        </div>
      </div>
    </div>
  </div>
  <FooterView />
</template>

<script>
import HeaderView from '@/components/HeaderView.vue';
import FooterView from '@/components/FooterView.vue';

export default {
  name: "DetailsView",
  data() {
    return {
      user: null,
      user_avatar: null,
      user_id: null,
      user_login: null,
      profileUrl:null,
      created:null,
      repos:null
    };
  },
  methods: {
    async getUser() {
      const req = await fetch(`http://localhost:8080/api_github/users/${this.$route.params.repo}`);
      const data = await req.json();
      this.user = data;
      //resgatar dados

      this.user_id = data.id;
      this.user_avatar = data.avatar_url;
      this.created = data.created_at;
      this.user_login = data.login;
      this.profileUrl = data.html_url;
      console.log(data);
    },
    async getUserRepo() {
      const req = await fetch(`http://localhost:8080/api_github/users/${this.$route.params.repo}/repos`);
      const data = await req.json();
      this.repos = data;
    }
  },
  mounted() {
    this.getUser(),
    this.getUserRepo()
  },
  components: { HeaderView, FooterView }
}
</script>
<style scoped>
.details {
  display: flex;
  flex-direction: row;
  color:#000;
  width: 100%;
  padding: 30px 0px;
}

.details .member {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 50%;
  height: 300px;
  padding-left: 10px;

}

.details .repos {
  width: 50%;
}

.avatar, .avatar img  {
  width: 300px;
  height: 300px;
  margin-right: 10px;
}

.member .info {
  width:40%;
  padding: 10px;
}

.member .info p {
  text-align: left;
  font-size: 14px;
  margin-bottom: 10px;
}

.member .info span {
  font-weight: bold;
}

.table-heading-repos, 
.table-rows-repos, 
.table-row-repos{
  display: flex;
  flex-wrap: wrap;

}

.table-heading-repos {
  background-color:#343a40;
  height:50px;
  align-items: center;
  
}

.table-heading-repos {
  color:#fff;
}

.table-row-repos {
flex-wrap: wrap;
}

.table-row-repos div {
  font-size:14px;
  }

.table-heading-repos .id, 
.table-row-repos .id {
  width: 75px;
  padding: 10px;
}

.table-heading-repos .repo, 
.table-row-repos .repo {
  width: 200px;
  padding: 10px 0;
}

.table-heading-repos .url, 
.table-row-repos .url {
  width: auto;
  padding: 10px 0;
}

.table-row-repos .url a{
  text-decoration: none;
}

.member .button  {
  display: flex;
  width: 100%;
  margin: 20px 0;
  
}

.member .button button {
  background-color:#343a40;
  padding: 10px 15px;
  color:#fff;
  border-radius:5px;
  cursor: pointer;
}

</style>

