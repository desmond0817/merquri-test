<template>
  <section class="" style="height: 100%">
    <div class="topbar is-flex">
      <b-button
        type="is-ghost"
        class="has-text-white topbar-left-btn d-transition"
        icon-right="menu"
        size="md"
        v-if="!expand"
        @click="expand = true"
      ></b-button>

      <b-button
        type="is-ghost"
        class="has-text-white topbar-left-btn d-transition"
        icon-right="close"
        size="md"
        v-if="expand"
        @click="expand = false"
      ></b-button>
      <b-image
        :src="require('@/assets/merquri-logo.png')"
        alt="The Merquri Logo"
        style="width: 115px"
      ></b-image>

      <b-field class="ml-auto py-1 pr-2">
        <b-autocomplete
          placeholder="Search"
          v-model="name"
          :data="filteredDataArray"
          icon="magnify"
          custom-class="search-input"
          clearable
          @select="(option) => (selected = option)"
        >
          <template #empty>No results found</template>
        </b-autocomplete>
      </b-field>
    </div>

    <transition name="slide-fade">
      <aside class="menu d-sidebar rd-poppins" v-if="expand">
        <NavigationMenu @close-menu="expand = false" />
      </aside>
    </transition>

    <div>
      <router-view />
    </div>
    <div class="modal-background" v-if="expand"></div>
  </section>
</template>
<script>
import NavigationMenu from "@/components/NavigationMenu.vue";

export default {
  name: "DashboardLayout",
  components: { NavigationMenu },
  data() {
    return {
      expand: false,
      nameList: [
        { name: "John", age: 24, occupation: "Engineer" },
        { name: "Doe", age: 28, occupation: "Doctor" },
        { name: "Michael", age: 32, occupation: "Teacher" },
        { name: "Daryl", age: 29 },
      ],
      name: "",
    };
  },
  computed: {
    filteredDataArray() {
      return this.nameList
        .map((item) => {
          return item.name;
        })
        .filter((option) => {
          return (
            option.toString().toLowerCase().indexOf(this.name.toLowerCase()) >=
            0
          );
        });
    },
  },
};
</script>

<style>
.topbar {
  height: 70px;
  position: fixed;
  background: #2945c2;
  width: 100%;
  padding: 0.6rem;
  z-index: 1;
}
.topbar-left-btn {
  font-family: "Open Sans", Arial;
  font-size: 15px;
  padding-bottom: 1.5em;
  padding-left: 1.3em;
  padding-right: 1.3em;
  padding-top: 1.5em;
  margin-right: 0.5rem;
}

.search-input {
  background-color: #5169ce !important;
  border: 1px solid transparent !important;
  color: white !important;
  width: 259px;
}
.search-input:focus {
  border: 1px solid white !important;
  color: white !important;
}
.search-input:focus ~ .icon {
  color: white !important;
}
::placeholder {
  color: white !important;
  opacity: 1; /* Firefox */
}

.d-transition {
  transition-duration: 0.5s;
  animation: fadeIn 0.5s;
}

.d-sidebar {
  position: fixed;
  margin-top: 70px;
  background: #fff;
  padding: 0.2rem;
  height: calc(100% - 70px);
  z-index: 1 !important;
  border-right: 1px solid #f4f4fa;
  border-left: 1px solid #f4f4fa;
}

.slide-fade-enter-active {
  transition: all 0.36s ease;
}
.slide-fade-leave-active {
  transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(-190px) !important;
  opacity: 0;
}

input {
  border-radius: 0.5rem !important;
}
</style>
