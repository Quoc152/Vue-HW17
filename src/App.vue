<template>
  <div class="container h-screen flex flex-col justify-center items-center p-4">
    <h1 class="text-2xl font-bold mb-4">Google Login Demo</h1>
    <GoogleLogin v-if="!accessToken" />
    <div v-else>
      <h2 class="text-xl mb-2">User Information:</h2>
      <pre>{{ userInfo }}</pre>
      <Button @click="signOut" class="mt-4">Sign Out</Button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import GoogleLogin from "./components/GoogleLogin.vue";
import { Button } from "@/components/ui/button";

const accessToken = ref("");
const userInfo = ref(null);

const fetchUserInfo = async (token) => {
  const response = await fetch(
    "https://www.googleapis.com/oauth2/v3/userinfo",
    {
      headers: { Authorization: `Bearer ${token}` },
    }
  );
  return await response.json();
};

const signOut = () => {
  accessToken.value = "";
  userInfo.value = null;
  window.location.hash = "";
};

onMounted(async () => {
  const hash = window.location.hash.substring(1);
  const params = new URLSearchParams(hash);
  const token = params.get("access_token");

  if (token) {
    accessToken.value = token;
    console.log("Access Token:", token);  
    userInfo.value = await fetchUserInfo(token);
    console.log("User Info:", userInfo.value);
  }
});
</script>
