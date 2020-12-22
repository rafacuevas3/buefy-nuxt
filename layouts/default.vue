<template>
  <div>
    <nav
      class="navbar header has-shadow is-primary"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <a class="navbar-item" href="/">Nuxt with Buefy Table</a>

        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
    </nav>


    <section class="main-content columns">
      <aside class="column is-2 section">
        <b-menu>
          <b-menu-list label="Menu">
            <nuxt-link :to="{ name: 'user.account' }" exact-active-class="is-active">
              <b-icon icon="account" size="is-small"/> My Account
            </nuxt-link>

            <nuxt-link :to="{ name: 'index' }" exact-active-class="is-active">
              <b-icon icon="home" size="is-small"/> Dashboard
            </nuxt-link>
            
            <b-menu-item expanded :active="isActive">
              <template slot="label" slot-scope="props">
                <b-icon icon="account" size="is-small"/>

                Producers
                
                <b-icon class="is-pulled-right" :icon="props.expanded ? 'menu-down' : 'menu-up'"></b-icon>
              </template>


              <nuxt-link :to="{ name: 'producer.add' }" exact-active-class="is-active">
                <b-icon icon="plus" size="is-small"/> New producer
              </nuxt-link>

              <nuxt-link :to="{ name: 'producer.active' }" exact-active-class="is-active">
                <b-icon icon="check" size="is-small"/> Active producers
              </nuxt-link>

              <nuxt-link :to="{ name: 'productions.waiting' }" exact-active-class="is-active">
                <b-icon icon="clock" size="is-small"/> Waiting productions
              </nuxt-link>

              <nuxt-link :to="{ name: 'productions.review' }" exact-active-class="is-active">
                <b-icon icon="check" size="is-small"/> Review productions
              </nuxt-link>

              <nuxt-link :to="{ name: 'productions.edit' }" exact-active-class="is-active">
                <b-icon icon="pencil" size="is-small"/> Edit production
              </nuxt-link>
            </b-menu-item>
            
          </b-menu-list>
        </b-menu>
      </aside>

      <div class="container column is-10">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isActive: false,
      items: [
        {
          title: 'Dashboard',
          icon: 'home',
          to: { name: 'index' },
        },
        {
          title: 'Nueva productora',
          icon: 'plus',
          to: { name: 'add.producer' },
        },
      ],
    }
  },
}
</script>
