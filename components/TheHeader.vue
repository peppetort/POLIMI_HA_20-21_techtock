<template>
  <div class="container">
    <div class="header">
      <div class="logo">
        <NuxtLink to="/">
          <img loading="lazy" src="/logo-long.svg" alt="company logo icon" />
        </NuxtLink>
      </div>
      <div class="nav-mobile">
        <img
          loading="lazy"
          id="icon"
          src="/menu.svg"
          alt="burger menu icon"
          @click="toggleMenu"
        />
      </div>
      <div class="nav">
        <div class="dropdown">
          <NuxtLink to="/areas">Areas</NuxtLink>
          <div class="dropdown-content">
            <NuxtLink
              v-for="area in areas"
              :key="area.id"
              :to="`/areas/${area.id}`"
              >{{ area.title }}</NuxtLink
            >
          </div>
        </div>
        <div class="dropdown">
          <NuxtLink to="/products">Products</NuxtLink>
          <div class="dropdown-content">
            <NuxtLink
              v-for="area in areas"
              :key="area.id"
              :to="`/products/area/${area.id}`"
              >{{ area.title }} products</NuxtLink
            >
          </div>
        </div>
        <div class="dropdown">
          <NuxtLink to="/roles">Team</NuxtLink>
          <div class="dropdown-content">
            <NuxtLink
              v-for="role in roles"
              :key="role.id"
              :to="`/roles/${role.id}`"
              >{{ role.title }}</NuxtLink
            >
          </div>
        </div>
        <NuxtLink to="/company">Company</NuxtLink>
        <NuxtLink to="/contacts">Contacts</NuxtLink>
      </div>
    </div>
    <div class="mobile-menu" id="mobile-menu" @click="toggleMenu">
      <NuxtLink to="/areas">Areas</NuxtLink>
      <NuxtLink to="/products">Products</NuxtLink>
      <NuxtLink to="/roles">Team</NuxtLink>
      <NuxtLink to="/company">Company</NuxtLink>
      <NuxtLink to="/contacts">Contacts</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      areas: this.$store.state.areas,
      roles: this.$store.state.roles
    }
  },
  mounted() {
    window.addEventListener('resize', (e) => {
      if (window.innerWidth > 900) {
        document.getElementById('mobile-menu').style.display = 'none'
        document.getElementById('icon').setAttribute('src', '/menu.svg')
        document.getElementById('icon').setAttribute('alt', 'X icon')
      }
    })
  },
  methods: {
    toggleMenu() {
      var icon = document.getElementById('icon')
      var menu = document.getElementsByClassName('mobile-menu')[0]

      if (menu.style.display === 'flex') {
        menu.style.display = 'none'
        icon.setAttribute('src', '/menu.svg')
      } else {
        menu.style.display = 'flex'
        icon.setAttribute('src', '/close.svg')
      }
    }
  }
}
</script>

<style scoped>
div.container {
  height: auto;
  display: flex;
  flex-direction: column;
  width: 100%;
  top: 0;
  position: fixed;
  z-index: 1;
}

div.header {
  height: 40px;
  background: black;
  display: flex;
  flex-direction: row;
  padding: 10px;
  justify-content: space-between;
}

div.logo {
  height: 40px;
  width: auto;
}

div.logo img {
  width: auto;
  height: 100%;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

div.nav {
  height: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-right: 40px;
}

div.nav a {
  color: #f2f2f2;
  text-align: center;
  padding: 10px;
  font-weight: bold;
  margin-right: 10px;
}

div.nav a:hover {
  color: #bdbdbd;
}

div.dropdown-content {
  display: none;
  flex-direction: column;
  position: absolute;
  top: 50px;
  background: black;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
}

div.dropdown-content a {
  text-align: left;
  border-radius: 0px;
}

.dropdown:hover .dropdown-content {
  display: flex;
}

.dropdown:hover > a {
  background: black;
  color: white;
}

div.nav-mobile {
  display: none;
  align-items: center;
}

div.nav-mobile img {
  width: auto;
  height: 35px;
  color: #f2f2f2;
  display: block;
}

div.mobile-menu {
  display: none;
  background: black;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 10px;
}

div.mobile-menu a {
  background: black;
  color: white;
  font-weight: bold;
  width: 150px;
  padding: 10px;
  border-radius: 5px;
  margin-top: 10px;
}

@media (max-width: 900px) {
  div.nav {
    display: none;
  }

  div.nav-mobile {
    display: flex;
  }
}
</style>
