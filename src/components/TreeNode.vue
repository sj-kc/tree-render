<template>
  <div :class="className">
    <div @click="addNode(node)">
      {{ node.name }}
    </div>
    <div v-if="hasChildren">
      <TreeNode
        v-for="child in node.children"
        :key="child.id"
        :node="child"
        :className="'q-ml-md'"
        @addNode="addNode"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "TreeNode",
  props: {
    node: {
      type: Object,
      required: true,
    },

    className: {
      type: String,
      default: "q-ma-md",
    },
  },
  computed: {
    hasChildren() {
      const { children } = this.node;
      return children && children.length > 0;
    },
  },
  methods: {
    addNode(parentNode) {
      this.$emit("addNode", parentNode);
    },
  },
};
</script>
