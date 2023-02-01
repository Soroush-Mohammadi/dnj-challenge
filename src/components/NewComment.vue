<template>
  <div class="container">
    <form @submit="addComment($event)">
      <img :src="user.avatar" />
      <input type="text" placeholder="reply" v-model="newComment" />
    </form>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
    },
  },
  name: "create-diccusion",
  data() {
    return {
      newComment: "",
    };
  },
  computed: {
    user() {
      return this.$store.state.user;
    },
  },
  methods: {
    addComment(e) {
      e.preventDefault();
      const comment = {
        id: this.id,
        text: this.newComment,
        likes: 0,
        user: {
          name: this.$store.state.user.name,
          avatar: this.$store.state.user.avatar,
        },
      };

      this.$store.commit("addComment", comment);
      this.newComment = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 600px;
  height: auto;
  margin-left: 80px;

  form {
    display: flex;
    column-gap: 30px;
    align-items: center;
    input {
      padding: 5px;
      height: 30px;
      width: 100%;
      border-radius: 10px;
      border: 0.5px solid rgb(206, 206, 206);
      font-size: 20px;
    }
    input:focus {
      outline: none;
    }
    img {
      width: 60px;
    }
  }
}
</style>
