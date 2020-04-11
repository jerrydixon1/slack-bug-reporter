<template>
  <section class="section">
    <div class="columns is-mobile">
      <card title="Bug Form">
        <BugForm @update="updateBugData" />
      </card>

      <card title="Bug Report" icon="arrange-bring-to-front">
        <BugReport :bug-json="bugJson" />
      </card>
    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'
import BugForm from '~/components/BugForm'
import BugReport from '~/components/BugReport'

export default {
  name: 'HomePage',
  components: {
    Card,
    BugForm,
    BugReport
  },
  data() {
    return {
      bugJson: ''
    }
  },
  methods: {
    updateBugData(data) {
      this.bugJson = JSON.stringify(data)
    }
  }
}
</script>
