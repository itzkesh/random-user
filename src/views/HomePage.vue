<script setup>
import { ref, onMounted } from 'vue'

const user = ref(null)

const getUser = async () => {
  const res = await fetch('https://randomuser.me/api/')
  const data = await res.json()
  user.value = data.results[0]
}

onMounted(() => {
  getUser()
})
</script>

<template>
  <div class="app">

    <div class="profile-container">

      <!-- Left Side -->
      <div class="left-side">

        <img
          v-if="user"
          :src="user.picture.large"
          class="profile-img"
        />

        <h1 v-if="user">
          {{ user.name.first }} {{ user.name.last }}
        </h1>

        <p class="email">
          {{ user?.email }}
        </p>

        <button @click="getUser" class="generate-btn">
          Generate User
        </button>

      </div>

      <!-- Right Side -->
      <div v-if="user" class="right-side">

        <div class="info-card">
          <span>Phone</span>
          <h3>{{ user.phone }}</h3>
        </div>

        <div class="info-card">
          <span>Country</span>
          <h3>{{ user.location.country }}</h3>
        </div>

        <div class="info-card">
          <span>City</span>
          <h3>{{ user.location.city }}</h3>
        </div>

        <div class="info-card">
          <span>Username</span>
          <h3>{{ user.login.username }}</h3>
        </div>

      </div>

    </div>

  </div>
</template>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

body{
  font-family: 'Poppins', sans-serif;
}

/* Main Background */
.app{
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  background:
    radial-gradient(circle at top left, #1e293b, #020617);
  padding:40px;
}

/* Main Card */
.profile-container{
  width:100%;
  max-width:1100px;
  background:#0f172a;
  border-radius:30px;
  overflow:hidden;
  display:grid;
  grid-template-columns: 1fr 1fr;
  box-shadow:0 20px 60px rgba(0,0,0,0.5);
}

/* Left */
.left-side{
  background:linear-gradient(180deg,#2563eb,#7c3aed);
  padding:60px 40px;
  text-align:center;
  color:white;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
}

.profile-img{
  width:180px;
  height:180px;
  border-radius:50%;
  object-fit:cover;
  border:6px solid rgba(255,255,255,0.3);
  margin-bottom:25px;
  box-shadow:0 10px 30px rgba(0,0,0,0.3);
}

.left-side h1{
  font-size:36px;
  font-weight:700;
  margin-bottom:10px;
}

.email{
  opacity:0.9;
  margin-bottom:30px;
  font-size:15px;
}

/* Button */
.generate-btn{
  background:white;
  color:#2563eb;
  border:none;
  padding:15px 35px;
  border-radius:50px;
  font-size:15px;
  font-weight:600;
  cursor:pointer;
  transition:0.3s ease;
}

.generate-btn:hover{
  transform:scale(1.05);
  background:#e0e7ff;
}

/* Right */
.right-side{
  padding:50px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:25px;
  background:#0f172a;
}

/* Cards */
.info-card{
  background:#111c33;
  border:1px solid rgba(255,255,255,0.05);
  border-radius:20px;
  padding:30px 25px;
  transition:0.3s ease;
}

.info-card:hover{
  transform:translateY(-6px);
  background:#172554;
  border-color:#3b82f6;
}

.info-card span{
  color:#94a3b8;
  font-size:14px;
  display:block;
  margin-bottom:12px;
}

.info-card h3{
  color:white;
  font-size:20px;
  font-weight:600;
  word-break:break-word;
}

/* Mobile */
@media(max-width:900px){

  .profile-container{
    grid-template-columns:1fr;
  }

  .right-side{
    grid-template-columns:1fr;
  }

}
</style> 