<template>
  <SmartModal v-if="show" @close="hideModal">
    <div slot="header">
      <div class="row-wrapper">
        <h3 class="title">{{ $t("confirm") }}</h3>
        <div>
          <button class="icon" @click="hideModal">
            <i class="material-icons">close</i>
          </button>
        </div>
      </div>
    </div>
    <div slot="body" class="flex flex-col">
      <label>{{ title }}</label>
    </div>
    <div slot="footer">
      <div class="row-wrapper">
        <span></span>
        <span>
          <button class="icon" @click="hideModal">
            {{ no }}
          </button>
          <button class="icon primary" @click="resolve">
            {{ yes }}
          </button>
        </span>
      </div>
    </div>
  </SmartModal>
</template>

<script>
export default {
  props: {
    show: Boolean,
    title: "",
    yes: {
      type: String,
      default: function () {
        return this.$t("yes")
      },
    },
    no: {
      type: String,
      default: function () {
        return this.$t("no")
      },
    },
  },
  async mounted() {
    this._keyListener = function (e) {
      if (e.key === "Escape") {
        e.preventDefault()
        this.hideModal()
      }
    }
    document.addEventListener("keydown", this._keyListener.bind(this))
  },
  methods: {
    hideModal() {
      this.$emit("hide-modal")
    },
    resolve() {
      this.$emit("resolve")
    },
  },
  beforeDestroy() {
    document.removeEventListener("keydown", this._keyListener)
  },
}
</script>
