<template>
  <div class="choices-input-container" :id="'choices-input-' + id"
    :style="`
      border-color: ${colors[0]};
      background-color: ${colors[1]};
    `"
    >
    <button class="choice" v-for="c in choices" :key="c" @click="onClickChoice(c)"
      :style="`
        background-color: ${active === c ? colors[0] : colors[1]};
        color: ${active === c ? colors[1] : colors[0]};
        border-color: ${colors[0]};
      `"
    >
        {{ c }}
    </button>
  </div>
</template>

<script>
export default {
  name: "ChoicesInput",
  props: {
    value: {
      type: String,
      default: '',
    },
    colors: {
      type: Array,
      default: () => ["#2196f3", "white"],
    },
    choices : {
      type: Array,
      default: () => ["Yes", "No"],
    },
  },
  data() {
    return {
      id: "",
      active: this.value??this.choices[0],
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
    onClickChoice(val) {
      this.active = val;
    },
  },
};
</script>

<style scoped>
.choices-input-container {
  position: relative;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border-radius: 5px;
  border: 1px solid #2196f3;
  overflow: hidden;
}

.choice {
  padding: 7px 10px;
  margin: 0;
  font-size: 13px;
  font-weight: 500;
  text-align: center;
  cursor: pointer;
  border: none;
  outline: none;
  border-radius: 0;
  background: white;
  color: #2196f3;
  border-right: 1px solid #2196f3;
}

.choice:last-child {
  border-right: none;
}

</style>
