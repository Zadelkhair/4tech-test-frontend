<template>
  <div class="toggle-input-container" :id="'toggle-input-' + id">
    <button
      class="toggle"
      :class="{ active: active }"
      @click="onClickToggle"
      :style="`
        background-color: ${active ? colors[0] : colors[1]};
        transform: scale(${scale});
      `"
    >
      <div class="toggle-cerc"></div>
    </button>
  </div>
</template>

<script>
export default {
  name: "ToggleInput",
  props: {
    value: {
      type: Boolean,
      default: false,
    },
    scale: {
      type: Number,
      default: 1,
    },
    colors: {
      type: Array,
      default: () => ["#2196f3", "#e0e0e0"],
    },
  },
  data() {
    return {
      id: "",
      active: this.value,
    };
  },
  watch: {
    active() {
      // emit the value to the parent component
      this.$emit("input", this.active);
    },
  },
  created() {
    this.id = Math.random().toString(36).substr(2, 9);
  },
  mounted() {},
  methods: {
    onClickToggle() {
      this.active = !this.active;
    },
  },
};
</script>

<style scoped>
.toggle-input-container {
  position: relative;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.toggle {
  position: relative;
  width: 50px;
  height: 30px;
  background-color: #e0e0e0;
  border-radius: 15px;
  transition: background-color 0.3s ease;
}

.toggle .toggle-cerc {
  position: absolute;
  top: 2px;
  left: 2px;
  width: 26px;
  height: 26px;
  background-color: #fff;
  border-radius: 50%;
  transition: left 0.3s ease;
}

.toggle.active {
  background-color: #2196f3;
}

.toggle.active .toggle-cerc {
  left: 22px;
}
</style>
