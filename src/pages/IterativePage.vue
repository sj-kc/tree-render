<template>
  <div>
    <div
      v-for="item in flattenedNodes"
      :key="item.id"
      :style="{
        marginLeft: item.depth * 20 + 'px',
      }"
      @click="addNode(item.node)"
    >
      {{ item.node.name }}
    </div>

    <q-btn class="q-ma-md" @click="addParent">Add parent</q-btn>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  name: "IterativePage",
  setup() {
    const nodes = ref([
      {
        id: Date.now(),
        name: `- Parent Node ${Date.now()}`,
        children: [],
      },
    ]);

    const flattenedNodes = computed(() => {
      const stack = nodes.value.map((node) => ({ node, depth: 1 }));
      const result = [];

      while (stack.length > 0) {
        const { node, depth } = stack.shift();
        result.push({ node, depth });

        if (node.children && node.children.length > 0) {
          node.children.forEach((child) => {
            stack.unshift({ node: child, depth: depth + 1 });
          });
        }
      }

      return result;
    });

    const addNode = (parentNode) => {
      const newNode = {
        id: Date.now(),
        name: `- Node ${Date.now()}`,
        children: [],
      };

      parentNode.children.push(newNode);
    };

    const addParent = () => {
      const newNode = {
        id: Date.now(),
        name: `- Parent Node ${Date.now()}`,
        children: [],
      };

      nodes.value.push(newNode);
    };

    return {
      nodes,
      flattenedNodes,
      addNode,
      addParent,
    };
  },
};
</script>

<style>
.q-ml-md {
  margin-left: 1rem;
}
</style>
