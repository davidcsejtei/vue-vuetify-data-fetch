<template>
  <v-container class="grey lighten-5">
    <v-row no-gutters justify="center">
      <v-col v-if="loading" align="center">
        <v-progress-circular
          indeterminate
          color="primary"
        ></v-progress-circular>
      </v-col>
      <v-col v-if="!loading">
        <v-card class="pa-2" outlined tile>
          <v-card class="mx-auto" max-width="300" tile>
            <v-subheader>TODOs</v-subheader>
            <v-list dense>
              <v-list-item-group v-model="todos" color="primary">
                <v-list-item v-for="(todo, i) in todos" :key="i">
                  <v-list-item-content>
                    <v-list-item-title v-text="todo.title"></v-list-item-title>
                    <v-list-item-subtitle
                      v-text="!!todo.completed ? 'completed' : 'not completed'"
                    ></v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
              </v-list-item-group>
            </v-list>
          </v-card>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    loading: false,
    todos: [],
  }),
  mounted: async function () {
    this.loading = true;
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    this.todos = await response.json();
    this.loading = false;
  },
};
</script>
