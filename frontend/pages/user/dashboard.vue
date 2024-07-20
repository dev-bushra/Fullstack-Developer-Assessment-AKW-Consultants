<template>
  <v-row class="main-wrapper mt-5">
    <v-col cols="12" class="text-center my-5" align-center>
      <h1>User Dashboard</h1>
      <a href="/">LogOut</a>
    </v-col>
    <v-col cols="12" align-center>
      <form @submit.prevent="addEntry" v-if="canEdit" class="form-wrapper">
        <v-row class="mx-auto">
          <v-spacer></v-spacer>
          <v-col cols="2"><v-text-field v-model="entryName" class="p-0 m-0" type="text" label="Name/Title"
              placeholder="Name/Title" outlined dense required></v-text-field></v-col>
          <v-col cols="2">
            <input type="file" @change="onFileChange" />
          </v-col>
          <v-spacer></v-spacer>
        </v-row>
        <v-row cols="12">
          <v-btn type="submit" class="w-full elevation-0 mx-auto" elevation="0" color="success" width="350">
            Save
          </v-btn>
        </v-row>
      </form>
    </v-col>
    <v-row class="mx-5 mt-5">
      <v-col cols="3" align-center v-for="entry in filteredEntries" :key="entry.id">
        <v-card class="mx-auto" max-width="344" outlined>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">
                {{ entry.id }}
              </div>
              <v-list-item-title class="text-h5 mb-1">
                {{ entry.name }}
              </v-list-item-title>
              <v-list-item-subtitle>{{ entry.time }}</v-list-item-subtitle>
            </v-list-item-content>
            <img :src="entry.image" alt="Entry Image" />
          </v-list-item>
          <v-card-actions>
            <v-btn v-if="canEdit" @click="editEntry(entry.id)" outlined rounded text>
              Edit
            </v-btn>
            <v-btn v-if="canDelete" @click="deleteEntry(entry.id)" outlined rounded text>
              Delete
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      entryName: '',
      entryImage: null,
      entries: [],
      idCounter: 1,
      user: {
        username: 'user1', // This should be set dynamically based on the logged-in user
        permissions: {
          canEdit: true,
          canDelete: true,
          canView: true,
          canViewAll: false
        }
      }
    };
  },
  computed: {
    canEdit() {
      return this.user.permissions.canEdit;
    },
    canDelete() {
      return this.user.permissions.canDelete;
    },
    filteredEntries() {
      if (this.user.permissions.canViewAll) {
        return this.entries;
      } else {
        return this.entries.filter(entry => entry.username === this.user.username);
      }
    }
  },
  methods: {
    onFileChange(e) {
      const file = e.target.files[0];
      const reader = new FileReader();
      reader.onload = (e) => {
        this.entryImage = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    addEntry() {
      const newEntry = {
        id: this.idCounter++,
        name: this.entryName,
        image: this.entryImage,
        time: new Date().toLocaleString(),
        username: this.user.username // Associate the entry with the current user
      };
      this.entries.unshift(newEntry);
      this.entryName = '';
      this.entryImage = null;
    },
    editEntry(id) {
      // Edit entry logic
    },
    deleteEntry(id) {
      this.entries = this.entries.filter(entry => entry.id !== id);
    }
  }
};
</script>

<style scoped>
h1 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

form {
  margin-bottom: 1rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
}

img {
  max-width: 100px;
  margin-bottom: 1rem;
}

[type="file"] {
  color: #878787;
}

[type="file"]::-webkit-file-upload-button {
  background: #ED1C1B;
  border: 2px solid #ED1C1B;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;
  font-size: 12px;
  outline: none;
  padding: 10px 25px;
  text-transform: uppercase;
  transition: all 1s ease;
}

[type="file"]::-webkit-file-upload-button:hover {
  background: #fff;
  border: 2px solid #535353;
  color: #000;
}
</style>
