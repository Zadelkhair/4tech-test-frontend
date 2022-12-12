<template>
  <div class="range-input-container" :id="'range-input-' + id">
    <div class="bar">
      <div class="bar-fill"
        :style="`
          background: ${colors[1]};
        `"
      >
        <div class="left-side-cercle">
          <div class="cercle"
            :style="`
              background: ${colors[0]};
            `"
          ></div>
        </div>
        <div class="right-side-cercle">
          <div class="cercle"
            :style="`
              background: ${colors[0]};
            `"
          ></div>
        </div>
        <div class="values"
          :style="`
            color: ${colors[0]};
          `"
        >
          <div class="from">{{ from | round | priceFilter }}{{ " "+unit }}</div>
          <div class="to">{{ to | round | priceFilter }}{{ " "+unit }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BetweenInput",
  props: {
    value: {
      type: Array,
      default: () => [],
    },
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 100,
    },
    step: {
      type: Number,
      default: 1,
    },
    unit: {
      type: String,
      default: "",
    },
    colors: {
      type: Array,
      default: () => ['#004a5d', '#3c7381'],
    },
  },
  data() {
    return {
      id: "",
      from: this.value[0] || this.min,
      to: this.value[1] || this.max,
    };
  },
  filters: {
    round(value) {
      return Math.round(value);
    },
    priceFilter(value) {
      if (value == null) return "Prix non communiqué";
      // price filter without coma
      return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
    },
  },
  watch: {
    from() {
      this.setBarFillPosition();
    },
    to() {
      this.setBarFillPosition();
    },
    value() {
      this.from = this.value[0] || this.min;
      this.to = this.value[1] || this.max;
    },
  },
  created() {
    this.id = Math.random().toString(36).substr(2, 9);
  },
  mounted() {
    // get the range-input

    this.setBarFillPosition();
    this.setBarFillEvents();
  },
  methods: {
    setBarFillPosition() {
      // get the bar fill element
      let rangeInput = document.querySelector("#range-input-" + this.id);
      let bar = rangeInput.querySelector(".bar");
      let barFill = bar.querySelector(".bar-fill");

      if (!barFill) return;

      // get the left value and convert it to percentage
      let left = ((this.from - this.min) / (this.max - this.min)) * 100;
      // get the right value and convert it to percentage
      // let right = (this.max - this.to) / (this.max - this.min) * 100;
      // get the width value and convert it to percentage
      let width = ((this.to - this.from) / (this.max - this.min)) * 100;

      // set the bar fill element style
      barFill.style.left = left + "%";
      barFill.style.width = width + "%";
    },
    setBarFillEvents() {
      // get the range-input
      let rangeInput = document.querySelector("#range-input-" + this.id);
      let bar = rangeInput.querySelector(".bar");
      let barFill = bar.querySelector(".bar-fill");

      // add drag and drop enevent listener to the left side cercle
      // get left side cercle element
      let leftSideCercle = bar.querySelector(".left-side-cercle");
      // add drag and drop enevent listener to the left side cercle

      let leftdown = (e) => {
        console.log("mouse down");

        // diselect text
        window.getSelection().removeAllRanges();
        // disable text selection
        document.onselectstart = function () {
          return false;
        };

        let move = (e) => {
          console.log("mouse move");

          // if touch
          if (e.touches) e = e.touches[0];

          // get mouse position in bar
          let mousePosition = e.clientX - bar.getBoundingClientRect().left;

          // convert mouse position to percentage
          let mousePositionPercentage = (mousePosition / bar.offsetWidth) * 100;

          if (mousePositionPercentage < 0)
            mousePositionPercentage = 0;
          else if (mousePositionPercentage > 100)
            mousePositionPercentage = 100;

          // set the left value
          let from =
            ((this.max - this.min) * mousePositionPercentage) / 100 + this.min;

          if(from < this.min) from = this.min;
          else if(from > this.max) from = this.max;

          if(from > this.to) from = this.to;

          this.from = from;
        };

        let up = () => {
          console.log("mouse up");

          // emit the value
          this.$emit("input", [this.from, this.to]);

          // leftSideCercle.removeEventListener("mousemove", move);
          // leftSideCercle.removeEventListener("mouseup", up);
          // leftSideCercle.removeEventListener("mouseleave", up);

          let newLeftSideCercle = leftSideCercle.cloneNode(true);
          // get parent element
          let parent = leftSideCercle.parentElement;
          // remove the leftSideCercle
          leftSideCercle.remove();
          // add the new leftSideCercle
          parent.appendChild(newLeftSideCercle);

          // set the events again
          this.setBarFillEvents();

          // enable text selection
          document.onselectstart = function () {
            return true;
          };
        };

        // add mouse move event listener
        leftSideCercle.addEventListener("mousemove", move);
        // touch move event listener
        leftSideCercle.addEventListener("touchmove", move);

        // add mouse up event listener
        leftSideCercle.addEventListener("mouseup", up);
        // touch end event listener
        leftSideCercle.addEventListener("touchend", up);

        // add mouse leave event listener
        leftSideCercle.addEventListener("mouseleave", up);
        // touch cancel event listener
        leftSideCercle.addEventListener("touchcancel", up);
      };

      leftSideCercle.addEventListener("mousedown", leftdown);
      leftSideCercle.addEventListener("touchstart", leftdown);

      // add drag and drop enevent listener to the right side cercle
      // get right side cercle element
      let rightSideCercle = bar.querySelector(".right-side-cercle");
      // add drag and drop enevent listener to the right side cercle

      let rightdown = (e) => {
        console.log("mouse down");

        // diselect text
        window.getSelection().removeAllRanges();
        // disable text selection
        document.onselectstart = function () {
          return false;
        };

        let move = (e) => {
          console.log("mouse move");

          // if touch
          if (e.touches) e = e.touches[0];

          // get mouse position in bar
          let mousePosition = e.clientX - bar.getBoundingClientRect().left;

          // convert mouse position to percentage
          let mousePositionPercentage = (mousePosition / bar.offsetWidth) * 100;

          if (mousePositionPercentage < 0)
            mousePositionPercentage = 0;
          else if (mousePositionPercentage > 100)
            mousePositionPercentage = 100;

          // set the right value
          let to =
            ((this.max - this.min) * mousePositionPercentage) / 100 + this.min;

          if(to < this.min) to = this.min;
          else if(to > this.max) to = this.max;

          if(to < this.from) to = this.from;

          this.to = to;

        };

        let up = () => {
          console.log("mouse up");

          // emit the value
          this.$emit("input", [this.from, this.to]);

          // rightSideCercle.removeEventListener("mousemove", move);
          // rightSideCercle.removeEventListener("mouseup", up);
          // rightSideCercle.removeEventListener("mouseleave", up);

          let newRightSideCercle = rightSideCercle.cloneNode(true);
          // get parent element
          let parent = rightSideCercle.parentElement;
          // remove the rightSideCercle
          rightSideCercle.remove();
          // add the new rightSideCercle
          parent.appendChild(newRightSideCercle);

          // set the events again
          this.setBarFillEvents();

          // enable text selection
          document.onselectstart = function () {
            return true;
          };
        };

        // add mouse move event listener
        rightSideCercle.addEventListener("mousemove", move);
        // touch move event listener
        rightSideCercle.addEventListener("touchmove", move);

        // add mouse up event listener
        rightSideCercle.addEventListener("mouseup", up);
        // touch end event listener
        rightSideCercle.addEventListener("touchend", up);

        // add mouse leave event listener
        rightSideCercle.addEventListener("mouseleave", up);
        // touch cancel event listener
        rightSideCercle.addEventListener("touchcancel", up);
      };

      rightSideCercle.addEventListener("mousedown", rightdown);
      rightSideCercle.addEventListener("touchstart", rightdown);
    },
  },
};
</script>

<style scoped>
.range-input-container {
  width: 100%;
  height: 100%;
  position: relative;
  margin-bottom:30px;
  margin-top: 20px;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.bar {
  width:100%;
  /* width: calc(100% - 15px); */
  height: 100%;
  position: absolute;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  background-color: #e4e4e4;
  height: 4px;
}

.bar-fill {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #3a3a3a;
  border-radius: 5px;
}

.left-side-cercle,
.right-side-cercle {
  width: 50px;
  height: 50px;
  position: absolute;
  top: 50%;
  cursor: grab;
}

.left-side-cercle .cercle,
.right-side-cercle .cercle {
  width: 15px;
  height: 15px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #1c1c1c;
  border-radius: 50%;
}

.left-side-cercle {
  left: 0;
  transform: translate(-50%, -50%);
  z-index: 2;
}

.right-side-cercle {
  right: 0;
  transform: translate(50%, -50%);
  z-index: 2;
}

.range-input-container .bar-fill .values {
  position: absolute;
  transform: translate(-50%, -50%);
  top: 20px;
  left: 50%;
  min-width: calc(100% + 15px);
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 0;
  color: #101010;
  font-weight: 500;
  font-size: 14px;
  z-index: 0;
}

.range-input-container .bar-fill .values .from {
  left: 0;
  margin-right: 5px;
  /* no wrap text */
  white-space: nowrap;
}

.range-input-container .bar-fill .values .to {
  right: 0;
  white-space: nowrap;
}
</style>
