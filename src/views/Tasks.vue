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
                      <v-chip outlined color="grey">
                        Last Visit: N/A
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
          <v-divider></v-divider>
          <v-img src="graph.png" />
        </v-col>

        <!-- #################
      LEFT SIDE
      ################# -->
        <!-- <v-spacer></v-spacer> -->
        <v-col cols="7">
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
                  <h6>{{ currentPatient[0].age }} | Male</h6>
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
                  <v-icon>mdi-cards-heart</v-icon>
                  Blood Pressure
                  <h2 class="green--text">
                    {{ currentPatient[0].bloodPressure }}
                  </h2>
                  <h5>last checked: 7 days ago</h5>
                </v-col>
                <v-divider vertical></v-divider>
                <v-col>
                  <v-icon>mdi-heart-pulse</v-icon>
                  Heart Rate
                  <h2 class="red--text">{{ currentPatient[0].heartRate }}</h2>
                  <h5>last checked: 1 hour ago</h5>
                </v-col>
                <v-divider vertical></v-divider>
                <v-col>
                  <v-icon>mdi-scale</v-icon>
                  Weight
                  <h2>{{ currentPatient[0].weight }} lbs</h2>
                  <h5>last checked: 7 days ago</h5>
                </v-col>
                <v-divider vertical></v-divider>
                <v-col>
                  <v-icon>mdi-water-alert</v-icon>
                  Blood Glucose
                  <h2 class="yellow--text">
                    {{ currentPatient[0].bloodGlucose }}
                  </h2>
                  <h5>last checked: 7 days ago</h5>
                </v-col>
              </v-row>
              <v-row>
                Notes {{ currentPatient[0].lastVisit }}:
                {{ currentPatient[0].addNotes }}
              </v-row>
            </v-card-text>
          </v-card>
          <v-divider class="mt-7 mb-3"></v-divider>

          <v-card class="my-2">
            <v-card-title>
              Medication Times
            </v-card-title>
            <v-list>
              <!-- DO STUFF HERE FOR LISTING MED TIMES -->
              <v-list-item
                v-for="(med, i) in currentPatient[0].medDetes"
                :key="i"
              >
                <v-row>
                  <v-list-item-content>
                    <v-col cols="3">
                      <v-text-field
                        outlined
                        label="Medication name"
                        v-model="med.name"
                        readonly
                      >
                      </v-text-field>
                    </v-col>
                    <v-divider vertical></v-divider>
                    <v-col cols="2">
                      <v-text-field
                        outlined
                        label="Medication time"
                        v-model="med.time"
                        readonly
                      >
                      </v-text-field>
                    </v-col>
                    <v-divider vertical></v-divider>
                    <v-col cols="2">
                      <v-text-field
                        outlined
                        label="Dosage"
                        v-model="med.dose"
                        readonly
                      >
                      </v-text-field>
                    </v-col>
                    <v-divider vertical></v-divider>
                    <v-col cols="5">
                      <v-text-field
                        outlined
                        label="Notes"
                        clearable
                        v-model="med.notes"
                      >
                      </v-text-field>
                    </v-col>
                    <!-- <v-list-item-title>
                    
                  </v-list-item-title> -->
                  </v-list-item-content>
                </v-row>
              </v-list-item>
            </v-list>
          </v-card>
          <!-- #########################
          STUFF ADDED HERE 
          Heart Rate graph from Vuetify.js docs-->

          <!-- <v-card class="mx-auto mt-5" color="grey lighten-4" max-width="600">
            <v-card-title>
              <v-icon
                :color="checking ? 'red lighten-2' : 'indigo'"
                class="mr-12"
                size="64"
                @click="takePulse"
              >
                mdi-heart-pulse
              </v-icon>
              <v-row align="start">
                <div class="text-caption grey--text text-uppercase">
                  Heart rate
                </div>
                <div>
                  <span
                    class="text-h3 font-weight-black"
                    v-text="avg || '—'"
                  ></span>
                  <strong v-if="avg">BPM</strong>
                </div>
              </v-row>

              <v-spacer></v-spacer>

              <v-btn icon class="align-self-start" size="28">
                <v-icon>mdi-arrow-right-thick</v-icon>
              </v-btn>
            </v-card-title>

            <v-sheet color="transparent">
              <v-sparkline
                :key="String(avg)"
                :smooth="16"
                :gradient="['#f72047', '#ffd200', '#1feaea']"
                :line-width="3"
                :value="heartbeats"
                auto-draw
                stroke-linecap="round"
              ></v-sparkline>
            </v-sheet>
          </v-card> -->
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import TaskList from "@/components/Task-List.vue";

const exhale = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

export default {
  components: { TaskList },
  name: "Home",
  data() {
    return {
      checking: false,
      heartbeats: [],

      // dialog: false,
      // showPicker: false,
      // newTaskTitle: "",
      // newDate: "",
      // editingTaskId: 0,
      patientSelected: 1,
      patients: [
        {
          name: "Bob",
          id: 0,
          status: true,
          contact: true,
          lastVisit: "2021-11-05",
          age: 70,
          bloodPressure: "120/80 mm Hg -10/5",
          heartRate: "93 bpm + 12",
          weight: 180,
          bloodGlucose: "160 mg/dL +5",
          addNotes:
            "Seems that the blood pressure has been dropping over the months",
          medDetes: [
            {
              time: "8:00am",
              name: "Pillpack 1",
              dose: "500mg",
              notes: "Take two tablets orally",
            },
            {
              time: "5:00pm",
              name: "FloLipid",
              dose: "20mg",
              notes: " Shake well, take in evening on empty stomach.",
            },
            {
              time: "6:00pm",
              name: "Norvasc",
              dose: "5mg",
              notes: "Review doseage at next appointment",
            },
          ],
        },
        {
          name: "Joe",
          id: 1,
          status: true,
          contact: false,
          lastVisit: "2021-11-01",
          age: 76,
          bloodPressure: "115/79 mm Hg -2/0",
          heartRate: "82 bpm + 2",
          weight: 163,
          bloodGlucose: "145 mg/dL +3",
          addNotes: "Watch Heart Rate over the course of the next few months",
          medDetes: [
            {
              time: "8:00am",
              name: "Pillpack 1",
              dose: "N/A",
              notes: "Take on empty stomach before breakfast",
            },
            {
              time: "12:00pm",
              name: "Pillpack 2",
              dose: "N/A",
              notes: "Take with water",
            },
            {
              time: "5:00pm",
              name: "Pillpack 3",
              dose: "N/A",
              notes: "Shake well, take in evening on empty stomach",
            },
          ],
        },
        {
          name: "Raph",
          id: 2,
          status: false,
          contact: true,
          lastVisit: "2021-10-15",
          age: 79,
          bloodPressure: "130/87 mm Hg -4/2",
          heartRate: "97 bpm + 7",
          weight: 160,
          bloodGlucose: "173 mg/dL +8",
          addNotes: "This is an example note",
          medDetes: [
            {
              time: "12:00pm",
              name: "Riomet",
              dose: "850mg",
              notes: "Take with meals",
            },
            {
              time: "12:00pm",
              name: "Zegerid",
              dose: "40mg",
              notes: "n/a",
            },
            {
              time: "6:00pm",
              name: "Norvasc",
              dose: "10mg",
              notes: "Review dosage at next appointment",
            },
          ],
        },
      ],

      // tasks: [
      //   {
      //     id: 1,
      //     title: "Eat soup",
      //     finished: false,
      //     due: new Date().toISOString().substr(0, 10),
      //   },

      //   {
      //     id: 2,
      //     title: "Hit the vape",
      //     finished: false,
      //     due: new Date().toISOString().substr(0, 10),
      //   },

      //   {
      //     id: 3,
      //     title: "Get back to work",
      //     finished: false,
      //     due: new Date().toISOString().substr(0, 10),
      //   },
      // ],
    };
  },

  computed: {
    avg() {
      const sum = this.heartbeats.reduce((acc, cur) => acc + cur, 0);
      const length = this.heartbeats.length;

      if (!sum && !length) return 0;

      return Math.ceil(sum / length);
    },

    currentPatient() {
      return this.patients.filter((patient) => {
        return patient.id == this.patientSelected;
      });
    },
  },

  created() {
    this.takePulse(false);
  },

  methods: {
    heartbeat() {
      return Math.ceil(Math.random() * (120 - 80) + 80);
    },
    async takePulse(inhale = true) {
      this.checking = true;

      inhale && (await exhale(1000));

      this.heartbeats = Array.from({ length: 20 }, this.heartbeat);

      this.checking = false;
    },

    sortByDue: function() {
      this.tasks.sort((a, b) => {
        if (a.due > b.due) {
          return 1;
        } else {
          return -1;
        }
      });
    },

    // addTask() {
    //   this.dialog = false;
    //   if (this.newTaskTitle != "") {
    //     let newTask = {
    //       id: Date.now(),
    //       title: this.newTaskTitle,
    //       finished: false,
    //       due: new Date().toISOString().substr(0, 10),
    //     };
    //     this.tasks.push(newTask);
    //     this.newTaskTitle = "";
    //   }
    // },

    // deleteTask(id) {
    //   console.log("id: ", id);
    //   this.tasks = this.tasks.filter((task) => task.id !== id);
    // },

    // editTask(id) {
    //   this.editingTaskId = id;
    //   console.log("id: ", id);
    //   this.showPicker = true;
    // },

    // updateTask() {
    //   let currentTask = this.tasks.filter(
    //     (task) => task.id === this.editingTaskId
    //   );
    //   this.tasks = this.tasks.filter((task) => task.id !== this.editingTaskId);
    //   currentTask[0].due = this.newDate;
    //   this.tasks.push(currentTask[0]);
    //   this.showPicker = false;
    //   this.sortByDue();
    // },

    // clickMe() {
    //   this.dialog = false;
    //   this.newTaskTitle = "";
    // },

    // include() {
    //   return [document.querySelector(".included")];
    // },
  },
};
</script>
