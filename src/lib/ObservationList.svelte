<script lang="ts">
  import { onMount } from 'svelte';

  interface Observation {
    id: number;
    target_name: string;
    date_observed: string;
    file_path: string;
  }

  let observations: Observation[] = [];
  let loading = true;
  let error: string | null = null;

  async function fetchObservations() {
    try {
      const response = await fetch('http://127.0.0.1:8000/api/observations');
      if (!response.ok) throw new Error('Erreur serveur');
      observations = await response.json();
    } catch (e) {
      error = "Impossible de contacter le backend Python.";
    } finally {
      loading = false;
    }
  }

  onMount(fetchObservations);
</script>

<div class="container">
  <h2>Dernières observations</h2>

  {#if loading}
    <p class="status">Chargement des données...</p>
  {:else if error}
    <p class="status error">{error}</p>
  {:else if observations.length === 0}
    <p class="status">Aucune observation en base de données.</p>
  {:else}
    <div class="grid">
      {#each observations as obs}
        <div class="card">
          <div class="info">
            <strong>{obs.target_name}</strong>
            <span>{obs.date_observed}</span>
          </div>
          <code>{obs.file_path}</code>
        </div>
      {/each}
    </div>
  {/if}
</div>

<style>
  .container { margin-top: 1rem; }
  .status { font-style: italic; color: #666; }
  .error { color: #ff5555; }
  .grid { display: grid; gap: 1rem; }
  .card {
    background: #2a2a32;
    border: 1px solid #3f3f46;
    padding: 1rem;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
  .info { display: flex; justify-content: space-between; }
  code { font-size: 0.8rem; color: #888; overflow-wrap: break-word; }
</style>