<script>
  import { getContext } from 'svelte';
  import FlowComponent from '$lib/FlowComponent.svelte';
  import { writable } from 'svelte/store';

  const toggleTheme = getContext('toggleTheme');
  const darkMode = getContext('darkMode');
  
  // Sidebar state
  const sidebarOpen = writable(false);
  const toggleSidebar = () => sidebarOpen.update(v => !v);
</script>

<div class="min-h-screen bg-[--light-bg] dark:bg-[--dark-bg] flex flex-col">
  <!-- Minimal Header -->
  <header class="bg-[--light-primary] dark:bg-[--dark-primary] py-2 px-4 flex items-center justify-between">
    <h1 class="text-2xl font-bold tracking-tight text-[--light-primary-text] dark:text-[--dark-text]">
      GraphFlow
    </h1>
    <div class="flex gap-2">
      <button
        on:click={toggleSidebar}
        class="bg-[--light-secondary] text-[--light-primary] dark:bg-[--dark-secondary] dark:text-[--dark-text]
               px-3 py-1.5 rounded-lg shadow hover:shadow-lg transition-all duration-200"
      >
        {$sidebarOpen ? '✕' : '☰'}
      </button>
      <button
        on:click={toggleTheme}
        class="bg-[--light-secondary] text-[--light-primary] dark:bg-[--dark-secondary] dark:text-[--dark-text]
               px-3 py-1.5 rounded-lg shadow hover:shadow-lg transition-all duration-200"
      >
        {$darkMode ? '🌞' : '🌙'}
      </button>
    </div>
  </header>

  <!-- Main Content with Sidebar -->
  <div class="flex-1 flex overflow-hidden">
    <!-- Main Flow Component Area -->
    <main class="flex-1">
      <FlowComponent />
    </main>

    <!-- Collapsible Sidebar -->
    <aside class="bg-[--light-surface] dark:bg-[--dark-surface] w-80 transform transition-transform duration-300
                  {$sidebarOpen ? 'translate-x-0' : 'translate-x-full'} 
                  fixed right-0 top-[48px] bottom-0 shadow-lg overflow-y-auto">
      <div class="p-6 space-y-6">
        <section>
          <h2 class="text-xl font-semibold mb-4 text-[--light-text] dark:text-[--dark-text]">
            Export & Share
          </h2>
          <p class="mb-4 text-[--light-text]/80 dark:text-[--dark-text]/80">
            When you're done editing, export your graph as a JSON file.
          </p>
          <button
            class="w-full bg-[--light-primary] dark:bg-[--dark-primary] text-white px-6 py-3 rounded-lg
                   hover:shadow-lg transition-all duration-200"
          >
            Export Graph
          </button>
        </section>

        <!-- Additional sidebar content -->
        <section>
          <h2 class="text-xl font-semibold mb-4 text-[--light-text] dark:text-[--dark-text]">
            Graph Settings
          </h2>
          <!-- Add settings controls here -->
        </section>
      </div>
    </aside>
  </div>
</div>