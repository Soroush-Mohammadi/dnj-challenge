<template>
  <section class="discussion">
    <form @submit="addDescussion($event)">
      <img :src="user.avatar" />
      <input placeholder="Start a discussion" v-model="text" />
    </form>
  </section>
</template>

<script>
export default {
  data() {
    return {
      discussion: {},
      text: "",
    };
  },
  computed: {
    user() {
      return this.$store.state.user;
    },
    currentData() {
      const date = new Date();
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();
      return `${day}-${month}-${year}`;
    },
  },
  methods: {
    async addDescussion(e) {
      e.preventDefault();
      if (this.text.length > 0) {
        await this.setDiscussion();
        await this.$store.dispatch("addDiscussion", this.discussion);
      }
    },
    async setDiscussion() {
      this.discussion.id = await Math.floor(Math.random() * 100 + 1);
      this.discussion.likes = await 0;
      this.discussion.text = await this.text;
      this.discussion.user = {
        name: await this.user.name,
        avatar: await this.user.avatar,
      };
      this.discussion.replies = await [];
      this.discussion.iLikedIt = await false;
      this.discussion.date = await Math.floor(
        new Date(this.currentData).getTime() / 1000
      );
      console.log(this.discussion);
    },
  },
};
</script>

<style lang="scss">
.discussion {
  padding: 20px 0;
  background-color: rgb(213, 243, 253);
  form {
    display: flex;
    align-items: center;
    justify-content: center;
    column-gap: 20px;

    input {
      width: 600px;
      height: 30px;
      border-radius: 10px;
      border: 0.5px solid rgb(189, 188, 188);
      padding: 5px 20px;
      font-size: 18px;
    }
    input:focus {
      outline: none;
    }
  }
}
</style>
