<template>
  <div>
    <h1>Check Profile</h1>
    <input v-model="searchName" class="searchterm"> 
    <button v-on:click="search" class="buttonstyle">Search Name</button><br>
    <div v-if="DataList.id">
    <h2>User Name : {{DataList.login}}</h2>
    <img :src="DataList.avatar_url" :class = 'imgstyle'/><br>
    <button type="button" class="buttonstyle" v-on:click="site(DataList.html_url)">Go-to Github profile</button><br>
    <button class="buttonstyle" v-on:click="following">Following</button><br>
    <ul>
      <li v-for=" item in Following" v-bind:key="item"> 
        {{item.login}}
        <button type="button" v-on:click="site(item.html_url)">Go-to Github profile</button><br>
      </li>
    </ul>
    <button class="buttonstyle" v-on:click="followers">Followers</button><br>
    <ul>
      <li v-for=" item in Followers" v-bind:key="item"> 
        {{item.login}}
        <button type="button" v-on:click="site(item.html_url)">Go-to Github profile</button><br>
      </li>
    </ul>
  </div>
  </div>  
</template>

<script>
export default {
  name: "Myapp",
  searchName : '',
  data() {
    return {
      DataList: [],
      Following: [],
      Followers: []
    };
  },
  methods: {
    search(){
      fetch('https://api.github.com/users/'+this.searchName)
        .then(response => response.json())
        .then(data => (this.DataList = data));
    },
    followers() {
      fetch('https://api.github.com/users/'+ this.searchName +'/followers')
        .then(response => response.json())
        .then(data => (this.Followers = data))
        .then(this.Following = "");
    },
    following() {
      fetch('https://api.github.com/users/'+ this.searchName +'/following')
        .then(response => response.json())
        .then(data => (this.Following = data))
        .then(this.Followers ="");
    },
    site(url){
      window.location.href = url
    }
  }
};
</script>


<style scoped>
.buttonstyle {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.searchterm {
  position: relative;
  width: 20%;
  border: 3px solid #00B4CC;
  padding: 5px;
  height: 20px;
  border-radius: 5px 0 0 5px;
  outline: none;
  color: #9DBFAF;
}

.imgstyle {
  float: left;
  width:170px;
  height:170px;
  margin-right:15px;
}

</style>