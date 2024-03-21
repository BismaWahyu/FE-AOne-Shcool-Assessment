<template>
    <v-container v-if="userDetail">
        <v-card :title="userDetail.first_name">
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
            rounded="xl" 
            elevation="2" 
            color="#65A7DB" 
            variant="flat"
            class="mt-5"
            @click="backToList"
        >
            Back
        </v-btn>
    </v-container>
</template>

<script setup>
    import { useRoute, useRouter } from 'vue-router'

    const route = useRoute()
    const router = useRouter()
    const axios = useNuxtApp().$axios;

    const userId = route.params.id
    let isList = ref(false);
    let userDetail = ref(null)

    const getDetail = (id) => {
        isList.value = true;
        axios.get(`http://127.0.0.1:8000/api/users/${id}`).then((resp) => {
            userDetail.value = resp.data;
            isList.value = false
        })
    }

    const backToList = () => {
        router.push('/users')
    }

    onMounted(() => {
        getDetail(userId);
    })
</script>