<template>
  <div class="micro-music-bar">
    <!-- Botón play/pause -->
    <button @click="togglePlay" class="micro-btn" :class="{ playing: isPlaying }" title="Play/Pause">
      {{ isPlaying ? '⏸' : '▶' }}
    </button>
    
    <!-- Barra de progreso -->
    <div class="micro-progress">
      <div class="micro-progress-fill" :style="{ width: progressPercentage + '%' }"></div>
    </div>
    
    <!-- Tiempo actual -->
    <span class="micro-time">{{ formatTime(currentTime) }}</span>
    
    <!-- Control de volumen con hover -->
    <div class="volume-container">
      <button class="micro-btn volume-btn" @click="toggleMute" :class="{ muted: isMuted }" title="Silenciar">
        {{ volumeIcon }}
      </button>
      <div class="volume-slider-wrapper">
        <input 
          type="range" 
          min="0" 
          max="1" 
          step="0.01" 
          :value="volume" 
          @input="ajustarVolumen($event.target.value)"
          class="volume-slider"
        />
      </div>
    </div>
    
    <!-- Botón de stop -->
    <button @click="stop" class="micro-btn stop" title="Detener">
      ⏹
    </button>
  </div>
</template>

<script>
import sound from '../assets/cancion.mp3';

export default {
  name: 'MicroMusicBarWithVolume',
  data() {
    return {
      audio: new Audio(sound),
      isPlaying: false,
      currentTime: 0,
      duration: 0,
      volume: 0.7,
      isMuted: false,
      previousVolume: 0.7
    };
  },
  computed: {
    progressPercentage() {
      return this.duration ? (this.currentTime / this.duration) * 100 : 0;
    },
    volumeIcon() {
      if (this.isMuted || this.volume === 0) return '🔇';
      if (this.volume < 0.3) return '🔈';
      if (this.volume < 0.7) return '🔉';
      return '🔊';
    }
  },
  mounted() {
    this.setupAudio();
  },
  beforeUnmount() {
    this.audio.pause();
  },
  methods: {
    setupAudio() {
      this.audio.addEventListener('loadedmetadata', () => {
        this.duration = this.audio.duration;
      });
      
      this.audio.addEventListener('timeupdate', () => {
        this.currentTime = this.audio.currentTime;
      });
      
      this.audio.addEventListener('play', () => {
        this.isPlaying = true;
      });
      
      this.audio.addEventListener('pause', () => {
        this.isPlaying = false;
      });

      // Configurar volumen inicial
      this.audio.volume = this.volume;
    },

    togglePlay() {
      if (this.isPlaying) {
        this.audio.pause();
      } else {
        this.audio.play().catch(error => {
          console.error('Error al reproducir:', error);
        });
      }
    },

    stop() {
      this.audio.pause();
      this.audio.currentTime = 0;
      this.isPlaying = false;
    },

    ajustarVolumen(nivel) {
      const newVolume = parseFloat(nivel);
      this.volume = newVolume;
      this.audio.volume = newVolume;
      
      // Si ajustamos el volumen, quitamos el mute
      if (this.isMuted && newVolume > 0) {
        this.isMuted = false;
      }
    },

    toggleMute() {
      if (this.isMuted) {
        // Quitar mute
        this.audio.volume = this.previousVolume;
        this.volume = this.previousVolume;
        this.isMuted = false;
      } else {
        // Activar mute
        this.previousVolume = this.volume;
        this.audio.volume = 0;
        this.volume = 0;
        this.isMuted = true;
      }
    },

    formatTime(seconds) {
      if (isNaN(seconds)) return '0:00';
      const mins = Math.floor(seconds / 60);
      const secs = Math.floor(seconds % 60);
      return `${mins}:${secs.toString().padStart(2, '0')}`;
    }
  }
}
</script>

<style scoped>
.micro-music-bar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 30px;
  background: #2c5032;
  display: flex;
  align-items: center;
  padding: 0 10px;
  gap: 8px;
  z-index: 1000;
  border-bottom: 1px solid #34495e;
}

.micro-btn {
  background: none;
  border: none;
  color: white;
  font-size: 12px;
  cursor: pointer;
  padding: 4px;
  border-radius: 2px;
  transition: background-color 0.2s;
}

.micro-btn:hover {
  background: rgba(255, 255, 255, 0.1);
}

.micro-btn.playing {
  color: #3498db;
}

.micro-btn.stop {
  color: #e74c3c;
}

.micro-progress {
  flex: 1;
  height: 2px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 1px;
  overflow: hidden;
  min-width: 50px;
}

.micro-progress-fill {
  height: 100%;
  background: #3498db;
  transition: width 0.3s ease;
}

.micro-time {
  font-size: 10px;
  font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
  color: #95a5a6;
  min-width: 35px;
  text-align: center;
}

/* Contenedor de volumen */
.volume-container {
  display: flex;
  align-items: center;
  gap: 5px;
  position: relative;
}

.volume-btn {
  font-size: 11px;
  padding: 3px;
}

.volume-btn.muted {
  color: #e74c3c;
}

.volume-slider-wrapper {
  width: 0;
  overflow: hidden;
  transition: width 0.3s ease;
}

.volume-container:hover .volume-slider-wrapper {
  width: 60px;
}

.volume-slider {
  width: 60px;
  height: 3px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 2px;
  outline: none;
  -webkit-appearance: none;
  cursor: pointer;
}

.volume-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: white;
  cursor: pointer;
  transition: all 0.2s;
}

.volume-slider::-webkit-slider-thumb:hover {
  transform: scale(1.2);
}

.volume-slider::-moz-range-thumb {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: white;
  cursor: pointer;
  border: none;
}

/* Responsive para móviles */
@media (max-width: 768px) {
  .micro-music-bar {
    padding: 0 8px;
    gap: 6px;
  }
  
  .micro-time {
    min-width: 30px;
    font-size: 9px;
  }
  
  .micro-progress {
    min-width: 40px;
  }
  
  .volume-container:hover .volume-slider-wrapper {
    width: 40px;
  }
  
  .volume-slider {
    width: 40px;
  }
}

/* Efecto de transición suave para toda la barra */
.micro-music-bar {
  transition: all 0.3s ease;
}
</style>