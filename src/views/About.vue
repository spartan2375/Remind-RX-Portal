<template>
  <div>
    <div class="about pa-6">
      <h1>Settings</h1>
    </div>
    <div>
      <v-list class="pa-3">
        <v-list-item v-for="(setting, i) in settings" :key="i">
          <v-row justify="center">
            <v-col cols="4" class="d-flex justify-center">
              <v-btn outlined>
                <v-list-item-icon>
                  <v-icon :color="setting.color">{{ setting.icon }}</v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  {{ setting.title }}
                </v-list-item-content>
              </v-btn>
            </v-col>
            <v-col cols="8"
              >Lorem ipsum dolor sit amet consectetur adipisicing elit. Unde
              labore officiis cumque iure ipsa, enim, earum iste qui eos odit
              omnis illo. Eius veritatis consequuntur facilis architecto est
              quia deserunt.</v-col
            >
          </v-row>
        </v-list-item>
      </v-list>
    </div>
    <!-- <v-row justify="center">
      <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="primary" dark v-bind="attrs" v-on="on" class="included">
            <v-icon>mdi-plus</v-icon>
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
                  <v-text-field label="Email*" required></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">
              Close
            </v-btn>
            <v-btn color="blue darken-1" text @click="dialog = false">
              Add Task
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>

    <v-row>
      <v-spacer></v-spacer>
      <v-date-picker
        :elevation="3"
        v-model="date"
        v-show="showDatePicker"
        @input="showDatePicker = false"
      >
        <v-spacer></v-spacer>
        <v-btn text color="primary" @click="showDatePicker = false">
          Cancel
        </v-btn>
      </v-date-picker>
      <v-btn
        class="mx-10"
        fab
        dark
        right
        color="primary"
        @click="showDatePicker = !showDatePicker"
      >
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-row> -->
  </div>
</template>

<script>
import TaskList from "../components/Task-List.vue";
export default {
  components: { TaskList },
  data() {
    return {
      settings: [
        {
          title: "Keep me logged in",
          icon: "mdi-account-lock",
          color: "red",
        },
        {
          title: "Change password",
          icon: "mdi-lock-reset",
          color: "primary",
        },
        {
          title: "Change associated email",
          icon: "mdi-email-sync",
          color: "primary",
        },
        {
          title: "Import patient data to csv",
          icon: "mdi-file-import",
          color: "primary",
        },
        {
          title: "Export patient data to csv",
          icon: "mdi-file-export",
          color: "primary",
        },
        {
          title: "Deactivate account",
          icon: "mdi-account-cancel",
          color: "red",
        },
      ],
      TaskList,
      dialog: false,
      showDatePicker: false,
      date: "",
    };
  },

  methods: {
    clickMe() {
      console.log("Click Me");
      this.dialog = false;
    },

    include() {
      return [document.querySelector(".included")];
    },
  },
};
</script>
