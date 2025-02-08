<script>
  import { onMount, setContext } from 'svelte';
  import { writable } from 'svelte/store';
  import "../app.css";

  const darkMode = writable(false);

  function toggleTheme() {
    darkMode.update(current => {
      const newValue = !current;
      console.log('Theme value before DOM update:', newValue);
      document.documentElement.classList.toggle('dark', newValue);
      console.log('Dark class present:', document.documentElement.classList.contains('dark'));
      return newValue;
    });
  }

  onMount(() => {
    const isDark = document.documentElement.classList.contains('dark');
    console.log('Initial dark class:', isDark);
    darkMode.set(isDark);
  });

  setContext('toggleTheme', toggleTheme);
  setContext('darkMode', darkMode);
</script>

<div class="min-h-screen">
  <slot />
</div>