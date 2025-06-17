<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  export let message = "Are you sure?";
</script>

<div class="fixed inset-0 bg-black bg-opacity-50 dark:bg-opacity-70 flex items-center justify-center z-50 transition-all">
  <div class="bg-white dark:bg-gray-800 text-gray-900 dark:text-white p-6 rounded-lg shadow-lg text-center w-[90%] max-w-sm transition-colors duration-300">
    <p class="mb-4 text-lg">{message}</p>
    <div class="flex justify-center gap-4">
      <button
        on:click={() => dispatch('confirm')}
        class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded transition focus:ring-2 focus:ring-red-300"
      >
        Yes, Delete
      </button>
      <button
        on:click={() => dispatch('cancel')}
        class="bg-gray-300 hover:bg-gray-400 text-gray-800 dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white px-4 py-2 rounded transition focus:ring-2 focus:ring-gray-300"
      >
        Cancel
      </button>
    </div>
  </div>
</div>
