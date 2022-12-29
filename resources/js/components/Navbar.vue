<template>
  <nav v-if="hasNavbar" class="bg-white dark:bg-notion-dark border-b">
    <div class="max-w-7xl mx-auto px-8">
      <div class="flex items-center justify-between h-16">
        <div v-if="showAuth" class="flex items-center">
          <router-link :to="{ name: user ? 'home' : 'welcome' }" class="flex-shrink-0 font-semibold hover:no-underline flex items-center">
            42forms
          </router-link>
          <workspace-dropdown class="ml-6"/>
        </div>

        <div v-if="showAuth" class="hidden md:block pl-5 border-gray-300 border-r h-5"></div>
        <div v-if="showAuth" class="block">
          <div class="flex items-center">
            <div class="ml-3 mr-4 relative">
              <div class="relative inline-block text-left">
                <dropdown v-if="user" dusk="nav-dropdown">
                  <template #trigger="{toggle}">
                    <button id="dropdown-menu-button" type="button"
                            class="flex items-center justify-center w-full rounded-md  px-4 py-2 text-sm text-gray-700 dark:text-gray-50 hover:bg-gray-50 dark:hover:bg-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-gray-500"
                            dusk="nav-dropdown-button" @click.prevent="toggle()"
                    >
                      <img :src="user.photo_url" class="rounded-full w-6 h-6">
                      <p class="ml-2 hidden sm:inline">
                        {{ user.name }}
                      </p>
                    </button>
                  </template>

                  <router-link v-if="userOnboarded" :to="{ name: 'home' }"
                               class="block block px-4 py-2 text-md text-gray-700 hover:bg-gray-100 hover:text-gray-900 dark:text-gray-100 dark:hover:text-white dark:hover:bg-gray-600 flex items-center"
                  >
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 mr-2" fill="none" viewBox="0 0 24 24"
                         stroke="currentColor"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"
                      />
                    </svg>
                    My Forms
                  </router-link>

                  <router-link :to="{ name: 'settings.profile' }"
                               class="block block px-4 py-2 text-md text-gray-700 hover:bg-gray-100 hover:text-gray-900 dark:text-gray-100 dark:hover:text-white dark:hover:bg-gray-600 flex items-center"
                  >
                    <svg class="w-4 h-4 mr-2" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                         stroke="currentColor"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"
                      />
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                      />
                    </svg>
                    {{ $t('settings') }}
                  </router-link>

                  <a href="#"
                     class="block block px-4 py-2 text-md text-gray-700 dark:text-white hover:bg-gray-100 hover:text-gray-900 dark:text-gray-100 dark:hover:text-white dark:hover:bg-gray-600 flex items-center"
                     @click.prevent="logout"
                  >
                    <svg class="w-4 h-4 mr-2" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                         stroke="currentColor"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"
                      />
                    </svg>
                    {{ $t('logout') }}
                  </a>
                </dropdown>
                <div class="flex gap-2" v-else>
                  <router-link v-if="$route.name !== 'login'" :to="{ name: 'login' }"
                               class="text-gray-600 dark:text-white hover:text-gray-800 dark:hover:text-white px-0 sm:px-3 py-2 rounded-md text-sm"
                               active-class="text-gray-800 dark:text-white"
                  >
                    {{ $t('login') }}
                  </router-link>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import {mapGetters} from 'vuex'
import Dropdown from './common/Dropdown'
import axios from 'axios'
import WorkspaceDropdown from './WorkspaceDropdown'

export default {
  components: {
    WorkspaceDropdown,
    Dropdown
  },

  data: () => ({
    appName: window.config.appName,
  }),

  computed: {
    githubUrl: () => window.config.links.github_url,
    form() {
      if (this.$route.name && this.$route.name.startsWith('forms.show_public')) {
        return this.$store.getters['open/forms/getBySlug'](this.$route.params.slug)
      }
      return null
    },
    showAuth() {
      return this.$route.name && !this.$route.name.startsWith('forms.show_public')
    },
    hasNavbar() {
      if (this.isIframe) return false

      if (this.$route.name && this.$route.name.startsWith('forms.show_public')) {
        if (this.form) {
          // If there is a cover, or if branding is hidden remove nav
          if (this.form.cover_picture || this.form.no_branding) {
            return false
          }
        } else {
          return false
        }
      }
      return true
    },
    isIframe() {
      return window.location !== window.parent.location || window.frameElement
    },
    ...mapGetters({
      user: 'auth/user'
    }),
    userOnboarded() {
      return this.user && this.user.workspaces_count > 0
    },
    hasCrisp() {
      return window.config.crisp_website_id
    }
  },

  methods: {
    async logout() {
      // Log out the user.
      await this.$store.dispatch('auth/logout')

      // Reset store
      this.$store.dispatch('open/workspaces/resetState')
      this.$store.dispatch('open/forms/resetState')

      // Redirect to login.
      this.$router.push({name: 'login'})
    },
  }
}
</script>
