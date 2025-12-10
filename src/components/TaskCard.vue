<script setup>
const props = defineProps({
  id: {
    type: Number,
    required: true
  },
  columnId: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    default: ""
  },
  isLastColumn: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(["move-task"])

function handleMoveToNextColumn() {
  if (props.isLastColumn) {
    return
  }

  emit("move-task", {
    taskId: props.id,
    fromColumnId: props.columnId
  })
}
</script>

<template>
  <article class="rounded-lg bg-gray-800 p-4 shadow-md border border-gray-700">
    <h3 class="font-semibold text-sm text-white">
      {{ props.title }}
    </h3>

    <p v-if="props.description" class="text-xs text-gray-300 mt-1 leading-relaxed">
      {{ props.description }}
    </p>

    <div class="mt-3 flex justify-end">
      <button
          v-if="!props.isLastColumn"
          type="button"
          class="text-[11px] px-2 py-1 rounded bg-gray-700 hover:bg-gray-600 text-gray-100"
          @click="handleMoveToNextColumn"
      >
        Naar volgende kolom
      </button>
    </div>
  </article>
</template>

