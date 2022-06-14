<template>
  <slot :css="parsedTheme" />
</template>

<script>
const kebabize = (str) => str.replace(/[A-Z]+(?![a-z])|[A-Z]/g, ($, ofs) => (ofs ? "-" : "") + $.toLowerCase());

export default {
  name: "CssProvider",
  props: {
    css: {
      type: Object,
      default: () => {},
    }
  },
  computed: {
    parsedTheme() {
      let output = "";
      Object.entries(this.css).forEach(([cssKey,cssValue]) => {
        output += `--${kebabize(cssKey)}:${cssValue};`
      })
      return output
    },
  }
};
</script>
