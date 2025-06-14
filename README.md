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