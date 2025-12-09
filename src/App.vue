<script setup>
import TaskCard from "./components/TaskCard.vue"
import BoardColumn from "./components/BoardColumn.vue"

const columns = [
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
      },
      {
        id: 7,
        title: "Bug fixes opgelost",
        description: ""
      }
    ]
  }
]
</script>


<template>
  <main class="min-h-screen bg-gray-900 text-white px-6 py-8">
    <header class="mb-6">
      <h1 class="text-2xl font-bold">
        Mijn kanban board (dynamische versie)
      </h1>
      <p class="text-gray-400 text-sm mt-1">
        De kolommen en kaarten worden nu gegenereerd op basis van JavaScript data met v-for.
      </p>
    </header>

    <section class="flex gap-6 overflow-x-auto pb-4">
      <BoardColumn
          v-for="column in columns"
          :key="column.id"
          :title="column.title"
          :count="column.tasks.length"
      >
        <!-- taken per kolom komen in de volgende module -->
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

