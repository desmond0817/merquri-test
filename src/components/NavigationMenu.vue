<template>
  <ul class="menu-list">
    <div v-for="item in menuItems" :key="item.id">
      <router-link
        :to="item.path"
        custom
        exact
        v-slot="{ href, navigate, isExactActive }"
      >
        <li class="d-menu-item">
          <a
            class="d-menu-item-container"
            :href="href"
            @click="
              navigate();
              $emit('closeMenu');
            "
            :class="isExactActive ? 'is-activeTab' : 'not-activeTab'"
          >
            <b-icon :icon="item.icon"></b-icon>
            <div class="d-menu-item-label-position ml-3">{{ item.title }}</div>
          </a>
        </li>
      </router-link>
    </div>
  </ul>
</template>

<script>
export default {
  name: "MerchantLogin",
  data() {
    return {
      menuItems: [
        {
          id: 1,
          path: "/home",
          title: "Home",
          icon: "home-outline",
        },
        {
          id: 2,
          path: "/about",
          title: "About",
          icon: "cube-outline",
        },
      ],
    };
  },
};
</script>

<style>
.is-activeTab {
  background-color: #eaeffb !important;
  color: #2945c2 !important;
  border-radius: 0.5rem !important;
  font-weight: 500;
}
.not-activeTab {
  background-color: #fff;
  color: #676767 !important;
  border-radius: 0.5rem !important;
}

.d-menu-item {
  margin: 0px;
  padding: 0.4rem !important;
}
.d-menu-item-container {
  display: inline-flex !important;
  width: 100%;
  height: 40px;
}
.d-menu-item-label-position {
  font-size: 14px;
  transform: translate(0, +15%);
  min-width: 120px;
}
</style>
