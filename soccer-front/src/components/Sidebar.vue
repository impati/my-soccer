<template>
  <div id="sidebar" class="d-flex flex-column flex-shrink-0 p-3 bg-dark text-white">
    <router-link to="/" class="d-flex align-items-center mb-3 mb-md-0 me-md-auto text-white text-decoration-none">
      <i class="bi bi-bootstrap-fill me-2"></i>
      <span class="fs-4">Sidebar</span>
    </router-link>
    <hr>

    <ul class="nav nav-pills flex-column mb-auto">
      <li class="nav-item">
        <a href="#" class="nav-link text-white" @click="togglePlayerManagement">
          <i class="bi bi-house-door-fill me-2"></i>
          선수 관리
        </a>
        <ul v-if="isPlayerManagementOpen" class="nav flex-column ms-3">
          <li class="nav-item">
            <router-link to="/player-search" class="nav-link text-white">
              <i class="bi bi-search me-2"></i>
              선수 검색
            </router-link>
          </li>

          <li class="nav-item">
            <router-link to="/player-register" class="nav-link text-white">
              <i class="bi bi-plus-square-fill me-2"></i>
              선수 등록
            </router-link>
          </li>
        </ul>
      </li>

      <li class="nav-item">
        <a href="#" class="nav-link text-white" @click="toggleLeague">
          <i class="bi bi-house-door-fill me-2"></i>
          리그
        </a>
        <ul v-if="isLeague" class="nav flex-column ms-3">
          <li v-for="league in leagues" :key="league" class="nav-item">
            <router-link :to="`/${league.name}`" class="nav-link text-white">
              <i class="bi bi-plus-square me-2"></i>
              {{ league.leagueName }}
            </router-link>
          </li>
        </ul>
      </li>
    </ul>

    <hr>
    <div class="dropdown">
      <a href="#" class="d-flex align-items-center text-white text-decoration-none dropdown-toggle" id="dropdownUser1"
         data-bs-toggle="dropdown" aria-expanded="false">
        <img src="https://github.com/mdo.png" alt="" width="32" height="32" class="rounded-circle me-2">
        <strong>mdo</strong>
      </a>
      <ul class="dropdown-menu dropdown-menu-dark text-small shadow" aria-labelledby="dropdownUser1">
        <li><a class="dropdown-item" href="#">Settings</a></li>
        <li><a class="dropdown-item" href="#">Profile</a></li>
        <li>
          <hr class="dropdown-divider">
        </li>
        <li><a class="dropdown-item" href="#">Sign out</a></li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'AppSidebar',
  data() {
    return {
      isPlayerManagementOpen: false,
      isLeague: false,
      leagues: []
    }
  },
  methods: {
    togglePlayerManagement() {
      this.isPlayerManagementOpen = !this.isPlayerManagementOpen;
    },

    toggleLeague() {
      this.isLeague = !this.isLeague;
    }
  },
  mounted() {
    axios.get('http://localhost:8080/leagues')
    .then(response => {
      this.leagues = response.data;
    })
    .catch(error => {
      console.error('There was an error fetching the leagues:', error);
    });
  }
}
</script>

<style scoped>
#sidebar {
  height: 100vh; /* 사이드바가 화면 전체 높이를 차지하도록 설정 */
  width: 280px;
}

.nav-pills .nav-link {
  cursor: pointer;
}

.nav-link.active {
  background-color: #0d6efd; /* Change this to your desired active color */
}
</style>
