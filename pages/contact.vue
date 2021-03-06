<template>
  <section class="container">
    <siteHeader />
    <main>
      <sectionHero :hero="hero" />
      <div class="form-container">
        <form
          @submit.prevent="validateForm">

          <span
            :class="{'input--filled': name.length !== 0}"
            class="input">
            <input
              id="input-name"
              v-model="name"
              class="input-field"
              type="text">
            <label
              class="input-label"
              for="input-name">
              <span
                class="input-label-content"
                data-content="Name">Name</span>
            </label>
          </span>

          <span
            :class="{'input--filled': email.length !== 0}"
            class="input">
            <input
              id="input-email"
              v-model="email"
              class="input-field"
              type="email">
            <label
              class="input-label"
              for="input-email">
              <span
                class="input-label-content"
                data-content="Email Address">Email Address</span>
            </label>
          </span>

          <span
            :class="{'input--filled': message.length !== 0}"
            class="input textarea">
            <textarea
              id="input-message"
              v-model="message"
              class="input-field input-textarea"/>
            <label
              class="input-label input-label-textarea"
              for="input-message">
              <span
                class="input-label-content input-label-content-textarea"
                data-content="Message">Message</span>
            </label>
          </span>

          <button
            id="submit-form"
            :class="validatedClass"
            class="submit"
            type="submit"/>

        </form>
      </div>
    </main>
    <siteFooter />
  </section>
</template>

<script>
  import config from '~/components/config.json'
  import siteHeader from '~/components/header'
  import sectionHero from '~/components/section-hero'
  import siteFooter from '~/components/footer'

  export default {
    name: 'Contact',
    components: {
      siteHeader,
      sectionHero,
      siteFooter
    },
    head () {
      return {
        title: "Let's Work Together! | morsecodemedia.com",
        meta: [
          {
            hid: 'description',
            name: 'description',
            content: 'Looking for a website? Need an engaging email to drive customers to your site? Just asking for advice? I can tackle whatever challenge you have.'
          },
          { hid: 'ogtitle', property: 'og:title', content: "Let's Work Together! | morsecodemedia.com" },
          { hid: 'ogurl', property: 'og:url', content: 'https://www.morsecodemedia.com/contact/' },
          { hid: 'ogdescription', property: 'og:description', content: 'Looking for a website? Need an engaging email to drive customers to your site? Just asking for advice? I can tackle whatever challenge you have.' },
          { hid: 'twsite', name: 'twitter:site', content: 'https://www.morsecodemedia.com/contact/' },
          { hid: 'twtitle', name: 'twitter:title', content: "Let's Work Together! | morsecodemedia.com" },
          { hid: 'twdescription', name: 'twitter:description', content: 'Looking for a website? Need an engaging email to drive customers to your site? Just asking for advice? I can tackle whatever challenge you have.' },
          { hid: 'googlename', itemprop: 'name', content: "Let's Work Together! | morsecodemedia.com" },
          { hid: 'googledescription', itemprop: 'description', content: 'Looking for a website? Need an engaging email to drive customers to your site? Just asking for advice? I can tackle whatever challenge you have.' }
        ],
        link: [
          { hid: 'canonical', rel: 'canonical', href: 'https://www.morsecodemedia.com/contact/' }
        ]
      }
    },
    data() {
      return {
        hero: {
          'header': "Let's Work <br>Together",
          'copy': "Looking for a website? Need an engaging email to drive customers to your site? Just asking for advice? I can't wait to tackle whatever challenge you are having."
        },
        validatedClass: '',
        showThankYou: false,
        name: '',
        email: '',
        message: ''
      }
    },
    methods: {
      timeout: function(delay, args) {
        return new Promise(function(resolve) {
          setTimeout(resolve, delay, args);
        })
      },
      validateForm: async function() {
        // this.validatedClass = 'submitted'
        // await this.timeout(1000)
        // validate name, email and message
        // if validated
          //this.validatedClass = ''
          //await this.timeout(425)
          //this.validatedClass = 'validated'
          //await this.timeout(1000)
          // Hide Form and show thank you message
        // else
          // this.validatedClass = 'error'
          // put error classes on form fields as needed
          // await this.timeout(1500)
          // this.validatedClass = ''
      },
      sendEmail: async function() {
        let client = new postmark.Client('api-key')

        client.sendEmail({
          'From': '',
          'To': '',
          'Subject': '',
          'TextBody': ''
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .form-container {
    padding: 50px 0;
    display: flex;
    align-content: center;
    justify-content: center;
    form {
      width: 90vw;
    }
  }

  .input {
    position: relative;
    display: inline-block;
    margin: 20px 0px;
    width: calc(100% - 2em);
    vertical-align: top;
  }

  .input-field {
    position: relative;
    display: block;
    padding: 15px;
    border-radius: 0;
    background: $white;
    color: $dk-grey;
    font-size: 18px;
    font-weight: 400;
    -webkit-appearance: none;
    width: 100%;
    border: 1px solid $dk-grey;
    -webkit-transition: background-color 0.25s, border-color 0.25s;
    transition: background-color 0.25s, border-color 0.25s;
    &:focus {
      outline-color: $form-green;
      + .input-label {
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
        .input-label-content {
          -webkit-transform: translate3d(0, 100%, 0);
          transform: translate3d(0, 100%, 0);
        }
      }
      + .input-field {
        background-color: transparent;
        border-color: $form-green;
      }
    }
  }

  .input-textarea {
    height: 200px;
    &:focus {
      + .input-label {
        -webkit-transform: translate3d(0, 10px, 0);
        transform: translate3d(0, 10px, 0);
      }
    }
  }

  .input--filled {
    .input-label {
      -webkit-transform: translate3d(0, 0, 0);
      transform: translate3d(0, 0, 0);
    }
    .input-label-content {
      -webkit-transform: translate3d(0, 100%, 0);
      transform: translate3d(0, 100%, 0);
    }
    .input-field {
      background-color: transparent;
      border-color: $form-green;
    }
  }

  .textarea {
    &.input--filled {
      .input-label {
        -webkit-transform: translate3d(0, 10px, 0);
        transform: translate3d(0, 10px, 0);
      }
    }
  }

  .input-label {
    display: inline-block;
    padding: 0 15px;
    color: $dk-grey;
    font-weight: bold;
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    width: 100%;
    text-align: left;
    position: absolute;
    bottom: 80%;
    pointer-events: none;
    overflow: hidden;
    -webkit-transform: translate3d(0, 3em, 0);
    transform: translate3d(0, 3em, 0);
    -webkit-transition: -webkit-transform 0.25s;
    transition: transform 0.25s ;
    -webkit-transition-timing-function: ease-in-out;
    transition-timing-function: ease-in-out;
    &-textarea {
      bottom: 100%;
    }
    &-content {
      position: relative;
      display: block;
      padding: 20px 0;
      width: 100%;
      color: $dk-grey;
      -webkit-transition: -webkit-transform 0.25s;
      transition: transform 0.25s;
      -webkit-transition-timing-function: ease-in-out;
      transition-timing-function: ease-in-out;
      &-textarea {
        color: $dk-grey;
      }
      &::after {
        content: attr(data-content);
        position: absolute;
        font-weight: bold;
        bottom: 60%;
        left: 0;
        height: 100%;
        width: 100%;
        color: $form-green;
        padding: 0;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-size: 16px;
      }
    }
  }

  button {
    &.submit {
      outline: none;
      display: block;
      height: 40px;
      text-align: center;
      width: 175px;
      border-radius: 40px;
      background: rgba(255, 255, 255, .95);
      border: 2px solid $form-green;
      color: $form-green;
      font-size: 20px;
      justify-self: center;
      align-self: center;
      cursor: pointer;
      transition: all 0.25s ease;
      &:hover {
        color:$white;
        background: $form-green;
      }
      &:after {
        content: "Send Message";
      }
    }
    &.submitted {
      width: 40px;
      border-color: #6c757d;
      border-left-color: $form-green;
      border-right-color: $form-green;
      animation: rotating 1s 0.25s linear infinite;

      &:after {
        content:"";
      }
      &:hover {
        color: $form-green;
        background: none;
      }
    }
    &.validated {
      color: $white;
      background: $form-green;
      &:after {
        content:"Success";
        line-height: 0;
        padding: 0;
        margin: 0;
      }
      &:hover {
        background: none;
      }
    }
    &.error {
      color: $white;
      border: 2px solid $form-red;
      background: $form-red;
      &:after {
        content:"Error";
        line-height: 0;
        padding: 0;
        margin: 0;
      }
      &:hover {
        color: $white;
        background: none;
      }
    }
  }
  @keyframes rotating {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>
