<template>
  <nav class="topbar navbar fixed-top">
    <div class="container-fluid">
      <div>
        <img class="app-logo" src="../assets/img/viaphoton-logo.png" alt="" />
        <span class="app-name">Customer Portal</span>
      </div>
      <div class="d-flex">
         <div class="dropdown">
        <img class="btn user-img dropdown-toggle" :src="user.picture" alt="dropdown image" data-toggle="dropdown">
        <ul class="dropdown-menu">
            <li class="dropdown-item">Profile</li><hr>
            <li class="dropdown-item" @click="logout">Log Out</li>
        </ul>
    </div>
        <!-- <div class="dropdown">
             <img class="user-img dropdown-toggle" :src="user.picture" alt="" id="dropdownMenuLink" data-bs-toggle="dropdown" aria-expanded="false">
            <ul class="dropdown-menu" aria-labelledby="dropdownMenuLink">
                <li><a class="dropdown-item" href="#">Action</a></li>
                <li><a class="dropdown-item" href="#">Another action</a></li>
                <li><a class="dropdown-item" href="#">Something else here</a></li>
            </ul>
        </div> -->
      </div>
    </div>
  </nav>
</template>

<script>
import { useAuth0 } from "@auth0/auth0-vue"
export default {
setup() {
  const auth0 = useAuth0();
  const logout = () => {
    auth0.logout({ returnTo: window.location.origin });
  };
  return {
    user: auth0.user,
    logout
  }
}
}
</script>

<style lang="scss" scoped>
</style>