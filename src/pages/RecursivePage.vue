<template>
  <div>
    <TreeNode
      v-for="node in nodes"
      :key="node.id"
      :node="node"
      @addNode="addNode"
    />

    <q-btn class="q-ma-md" @click="addParent">Add parent</q-btn>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import TreeNode from "../components/TreeNode.vue";

export default defineComponent({
  name: "App",
  components: {
    TreeNode,
  },

  data() {
    return {
      nodes: [
        {
          id: Date.now(),
          name: `- Parent Node ${Date.now()}`,
          children: [],
        },
      ],
    };
  },

  methods: {
    addNode(parentNode) {
      const newNode = {
        id: Date.now(),
        name: `- Node ${Date.now()}`,
        children: [],
      };

      parentNode.children.push(newNode);
    },

    addParent() {
      const newNode = {
        id: Date.now(),
        name: `- Parent Node ${Date.now()}`,
        children: [],
      };

      this.nodes.push(newNode);
    },
  },
});
</script>
