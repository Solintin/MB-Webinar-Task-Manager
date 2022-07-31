<!-- eslint-disable -->
<template>
  <div>
    <div
      v-show="Overlay"
      :class="
        Overlay
          ? ' transform  translate-x-0'
          : ' transform  - translate-x-[1000px]'
      "
      class="px-10 flex justify-center cursor-pointer items-center overlay transform transition duration-300 bg-red-500"
    ></div>

    <div
      class="z-[12] booknow transform transition duration-300"
      v-show="Overlay"
      :class="Overlay ? ' translate-x-0' : '- translate-x-[1000px]'"
    >
      <div class="rounded-md bg-white px-4 pt-5 pb-1">
        <form @submit.prevent="editTask">
          <input
            required
            type="text"
            id="title"
            name="title"
            v-model="name"
            class="w-full p-3 border-2 rounded outline-none"
          />

          <div class="flex justify-between">
            <div
              @click="closeModal"
              class="bg-red-500 rounded my-4 py-3 px-4 text-[12px] font-medium text-white"
            >
              Cancel
            </div>
            <button
              class="bg-green-500 rounded my-4 py-3 px-4 text-[12px] font-medium text-white"
            >
              Continue
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<!-- eslint-disable -->

<script>
export default {
  props: ["Overlay", "closeModal", "data"],
  data() {
    return {
      name: "",
    };
  },
  mounted() {
    this.name = this.data.name;
  },
  methods: {
    editTask() {
      this.loading = true;
      let payload = {
        name: this.name,
        description: "Task",
      };
      axios
        .put(`/task/${data.id}`, payload)
        .then((response) => {
          console.log(response);
          this.$toast.success("Task updated successfully");
          location.reload();
          this.loading = false;
        })
        .catch((error) => {
          this.loading = false;

          console.log(error);
        });
    },
  },
};
</script>

<style></style>
