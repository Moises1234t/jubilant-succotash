# jubilant-succotash
CATRINA BOT MD OFICIAL 
catrina-bot MD/ 
module.exports = {
    nombre: 'adivina',
    ejecutar: (msg) => {
        // Extrae el número del mensaje
        const partes = msg.body.trim().split(' ');
        const intento = parseInt(partes[1]);
        const numeroSecreto = Math.floor(Math.random() * 10) + 1;

        if (!intento || isNaN(intento)) {
            msg.reply('Debes escribir un número. Ejemplo: #adivina 5');
            return;
        }

        if (intento === numeroSecreto) {
            msg.reply(`¡Felicidades! Adivinaste el número secreto (${numeroSecreto}) 🎉`);
        } else {
            msg.reply(`¡Ups! El número secreto era ${numeroSecreto}. Intenta de nuevo.`);
        }
    }
};
module.exports = {
    nombre: 'ppt', // El comando sería #ppt piedra, #ppt papel, #ppt tijera
    ejecutar: (msg) => {
        const opciones = ['piedra', 'papel', 'tijera'];
        const partes = msg.body.trim().split(' ');
        const eleccionUsuario = partes[1] ? partes[1].toLowerCase() : '';
        if (!opciones.includes(eleccionUsuario)) {
            msg.reply('Debes elegir: piedra, papel o tijera. Ejemplo: #ppt piedra');
            return;
        }
        const eleccionBot = opciones[Math.floor(Math.random() * 3)];
        let resultado = '';
        if (eleccionUsuario === eleccionBot) resultado = '¡Empate!';
        else if (
            (eleccionUsuario === 'piedra' && eleccionBot === 'tijera') ||
            (eleccionUsuario === 'papel' && eleccionBot === 'piedra') ||
            (eleccionUsuario === 'tijera' && eleccionBot === 'papel')
        ) resultado = '¡Ganaste! 🎉';
        else resultado = '¡Perdiste! 😢';

        msg.reply(`Tú: ${eleccionUsuario}\nBot: ${eleccionBot}\n${resultado}`);
    }
};
module.exports = {
    nombre: 'dado',
    ejecutar: (msg) => {
        const resultado = Math.floor(Math.random() * 6) + 1;
        msg.reply(`🎲 El dado cayó en: ${resultado}`);
    }
};
module.exports = {
    nombre: 'beso',
    ejecutar: (msg) => {
        if (!msg.mentionedIds || msg.mentionedIds.length === 0) {
            msg.reply('Menciona a quién quieres darle un beso. Ejemplo: #beso @usuario');
            return;
        }
        msg.reply(`💋 ${msg.author} le da un beso a ${msg.mentionedIds.join(', ')}!`);
    }
};