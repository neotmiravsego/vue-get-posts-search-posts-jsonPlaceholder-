<template>
  <div class="container">
    <div class="search-block__wrap">
      <div class="search-form">
        <div class="form-group">
          <button @click="filterArray" class="search-button">
            <img src="../../assets/search.svg" alt class="search-img" />
          </button>
          <input
            name="search"
            type="text"
            class="search-input"
            placeholder="Filter by author"
            v-model="search"
          />
        </div>
      </div>
    </div>
    <div class="post-list__wrap">
      <ul class="post-list">
        <li class="post-list__item" v-for="post in filteredPosts" :key="post.id">
          <div class="card-item">
            <h2 class="title-post">{{post.title}}</h2>
            <p class="content-post">{{post.body}}</p>
            <p class="author-post">{{post.user.name}}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
      posts: [],
      filteredPosts: [],
    };
  },
  methods: {
    filterArray() {
      if (!this.search) {
        this.filteredPosts = this.posts;
        return;
      }
      this.filteredPosts = this.posts.filter((el) => {
        return el.user.name.toLowerCase().includes(this.search);
      });
    },
    getData() {
      fetch("http://jsonplaceholder.typicode.com/posts")
        .then((response) => {
          return response.json();
        })
        .then((posts) => {
          fetch("http://jsonplaceholder.typicode.com/users")
            .then((response) => {
              return response.json();
            })
            .then((users) => {
              const postsWithUser = posts.map((post) => {
                let currentUser = null;
                users.forEach((user) => {
                  if (post.userId === user.id) {
                    currentUser = user;
                  }
                });
                return {
                  ...post,
                  user: currentUser,
                };
              });
              this.posts = postsWithUser;
              this.filteredPosts = postsWithUser;
            });
        });
    },
  },
  mounted() {
    this.getData();
  },
  // computed: {
  // Вижу 2 Реализации без кнопки и сразу искать при вводе какого-либо текста
  // filterArray - заменяем на итерируемый массив в V-for в post-list__item
  //     filterArray() {
  //     return this.filteredPosts = this.posts.filter((el) => {
  //       return el.user.name.includes(this.search);
  //     });
  //   },
  // }
};
</script>

<style lang="scss" scoped>
.container {
  margin: 0 auto;
  width: 100%;
  max-width: 1200px;
}
.search-block__wrap {
  margin-bottom: 15px;
}
.title-post {
  margin-bottom: 10px;
  color: #619fe8;
  text-align: left;
  @media (max-width: $MidlleWidth) {
    font-size: 18px;
  }
}
.content-post {
  margin-bottom: 20px;
  text-align: left;
  line-height: 22px;
  @media (max-width: $MidlleWidth) {
    font-size: 14px;
  }
}
.post-list {
  width: 100%;
  column-count: 3;
  @media (max-width: $TableWidth) {
    column-count: 2;
  }
  @media (max-width: $MobileWidth) {
    column-count: 1;
  }
  &__item {
    padding: 10px;
    height: max-content;
    page-break-inside: avoid;
    break-inside: avoid;
  }
}
.card-item {
  padding: 20px;
  background-color: white;
}
.author-post {
  color: #c9cdcf;
  text-align: left;
}
.search-img {
  width: 20px;
  height: 18px;
}
.search-button {
  padding: 5px 10px;
  background-color: white;
  outline: none;
  border: 1px solid gray;
  border-radius: 3px 0 0 3px;
  cursor: pointer;
}
.form-group {
  display: flex;
  justify-content: center;
  @media (max-width: $MidlleWidth) {
    padding: 0 10px;
    justify-content: start;
  }
}
.search-input {
  padding: 5px 10px;
  border: 1px solid gray;
  border-radius: 0 3px 3px 0;
  outline: none;
  color: gray;
  font-size: 16px;
  letter-spacing: 0.5px;
  @media (max-width: $MidlleWidth) {
    width: 100%;
  }
  &:focus {
    border: 1px solid #95c5fa;
    box-shadow: 0px 0px 3px 3px rgba(149, 197, 250, 1);
  }
}
</style>