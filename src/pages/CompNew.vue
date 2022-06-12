<template>
  <q-page padding>
    <Container>
      <h3>New Note</h3>
      <form @submit="submit">
        <q-input class="q-mt-sm" outlined v-model="note.title" label="Title"></q-input>
        <q-input class="q-mt-sm" outlined v-model="note.description" label="Description" dense></q-input>

        <q-card flat bordered class="q-mt-sm">
          <q-editor v-model="note.content" min-height="5rem"></q-editor>
        </q-card>

        <div class="q-mt-md">
          <q-btn to="/" type="reset">Cancel</q-btn>
          <q-btn class="q-ml-sm" color="positive" type="submit">Create</q-btn>
        </div>
      </form>
    </Container>
  </q-page>
</template>

<script>
import Container from 'components/AppContainer.vue'
import { defineComponent, reactive } from 'vue'
import { useLocalNotes } from 'src/helper'
import { useRouter } from 'vue-router'

export default defineComponent({
  components: {Container},
  name: "CompNew",
  setup() {
    const router = useRouter();
    const notes = useLocalNotes();

    const note =
      reactive({
        title: "",
        description: "",
        content: "",
      })
    const submit = () => {
      notes.value.unshift({
        ...note,
        createdAt: Date.now(),
        updatedAt: Date.now(),
      })
      router.push("/");

      note.title = "";
      note.description = "";
      note.content = "";
    }
    return {
      note,
      submit,
    }
  },
})
</script>


