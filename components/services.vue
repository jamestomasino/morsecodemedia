<template>
  <section
    v-if="services"
    class="services">
    <article
      v-for="service in services"
      :key="service.id">
      <header>
        <h2>{{ service.title }}</h2>
      </header>
      <p>{{ service.description }}</p>
    </article>
  </section>
</template>

<script>
  import { services } from '~/components/config.json'

  export default {
    name: 'Services',
    data() {
      return {
        services: services
      }
    }
  }
</script>

<style lang="scss" scoped>

  .services {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-template-rows: auto auto;
    grid-gap: 1px;
    article {
      padding: 30px;
      &:nth-of-type(odd) {
        background: $offwhite;
      }
      &:nth-of-type(even) {
        background: $eggshell;
      }
      h2 {
        font-size: 36px;
        padding-bottom: 15px;
        margin-bottom: 15px;
        text-transform: uppercase;
      }
    }
  }
  @media (min-width: 768px) {
    .services {
      grid-template-columns: repeat(2, 1fr);
      article {
        padding: 40px;
        h2 {
          font-size: 36px;
        }
      }
    }
  }
  @media (min-width: 992px) {
    .services {
      grid-template-columns: repeat(3, 1fr);
      article {
        h2 {
          font-size: 36px;
        }
      }
    }
  }
  @media (min-width: 1200px) {
    .services {
      grid-template-columns: repeat(3, 1fr);
    }
  }
</style>