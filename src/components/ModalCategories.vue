<template>
  <div class="backdrop" @click="handleBackdropCLick">
    <form autocomplete="off" class="modal" @click="addCategorie">
      Add categorie
      <input
        type="text"
        name="type"
        class="modal-input"
        placeholder="Type here"
      />

      <button type="submit" class="modal-btn">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  computed: {
    uid() {
      return this.$store.getters.uid;
    },

    categories() {
      return this.$store.getters.categories;
    },
  },

  methods: {
    handleBackdropCLick(e) {
      if (e.target === e.currentTarget) {
        this.$store.dispatch("toggleModal");
      }
    },

    addCategorie(e) {
      e.preventDefault();

      const text = e.currentTarget.elements.type.value.trim().toLowerCase();

      if (e.target.classList.contains("modal-btn")) {
        if (text === "") {
          alert("Enter sth");
          return;
        }

        if (this.categories.find((el) => el.type.includes(text))) {
          alert("You have this category");
          return;
        }

        const newCategorie = {
          id: Date.now(),
          uid: this.uid,
          type: text,
        };

        this.$store.dispatch("addCategorie", newCategorie);
        this.$store.dispatch("toggleModal");
      }
    },
  },
};
</script>
