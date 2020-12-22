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
            <b-menu-item icon="account" label="My Account">
              <b-menu-item label="Account data"></b-menu-item>
              <b-menu-item label="Addresses"></b-menu-item>
            </b-menu-item>

            <nuxt-link :to="{ name: 'index' }" exact-active-class="is-active">
              <b-icon icon="home" size="is-small"/> Dashboard
            </nuxt-link>
            
            <b-menu-item icon="account_balance" expanded :active="isActive">
              <template slot="label" slot-scope="props">
                Producers
                
                <b-icon class="is-pulled-right" :icon="props.expanded ? 'menu-down' : 'menu-up'"></b-icon>
              </template>

              <nuxt-link :to="{ name: 'add.producer' }" exact-active-class="is-active">
                <b-icon icon="plus" size="is-small"/> New producer
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
