<template>
  <div v-if="isLoading">Loading ...</div>
  <div v-else>
        <Topbar />
    <div class="container-fluid">
      <div class="row flex-nowrap dashboard">
        <Sidebar />
        <div class="col py-1 main-menu">
          <div class="main-menu-child">
            <Profile />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// Composition API
import { useAuth0 } from "@auth0/auth0-vue";
import Sidebar from "../components/Sidebar.vue";
import { onMounted, ref } from "vue";
import Topbar from '../components/Topbar.vue'
import Profile from "./Profile.vue"
export default {
  components: {
    Sidebar,
    Topbar,
    Profile
  },
  setup() {
    const auth0 = useAuth0();
    const accessToken = ref("");
    onMounted(async () => {
      accessToken.value = await auth0.getAccessTokenSilently();
    });
    const logout = () => {
      auth0.logout({ returnTo: window.location.origin });
    };
    return {
      logout,
      user: auth0.user,
      auth0,
      isAuthenticated: auth0.isAuthenticated,
      isLoading: auth0.isLoading,
      accessToken,
    };
  },
};
</script>