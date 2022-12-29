<template>
  <div>
    <div class="flex mt-6 mb-10">
      <div class="w-full md:max-w-6xl mx-auto px-4 flex justify-center flex-wrap">
        <div class="w-full lg:w-1/2 md:p-6">
          <div class="border rounded-md p-6 shadow-md sticky top-4">
            <h2 class="font-semibold text-2xl">
              Create an account
            </h2>
            <small>Sign up in less than 2 minutes.</small>

            <register-form />
          </div>
        </div>

      </div>
    </div>
    <open-form-footer />
  </div>
</template>

<script>
import OpenFormFooter from '../../components/pages/OpenFormFooter'
import Testimonials from '../../components/pages/welcome/Testimonials'
import RegisterForm from './components/RegisterForm'
import SeoMeta from '../../mixins/seo-meta'

export default {
  components: {
    Testimonials,
    OpenFormFooter,
    RegisterForm
  },

  middleware: 'guest',

  mixins: [SeoMeta],

  data: () => ({
    metaTitle: 'Register',
  }),

  computed: {
  },

  methods: {
  }
}
</script>
