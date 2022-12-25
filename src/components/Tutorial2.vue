<!-- <script lang="ts">
export default {
  data() {
    return {
      title: "My New Vue Title",
      message: "Welcom to Vue",
      textStatus: {
        red: true,
      },
      error: {
        firstName: false,
        lastName: false,
      },
      input: {
        firstName: "",
        lastName: "",
        isMember: false,
        isPremium: false,
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
    validateStringInput(inputElem: "firstName" | "lastName") {
      console.log(inputElem);
      if (!this.input[inputElem].length) return (this.error[inputElem] = true);
      this.error[inputElem] = false;
    },
    addUser() {
      if (!this.input.firstName || !this.input.lastName) return;
      this.users.push(this.input);
      this.input = {
        firstName: "",
        lastName: "",
        isMember: false,
        isPremium: false,
      };
      this.error = {
        firstName: false,
        lastName: false,
      };
    },
  },
  watch: {
    "input.firstName"() {
      this.validateStringInput("firstName");
    },
    "input.lastName"() {
      this.validateStringInput("lastName");
    },
  },
}; -->

<script setup lang="ts">
import { ref, watch } from "vue";

const title = ref("My New Vue Title");
const message = ref("Welcom to Vue");
const textStatus = ref({ red: true });
const users = ref([
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
]);
const input = ref({
  firstName: "",
  lastName: "",
  isMember: false,
  isPremium: false,
});
const error = ref({
  firstName: false,
  lastName: false,
});

watch(
  () => input.value.firstName,
  (cur: string, prev: string) => {
    validateStringInput("firstName");
  }
);

watch(
  () => input.value.lastName,
  (cur: string, prev: string) => {
    validateStringInput("lastName");
  }
);

const fullName = (firstName: string, lastName: string) => `${firstName} ${lastName}`;

const changeMemberStatus = (index: number) => {
  users.value[index].isMember = !users.value[index].isMember;
};
const changePremiumStatus = (index: number) => {
  users.value[index].isPremium = !users.value[index].isPremium;
};
const addUser = () => {
  if (!input.value.firstName || !input.value.lastName) return;
  users.value.push(input.value);
  input.value = {
    firstName: "",
    lastName: "",
    isMember: false,
    isPremium: false,
  };
  error.value = {
    firstName: false,
    lastName: false,
  };
};

const validateStringInput = (inputElem: "firstName" | "lastName") => {
  if (typeof input.value[inputElem] === "string" && !(input.value[inputElem] as string).length)
    return (error.value[inputElem] = true);
  error.value[inputElem] = false;
};
</script>

<template>
  <h1 :title="message" :class="textStatus">{{ title }}</h1>
  <div>
    <label for="firstName">FirstName: </label>
    <input
      v-model="input.firstName"
      @blur="validateStringInput('firstName')"
      type="text"
      id="firstName"
      placeholder="Enter the FirstName"
    />
    <p v-if="error.firstName" :class="textStatus">require first name.</p>
  </div>
  <div>
    <label for="lastName">LastName: </label>
    <input
      v-model="input.lastName"
      @blur="validateStringInput('lastName')"
      type="text"
      id="lastName"
      placeholder="Enter the LastName"
    />
    <p v-if="error.lastName" :class="textStatus">require last name.</p>
  </div>
  <div>
    <label for="isMember">isMember: </label>
    <input v-model="input.isMember" type="checkbox" id="isMember" />
  </div>
  <div>
    <label for="isPremium">isPremium: </label>
    <input v-model="input.isPremium" type="checkbox" id="isPremium" />
  </div>
  <button @click="addUser">ユーザー追加</button>
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
