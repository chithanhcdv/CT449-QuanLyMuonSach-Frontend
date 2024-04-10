<script>
export default {
    props: {
        borrowBooks: { type: Array, default: [] },
        activeIndex: { type: Number, default: -1 },
    },
    emits: ["update:activeIndex"],
    methods: {
        updateActiveIndex(index) {
            this.$emit("update:activeIndex", index);
        }
    }
};
</script>

<template>
  <ul class="list-group pt-3">
    <li
      class="list-group-item"
      v-for="(borrowBook, index) in borrowBooks"
      :key="borrowBook._id"
      :class="{ active: index === activeIndex}"
      @click="updateActiveIndex(index)"
    >
      {{ borrowBook.MADOCGIA }} - {{ borrowBook.MASACH }}
    </li>
  </ul>
</template>

