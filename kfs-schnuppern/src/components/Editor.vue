<script setup>
import { ref, onMounted, defineProps, watch } from 'vue'
import * as monaco from 'monaco-editor'

const props = defineProps(['task', 'nextUrl'])
const currentTask = ref(props.task)
const output = ref('')
const editorContainer = ref(null)
let editorInstance = null
const canGoToNext = ref(false)

const runCode = () => {
  if (!editorInstance) return
  try {
    output.value = String(eval(editorInstance.getValue()))

    canGoToNext.value = currentTask.value.correct_answer === String(eval(editorInstance.getValue()))
    console.log(output.value)
    console.log(
      (canGoToNext.value =
        currentTask.value.correct_answer === String(eval(editorInstance.getValue())))
    )
  } catch (error) {
    output.value = `Fehler: ${error.message}`
    console.log(error)
  }
}

onMounted(() => {
  if (!currentTask.value?.exampleCode) {
    currentTask.value.exampleCode = '"Task konnte nicht geladen werden!"'
  }

  editorInstance = monaco.editor.create(editorContainer.value, {
    value: currentTask.value.exampleCode,
    language: 'javascript',
    theme: 'vs-light',
    automaticLayout: true
  })
})

// Watch for task changes and update editor
watch(
  () => props.task,
  (newTask) => {
    if (editorInstance && newTask) {
      editorInstance.setValue(newTask.exampleCode)
      currentTask.value = newTask
    }
  },
  { immediate: true }
)
</script>

<template>
  <div class="flex flex-col w-full h-full">
    <!-- Go to next -->
    <div class="w-full flex justify-end">
      <a
        :href="canGoToNext ? nextUrl : ''"
        class="mb-2 max-w-fit px-5 py-2.5 text-sm font-medium text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        :class="{ 'bg-gray-300 cursor-not-allowed hover:bg-gray-400': !canGoToNext }"
      >
        Go to next task →
      </a>
    </div>

    <!-- Monaco Editor -->
    <div ref="editorContainer" class="h-full border rounded-lg"></div>

    <!-- Run Code -->
    <button @click="runCode" class="mt-4 px-4 py-2 bg-blue-500 text-white rounded">
      Code ausführen
    </button>

    <!-- Output -->
    <div class="output mt-4 p-3 border rounded bg-white text-black flex justify-start gap-4">
      <strong>Ausgabe:</strong>
      <p>{{ output }}</p>
    </div>
  </div>
</template>
