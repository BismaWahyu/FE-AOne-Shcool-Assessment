<template>
    <v-container>
        <v-card title="All Users">
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
    </v-container>
</template>

<script setup>
    const layout = 'default';
    const axios = useNuxtApp().$axios;
    import { useRouter } from 'vue-router'

    const router = useRouter()

    const headers = [
        { title: 'Avatar', align: 'start', key: 'avatar' },
        { title: 'First Name', key: 'first_name' },
        { title: 'Last Name', key: 'last_name' },
        { title: 'Email', key: 'email' },
    ];

    let isList = ref(false);

    let userList = ref([]);

    const getUserList = () => {
        isList.value = true;
        axios.get('http://127.0.0.1:8000/api/users').then((resp) => {
        userList.value = resp.data;
        isList.value = false;
        })
    }

    const getDetail = (id) =>{
        router.push(`/users/${id}`)
    }

    onMounted(() => {
        getUserList();
    });
</script>