<template>
  <section class="replies">
    <div class="container" v-for="rep in replies" :key="rep.id">
      <div class="reply-header">
        <img :src="rep.user.avatar" />
        <h4>{{ rep.user.name }}</h4>
      </div>
      <div class="reply-body">
        <p>{{ rep.text }}</p>
      </div>
      <div class="reply-footer">
        <div class="likes" @click="addReplyLikes(rep.id)">
          <img src="../assets/like.png" />
          <span>{{ rep.likes }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "app-reply",
  props: {
    replies: {
      type: Array,
    },
  },
  methods: {
    addReplyLikes(val) {
      this.$store.commit("addReplyLikes", val);
    },
  },
};
</script>

<style lang="scss">
.container {
  display: flex;
  flex-direction: column;
  margin: 20px 60px 0;

  .reply-header {
    display: flex;
    column-gap: 20px;
    img {
      border-radius: 50%;
    }
    h4 {
      font-size: 20px;
    }
  }

  .reply-body {
    margin-left: 100px;
    p {
      font-size: 20px;
    }
  }

  .reply-footer {
    .likes {
      display: flex;
      justify-content: space-around;
      align-items: center;
      width: 60px;
      height: 40px;
      border-radius: 10px;
      color: white;
      background-color: gray;
      cursor: pointer;
      img {
        width: 20px;
      }
      span {
        color: black;
        font-weight: bold;
      }
    }
  }
}
</style>
