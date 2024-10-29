<template>
  <Button @click="signIn">
    <Icon icon="mdi:google" class="mr-2 h-4 w-4" />
    Sign in with Google
  </Button>
</template>

<script setup>
import { Button } from "@/components/ui/button";
import { Icon } from "@iconify/vue";

const clientId = "643673703585-svnu369vkrejred3seeonoj4i8cma8sa.apps.googleusercontent.com";
const redirectUri = "http://localhost:5173";

const signIn = () => {
  const authUrl = `https://accounts.google.com/o/oauth2/v2/auth?client_id=${clientId}&redirect_uri=${redirectUri}&response_type=token&scope=email%20profile`;
  window.location.href = authUrl;
};
</script>
