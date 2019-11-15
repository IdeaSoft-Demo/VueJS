<template>
  <section class="main-wizard">
    <div class="progress-line">
      <div :style="{ width: progressBarWidth }"></div>
    </div>
    <div
      v-if="currentStep < steps.length"
      class="step-number"><span>{{ progress }}</span></div>
    <div class="wizard-step container">

      <step
        :is="activeStepComponent"
        @nextStep="increaseStep"
        @prevStep="decreaseStep" />
      <step-right-bar :step="currentStep"/>
    </div>

    <div
      class="illustration"
      v-if="currentStep === steps.length">
      <img
        src="@/assets/images/app/wizard-wrapper/card-illustration.png"
        width="935"
        alt="illustration" />
    </div>
  </section>
</template>

<script>
import ChooseProduct from '@/components/Wizard/steps/ChooseProduct'
import PlannedBudget from '@/components/Wizard/steps/PlannedBudget'
import LastStep from '@/components/Wizard/steps/LastStep'
import StepRightBar from '@/components/Wizard/StepRightBar'

export default {
  name: 'WizardWrapper',
  components: {
    ChooseProduct,
    PlannedBudget,
    LastStep,
    StepRightBar
  },

  props: {
    steps: {
      type: Array,
      default: () => ([])
    }
  },

  data () {
    return {
      currentStep: 1
    }
  },

  computed: {
    activeStepComponent () {
      return this.steps.find(step => step.order === this.currentStep).name
    },
    progressBarWidth () {
      let progress = 100 / (this.steps.length - 1) * this.currentStep
      return `${progress}%`
    },
    progress () {
      return `${this.currentStep}/${this.steps.length - 1} Steps`
    },
  },
  methods: {
    increaseStep (data) {
      this.currentStep++
    },
    decreaseStep () {
      this.currentStep--
    },
    sendData () {
      this.$log('send')
    }
  }
}
</script>
