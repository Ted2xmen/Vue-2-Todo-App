<template>
  <div class="pa-4">
    <h1>Todo Page</h1>
<v-container>

  
    <v-text-field
      v-model="newTodo"
      class="pa-3"
      @click:append="addTodo"
      @keyup.enter="addTodo"
      outlined
      clearable
      label="Add Task"
      append-icon="mdi-plus"
    ></v-text-field>




</v-container>





    <v-list class="pt-0" flat two-line>
      <div class="div" v-for="task in tasks" :key="task.id">
        <v-list-item

          @click="taskDone(task.id)"
          :class="{ white: !task.completed }"> <!-- green: task.completed, -->
         

          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.completed"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.completed }">
              
                {{ task.title }}
                 

              </v-list-item-title>

              <v-list-item-subtitle>

                {{ task.date }}

                <v-chip
                  class="ma-2"
                  color="green"
                  label
                  text-color="white"
                  small>
                
                  <v-icon left>
                    mdi-label
                  </v-icon>

                  {{ task.tag }} dd 

                </v-chip>

       
              </v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn @click.stop="deleteTask(task.id)" icon>
                <v-icon color="red">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>

          </template>
        </v-list-item>

        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
    import moment from 'moment';
    
    let date = moment().format('Do MMMM YYYY, h:mm');
export default {
  name: "Todo",


  data() {
    return {
     
      newTodo: "",
      tasks: [
        { id: Date.now()+1, tag: "Router", date: date, title: "Learn Vue Router", completed: false },
        { id: Date.now()+2, tag: "Vue", date: date, title: "Complete Vue Fundamentals", completed: false },
        { id: Date.now()+3, tag: "Vuex", date: date,  title: "Learn Vuex", completed: false },
      ],
    };
  },
  methods: {
    addTodo() {
      let newTask = {
        id: Date.now(),
        title: this.newTodo,
        date: date,
        tag: "",
        category: ["Personal", "Work"],
        completed: false,
      };
      this.tasks.push(newTask);
      this.newTodo = "";
    },

    taskDone(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.completed = !task.completed;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
 
}
}
</script>
