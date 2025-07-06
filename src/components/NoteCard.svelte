<script>
  import { createEventDispatcher } from 'svelte';
  export let note;
  const dispatch = createEventDispatcher();

  let editing = false;
  let editedTitle = note.title;
  let editedContent = note.content;

  function deleteMe() {
    dispatch('deletenote');
  }

  function saveEdit() {
    dispatch('updatenote', { id: note.id, title: editedTitle, content: editedContent });
    editing = false;
  }
</script>

<div class="bg-white dark:bg-gray-800 dark:text-white p-4 rounded shadow-md relative group transition-colors duration-300">

  {#if editing}
    <input
      bind:value={editedTitle}
      class="border dark:border-gray-600 p-2 w-full mb-2 rounded focus:ring-2 focus:ring-indigo-400 dark:bg-gray-700 dark:text-white"
    />
    <textarea
      bind:value={editedContent}
      class="border dark:border-gray-600 p-2 w-full mb-2 rounded resize-none focus:ring-2 focus:ring-indigo-400 dark:bg-gray-700 dark:text-white"
      rows="3"
    ></textarea>
    <button
      on:click={saveEdit}
      class="bg-green-500 text-white px-4 py-2 rounded hover:bg-green-600 transition"
    >
      💾 Save
    </button>
  {:else}
    <h2 class="text-xl font-bold text-gray-800 dark:text-white">{note.title}</h2>
    <p class="text-gray-700 dark:text-gray-300 mt-1">{note.content}</p>
    <p class="text-xs text-gray-400 mt-3">{new Date(note.createdAt).toLocaleString()}</p>

    <div class="absolute top-2 right-2 flex space-x-2 opacity-0 group-hover:opacity-100 transition-opacity duration-200">
  <button on:click={() => (editing = true)} aria-label="Edit">
    <img src="/icons/edit-icon.png" alt="Edit" title="Edit" class="w-6 h-6 hover:scale-110 transition-transform" />
  </button>
  <button on:click={deleteMe} aria-label="Delete">
    <img src="/icons/delete-icon.png" alt="Delete" title="Delete" class="w-6 h-6 hover:scale-110 transition-transform" />

  </button>
</div>

  {/if}
</div>
