<template>
  <div id="hamburger" :class="{ open: toggle }">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 57 67">
      <title>hamburger</title>
      <line
        class="line line2"
        x1="11"
        y1="33.5"
        x2="57"
        y2="33.5"
        fill="none"
        stroke="#000"
        stroke-miterlimit="10"
        stroke-width="3"
      />
      <path
        class="line line1"
        d="M13,51.5l39-39h0a3.83,3.83,0,0,0-.29-5.71A32,32,0,0,0,.06,30a33.08,33.08,0,0,0,.18,6A9.29,9.29,0,0,0,9.5,44h46"
        transform="translate(1.5 1.5)"
        fill="none"
        stroke="#000"
        stroke-miterlimit="10"
        stroke-width="3"
      />
      <path
        class="line line3"
        d="M13,12.5l39,39h0a3.83,3.83,0,0,1-.29,5.71A32,32,0,0,1,.06,34a33.08,33.08,0,0,1,.18-6A9.29,9.29,0,0,1,9.5,20h46"
        transform="translate(1.5 1.5)"
        fill="none"
        stroke="#000"
        stroke-miterlimit="10"
        stroke-width="3"
      />
    </svg>
  </div>
</template>

<script>
export default {
  props: {
    logo: {
      toggle: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
#hamburger {
  width: 20%;
  height: 20%;
}
#hamburger .line {
  fill: none;
  stroke: black;

  transition: stroke-dasharray 700ms cubic-bezier(0.4, 0, 0.2, 1),
    stroke-dashoffset 700ms cubic-bezier(0.4, 0, 0.2, 1);
}
#hamburger .line1 {
  stroke-dasharray: 55 300;
  stroke-dashoffset: -150;
}
#hamburger .line2 {
  stroke-dasharray: 48 300;
}
#hamburger .line3 {
  stroke-dasharray: 55 300;
  stroke-dashoffset: -150;
}
#hamburger.open .line1 {
  stroke-dashoffset: 0;
}
#hamburger.open .line2 {
  stroke-dasharray: 1 100;
  stroke-dashoffset: -21;
}
#hamburger.open .line3 {
  stroke-dashoffset: 0;
}
</style>
