<template>
  <div>
    test
    <svg
      id="hamburger"
      :class="{ open: isOpen }"
      @click.prevent="toggle"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 203.42 205"
    >
      <path
        class="line line1"
        d="M143.53,57.16H55.64a17.49,17.49,0,0,0-16,10.23c-.37.82-.73,1.65-1.06,2.49A62,62,0,0,0,34.2,92.94,69.06,69.06,0,0,0,103.26,162,76.74,76.74,0,0,0,180,85.26,85.26,85.26,0,0,0,94.74,0,94.74,94.74,0,0,0,0,94.74,105.26,105.26,0,0,0,105.26,200a116.57,116.57,0,0,0,48.26-10.39,24.68,24.68,0,0,0,7.33-39.93L144,132.87,55.38,44.22"
        transform="translate(2.5 2.5)"
      />
      <line class="line line2" x1="57.88" y1="90.54" x2="145.78" y2="90.54" />
      <path
        class="line line3"
        d="M54.88,118.92h87.9a17.48,17.48,0,0,0,16-10.22c.37-.82.72-1.66,1.06-2.5a62,62,0,0,0,4.42-23A69.07,69.07,0,0,0,95.15,14.08,76.73,76.73,0,0,0,18.42,90.82a85.26,85.26,0,0,0,85.26,85.26,94.74,94.74,0,0,0,94.74-94.73,104.84,104.84,0,0,0-9.1-42.87A20.56,20.56,0,0,0,156,32.24l-12,12L55.38,132.87"
        transform="translate(2.5 2.5)"
      />
    </svg>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
      this.$emit("toggle", this.isOpen);
    },
  },
  watch: {
    open(newValue, oldValue) {
      if (newValue !== oldValue) {
        this.toggle();
      }
    },
  },
};
</script>

<style scoped>
.line {
  transition: stroke-dasharray 900ms cubic-bezier(0.4, 0, 0.2, 1),
    stroke-dashoffset 900ms cubic-bezier(0.4, 0, 0.2, 1);
}
.line1 {
  stroke-dasharray: 87.9 1500;
  stroke-dashoffset: 0;
}
.line2 {
  stroke-dasharray: 87.9 0;
  stroke-dashoffset: 0;
}
.line3 {
  stroke-dasharray: 87.9 1500;
  stroke-dashoffset: 0;
}
#hamburger.open .line1 {
  stroke-dasharray: 125.9 1500;
  stroke-dashoffset: -932;
}

#hamburger.open .line2 {
  stroke-dasharray: 1 1500;
  stroke-dashoffset: -44;
}

#hamburger.open .line3 {
  stroke-dasharray: 125.9 1500;
  stroke-dashoffset: -746;
}
</style>
