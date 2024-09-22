<template>
  <div class="wrapper">
    <div class="filter-panel">
      <button @click="filterByGender('Male')">
        Male
      </button>
      <button @click="filterByGender('Female')">
        Female
      </button>
      <button @click="filterByGender(null)">
        All
      </button>
    </div>
    <div class="user-cards">
      <div v-if="filteredUsers.length === 0">
        Дані відсутні
      </div>
      <div
        v-for="user in filteredUsers"
        :key="user.firstName"
        class="user-card"
        :class="ageColorClass(user.age)"
      >
        <div class="user-card-header">
          <img
            class="user-card-banner"
            :src="bannerSrc"
          >
          <img
            class="user-card-photo"
            :src="user.photoSrc"
          >
        </div>
        <div class="user-card-content">
          <div class="user-card-content-credentials">
            <span class="user-card-content-first-name">{{
              user.firstName
            }}</span>
            <span class="user-card-content-last-name">{{ user.lastName }}</span>
          </div>
          <div class="user-card-content-additional-info">
            <div
              v-if="user.age > 18"
              class="user-card-content-field"
            >
              <div class="user-card-content-field-value">
                {{ user.age }}
              </div>
              <div class="user-card-content-field-label">
                Вік
              </div>
            </div>

            <div class="user-card-content-field">
              <div class="user-card-content-field-value">
                {{ user.gender }}
              </div>
              <div class="user-card-content-field-label">
                Стать
              </div>
            </div>
            <div class="user-card-content-field">
              <div class="user-card-content-field-value">
                {{ user.position }}
              </div>
              <div class="user-card-content-field-label">
                Позиція
              </div>
            </div>
          </div>
          <div class="user-card-content-hobbies">
            <div class="user-card-content-hobbies-header">
              Хобі
            </div>
            <div
              v-for="hobby in user.hobbies"
              :key="hobby"
              class="user-card-content-hobbies-hobby"
            >
              {{ "< " + hobby + " >" }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, computed } from "vue";

const users = ref([
  {
    firstName: "Tom",
    lastName: "Ford",
    age: 22,
    gender: "Male",
    position: "Programmer",
    photoSrc: "images/face.jpg",
    hobbies: ["reading", "skiing", "films"],
  },
  {
    firstName: "Alice",
    lastName: "Blue",
    age: 35,
    gender: "Female",
    position: "QA",
    photoSrc: "images/face.jpg",
    hobbies: ["drawing", "traveling", "reading"],
  },
  {
    firstName: "Vicy",
    lastName: "Lyp",
    age: 25,
    gender: "Female",
    position: "Doctor",
    photoSrc: "images/face.jpg",
    hobbies: ["drawing", "traveling", "reading"],
  },
  {
    firstName: "John",
    lastName: "Dev",
    age: 45,
    gender: "Male",
    position: "Business analyst",
    photoSrc: "images/face.jpg",
    hobbies: ["reading", "skiing", "films"],
  },
  {
    firstName: "Luie",
    lastName: "Frau",
    age: 65,
    gender: "Female",
    position: "waitress",
    photoSrc: "images/face.jpg",
    hobbies: ["drawing", "traveling", "reading"],
  },
  {
    firstName: "John",
    lastName: "Doe",
    age: 32,
    gender: "Male",
    position: "Project Manager",
    photoSrc: "images/face.jpg",
    hobbies: ["reading", "skiing", "films"],
  },
  {
    firstName: "Ann",
    lastName: "Bev",
    age: 19,
    gender: "Female",
    position: "Product Manager",
    photoSrc: "images/face.jpg",
    hobbies: ["drawing", "traveling", "reading"],
  },
  {
    firstName: "little",
    lastName: "little",
    age: 4,
    gender: "Female",
    position: "Product Manager",
    photoSrc: "images/face.jpg",
    hobbies: ["drawing", "traveling", "reading"],
  },
]);

const bannerSrc = ref("images/background.jpg");
const selectedGender = ref(null);

const filteredUsers = computed(() => {
  if (!selectedGender.value) return users.value;
  return users.value.filter((user) => user.gender === selectedGender.value);
});

const ageColorClass = (age) => {
  if (age >= 60) return "age-red";
  if (age >= 30) return "age-yellow";
  if (age < 30) return "age-green";
  return "";
};

const filterByGender = (gender) => {
  selectedGender.value = gender;
};
</script>

<style scoped>
.wrapper {
  width: 100%;
  min-height: 100vh;
  background-color: #c0c0c0;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  gap: 1em;
}
.filter-panel {
  display: flex;
  gap: 1em;
  margin-top: 1em;
  justify-content: center;
  width: 100%;
}

.filter-panel button {
  outline: none;
  border: none;
  width: 100px;
  height: 40px;
  border-radius: 10%/10px;
  background-color: #333333;
  color: #fff;
}

.user-cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2em;
  height: 100%;
}
.user-card {
  width: 450px;
  height: 700px;
  border-radius: 5%/18px;
  background-color: #fff;
  padding: 1em;
}
.user-card-header {
  position: relative;
  object-fit: cover;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.user-card-banner {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 5%/18px;
}
.user-card-photo {
  position: relative;
  z-index: 1;
  width: 152px;
  height: 152px;
  transform: translateY(100px);
  background-color: #333;
  border: 3px solid white;
  border-radius: 50%;
}
.user-card-content {
  margin-top: 100px;
  overflow-y: scroll;
  height: 400px;
}

.user-card-content-first-name,
.user-card-content-last-name {
  font-size: 2em;
}

.user-card-content-credentials {
  display: flex;
  justify-content: center;
  gap: 1em;
}
.user-card-content-field {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.user-card-content-additional-info {
  margin-top: 1em;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}
.user-card-content::-webkit-scrollbar {
  width: 2px;
}

.user-card-content-field {
  width: 200px;
  height: 150px;
  background-color: #ffe8e8;
  border-radius: 5%/10px;
  flex-grow: 1;
}
.user-card-content-field-label {
  margin-top: 1em;
  font-size: 1em;
  color: #33333389;
}
.user-card-content-field-value {
  font-size: 1.5em;
  color: #333333;
}
.user-card-content-hobbies-header {
  text-align: center;
  font-size: 1.3em;
  color: #333333;
  margin: 10px 0;
}
.user-card-content-hobbies-hobby {
  text-align: center;
  font-size: 1.5em;
  color: #333333;
  margin-top: 20px;
}
.age-green {
  background-color: rgb(227, 255, 227);
}

.age-yellow {
  background-color: #fff999;
}

.age-red {
  background-color: #ff6666;
}
</style>
