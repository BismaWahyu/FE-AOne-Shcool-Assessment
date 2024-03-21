<template>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
</template>

<script setup>
  const router = useRouter()

  const nav = [
    { label: 'Users', to: '/users' },
    { label: 'About', to: '/about' },
  ]
</script>