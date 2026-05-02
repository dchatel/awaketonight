<script lang="ts">
  import { getCurrentWindow } from '@tauri-apps/api/window';
  const appWindow = getCurrentWindow();

  // Fonctions pour les boutons de contrôle
  const minimize = () => appWindow.minimize();
  const toggleMaximize = () => appWindow.toggleMaximize();
  const close = () => appWindow.close();
</script>

<!-- L'attribut data-tauri-drag-region permet de déplacer la fenêtre en glissant cette div -->
<div data-tauri-drag-region class="titlebar">
  <div class="logo">🔭 AwakeTonight</div>
  
  <div class="window-controls">
    <button class="control-btn" on:click={minimize}>
      <img src="https://api.iconify.design/mdi:window-minimize.svg?color=white" alt="min" />
    </button>
    <button class="control-btn" on:click={toggleMaximize}>
      <img src="https://api.iconify.design/mdi:window-maximize.svg?color=white" alt="max" />
    </button>
    <button class="control-btn close" on:click={close}>
      <img src="https://api.iconify.design/mdi:close.svg?color=white" alt="close" />
    </button>
  </div>
</div>

<style>
  .titlebar {
    height: 40px;
    background: #1a1a1d; /* Couleur très sombre style CouchPotato */
    display: flex;
    justify-content: space-between;
    align-items: center;
    user-select: none; /* Empêche de sélectionner le texte de la barre */
    border-bottom: 1px solid #333;
  }

  .logo {
    padding-left: 15px;
    font-size: 0.9rem;
    font-weight: bold;
    color: #aaa;
    pointer-events: none; /* Laisse le clic passer à la zone de drag en dessous */
  }

  .window-controls {
    display: flex;
    height: 100%;
  }

  .control-btn {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    width: 45px;
    height: 100%;
    border: none;
    background: transparent;
    cursor: pointer;
    transition: background 0.2s;
  }

  .control-btn:hover {
    background: #333;
  }

  .control-btn.close:hover {
    background: #e81123; /* Rouge classique Windows au survol */
  }

  .control-btn img {
    width: 16px;
    height: 16px;
  }
</style>