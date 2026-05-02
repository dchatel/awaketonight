<script lang="ts">
  import { onMount } from 'svelte';
  import Titlebar from './lib/Titlebar.svelte';
  import ObservationList from './lib/ObservationList.svelte';
    import { getCurrentWindow } from '@tauri-apps/api/window';
    import app from './main';

  const appWindow = getCurrentWindow();
  let isMaximized = false;

  onMount(async () => {
    isMaximized = await appWindow.isMaximized();

    await appWindow.onResized(async () => {
      isMaximized = await appWindow.isMaximized();
    });
  });
</script>

<div class="app-container" class:is-maximized={isMaximized}>
  <div class="app-shell" class:is-maximized={isMaximized}>
    <Titlebar />
    <main class="content">
      <ObservationList />
    </main>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    overflow: hidden; /* Empêche le scroll sur toute la fenêtre, on scrollera le contenu */
  }

  .app-container {
    width: 100vw;
    height: 100vh;
    padding: 4px;
    display: flex;
    background: transparent;
  }

  .app-container.is-maximized {
    padding: 0;
  }

  .app-shell {
    flex: 1;
    display: flex;
    flex-direction: column;
    background-color: #121214;
    border: 1px solid #333;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.8); 
    overflow: hidden;
  }

  .app-shell.is-maximized {
    border-radius: 0;
    border: none;
    box-shadow: none;
  }

  .content {
    flex: 1;
    overflow-y: auto; /* Seul le contenu scrolle, la barre de titre reste fixe */
    padding: 20px;
  }
</style>