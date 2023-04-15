<template>
  <v-app>
    <v-main class="pa-10">
      <v-col cols="8">
        <v-autocomplete
          v-model="values"
          :items="items"
          outlined
          chips
          small-chips
          label="Select Items"
          multiple
          item-text="title"
          item-value="id"
        >
          <template v-slot:selection>
            <div></div>
          </template>
          <template v-slot:prepend-item>
            <v-list-item>
              <v-list-item-action>
                <v-checkbox
                  v-model="selectAll"
                  @change="handleSelectAll"
                ></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title>Select All</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
          </template>
        </v-autocomplete>
      </v-col>
      <v-col cols="8">
        <v-autocomplete
          v-model="values"
          :items="items"
          outlined
          chips
          small-chips
          label="Select Items"
          multiple
          item-text="title"
          item-value="id"
        >
          <template v-slot:selection>
            <div></div>
          </template>
          <template v-slot:prepend-item>
            <v-list-item>
              <v-list-item-action>
                <v-checkbox
                  v-model="selectAll"
                  @change="handleSelectAll"
                ></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title>Select All</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
          </template>
          <template v-slot:item="{ item }">
            <div>
              <input type="checkbox" :checked="item.checked" />
              <label for="">{{ item.title }}</label>
            </div>
          </template>
        </v-autocomplete>
      </v-col>
      <v-col cols="8">
        <v-btn @click="handleSubmit" color="primary">Submit</v-btn>
      </v-col>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      isShowContent: false,
      items: [],
      values: [],
      selectAll: false,
    };
  },

  created() {
    fetch('https://jsonplaceholder.typicode.com/photos')
      .then((response) => response.json())
      .then(
        (json) =>
          (this.items = json
            .slice(0, 1000)
            .map((j) => ({ ...j, checked: false })))
      );
  },

  methods: {
    handleSubmit() {
      console.log(this.values);
    },

    handleSelectAll() {
      if (this.selectAll) {
        // this.values = this.items.map((item) => item.id);
        this.items = this.items.map((item) => ({ ...item, checked: true }));
      } else {
        // this.values = [];
        this.items = this.items.map((item) => ({ ...item, checked: false }));
      }
    },
  },
};
</script>
