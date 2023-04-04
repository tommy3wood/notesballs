<template>
  <div class="notes">
    <div class="card has-background-success-dark p-4 mb-5">
      <div class="field">
        <label class="label">Message</label>
        <div class="control">
          <textarea
            v-model="newNote"
            ref="newNoteRef"
            class="textarea"
            placeholder="Add a new note..."
          />
        </div>
      </div>
      <div class="field is-grouped is-grouped-right">
        <div class="control">
          <button
            @click="addNote"
            :disabled="!newNote"
            class="button is-link has-background-success"
          >
            Add New Note
          </button>
        </div>
      </div>
      <Note
        v-for="note in notes"
        :key="note.id"
        :note="note"
        @deleteClicked="deleteNote"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Note from "@/components/notes/Note.vue";
const newNote = ref("");
const newNoteRef = ref(null);

const notes = ref([
  {
    id: "1",
    content:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptates quas est, tenetur nisi ab at earum reprehenderit iusto doloremque inventore quaerat repellat beatae sapiente aut necessitatibus distinctio iste cum modi.",
  },
  {
    id: "2",
    content:
      "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Id fugiat sit nesciunt aliquam, totam adipisci iusto quae sequi qui tempora perspiciatis inventore unde minima, temporibus tenetur. Modi optio quae consequatur.",
  },
  {
    id: "3",
    content:
      "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Officiis, odio repudiandae delectus pariatur vitae ad nemo consequatur cupiditate obcaecati ab nesciunt a modi hic minima accusantium cumque, fuga suscipit iure!",
  },
]);

const addNote = () => {
  let id = notes.value.length + 1;
  let note = {
    id: id.toString(),
    content: newNote.value,
  };
  newNote.value = "";
  newNoteRef.value.focus();
  notes.value.unshift(note);
};

const deleteNote = (id) => {
  notes.value = notes.value.filter((note) => {
    return note.id !== id;
  });
};
</script>
