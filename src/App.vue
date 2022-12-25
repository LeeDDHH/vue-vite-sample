<!-- <script setup lang="ts">
// import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style> -->

<script lang="ts">
export default {
  data() {
    return {
      title: "My New Vue Title",
      message: "Welcom to Vue",
      textStatus: {
        red: true,
      },
      users: [
        {
          firstName: "John",
          lastName: "Smith",
          isMember: true,
          isPremium: true,
        },
        {
          firstName: "Taro",
          lastName: "Shinjuku",
          isMember: false,
          isPremium: true,
        },
        {
          firstName: "Hanako",
          lastName: "Shibuya",
          isMember: true,
          isPremium: false,
        },
      ],
    };
  },
  computed: {
    fullName: () => (firstName: string, lastName: string) => {
      return firstName + " " + lastName;
    },
  },
  methods: {
    changeMemberStatus(index: number) {
      return (this.users[index].isMember = !this.users[index].isMember);
    },
    changePremiumStatus(index: number) {
      return (this.users[index].isPremium = !this.users[index].isPremium);
    },
  },
};

// <script setup lang="ts">
// import { ref } from "vue";

// const title = ref("My New Vue Title");
// const message = ref("Welcom to Vue");
// const textStatus = ref({ red: true });
// const user = ref({
//   firstName: "John",
//   lastName: "Smith",
//   isMember: true,
//   isPremium: true,
// });

// const fullName = `${user.value.firstName} ${user.value.lastName}`;

// const changeMemberStatus = () => {
//   user.value.isMember = !user.value.isMember;
// };
// const changePremiumStatus = () => {
//   user.value.isPremium = !user.value.isPremium;
// };
</script>

<template>
  <h1 :title="message" :class="textStatus">{{ title }}</h1>
  <h2>ユーザーのデータ</h2>
  <div v-for="(user, index) in users" :key="index">
    <p>Name: {{ fullName(user.firstName, user.lastName) }}</p>
    <p v-if="user.isMember">メンバーです</p>
    <p v-else>メンバーではありません</p>
    <p v-if="user.isPremium">プレミアムメンバーです</p>
    <p v-else>プレミアムメンバーではありません</p>
    <button @click="changeMemberStatus(index)">メンバー状態切り替え</button>
    <button @click="changePremiumStatus(index)">プレミアムメンバー状態切り替え</button>
  </div>
</template>

<style scoped>
.red {
  color: red;
}
</style>
