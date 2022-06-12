<template>
  <q-page padding>
    <Container>
      <div class="row items.center justify-between">
        <h3>Your Notes</h3>
        <div>
          <q-btn round color="positive" icon="add" to="/new"></q-btn>
        </div>
      </div>

      <NoteCard
        v-for="({title,description}, idx) in notes"
        :key="idx"
        :title="title"
        :description="description"
        @click="router.push(`/note/${idx}`)"
      />
      <div v-if="notes.length === 0">You have not created any notes.</div>
    </Container>
  </q-page>
</template>

<script>
/* eslint-disable */
import Container from 'components/AppContainer.vue'
import NoteCard from 'src/components/NoteCard.vue'
import {useLocalNotes} from "src/helper";
import {defineComponent} from 'vue'
import {useRouter} from "vue-router";

export default defineComponent({
  components: {NoteCard, Container},
  name: 'IndexPage',
  setup() {
    const router = useRouter();
    const notes = useLocalNotes();
    return {
      notes,
      router
    }
  },
})
</script>
