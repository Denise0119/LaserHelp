<template>
  <nav class="bg-white">
    <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8">
      <div class="relative flex items-center justify-between h-18">
        <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
          <button
            type="button"
            class="
              inline-flex
              items-center
              justify-center
              p-2
              rounded-md
              text-gray-400
              hover:text-white hover:bg-gray-700
              focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white
            "
            aria-controls="mobile-menu"
            aria-expanded="false"
          >
            <span class="sr-only">Open main menu</span>
            <svg
              class="block h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
            </svg>
            <svg
              class="hidden h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <div
          class="
            flex-1 flex
            items-center
            justify-center
            sm:items-stretch sm:justify-between
          "
        >
          <div class="flex-shrink-0 flex items-center">
            <img
              class="block lg:hidden h-8 w-auto"
              src="/_nuxt/assets/logo.png"
              alt="Workflow"
            />
            <img
              class="hidden lg:block h-12 w-auto"
              src="../assets/logo.png"
              alt="Workflow"
            />
          </div>
          <div class="hidden sm:block sm:ml-6">
            <div class="flex space-x-4 float-right">
              <a
                href="/instanthelp"
                class="
                  text-black
                  px-3
                  py-6
                  text-md
                  font-bold
                  border-b-3 border-yellow-500
                "
                :class="activeClass == 'instanthelp' ? 'active_menu' : ''"
                >GET INSTANT HELP</a
              >

              <a
                href="/helpclients"
                class="text-black px-3 py-6 text-md font-bold"
                :class="activeClass == 'helpclients' ? 'active_menu' : ''"
                >HELP CLIENTS</a
              >

              <a
                href="/message/"
                class="text-black px-3 py-5 text-md font-medium"
                :class="activeClass == 'message' ? 'active_menu' : ''"
              >
                <img
                  src="../assets/CHAT.png"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  alt=""
                />
              </a>

              <a href="#" class="text-black px-3 py-5 text-md font-medium">
                <img
                  src="../assets/NOTIFICATION .png"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  alt=""
                />
              </a>
              <a href="#" class="text-black px-3 py-5 text-md font-medium">
                <img
                  src="../assets/SETTINGS .png"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  alt=""
                />
              </a>
            </div>
          </div>
        </div>
        <div
          class="
            absolute
            inset-y-0
            right-0
            flex
            items-center
            pr-2
            sm:static sm:inset-auto sm:ml-6 sm:pr-0
          "
        >
          <!-- Profile dropdown -->
          <div class="ml-3 relative">
            <div>
              <button
                type="button"
                class="
                  bg-gray-800
                  flex
                  text-sm
                  rounded-full
                  focus:outline-none
                  focus:ring-2
                  focus:ring-offset-2
                  focus:ring-offset-gray-800
                  focus:ring-white
                "
                id="user-menu-button"
                aria-expanded="false"
                aria-haspopup="true"
              >
                <span class="sr-only">Open user menu</span>
                <img
                  class="h-8 w-8 rounded-full"
                  src="../assets/avatar.jpg"
                  alt=""
                />
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Mobile menu, show/hide based on menu state. -->
    <div class="sm:hidden" id="mobile-menu">
      <div class="px-2 pt-2 pb-3 space-y-1">
        <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
        <a
          href="/instanthelp"
          class="
            bg-gray-900
            text-white
            block
            px-3
            py-2
            rounded-md
            text-base
            font-medium
          "
          aria-current="page"
          >GET INSTANT HELP</a
        >

        <a
          href="/helpclients"
          class="
            text-gray-300
            hover:bg-gray-700 hover:text-white
            block
            px-3
            py-2
            rounded-md
            text-base
            font-medium
          "
          >HELP CLIENTS</a
        >

        <a
          :href="'/message/' + this.userId"
          class="
            text-gray-300
            hover:bg-gray-700 hover:text-white
            block
            px-3
            py-2
            rounded-md
            text-base
            font-medium
          "
        >
          <img
            src="../assets/CHAT.png"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            alt=""
          />
        </a>

        <a
          href="#"
          class="
            text-gray-300
            hover:bg-gray-700 hover:text-white
            block
            px-3
            py-2
            rounded-md
            text-base
            font-medium
          "
        >
          <img
            src="../assets/NOTIFICATION .png"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            alt=""
          />
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      userId: null,
    };
  },
  async mounted() {
    await this.getUserId();
  },
  async created() {
    await this.getUserId();
  },
  props: {
    activeClass: String,
  },

  methods: {
    getUserId() {
      this.userId = this.$store.state.localStorage.user.id;
    },
  },
};
</script>


<style>
a.active_menu {
  border-bottom: -2px solid rgba(245, 158, 11, var(--tw-border-opacity));
}
</style>
