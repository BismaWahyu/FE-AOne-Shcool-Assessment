<template>
  <v-app>
    <v-navigation-drawer app class="dark-theme-1">
      <v-container>
        <v-img 
          src="/assets/logo.png" 
          width="150" 
          class="ml-4"
        />
        
        <v-list dense>
          <v-list-item style="background-color: aqua; cursor: pointer;">
            <v-list-item-icon class="mr-2">
              <v-icon>mdi-information</v-icon>
            </v-list-item-icon>
            <v-list-item-content>About</v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-icon class="mr-2">
              <v-icon>mdi-account-group</v-icon>
            </v-list-item-icon>
            <v-list-item-content>Users</v-list-item-content>
          </v-list-item>
        </v-list>
      </v-container>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-container class="d-flex justify-space-between">
        <div>
          <span class="header-title">Users</span>
        </div>
        <div class="profile-menu">
          <span class="mr-3">Jones Ferdinand</span>
          <v-avatar color="primary" size="36">
            <img src="/assets/avatar.png" alt="Avatar">
          </v-avatar>
        </div>
      </v-container>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-card title="All Users">
          <v-data-table
            :headers="headers"
            :items="users"
            items-per-page="5"
            dense
          >
            <template v-slot:item="{ item }">
              <tr>
                <td>
                  <v-avatar color="primary" size="40">
                    <img :src="item.avatar" alt="Avatar">
                  </v-avatar>
                </td>
                <td>{{ item.full_name }}</td>
                <td>{{ item.email }}</td>
              </tr>
            </template>
          </v-data-table>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default{
    data() {
      return {
        headers: [
          { text: ' ', value: 'avatar' },
          { text: 'Full Name', value: 'full_name' },
          { text: 'Email', value: 'email' },
        ],
        users: [
          { avatar: 'https://reqres.in/img/faces/1-image.jpg', full_name: 'Tom Cruise', email: 'george.bluth@regres.in' },
          { avatar: 'https://reqres.in/img/faces/2-image.jpg', full_name: 'Matt Damon', email: 'janet.weaver@reqres.in' },
          { avatar: 'https://reqres.in/img/faces/3-image.jpg', full_name: 'Chris Evans', email: 'charles.monis@regres.in' },
          { avatar: 'https://reqres.in/img/faces/4-image.jpg', full_name: 'Christian Bale', email: 'tracey.ramos@regres.in' },
        ],
      }
    },
    methods: {
      
    },
    head() {
      return {
        title: 'AOne School | Challenge',
      }
    }
  }
</script>

<style scoped>
  .dark-theme-1{
    background-color: #333;
    color: #ffffff;
  }
  .dark-theme-2{
    background-color: #4F4F4F;
    color: #ffffff
  }
  .fab{
    position: absolute;
    bottom: 0;
    right: 0;
  }
  .fab-items{
    z-index: 1;
    transition: transform 0.3s ease;
  }
  .move-expand{
    transform: translateX(120px);
  }
  .inbox-selected{
    transform: translateX(20px)
  }
  .inbox-switch{
    transform: translateX(-75px);
  }
  .task_selected{
    transform: translateX(115px);
  }
  .inbox-container{
    position: fixed;
    bottom: 85px;
    right: 20px;
  }
  .light-avatar{
    background-color: #2F80ED;
    border-radius: 100%;
  }
  .dark-avatar{
    background-color: #E0E0E0;
    border-radius: 100%;
  }
  .profile-menu {
    display: flex;
    align-items: center;
  }
  .header-title{
    font-weight: bold;
    font-size: 22px;
  }
  .item-title{
    color:#2F80ED;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
  }
  .item-person{
    font-size: 14px;
    font-weight: bold;
  }
  .item-subject{
    font-size: 12px;
  }
  .item-date{
    font-size: 11px;
  }
  .chatroom-title{
    color:#2F80ED;
    font-weight: bold;
    font-size: 16px;
    flex: 1;
    overflow-y: auto;
  }
  .chatroom-subtitle{
    font-size: 10px;
  }
  .msg-container{
    display: flex;
    flex-direction: column;
    margin-left: 30px;
    margin-right: 30px;
    margin-top: -500px;
  }
  .other-msg-item{
    background-color: #FCEED3;
    min-width: 250px; 
    max-width: 500px;
    width: fit-content;
    border-radius: 4%;
    padding: 15px;
  }
  .my-msg-item{
    background-color: #EEDCFF;
    min-width: 250px; 
    max-width: 380px;
    width: fit-content;
    border-radius: 4%;
    padding: 15px;
    margin-bottom: 20px;
    align-self: flex-end;
  }
  .msg-field{
    position: absolute;
    bottom: 0;
    left: 0;
    margin-left: 15px;
    width: 700px; 
    display: flex; 
    align-items: stretch;
  }
  .type-field{
    width: 100%;
  }
  .send-button{
    margin-left: 10px;
    height: 55px;
  }
  .msg-content{
    font-size: 14px;
  }
  .msg-time{
    font-size: 12px;
    margin-top:15px;
  }
</style>