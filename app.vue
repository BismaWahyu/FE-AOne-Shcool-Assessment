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
          <v-list-item style="cursor: pointer;">
            <v-list-item-icon class="mr-2">
              <v-icon>mdi-information</v-icon>
            </v-list-item-icon>
            <v-list-item-content>About</v-list-item-content>
          </v-list-item>
          <v-list-item style="cursor: pointer;">
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
        <v-card v-if="userDetail === null" title="All Users">
          <v-skeleton-loader :loading="isList" type="table">
            <v-data-table
              :headers="headers"
              :items="userList"
              item-value="name"
            >
              <template v-slot:headers="{ columns }">
                <tr>
                  <template v-for="column in columns" :key="column.key">
                    <td>
                      <span class="mr-2 cursor-pointer" >{{ column.title }}</span>
                    </td>
                  </template>
                </tr>
              </template>          
                <template v-slot:item="{ item }">
                  <tr>
                    <td>
                      <v-avatar color="primary" size="40">
                        <img :src="item.avatar" alt="Avatar">
                      </v-avatar>
                    </td>
                    <td>{{ item.first_name }}</td>
                    <td>{{ item.last_name }}</td>
                    <td>{{ item.email }}</td>
                    <td>
                      <v-btn 
                        rounded="xl" 
                        elevation="2" 
                        color="#65A7DB" 
                        variant="flat"
                        @click="getDetail(item.id)"
                      >
                        View Detail
                      </v-btn>
                    </td>
                  </tr>
                </template>
            </v-data-table>
          </v-skeleton-loader>
        </v-card>

        <v-card v-if="userDetail !== null" :title="userDetail.first_name">
          <div class="d-flex">
            <div>
              <v-img 
                :src="userDetail.avatar" 
                width="350" 
                class="mx-4 my-4 rounded-xl"
              />
            </div>
            <div class="my-4 mx-5">
              <div class="mb-5">
                <p class="label-title">First Name</p>
                <span class="text-slate-400">{{ userDetail.first_name }}</span>
              </div>
              <div>
                <p class="label-title">Last Name</p>
                <span class="text-slate-400">{{ userDetail.last_name }}</span>
              </div>
              <div>
                <p class="label-title">Email</p>
                <span class="text-slate-400">{{ userDetail.email }}</span>
              </div>
            </div>
          </div>
        </v-card>
        <v-btn 
          v-if="userDetail !== null"
          rounded="xl" 
          elevation="2" 
          color="#65A7DB" 
          variant="flat"
          class="mt-5"
          @click="backToList()"
        >
          Back
        </v-btn>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
  const axios = useNuxtApp().$axios;

  const headers = [
    { title: 'Avatar', align: 'start', key: 'avatar' },
    { title: 'First Name', key: 'first_name' },
    { title: 'Last Name', key: 'last_name' },
    { title: 'Email', key: 'email' },
  ];

  let isList = ref(false);

  let userList = ref([]);
  let userDetail = ref(null)

  const getUserList = () => {
    isList.value = true;
    axios.get('http://127.0.0.1:8000/api/users').then((resp) => {
      userList.value = resp.data;
      isList.value = false;
    })
  }

  const getDetail = (id) => {
    isList.value = true;
    axios.get(`http://127.0.0.1:8000/api/users/${id}`).then((resp) => {
      userDetail.value = resp.data;
      isList.value = false
    })
  }

  const backToList = () => {
    getUserList();
    userDetail.value = null;
  }

  onMounted(() => {
    getUserList(); // Call getUserList when the component is mounted
  });
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
  .profile-menu {
    display: flex;
    align-items: center;
  }
  .header-title{
    font-weight: bold;
    font-size: 22px;
  }
  .label-title{
    font-weight: bold;
    font-size: 21;
  }
</style>