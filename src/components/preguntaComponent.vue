<template>
    <div class="text-white flex flex-col items-center space-y-4 p-4 bg-gradient-to-br from-lime-700 via-lime-600 to-yellow-300 min-h-screen justify-center items-center">
        <h2 class="text-2xl font-bold">¿Quién es la persona más increíble, inteligente, amable, sorprendente y especial que conoces?</h2>
        <label for="respuesta" class="text-lg">Tu respuesta:</label>
        <input class="border border-white-800 outline-none p-2 rounded" id="respuesta" v-model="respuesta" type="text" @keyup.enter="cambiarMensaje" />
        <button class="bg-green-900 cursor-pointer hover:bg-green-700 hover:scale-120 transition duration-300 text-white p-2 rounded" @click="cambiarMensaje">Enviar</button>
        <p v-if="respuesta === 'yisus' || respuesta === 'Yisus'" class="text-lg">Correcto!</p>
        <p v-else class="text-lg">{{ mensaje[mensajeIndex] }}</p>
    </div>
</template>

<script setup>
    import { ref } from 'vue'
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
    function cambiarMensaje() {
        if (respuesta.value !== 'yisus' || respuesta.value !== 'Yisus') {
            mensajeIndex.value = Math.floor(Math.random() * mensaje.length)
        }
    }
</script>
