<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-t from-blue-900 to-slate-900 px-2 sm:px-8 py-4">
    <div class="w-full max-w-md p-4 sm:p-8">
      <h2 class="text-xl sm:text-2xl font-bold text-white text-center mb-4">¿Quién es la persona más increíble, inteligente, amable, sorprendente y especial que conoces?</h2>
      <label for="respuesta" class="text-base sm:text-lg text-white mb-2 block">Tu respuesta:</label>
      <input
        class="w-full border border-white-800 outline-none p-2 sm:p-3 rounded text-white mb-4 transition-all duration-200"
        id="respuesta"
        v-model="respuesta"
        type="text"
        @keyup.enter="cambiarMensaje"
      />
      <div class="flex flex-col sm:flex-row gap-2 sm:gap-4 justify-center items-center mb-4">
        <button
          v-if="respuesta !== 'jhosep' && respuesta !== 'Jhosep'"
          class="bg-sky-800 cursor-pointer hover:bg-sky-900 hover:scale-110 transition duration-300 text-white p-2 sm:p-3 rounded w-full sm:w-auto"
          @click="cambiarMensaje"
        >Enviar...</button>
        <button
          v-if="respuesta === 'jhosep' || respuesta === 'Jhosep'"
          class="bg-sky-800 cursor-pointer hover:bg-sky-900 hover:scale-140 transition duration-300 text-white p-2 sm:p-3 rounded w-full sm:w-auto"
          @click="felicitarMensaje"
        >Aceptalo 😉</button>
      </div>
      <p v-if="respuesta !== 'jhosep' && respuesta !== 'Jhosep'" class="text-base sm:text-lg text-white text-center mb-2">{{ mensaje[mensajeIndex] }}</p>
      <p v-show="mostrarFelicitaciones" class="text-base sm:text-lg text-white text-center mb-2">{{ mensajeFelicitaciones }}</p>
      <reproductor-componente ref="reproductor" v-show="mostrarReproductor" />
    </div>
  </div>
</template>

<script setup>
    import { ref } from 'vue'
    import reproductorComponente from './reproductorComponente.vue';
    const reproductor = ref(null)
    const mostrarReproductor = ref(false)
    const mostrarFelicitaciones = ref(false)
    const respuesta = ref('')
    const mensajeIndex = ref('')
    const mensaje = [
    '¡Incorrecto! 🚫 No te preocupes, es una respuesta difícil si no tienes buen gusto. 😉',
    'Ese no es el camino. El camino correcto lleva a una persona mucho más increíble que esa. ✨',
    '¿En serio? 🤔 ¿Esa fue tu respuesta? Vaya, pensé que tenías mejor criterio. 🤦‍♂️',
    'La respuesta es tan obvia que casi me ofende que no la sepas. Inténtalo de nuevo, y esta vez, piensa con el corazón. ❤️‍🔥',
    '¡Uf, ni cerca! 😬 Parece que te hace falta un poco de... "iluminación". ✨💡',
    'Falso. ❌ La persona que buscas es la combinación perfecta de todas esas cualidades. ¡Sigue buscando! 🕵️‍♀️',
    '¡Error 404: Persona increíble no encontrada en tu respuesta! 🤖',
    '¡Casi! 🤏 Si "casi" fuera una victoria, ya serías un campeón. 🏆 Sigue intentando, aunque dudo que sirva de mucho. 😉',
    '¿Esa es tu respuesta? 😮 Qué atrevido. Y también, qué equivocado. 😅',
    '¡No! 🙅‍♀️ La respuesta es un secreto que solo los genios conocen. ¿Eres un genio? 🤔',
    'La persona que buscas es mucho más increíble que eso. Inténtalo otra vez, ¡tú puedes! 💪',
    '¡Incorrecto! Pero no te desanimes, incluso los mejores fallan a veces. 🌟',
    '¡Wow! Esa respuesta fue... creativamente incorrecta. 🎨❌',
    'Ni por casualidad. ☘️ La suerte no está de tu lado hoy. 🎲',
    '¡Ja! Esa respuesta demuestra una imaginación... interesante. 🧠💫',
    '¿Estás adivinando o tirando dardos a un tablero? 🎯 Porque fallaste el blanco. ❌',
    'Esa persona sería un impostor. La real es mucho más espectacular. 🌟',
    '¡Nop! 🙊 Parece que tu detector de awesomeness necesita calibrarse. ⚙️',
    'Incorrecto, pero te doy puntos por originalidad. 🎭❌',
    '¡Uy, no! 😬 Ese es el equivalente humano de un pantallazo azul. 💻🔵',
    'Si fuera así de fácil, no sería un desafío. 🧩 Sigue intentando!',
    '¡Fallo épico! ⚔️ Pero no te rindas, los héroes se levantan después de caer. 🦸‍♂️',
    'Esa respuesta tiene tanto sentido como un pulpo en un monopatín. 🐙🛹',
    '¡Incorrecto! 🔔 Pero suena bien para una campana de error. 🔕',
    'Ni frío ni caliente... ¡estás congelado! ❄️❌',
    ];
    const mensajeFelicitaciones = "Muy buenas noches, señorita. ¡Feliz cumpleaños! Espero que lo pases tan especial como lo eres tú (sí, te robé la frase). Sabes siempre he pensado que nací en el tiempo equivocado, pero desde que te conocí, pensé que no solo nací en el momento correcto, sino que no querría haber nacido en ningún otro instante que no me llevara a conocer a una persona tan random, loca, divertida, ingeniosa, inteligente y única como tú. Cuando me felicitaste tú, dijiste que nos conocemos hace poco, pero ahora nos conocemos hace un año y puedo asegurar que tampoco necesitaba tanto para decir que no solo como tu amistad, sino como tú muy, muy, pocos, como diría Reik, como aguja en un pajar JAJAJA. Me alegro mucho de haberte conocido Helen, me has ayudado más de lo que eres conciente y no quiero ni imaginar cómo sería si no te hubiera conocido porque sé que me hubiera vuelto loco acá y te deseo un muy feliz cumpleaños y que estés muy bien y feliz no solo hoy sino siempre, porque te lo mereces, eres una gran persona y te mereces lo mejor. Y Quiero que recuerdes esto siempre, incluso si ya no hablamos y no te lo pueda recordar, siempre recuerda que eres tan valiosa que... Feliz cumpleaños ✨🤍"

    function cambiarMensaje() {
        if (respuesta.value !== 'jhosep' || respuesta.value !== 'Jhosep') {
            mensajeIndex.value = Math.floor(Math.random() * mensaje.length)
        }
    }

    function felicitarMensaje(){
      if (reproductor.value && reproductor.value.togglePlay) {
          reproductor.value.togglePlay()
      }
      mostrarReproductor.value = true
      mostrarFelicitaciones.value = true
    }

</script>

<style scoped>
/* Mejoras para input y botones en pantallas pequeñas */
@media (max-width: 640px) {
  input {
    font-size: 15px;
    padding: 8px;
  }
  button {
    font-size: 15px;
    padding: 8px;
  }
  h2 {
    font-size: 18px;
  }
}
</style>
