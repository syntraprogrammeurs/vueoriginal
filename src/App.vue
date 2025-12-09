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

const newTaskTitle = ref("")
const newTaskDescription = ref("")
const nextTaskId = ref(6)

function handleAddTask() {
  const title = newTaskTitle.value.trim()
  const description = newTaskDescription.value.trim()

  if (!title) {
    // extra veiligheid: formulierknop is al disabled, maar we controleren het hier ook
    return
  }

  const todoColumn = columns.value.find(column => column.id === "todo")
  if (!todoColumn) {
    return
  }

  todoColumn.tasks.push({
    id: nextTaskId.value++,
    title,
    description
  })

  newTaskTitle.value = ""
  newTaskDescription.value = ""
}
</script>





<template>
  <main class="min-h-screen bg-gray-900 text-white px-6 py-8">
    <header class="mb-6 space-y-4">
      <div>
        <h1 class="text-2xl font-bold">
          Mijn kanban board (dynamische versie)
        </h1>
        <p class="text-gray-400 text-sm mt-1">
          De kolommen en kaarten worden gegenereerd op basis van JavaScript data met v-for.
        </p>
      </div>

      <form
          class="bg-gray-800 rounded-xl p-4 flex flex-col gap-3 max-w-xl"
          @submit.prevent="handleAddTask"
      >
        <h2 class="text-sm font-semibold uppercase tracking-wide text-gray-200">
          Nieuwe taak toevoegen aan "To Do"
        </h2>

        <div class="flex flex-col gap-1">
          <label class="text-xs text-gray-300" for="task-title">
            Titel
          </label>
          <input
              id="task-title"
              type="text"
              class="rounded-lg bg-gray-900 border border-gray-700 px-3 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-red-600"
              v-model="newTaskTitle"
              placeholder="Korte titel, bijvoorbeeld: Loginpagina afwerken"
          />
        </div>

        <div class="flex flex-col gap-1">
          <label class="text-xs text-gray-300" for="task-description">
            Beschrijving (optioneel)
          </label>
          <textarea
              id="task-description"
              rows="10"
              class="rounded-lg bg-gray-900 border border-gray-700 px-3 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-600"
              v-model="newTaskDescription"
              placeholder="Extra details over de taak"
          ></textarea>
        </div>

        <div class="flex justify-end">
          <button
              type="submit"
              class="px-4 py-2 bg-blue-600 rounded-lg text-sm font-medium hover:bg-blue-500 disabled:opacity-50 disabled:cursor-not-allowed"
              :disabled="newTaskTitle.trim().length === 0"
          >
            Taak toevoegen
          </button>
        </div>
      </form>
    </header>

    <section class="flex gap-6 overflow-x-auto pb-4">
      <BoardColumn
          v-for="column in columns"
          :key="column.id"
          :title="column.title"
          :count="column.tasks.length"
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



