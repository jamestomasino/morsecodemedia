<template>
  <nuxt-link
    v-lazy-container="{ selector: 'img' }"
    :to="'/case-studies/' + cs.title | lowerKebab"
    :class="styleClasses"
    class="case-study"
    role="link">
    <img
      :data-src="buildImage(cs.img)"
      :data-loading="loadingColors[Math.floor(Math.random()*loadingColors.length)]"
      role="presentation">
    <div class="overlay">
      <h3>
        {{ cs.title }}
        <br>
        <span>&mdash; View Project &mdash;</span>
      </h3>
    </div>
    <span
      v-if="cs.needsPassword"
      class="requires-password">
      <font-awesome-icon icon="lock" />
    </span>
  </nuxt-link>
</template>

<script>
  import Vue from 'vue'
  import VueLazyload from 'vue-lazyload'
  import { library } from '@fortawesome/fontawesome-svg-core'
  import { faLock, faLockOpen } from '@fortawesome/free-solid-svg-icons'
  import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

  library.add(faLock, faLockOpen)
  Vue.component('font-awesome-icon', FontAwesomeIcon)

  Vue.use(VueLazyload, {
    preLoad: 1.3,
    attempt: 1
  })

  export default {
    name: 'CaseStudyListing',
    filters: {
      lowerKebab: function(term) {
        return term.toLowerCase().replace(/[.\s]/g, '-').replace(/[&#,+()$~%'":*?<>{}]/g, '' )
      }
    },
    props: {
      cs: {
        type: Object,
        required: true,
        twoWay: true,
        default: () => {}
      },
      styleClasses: {
        type: String,
        required: false,
        default: ''
      }
    },
    data() {
      return {
        loadingColors: [
          'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQYV2PQ09P7DwACogGKJIM9sQAAAABJRU5ErkJggg=='
        ]
      }
    },
    methods: {
      buildImage(imageSrc) {
        if (imageSrc) {
          if (imageSrc.substr(0,4) === 'http') {
            return imageSrc
          } else {
            return require(`../assets/images${imageSrc}`)
          }
        }
      }
    }
  }
</script>

<style lang="scss">

</style>
