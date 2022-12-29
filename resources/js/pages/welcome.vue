<template>
  <div>
    <div class="flex flex-col">
      <div class="w-full ">

      </div>
      <open-form-footer class=""/>
    </div>
  </div>
</template>

<script>
import {mapGetters} from 'vuex'
import Features from '~/components/pages/welcome/Features'
import MoreFeatures from '~/components/pages/welcome/MoreFeatures'
import OpenFormFooter from '../components/pages/OpenFormFooter'
import Testimonials from '../components/pages/welcome/Testimonials'
import SeoMeta from '../mixins/seo-meta'

export default {
  components: {Testimonials, OpenFormFooter, Features, MoreFeatures},

  layout: 'default',

  mixins: [SeoMeta],

  data: () => ({
    title: window.config.appName,
    metaTitle: 'Create beautiful & open-source forms for free',
  }),

  mounted() {
  },

  methods: {
    // openCrisp () {
    //   window.$crisp.push(['do', 'chat:show'])
    //   window.$crisp.push(['do', 'chat:open'])
    //   window.$crisp.push(['do', 'message:send', ['text', "Hi! I'd like to learn more about OpnForm"]])
    // }
  },

  computed: {
    ...mapGetters({
      authenticated: 'auth/check'
    }),
    configLinks: () => window.config.links
  }
}
</script>

<style lang="scss" scoped>

.customer-logo-container {
  max-width: 130px;
  width: 100%;
}

@screen md {
  #macbook-video {
    position: absolute;
    max-width: 84.8% !important;
    right: 0px;
    top: 6.8%;
  }
}
</style>
