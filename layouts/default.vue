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
                <v-list-item style="cursor: pointer;" @click="movePage('/about')">
                    <v-list-item-icon class="mr-2">
                    <v-icon>mdi-information</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>About</v-list-item-content>
                </v-list-item>
                <v-list-item style="cursor: pointer;" @click="movePage('/users')">
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
            <span class="header-title">pageTitle</span>
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
            <slot />
        </v-main>
    </v-app>
</template>

<script setup>
    import { useRouter } from 'vue-router'

    const router = useRouter()

    const movePage = (page) => {
        router.push(page)
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
    .active{
        background-color: rgba(0, 0, 0, 0.3);
    }
    h2{
        font-size: 28px;
        font-weight: bold;
        margin-bottom: 15px;
    }
</style>