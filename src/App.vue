<script setup>
import { ref, reactive, watchEffect, computed } from "vue";

const ShowTodo = ref(false);
const newTodo = ref("");
const increase = computed(() => {
  return newTodo.value.length;
});
const List_Item = reactive(JSON.parse(localStorage.getItem("Todo")) || []);

function AddTodo() {
  ShowTodo.value = !ShowTodo.value;
}

function Actived(e) {
  e.isActived = !e.isActived;
}

function SaveTodo() {
  let newObject = {
    id: List_Item.length + 1,
    label: newTodo.value,
    isActived: false,
  };
  List_Item.push(newObject);

  newTodo.value = "";
}

function DeleteTodo(id) {
  const GetID = JSON.parse(localStorage.getItem("Todo"));

  let jj = GetID.findIndex((element) => element.id === id);

  List_Item.splice(jj, 1);

  // localStorage.setItem("Todo", JSON.stringify(List_Item));
}

watchEffect(() => {
  localStorage.setItem("Todo", JSON.stringify(List_Item));
});
</script>

<script>
export default {
  name: "BootstrapCard",
};
</script>

<template>
  <div class="bg-color">
    <div class="container">
      <div class="header">
        <h1 class="h1">Todo List</h1>
        <div class="btns">
          <button @click="AddTodo" v-if="ShowTodo" class="btn cancale-btn">
            Cancale
          </button>
          <button @click="AddTodo" v-else class="btn btn-primy">
            Add Todo
          </button>
        </div>
      </div>
      <form action="" class="form forms" v-if="ShowTodo">
        <input
          v-model.trim="newTodo"
          type="text"
          maxlength="20"
          name=""
          id="input"
          class="input-group input"
          placeholder="Add a Todo"
        />
        <button
          :disabled="!newTodo.length"
          @click.prevent="SaveTodo"
          class="btn btn1"
        >
          Save
        </button>
      </form>
      <h6 v-if="ShowTodo">{{ increase }}/20</h6>

      <ul class="ul" v-if="List_Item.length">
        <li
          class="list li"
          @click="Actived(item)"
          :class="{ isACTIVE: item.isActived }"
          v-for="item in List_Item"
          :key="item.id"
        >
          {{ item.label }}
          <button
            v-if="item.isActived"
            class="btn delete"
            @click="DeleteTodo(item.id)"
          >
            Remove
          </button>
        </li>
      </ul>
      <h2 v-else class="h2" id="h2">No Yet!!!!!!!!</h2>
    </div>
  </div>
</template>

<style scoped>
#h2 {
  text-align: start;
  padding: 20px;
}
h6 {
  margin-left: 20px;
  position: relative;
  top: -20px;
}

.delete {
  text-decoration-line: none;
  background-color: rgba(255, 0, 0, 0.566);
  height: 40px;
  margin: 0px;
  color: white;
  width: 150px;
  z-index: 5000;
}
ul {
  width: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  margin-bottom: 2rem;
}

.li {
  list-style: none;
  width: 100%;
  height: 50px;
  margin: 10px;
  background-color: rgba(216, 216, 216, 0.354);
  border-radius: 10px;
  font-size: 20px;
  text-align: start;
  padding: 10px;
  transition: ease 0.2s;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.li:hover {
  background-color: transparent;
  color: rgba(0, 0, 0, 0.5);
}

form {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 20px;
}
#input {
  width: 80%;
  height: 50px;
  border: none;
  padding: 20px;
  border-radius: 7px;
}

.btn1 {
  width: 150px;
  margin: 20px;
  height: 50px;
  background-color: black;
  color: white;
}

.bg-color {
  background-color: white;
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
}

.isACTIVE {
  text-decoration-line: line-through;
  color: rgba(0, 0, 0, 0.5);
  background-color: transparent;
}

.container {
  background-color: rgba(0, 0, 0, 0.249);
  width: 100%;
  /* height: 500px; */
  margin-top: 100px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.34);
  border-radius: 15px;
}
.header {
  display: flex;
  justify-content: space-between;
}

.h1 {
  text-align: start;
  padding: 20px;
}

.cancale-btn {
  width: 150px;
  height: 50px;
  background-color: rgba(0, 0, 0, 0.3);
  color: white;
  margin-top: 20px;
}
.btn-primy {
  width: 150px;
  height: 50px;
  background-color: rgba(0, 0, 255, 0.347);
  margin-top: 20px;
}

@media screen and (max-width: 485px) {
  .container {
    width: 90%;
  }
}
@media screen and (max-width: 385px) {
  .h1 {
    font-size: 23px;
  }
  .cancale-btn {
    width: 100px;
    height: 50px;
  }
  .btn-primy {
    width: 100px;
    height: 50px;
  }
  .btn1 {
    width: 100px;
    height: 40px;
    font-size: 10px;
  }

  #input {
    width: 80%;
    height: 40px;
  }
  .li {
    font-size: 12px;
  }
  .delete {
    height: 40px;

    width: 80px;
  }
}

@media screen and (max-width: 305px) {
  .h1 {
    font-size: 17px;
  }
  .cancale-btn {
    width: 80px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 12px;
  }
  .btn-primy {
    width: 80px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 12px;
  }

  .btn1 {
    width: 70px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 12px;
  }
  input.input {
    width: 80%;
    height: 30px;
  }

  .li {
    height: 40px;
    width: 110%;
    font-size: 12px;
  }
  ul {
    margin-left: -10px;
  }
  .delete {
    height: 30px;
    width: 60px;
    font-size: 10px;
  }
}
</style>
