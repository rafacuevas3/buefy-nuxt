<template>
  <section class="section">
    <div class="columns is-mobile">
      <Table/>
    </div>
  </section>
</template>

<script >
import Table from '~/components/Table'

export default {
  name: 'HomePage',

  components: {
    Table,
  },
}
</script>
