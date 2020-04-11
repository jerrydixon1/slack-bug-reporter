<template>
  <section class="bug-report">
    <div class="actions">
      <b-button @click="copy">Copy to clipboard</b-button>
    </div>
    <div id="bug-report-contents" class="contents">
      <!-- Description -->
      <p>
        <span v-if="bugData.description">
          <span v-if="bugData.tags && bugData.tags.length">
            <span v-for="(tag, i) in bugData.tags" :key="i"
              ><code>{{ tag }}</code
              >&nbsp;</span
            >
          </span>
          {{ bugData.description }}
        </span>
        <i v-else>
          No description provided!
        </i>
      </p>
      <br />

      <!-- Expected Behavior -->
      <p>
        <strong>Expected Behavior: </strong>
        <span v-if="bugData.expectedBehavior">
          {{ bugData.expectedBehavior }}
        </span>
        <i v-else>
          No expected behavior provided!
        </i>
      </p>
      <br />

      <!-- Actual Behavior -->
      <p>
        <strong>Actual Behavior: </strong>
        <span v-if="bugData.actualBehavior">
          {{ bugData.actualBehavior }}
        </span>
        <i v-else>
          No actual behavior provided!
        </i>
      </p>
      <br />

      <!-- Steps to reproduce -->
      <div>
        <strong>Steps to reproduce: </strong>
        <ol v-if="bugData.stepsToReproduce">
          <li v-for="(step, i) in bugData.stepsToReproduce" :key="i">
            {{ step }}
          </li>
        </ol>
        <i v-else>
          No steps to reproduce provided!
        </i>
      </div>
      <br />

      <!-- Process URL -->
      <p v-if="bugData.processUrl">
        <strong>Process URL: </strong>
        <a :href="bugData.processUrl">
          {{ bugData.processUrl }}
        </a>
      </p>
      <br />

      <!-- Job ID -->
      <p v-if="bugData.jobId">
        <strong>Job ID: </strong>
        <code>
          {{ bugData.jobId }}
        </code>
      </p>
      <br />

      <!-- Image/Video URL -->
      <p v-if="bugData.mediaUrl">
        <strong>Screenshot/Video: </strong>
        <a :href="bugData.mediaUrl">
          {{ bugData.mediaUrl }}
        </a>
      </p>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    bugJson: {
      type: String,
      default: '{}'
    }
  },
  computed: {
    bugData() {
      console.log('bug json: ', this.bugJson)
      try {
        return JSON.parse(this.bugJson)
      } catch (err) {
        return {}
      }
    }
  },
  methods: {
    copy() {
      const text = document.getElementById('bug-report-contents')
      let range
      let selection
      if (document.body.createTextRange) {
        // ms
        range = document.body.createTextRange()
        range.moveToElementText(text)
        range.select()
      } else if (window.getSelection) {
        // all others
        selection = window.getSelection()
        range = document.createRange()
        range.selectNodeContents(text)
        selection.removeAllRanges()
        selection.addRange(range)
      }
      document.execCommand('copy')
      this.$buefy.toast.open('Copied bug report to clipboard')
    }
  }
}
</script>

<style lang="scss" scoped>
section.bug-report {
  &,
  & * {
    text-align: left;
  }
  p {
    margin: 0;
  }
  code {
    padding: 0.25rem;
    + code {
      border-radius: 4px;
      margin-left: 0.25rem;
    }
  }
  .contents {
    margin-top: 1rem;
  }
}
</style>
