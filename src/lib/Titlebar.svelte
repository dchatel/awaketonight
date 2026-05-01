<script lang="ts">
  import { getCurrentWindow } from '@tauri-apps/api/window';
  const appWindow = getCurrentWindow();

  // Fonction pour déclencher le déplacement de la fenêtre
  const handleMouseDown = async (e: MouseEvent) => {
    // On ne déclenche le drag que si c'est le clic gauche
    // et que l'utilisateur n'a pas cliqué sur un bouton
    if (e.buttons === 1 && (e.target as HTMLElement).classList.contains('titlebar')) {
      await appWindow.startDragging();
    }
  };

  const minimize = () => appWindow.minimize();
  const toggleMaximize = () => appWindow.toggleMaximize();
  const close = () => appWindow.close();
</script>

<!-- On utilise on:mousedown pour attraper le clic -->
<div 
  class="titlebar" 
  on:mousedown={handleMouseDown}
  role="presentation"
>
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
    background: #1a1a1d;
    display: flex;
    justify-content: space-between;
    align-items: center;
    user-select: none;
    border-bottom: 1px solid #333;
    /* On s'assure que le curseur montre que c'est déplaçable */
    cursor: default;
  }

  .logo {
    padding-left: 15px;
    font-size: 0.9rem;
    font-weight: bold;
    color: #aaa;
    /* IMPORTANT : pointer-events: none permet au clic de 
       passer à travers le texte et d'atteindre la div .titlebar */
    pointer-events: none;
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