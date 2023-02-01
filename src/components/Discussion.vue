<template>
  <section class="comments">
    <CreateDiscussion />
    <div class="container" v-for="(disc, index) in discussions" :key="disc.id">
      <div class="comm-header">
        <img :src="disc.user?.avatar" />
        <h2>
          {{ disc.user.name }}<span>{{ getTime[index] }}</span>
        </h2>
      </div>
      <div class="comm-footer">
        <div class="comm-content">
          <p>{{ disc.text }}</p>
        </div>
        <div class="comm-btn">
          <div class="badge" @click="addLikes(disc.id)">
            <img src="../assets/like.png" alt="" />
            <span>{{ disc.likes }}</span>
          </div>
          <button>Reply</button>
        </div>
        <Reply v-if="disc.replies" :replies="disc.replies" />
        <NewComment v-if="disc.replies" :id="disc.id" />
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import Reply from "./Reply.vue";
import NewComment from "./NewComment.vue";
import CreateDiscussion from "./CreateDiscussion.vue";
import moment from "moment";
export default {
  name: "app-descussion",
  components: {
    Reply,
    NewComment,
    CreateDiscussion,
  },
  computed: {
    discussions() {
      return this.$store.state.discussions;
    },
    getTime() {
      return this.discussions.map((dis) => moment(dis.date).format("HH:mm:ss"));
    },
  },
  methods: {
    addLikes(val) {
      this.$store.commit("addLikes", val);
    },
  },
};
</script>

<style lang="scss">
.comments {
  border: 0.5px solid rgb(197, 197, 197);
  width: 1000px;
  background-color: rgb(191, 236, 251);
}
.container {
  width: 800px;
  margin-bottom: 20px;
  // background-color: rgb(214, 212, 212);
}

h2 {
  span {
    margin-left: 10px;
  }
}

.comm-header {
  display: flex;
  column-gap: 10px;

  h2 {
    span {
      color: rgb(0, 109, 145);
      font-size: 18px;
    }
  }
}

img {
  width: 80px;
  height: auto;
  border-radius: 50%;
}

.comm-content {
  font-size: 22px;
  width: 600px;
  margin-left: 100px;
}

.comm-footer {
  display: flex;
  flex-direction: column;
  width: 400px;
  button {
    display: inline-block;
  }
}

.comm-btn {
  display: flex;
  column-gap: 30px;
  margin-left: 20px;
  button {
    font-size: 18px;
    color: darkblue;
    width: 100px;
    height: 40px;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }
  .badge {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 60px;
    border-radius: 10px;
    color: white;
    background-color: gray;
    cursor: pointer;
    img {
      width: 20px;
    }
    span {
      color: rgb(0, 0, 0);
      font-weight: bold;
    }
  }
}
</style>
