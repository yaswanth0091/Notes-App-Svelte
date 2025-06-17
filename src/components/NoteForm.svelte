<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  let title = '';
  let content = '';

  function submitForm() {
    if (!title || !content) return;
    dispatch('addnote', { title, content, createdAt: new Date().toISOString() });
    title = '';
    content = '';
  }
</script>

<div class="bg-white dark:bg-gray-800 p-4 rounded shadow-md transition-colors duration-300">
  <input
    bind:value={title}
    placeholder="Title"
    class="border p-2 w-full mb-2 rounded bg-white dark:bg-gray-700 dark:text-white dark:border-gray-600 placeholder-gray-500 dark:placeholder-gray-400 focus:ring-2 focus:ring-blue-400 transition"
  />

  <textarea
    bind:value={content}
    placeholder="Content"
    class="border p-2 w-full mb-2 rounded resize-none bg-white dark:bg-gray-700 dark:text-white dark:border-gray-600 placeholder-gray-500 dark:placeholder-gray-400 focus:ring-2 focus:ring-blue-400 transition"
    rows="3"
  />

  <button
    on:click={submitForm}
    class="bg-blue-500 hover:bg-blue-600 text-white font-semibold px-4 py-2 rounded transition"
  >
    ➕ Add Note
  </button>
</div>
