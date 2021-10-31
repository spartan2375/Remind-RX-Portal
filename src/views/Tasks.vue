<template>
  <div class="home pa-3">
    <!-- <v-text-field
      class="hidden-md-and-down"
      label="New Task"
      append-outer-icon="mdi-plus"
      clearable
      v-model="newTaskTitle"
      @click:append-outer="addTask"
      @keyup.enter="addTask"
    ></v-text-field> -->

    <!-- <task-list
      :tasks="tasks"
      :is-active="false"
      subtitle="Active Tasks"
      v-on:edit-task="editTask"
    >
    </task-list>
    <task-list
      :tasks="tasks"
      :is-active="true"
      subtitle="Completed Tasks"
      v-on:delete-task="deleteTask"
    >
    </task-list> -->

    <!-- <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          class="included hidden-lg-and-up"
          absolute
          fab
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
          right
        >
          <v-icon class="included">mdi-plus</v-icon>
        </v-btn>
      </template>
      <v-card
        v-click-outside="{
          handler: clickMe,
          include: include,
        }"
      >
        <v-card-title>
          <span class="headline">Add Task</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  label="Task Title*"
                  v-model="newTaskTitle"
                  autofocus
                  required
                  @keyup.enter="addTask"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Close
          </v-btn>
          <v-btn color="blue darken-1" text @click="addTask"> Add Task </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog
      ref="dialog"
      v-model="showPicker"
      :return-value.sync="newDate"
      width="290px"
    >
      <v-date-picker v-model="newDate" scrollable>
        <v-spacer></v-spacer>
        <v-btn text color="primary" @click="showPicker = false"> Cancel </v-btn>
        <v-btn text color="primary" @click="updateTask"> OK </v-btn>
      </v-date-picker>
    </v-dialog> -->
    <v-container fluid class="ma-0">
      <v-row>
        <v-col cols="5">
          <v-list>
            <v-list-item-group v-model="patientSelected" color="primary">
              <v-list-item
                v-for="patient in patients"
                :key="patient.id"
                class="my-2"
              >
                <v-list-item-avatar size="50">
                  <img v-bind:src="patient.name + '.jpg'" />
                </v-list-item-avatar>
                <v-list-item-content>
                  <v-list-item-title> {{ patient.name }} </v-list-item-title>
                  <v-row dense>
                    <v-col>
                      <v-chip
                        :class="[
                          patient.status ? 'green' : 'red',
                          patient.status ? 'green--text' : 'red--text',
                        ]"
                        outlined
                      >
                        Medication Status:
                        <v-icon v-if="patient.status"> mdi-cards-heart</v-icon>
                        <v-icon v-else> mdi-heart-broken</v-icon>
                      </v-chip>
                    </v-col>
                    <v-col>
                      <v-chip
                        :class="[
                          patient.contact ? 'green' : 'red',
                          patient.contact ? 'green--text' : 'red--text',
                        ]"
                        outlined
                      >
                        Contact Availability:
                        <v-icon v-if="patient.contact">mdi-check</v-icon>
                        <v-icon v-else>mdi-close</v-icon>
                      </v-chip>
                    </v-col>

                    <v-col>
                      <v-chip outlined color="primary">
                        Last Visit: {{ patient.lastVisit }}
                      </v-chip>
                    </v-col>
                    <v-spacer></v-spacer>
                    <v-btn icon>
                      <v-icon color="primary">mdi-cog</v-icon>
                    </v-btn>
                  </v-row>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-col>

        <!-- #################
      LEFT SIDE
      ################# -->
        <!-- <v-spacer></v-spacer> -->
        <v-col cols="5">
          <v-card>
            <v-card-title>
              <v-avatar size="75" class="mr-2">
                <img :src="currentPatient[0].name + '.jpg'" />
              </v-avatar>
              <v-row>
                <v-col>
                  <h6>
                    Last seen in office: {{ currentPatient[0].lastVisit }}
                  </h6>
                  <h5>{{ currentPatient[0].name }}</h5>
                  <h6>70 years | Male</h6>
                </v-col>

                <v-btn icon large color="primary">
                  <v-icon>
                    mdi-information
                  </v-icon>
                </v-btn>
                <v-btn icon large color="red">
                  <v-icon>
                    mdi-close
                  </v-icon>
                </v-btn>
              </v-row>
            </v-card-title>
            <v-divider></v-divider>
            <v-card-text>
              <v-row>
                <v-col>
                  <h4>asdf</h4>
                </v-col>
                <v-col>
                  <h4>test</h4>
                </v-col>
                <v-col>
                  <h4>again</h4>
                </v-col>
                <v-col>
                  <h4>and again</h4>
                </v-col>
              </v-row>
              <v-row>
                asdf
              </v-row>
            </v-card-text>
          </v-card>

          <v-list>
            <!-- DO STUFF HERE FOR LISTING MED TIMES -->
          </v-list>

          <img src="graph.png" />
          <img src="example.png" />
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi
            necessitatibus quis totam ducimus assumenda cupiditate consequuntur.
            Aspernatur eaque sunt, molestias possimus recusandae cumque. Fugiat
            dolore minus natus labore in pariatur.
          </p>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import TaskList from "@/components/Task-List.vue";

export default {
  components: { TaskList },
  name: "Home",
  data() {
    return {
      dialog: false,
      showPicker: false,
      newTaskTitle: "",
      newDate: "",
      editingTaskId: 0,
      patientSelected: 1,
      patients: [
        {
          name: "Bob",
          id: 0,
          status: true,
          contact: true,
          lastVisit: "2021-11-05",
        },
        {
          name: "Joe",
          id: 1,
          status: true,
          contact: false,
          lastVisit: "2021-11-01",
        },
        {
          name: "Raph",
          id: 2,
          status: false,
          contact: true,
          lastVisit: "2021-10-15",
        },
      ],

      tasks: [
        {
          id: 1,
          title: "Eat soup",
          finished: false,
          due: new Date().toISOString().substr(0, 10),
        },

        {
          id: 2,
          title: "Hit the vape",
          finished: false,
          due: new Date().toISOString().substr(0, 10),
        },

        {
          id: 3,
          title: "Get back to work",
          finished: false,
          due: new Date().toISOString().substr(0, 10),
        },
      ],
    };
  },

  computed: {
    currentPatient() {
      return this.patients.filter((patient) => {
        return patient.id == this.patientSelected;
      });
    },
  },

  methods: {
    sortByDue: function() {
      this.tasks.sort((a, b) => {
        if (a.due > b.due) {
          return 1;
        } else {
          return -1;
        }
      });
    },

    addTask() {
      this.dialog = false;
      if (this.newTaskTitle != "") {
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          finished: false,
          due: new Date().toISOString().substr(0, 10),
        };
        this.tasks.push(newTask);
        this.newTaskTitle = "";
      }
    },

    deleteTask(id) {
      console.log("id: ", id);
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },

    editTask(id) {
      this.editingTaskId = id;
      console.log("id: ", id);
      this.showPicker = true;
    },

    updateTask() {
      let currentTask = this.tasks.filter(
        (task) => task.id === this.editingTaskId
      );
      this.tasks = this.tasks.filter((task) => task.id !== this.editingTaskId);
      currentTask[0].due = this.newDate;
      this.tasks.push(currentTask[0]);
      this.showPicker = false;
      this.sortByDue();
    },

    clickMe() {
      this.dialog = false;
      this.newTaskTitle = "";
    },

    include() {
      return [document.querySelector(".included")];
    },
  },
};
</script>
