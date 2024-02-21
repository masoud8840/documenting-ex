<template>
  <div class="lg:relative" ref="ctr">
    <div
      class="w-12 h-12 border bg-light-1 rounded-full flex items-center justify-center cursor-pointer"
      :class="{
        'border-primary text-primary': searchText,
        'border-border-2-light text-text-hint-dark': !searchText,
      }"
      @click="expand = true"
    >
      <MyIcon name="search" class="" />
    </div>
    <TransitionFade>
      <form
        v-if="expand"
        @submit.prevent="submit"
        class="absolute right-0 top-0 left-0 lg:end-auto mx-4 lg:mx-0 mt-4 lg:mt-0 z-40 flex justify-center border border-primary bg-light-1 rounded-full shadow-md overflow-hidden duration-300 h-12"
      >
        <button
          type="submit"
          class="w-12 h-full flex items-center justify-center cursor-pointer -ms-px"
          @click="submit"
        >
          <MyIcon name="search" class="text-primary" />
        </button>
        <input
          v-model="searchText"
          :placeholder="$language.search()"
          class="text-text-secondary-dark w-full lg:w-64 h-full pe-6 ps-0 outline-none"
          @input="change"
        />
      </form>
    </TransitionFade>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import MyIcon from "./MyIcon.vue";
import TransitionFade from "./TransitionFade.vue";

export default Vue.extend({
  components: { MyIcon, TransitionFade },
  model: {
    prop: "searchText",
    event: "change",
  },
  data() {
    return {
      searchText: "",
      expand: false,
      k: 0,
    };
  },
  watch: {
    expand() {},
  },
  methods: {
    clickOutside(e: any) {
      if (
        // @ts-ignore
        !this.$refs.ctr?.contains(e.target)
      ) {
        this.expand = false;
      }
    },
    change(e: any) {
      this.$emit("change", e.target.value.replace("<", "").replace(">", ""));
    },
    submit() {
      this.$emit("submit", this.searchText.replace("<", "").replace(">", ""));
    },
  },
  mounted() {
    if (process.browser) {
      document.addEventListener("click", this.clickOutside);
    }
  },
  destroyed() {
    if (process.browser) {
      document.removeEventListener("click", this.clickOutside);
    }
  },
});
</script>

<style lang="scss" scoped></style>
