<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <el-container>
      <el-header>
        cabeçalho
        <el-divider />
      </el-header>
      <el-main>
        <div v-for="item in items" :key="item.title">
          <el-row type="flex" justify="left">
            <el-checkbox
              v-model="item.status"
              @mouseover.native="hoverTask = true"
              @mouseleave.native="hoverTask = false"
            >
              {{ item.title }}
            </el-checkbox>

            <span v-show="hoverTask">
              aparece
            </span>
          </el-row>
        </div>
      </el-main>
      <el-footer>
        <el-divider />
        <el-row type="flex" justify="center" :gutter="12">
          <el-col :md="23" :xs="20">
            <el-input v-model="titleInput" @keyup.enter.native="addTask()" />
          </el-col>
          <el-col :md="1" :xs="1">
            <!-- <el-button
              @click="addTask()"
              :disabled="titleInput.length === 0"
              round
              type="primary"
            >
              Adicionar
            </el-button> -->
            <el-button
              icon="el-icon-plus"
              @click="addTask()"
              :disabled="titleInput.length === 0"
              circle
            ></el-button>
          </el-col>
        </el-row>
        <!-- <el-button @click="visible = true">Button</el-button> -->
      </el-footer>
    </el-container>
  </div>
</template>

<script>
  // import HelloWorld from "./components/HelloWorld.vue";

  export default {
    name: "App",

    data: function() {
      return {
        visible: false,
        items: [
          {
            title: "Foo",
            status: false,
          },
        ],
        // exemplo de obj task api google (https://developers.google.com/tasks/reference/rest/v1/tasks#Task):
        objTask: {
          kind: "tasks#task",
          id: "string",
          etag: "string",
          title: "string",
          // Last modification time of the task (as a RFC 3339 timestamp).
          updated: "string",
          selfLink: "string",
          // Parent task identifier. This field is omitted if it is a top-level task.
          // This field is read-only.
          // Use the "move" method to move the task under a different parent or to the top level.
          parent: "string",
          position: "string",
          // descripton
          notes: "string",
          // This is either "needsAction" or "completed".
          status: "string",
          // data da tarefa (ready only)
          due: "string",
          // data que a tarefa foi feita
          completed: "string",
          // se foi deletada
          deleted: "boolean",
          // Flag indicating whether the task is hidden. This is the case if the task had been marked completed when the task list was last cleared. The default is False. This field is read-only.
          hidden: "boolean",
          links: [
            {
              type: "string",
              description: "string",
              link: "string",
            },
          ],
        },
        checked: false,
        titleInput: "",
        hoverTask: false,
      };
    },

    methods: {
      addTask() {
        if (this.titleInput.length === 0) {
          return;
        }
        this.items.push({ title: this.titleInput, status: false });
        this.titleInput = "";
      },
    },
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
