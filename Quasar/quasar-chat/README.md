# Quasar App (quasar-chat)

Aplicacion web  de un chat construiida mediante Vue 3 + Quasar + Vite + Firebase 9
Con autentificacion mediante la cuenta de google
## Install the dependencies
```bash
yarn
# or
npm install
```

### inicio aplicacion modo desarolollo (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```
ó
```bash
npm RUN dev
```

### construccion de la aplicacion para produccion
```bash
quasar build
```
ó
```bash
npm RUN build
```

### Despliegue firebase google
Despues de tener configurado el archivo de entorno (toma de ejemplo .env_example) con la informacion de firebase hacemos login a la cuenta de google
```bash
firebase login
```
inicializa el projecto
```bash
firebase init
```
y por ultimo lo despliegas con el siguente comando:
```bash
firebase deploy
```
### Customize the configuration
See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-vite/quasar-config-js).
