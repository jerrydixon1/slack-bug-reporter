<template>
  <b-field class="steps-to-reproduce" label="Steps to reproduce">
    <div v-for="(step, i) in stepList" :key="i" class="step-input">
      <b-input v-model="stepList[i]" />
      <b-button type="is-danger" @click="removeStep(i)">
        <b-icon icon="trash" size="is-small" />
      </b-button>
    </div>

    <b-input
      v-model="newStep"
      placeholder="Type and press enter to add a new step"
      @keyup.native.enter="addStep()"
    />
  </b-field>
</template>

<script>
export default {
  data() {
    return {
      newStep: '',
      stepList: []
    }
  },
  computed: {
    enteredSteps() {
      const steps = this.stepList.filter((step) => !!step)
      if (this.newStep) {
        steps.push(this.newStep)
      }
      return steps
    }
  },
  watch: {
    enteredSteps() {
      this.$emit('update', this.enteredSteps)
    }
  },
  methods: {
    removeStep(i) {
      this.stepList.splice(i, 1)
    },
    addStep() {
      if (this.newStep) {
        this.stepList.push(this.newStep)
        this.newStep = ''
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.steps-to-reproduce {
  display: flex;
  flex-direction: column;
  > .control {
    .input {
      border-top-left-radius: 4px !important;
      border-bottom-left-radius: 4px !important;
      border-top-right-radius: 4px !important;
      border-bottom-right-radius: 4px !important;
    }
  }
  .step-input {
    display: flex;
    .control {
      width: 100%;
    }
    .button {
      border-radius: 0;
      border-top-right-radius: 4px;
      border-bottom-right-radius: 4px;
      background: #94291e;
    }
    & + *,
    .control + .control {
      margin-top: 0.5rem;
    }
  }
}
</style>
