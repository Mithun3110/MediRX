<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute();
let userData = ref({});
const loadUserData = async () => {
  try {
    const hallResponse = await axios
      .get("https://nfc-smart-card.herokuapp.com" + "/user/" + route.params.id)
      .then((res) => {
        console.log(res.data);
        userData.value = res.data.user;
      });
  } catch (err) {
    console.log(err);
  }
};

onMounted(() => {
  loadUserData();
});
</script>

<template>
  <div id="settings-screen" class="flex flex-col justify-center items-center">
    <img
      class="w-48 h-48 rounded-full"
      src="https://www.pngall.com/wp-content/uploads/5/User-Profile-PNG.png"
      alt="Rounded avatar"
    />
    <h2 class="text-2xl font-medium">{{ userData.name }}</h2>
    <h3 class="text-xl font-medium my-4">Personal Information</h3>
    <p><span class="font-medium">Date of birth :</span> {{ userData.dob }}</p>
    <p><span class="font-medium">City :</span> {{ userData.city }}</p>
    <p><span class="font-medium">State :</span> {{ userData.state }}</p>
    <h3 class="text-xl font-medium my-4">Recent Appointments</h3>
  </div>
</template>
