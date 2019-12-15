/* eslint-disable vue/no-unused-components */
<template>
  <header class="block">
    <section class="sub-section">
      <h1 class="name">
        George Baldwin
      </h1>
      <h2 class="pitch">
        {{ summary }}
      </h2>
      <!-- <Tree /> -->
    </section>
  </header>
</template>

<script>
// import Tree from "./p5/trees";
export default {
  name: "Header",
  components: {
    // Tree
  },
  props: {
    title: { type: String, default: "George Baldwin" },
    summary: { type: String, default: "summary" }
  },
  data: function() {
    return {
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/global-vars.scss";
.name,
.pitch {
  color: $highlight;
  max-width: 780px;
}
.name {
  font-size: 5em;
  margin-bottom: 0.75em;
  &:hover {
  }
}
.pitch {
  user-select: none;
  font-size: 1.8em;
  font-weight: normal;
}
</style>