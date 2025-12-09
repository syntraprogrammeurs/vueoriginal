<script setup>
import { ref } from "vue"
import TaskCard from "./components/TaskCard.vue"
import BoardColumn from "./components/BoardColumn.vue"

const columns = ref([
  {
    id: "todo",
    title: "To Do",
    tasks: [
      {
        id: 1,
        title: "Nieuwe cursusstructuur uitwerken",
        description: "Modules herzien en oefeningen toevoegen."
      },
      {
        id: 2,
        title: "Design voor dashboard maken",
        description: "Wireframes en kleurenpalet bepalen."
      }
    ]
  },
  {
    id: "doing",
    title: "Doing",
    tasks: [
      {
        id: 3,
        title: "API koppeling testen",
        description: "Controleer foutafhandeling en timeouts."
      }
    ]
  },
  {
    id: "done",
    title: "Done",
    tasks: [
      {
        id: 4,
        title: "Vite project opgezet",
        description: "Basisconfiguratie met Vue en Tailwind."
      },
      {
        id: 5,
        title: "Component structuur bepaald",
        description: ""
      },
      {
        id: 6,
        title: "Tailwind integratie getest",
        description: ""
      }
    ]
  }
])

const nextTaskId = ref(7)

function handleAddTaskToColumn(payload) {
  const { columnId, title, description } = payload

  const column = columns.value.find(col => col.id === columnId)
  if (!column) {
    return
  }

  column.tasks.push({
    id: nextTaskId.value++,
    title,
    description
  })
}
</script>

<template>
  <main class="min-h-screen bg-gray-900 text-white px-6 py-8">
    <header class="mb-6">
      <h1 class="text-2xl font-bold">
        Mijn kanban board (per kolom taken toevoegen)
      </h1>
      <p class="text-gray-400 text-sm mt-1">
        Kolommen en kaarten worden gegenereerd op basis van JavaScript data. Nieuwe taken worden per kolom toegevoegd via een formulier binnen die kolom.
      </p>
    </header>

    <section class="flex gap-6 overflow-x-auto pb-4">
      <BoardColumn
          v-for="column in columns"
          :key="column.id"
          :id="column.id"
          :title="column.title"
          :count="column.tasks.length"
          @add-task="handleAddTaskToColumn"
      >
        <TaskCard
            v-for="task in column.tasks"
            :key="task.id"
            :title="task.title"
            :description="task.description"
        />
      </BoardColumn>
    </section>
  </main>
</template>

