<template>
  <div><h1>nsdfnjsdfnjksdfnjkldsfjknsdf</h1></div>
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
