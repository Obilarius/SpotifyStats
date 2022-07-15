<template>
  <div class="container">
    <h1>Hey 🤙</h1>
    <div id="idtokenSection">
      <div class="mb-3">
        <label for="clientId" class="form-label">Client ID</label>
        <input type="text" class="form-control" id="clientId" placeholder="" v-model="clientId" />
      </div>
      <div class="mb-3">
        <label for="clientSecret" class="form-label">Client Secret</label>
        <input type="text" class="form-control" id="clientSecret" placeholder="" v-model="clientSecret" />
      </div>
      <input class="btn btn-primary btn-lg" type="button" @click="requestAuthorization" value="Request Authorization" /><br />
    </div>
  </div>
</template>

<script setup lang="ts">
// https://www.youtube.com/watch?v=1vR3m0HupGI
const clientId = ref("f23c52783769431bb71cb3ebf44346e5")
const clientSecret = ref("4b21061d5a954f13b7de70b7dd344b2e")

const requestAuthorization = () => {
  localStorage.setItem("client_id", clientId.value)
  localStorage.setItem("client_secret", clientSecret.value)

  let url = "https://accounts.spotify.com/authorize"
  url += `?client_id=${clientId.value}`
  url += `&response_type=code`
  url += `&redirect_uri=http://localhost:3001/`
  url += `&show_dialog=true`
  url += `&scope=user-read-private user-read-email user-modify-playback-state user-read-playback-position user-library-read streaming user-read-playback-state user-read-recently-played playlist-read-private`

  window.location.href = url // Show Spotify's authorization screen
}

onMounted(() => {
  console.log("Search: ", window.location.search)
})
</script>
