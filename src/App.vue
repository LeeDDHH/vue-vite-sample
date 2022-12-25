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

<!-- <script lang="ts"> -->
<script setup lang="ts">
import { ref } from "vue";

const title = ref("My New Vue Title");
const message = ref("Welcom to Vue");
const textStatus = ref({ red: true });
const user = ref({
  firstName: "John",
  lastName: "Smith",
  isMember: true,
  isPremium: true,
});

const fullName = `${user.value.firstName} ${user.value.lastName}`;

const changeMemberStatus = () => {
  user.value.isMember = !user.value.isMember;
};
const changePremiumStatus = () => {
  user.value.isPremium = !user.value.isPremium;
};

// export default {
//   data() {
//     return {
//       title: "My New Vue Title",
//       message: "Welcom to Vue",
//       textStatus: {
//         red: true,
//       },
//       user: {
//         firstName: "John",
//         lastName: "Smith",
//         isMember: true,
//         isPremium: true,
//       },
//     };
//   },
//   computed: {
//     fullName() {
//       return this.user.firstName + " " + this.user.lastName;
//     },
//   },
//   methods: {
//     changeMemberStatus() {
//       this.user.isMember = !this.user.isMember;
//     },
//     changePremiumStatus() {
//       this.user.isPremium = !this.user.isPremium;
//     },
//   },
// };
</script>

<template>
  <h1 :title="message" :class="textStatus">{{ title }}</h1>
  <h2>{{ fullName }}さんのデータ</h2>
  <p>Name: {{ fullName }}</p>
  <p v-if="user.isMember">メンバーです</p>
  <p v-else>メンバーではありません</p>
  <p v-if="user.isPremium">プレミアムメンバーです</p>
  <p v-else>プレミアムメンバーではありません</p>
  <button @click="changeMemberStatus">メンバー状態切り替え</button>
  <button @click="changePremiumStatus">プレミアムメンバー状態切り替え</button>
</template>

<style scoped>
.red {
  color: red;
}
</style>
