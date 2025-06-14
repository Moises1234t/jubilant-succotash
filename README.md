# jubilant-succotash
CATRINA BOT MD OFICIAL 
mkdir whatsapp-bot
cd whatsapp-bot
npm init -y
npm install whatsapp-web.js qrcode-terminal
const { Client, LocalAuth } = require('whatsapp-web.js');
const qrcode = require('qrcode-terminal');

const client = new Client({
    authStrategy: new LocalAuth()
});

client.on('qr', (qr) => {
    qrcode.generate(qr, { small: true });
});

client.on('ready', () => {
    console.log('Bot listo!');
});

// Responde en grupos y privados
client.on('message', async msg => {
    if (msg.body === '!hola') {
        // Si el mensaje viene de un grupo
        if (msg.from.endsWith('@g.us')) {
            msg.reply('¡Hola grupo!');
        } else {
            // Mensaje privado
            msg.reply('¡Hola, este es un mensaje privado!');
        }
    }
});

client.initialize();