<script>
  import NoteCard from './components/NoteCard.svelte';
  import NoteForm from './components/NoteForm.svelte';
  import ConfirmModal from './components/ConfirmModal.svelte';

  let notes = [];
  let isLoading = false;
  let showModal = false;
  let noteToDelete = null;
  let search = '';
  let dark = false;

  const API_URL = 'https://6851670f8612b47a2c09eb0f.mockapi.io/api/v1/notes';

  // Dark mode reactive toggle
  $: {
    if (dark) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  }

  // Fetch notes from API
  async function fetchNotes() {
    isLoading = true;
    try {
      const res = await fetch(API_URL);
      notes = await res.json();
    } catch (err) {
      console.error('Failed to fetch notes', err);
    } finally {
      isLoading = false;
    }
  }

  // Filter notes based on search
  $: filteredNotes = notes.filter(note =>
  note.title.toLowerCase().includes(search.toLowerCase())
);


  // Add note and refresh
  async function handleAddNote(e) {
    const newNote = e.detail;
    try {
      await fetch(API_URL, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(newNote)
      });
      await fetchNotes();
    } catch (err) {
      console.error('Failed to add note', err);
    }
  }

  // Ask for confirmation before delete
  function askDelete(id) {
    noteToDelete = id;
    showModal = true;
  }

  function cancelDelete() {
    noteToDelete = null;
    showModal = false;
  }

  // Confirm and perform delete with real-time update
  async function confirmDelete() {
    if (!noteToDelete) return;
    isLoading = true;
    try {
      await fetch(`${API_URL}/${noteToDelete}`, { method: 'DELETE' });
      await fetchNotes();
    } catch (err) {
      console.error('Failed to delete note', err);
    } finally {
      isLoading = false;
      noteToDelete = null;
      showModal = false;
    }
  }

  // Update note and refresh list
  async function handleUpdateNote(e) {
    const { id, title, content } = e.detail;
    try {
      await fetch(`${API_URL}/${id}`, {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ title, content })
      });
      await fetchNotes();
    } catch (err) {
      console.error('Failed to update note', err);
    }
  }

  // Initial load
  fetchNotes();
</script>

<main class="min-h-screen bg-gray-50 dark:bg-gray-900 transition-colors duration-300">
  <div class="max-w-2xl mx-auto p-4 space-y-6">
    <h1 class="text-3xl font-bold text-center text-gray-800 dark:text-white">My Notes App</h1>

    <div class="text-right mb-4">
      <button
        on:click={() => (dark = !dark)}
        class="px-4 py-2 rounded text-sm bg-gray-200 dark:bg-gray-700 dark:text-white"
      >
        {dark ? '🌞 Light Mode' : '🌙 Dark Mode'}
      </button>
    </div>

    <input
      type="text"
      placeholder="Search by title..."
      bind:value={search}
      class="w-full border border-gray-300 p-2 rounded bg-white dark:bg-gray-700 dark:text-white dark:border-gray-600"
    />

    <NoteForm on:addnote={handleAddNote} />

    {#if isLoading}
      <div class="text-center text-gray-500 dark:text-gray-300">Loading...</div>
    {:else if filteredNotes.length === 0}
      <div class="text-center text-gray-500 dark:text-gray-300">No notes found.</div>
    {:else}
      <div class="space-y-4">
        {#each filteredNotes as note (note.id)}
          <NoteCard
            {note}
            on:deletenote={() => askDelete(note.id)}
            on:updatenote={handleUpdateNote}
          />
        {/each}
      </div>
    {/if}

    {#if showModal}
      <ConfirmModal
        message="Are you sure you want to delete this note?"
        on:confirm={confirmDelete}
        on:cancel={cancelDelete}
      />
    {/if}
  </div>
</main>

<style>
  html {
    transition: background-color 0.3s ease;
  }

  main {
    font-family: system-ui, sans-serif;
  }
</style>
