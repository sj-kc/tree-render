<template>
  <div>
    <div v-for="node in nodes" :key="node.id" class="q-ma-md">
      <div @click="addNode(node)">{{ node.name }}</div>
      <div v-if="node?.children?.length">
        <div
          v-for="child in node.children"
          :key="child.id"
          @click="addNode(child)"
          class="q-ml-md"
        >
          <span class="">{{ child.name }}</span>

          <div v-if="child.children?.length">
            <div
              v-for="grandChild in child.children"
              :key="grandChild.id"
              @click="addNode(grandChild)"
              class="q-ml-md"
            >
              <span>{{ grandChild.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <q-btn class="q-ma-md" @click="addParent">Add parent</q-btn>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IterativePage",
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
