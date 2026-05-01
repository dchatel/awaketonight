<script lang="ts">
  import Titlebar from './lib/Titlebar.svelte';
  import ObservationList from './lib/ObservationList.svelte';
</script>

<div class="app-shell">
  <Titlebar />
  
  <main class="content">
    <ObservationList />
  </main>
</div>

<style>
  :global(body) {
    margin: 0;
    overflow: hidden; /* Empêche le scroll sur toute la fenêtre, on scrollera le contenu */
  }

  .app-shell {
    display: flex;
    flex-direction: column;
    height: 100vh;
    background-color: #121214;
    color: #e1e1e6;
    border: 1px solid #333; /* Pour simuler une bordure fine de fenêtre */
    box-sizing: border-box;
  }

  .content {
    flex: 1;
    overflow-y: auto; /* Seul le contenu scrolle, la barre de titre reste fixe */
    padding: 20px;
  }
</style>