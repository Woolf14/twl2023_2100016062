<template>
  <div class="h-screen   bg-gray-800" id="side-bar"
    :class="dataOpenSideBar == true ? 'side-bar-visible' : 'side-bar-close'">
    <div class="bg-gray-700 h-[50px] flex justify-center items-center ">
      <div class="text-xl font-bold text-center flex items-center justify-center text-white h-full"
        v-show="dataOpenSideBar">AcademicHub</div>
      <img src="../assets/Logo.jpeg" v-show="!dataOpenSideBar"
        class="p-1 w-8 h-8 rounded-full ring-2 ring-gray-100 dark:ring-gray-500 " alt="Avatar" />
    </div>
    <div class="flex flex-col justify-between h-[calc(100vh-3rem)] bg-gray-900 overflow-auto">
      <div class="menu-man text-left px-2 whitespace-nowrap ">
        <div class="profile flex justify-center items-center text-center p-2 ">
          
        </div>
        <div class="   py-3 rounded-sm cursor-pointer text-gray-300 hover:text-white">
          <router-link to="/" class="px-2 flex space-x-2"><span class="pi pi-prime" v-tooltip.right="'Dashboard'"></span>
            <span v-show="dataOpenSideBar">Dashboard</span></router-link>
        </div>
        <div class="   py-3 rounded-md cursor-pointer  text-gray-300 hover:text-white">
          <router-link to="/Mahasiswa" class="px-2 flex space-x-2"><span class="pi pi-users " v-tooltip.right="'Mahasiswa'"></span>
            <span v-show="dataOpenSideBar">Mahasiswa</span></router-link>
        </div>
        <div class="   py-3 rounded-md cursor-pointer  text-gray-300 hover:text-white">
          <router-link to="/Dosen" class="px-2 flex space-x-2"><span class="pi pi-user "
              v-tooltip.right="'Dosen'"></span> <span v-show="dataOpenSideBar">Dosen</span></router-link>
        </div>
        <div class="  py-3 rounded-md cursor-pointer text-gray-300 hover:text-white">
          <router-link to="/contact" class="px-2 flex space-x-2"><span class="pi pi-whatsapp  "
              v-tooltip.right="'Contact'"></span> <span v-show="dataOpenSideBar">Contact</span></router-link>
        </div>
        <div class="  py-3 rounded-md cursor-pointer text-gray-300 hover:text-white">
          <router-link to="/customer" class="px-2 flex space-x-2"><span class="pi pi-shield "
              v-tooltip.right="'Customer'"></span> <span v-show="dataOpenSideBar">Customer</span></router-link>
        </div>
        <div class="  py-3 rounded-md cursor-pointer text-gray-300 hover:text-white">
          <router-link to="/setting" class="px-2 flex space-x-2"><span class="pi pi-cog"
              v-tooltip.right="'Setting'"></span> <span v-show="dataOpenSideBar">Setting</span></router-link>
        </div>
      </div>
      <div class="menu-man text-left px-2 justify-self-end whitespace-nowrap">
        <div class="py-3 rounded-md cursor-pointer text-gray-300 hover:text-white">
          <a href="https://github.com/Woolf14" target="_blank" class="px-2 flex space-x-2"><span class="pi pi-github"
              v-tooltip.right="'About Me'"></span> <span v-show="dataOpenSideBar">About Me</span></a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dataOpenSideBar: Boolean
  },

}
</script>

<style>
.p-tooltip-text {
  font-size: 10px !important;
}

#side-bar {
  overflow: hidden;
  transition: 300ms;
}

.side-bar-visible {
  width: 250px !important;
}

.side-bar-close {
  width: 50px !important;
}</style>