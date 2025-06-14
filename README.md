# jubilant-succotash
CATRINA BOT MD OFICIAL 
catrina-bot/
├── src/
│   ├── comandos/
│   │   ├── juegoAdivinanumero.js
│   │   ├── piedraPapelTijera.js
│   │   └── beso.js
│   └── bot.js
├── package.json
└── README.md
module.exports = {
  nombre: 'adivina',
  ejecutar: (msg) => {
    const numero = Math.floor(Math.random() * 10) + 1;
    msg.reply(`Adivina un número del 1 al 10. Escribe #adivina [número] para intentar.`);
    // Podrías guardar el número secreto en una base de datos o en memoria si quieres que el juego continúe.
  }
};
const { Client, LocalAuth } = require('whatsapp-web.js');
const fs = require('fs');
const path = require('path');
const qrcode = require('qrcode-terminal');

const client = new Client({ authStrategy: new LocalAuth() });
const comandos = new Map();

// Cargar comandos automáticamente
const archivosComandos = fs.readdirSync(path.join(__dirname, 'comandos')).filter(f => f.endsWith('.js'));
for (const file of archivosComandos) {
  const comando = require(`./comandos/${file}`);
  comandos.set(comando.nombre, comando);
}

client.on('qr', qr => qrcode.generate(qr, { small: true }));
client.on('ready', () => console.log('CATRINA BOT MD OFICIAL listo!'));

client.on('message', async msg => {
  if (!msg.from.endsWith('@g.us')) return; // Solo grupos
  if (!msg.body.startsWith('#')) return;

  const partes = msg.body.slice(1).split(' ');
  const nombreComando = partes[0].toLowerCase();
  const comando = comandos.get