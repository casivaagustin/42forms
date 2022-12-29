<template>
  <div>
    <div class="flex mt-6 mb-10">
      <div class="w-full md:max-w-6xl mx-auto px-4 flex justify-center	 flex-wrap">
          <div class="border rounded-md p-6 shadow-md sticky top-4">
            <h2 class="font-semibold text-2xl">
              Login
            </h2>
            <small>Welcome back! Please enter your details.</small>
            <login-form />
          </div>
      </div>
    </div>
    <open-form-footer />
  </div>
</template>

<script>
import OpenFormFooter from '../../components/pages/OpenFormFooter'
import Testimonials from '../../components/pages/welcome/Testimonials'
import LoginForm from './components/LoginForm'
import SeoMeta from '../../mixins/seo-meta'

export default {
  components: {
    OpenFormFooter,
    Testimonials,
    LoginForm
  },

  middleware: 'guest',

  mixins: [SeoMeta],

  data: () => ({
    metaTitle: 'Login',
  }),

  methods: {

  }
}
</script>
