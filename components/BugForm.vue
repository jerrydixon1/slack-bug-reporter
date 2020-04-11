<template>
  <form>
    <b-field label="Tags">
      <b-taginput
        v-model="bugData.tags"
        ellipsis
        icon="label"
        placeholder="Press enter to add (e.g. 'Bug', 'Usability')"
        class="tags-input"
      >
      </b-taginput>
    </b-field>
    <b-field label="Description">
      <b-input
        v-model="bugData.description"
        placeholder="(Required) Provide a short description of the bug"
        required
      />
    </b-field>
    <b-field label="Expected Behavior">
      <b-input
        v-model="bugData.expectedBehavior"
        placeholder="(Required) Describe the expected/ideal behavior"
        required
        type="textarea"
        rows="2"
      />
    </b-field>
    <b-field label="Actual Behavior">
      <b-input
        v-model="bugData.actualBehavior"
        placeholder="(Required) Describe the actual behavior encountered"
        required
        type="textarea"
        rows="2"
      />
    </b-field>
    <BugFormSteps @update="updateStepsToReproduce" />
    <b-field label="Process URL">
      <b-input
        v-model="bugData.processUrl"
        placeholder="(Optional) Provide a link to a specific process"
      />
    </b-field>
    <b-field label="Job ID">
      <b-input
        v-model="bugData.jobId"
        placeholder="(Optional) Provide a specific Job ID"
      />
    </b-field>
    <b-field label="Image/Video URL">
      <b-input
        v-model="bugData.mediaUrl"
        placeholder="(Optional) Enter a URL of a screenshot or screen capture"
      />
    </b-field>
  </form>
</template>

<script>
import BugFormSteps from '~/components/BugFormSteps'

export default {
  components: {
    BugFormSteps
  },
  data() {
    return {
      bugData: {
        stepsToReproduce: []
      }
    }
  },
  watch: {
    bugData: {
      deep: true,
      handler() {
        this.$emit('update', this.bugData)
      }
    }
  },
  methods: {
    updateStepsToReproduce(newSteps) {
      this.bugData.stepsToReproduce.length = 0
      this.bugData.stepsToReproduce.push(...newSteps)
    }
  }
}
</script>

<style lang="scss" scoped>
form {
  > * + * {
    margin-top: 1.5rem;
  }
  text-align: left;
  .textarea:not([rows]) {
    min-height: 80px;
  }
  /deep/ .control.has-icons-left .input {
    padding-left: 0.5rem !important;
  }
}
</style>
