# Portfolio Lab: generador de portafolios de inversión con IA 📈

![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-4-646CFF?logo=vite&logoColor=white)
![Claude](https://img.shields.io/badge/IA-Claude_API-D97757)

Aplicación web que, a partir de una lista de activos (acciones, ETF, criptomonedas) y un **perfil de riesgo**, usa un modelo de lenguaje para generar un **análisis técnico por activo** y proponer **tres portafolios** (conservador, moderado y agresivo) con la distribución óptima del capital.

> Fork de [josesastoquea23/generateinvestmentportfolio](https://github.com/josesastoquea23/generateinvestmentportfolio). En este fork armé el proyecto para ejecutarlo con **Vite** (`package.json`, `vite.config.js`, `index.html`, `main.jsx`).

## Funcionalidades

- Ingreso libre de tickers (por ejemplo `AAPL, MSFT, BTC-USD, GLD`).
- Selección del perfil: 🛡️ **Conservador**, ⚖️ **Moderado** o 🚀 **Agresivo**.
- Por cada activo: señal tipo semáforo e indicadores **RSI, MACD, Bandas de Bollinger, SMA 50/200 y volumen**.
- Tres portafolios con su asignación porcentual y una **tesis de inversión** para el perfil elegido.
- Lectura robusta de la respuesta del modelo: si el JSON llega incompleto, el parser lo repara.

## Cómo funciona

```
Tickers + perfil ──► prompt estructurado ──► Claude (Messages API) ──► JSON ──► dashboard
```

El componente principal (`portfolio-analyzer.jsx`) le pide al modelo un JSON con una estructura fija (activos, indicadores, portafolios y asignaciones que suman 1.0) y lo convierte en pestañas de resumen, análisis técnico y portafolios.

## Cómo ejecutarlo

```bash
git clone https://github.com/yeimy07/generateinvestmentportfolio.git
cd generateinvestmentportfolio
npm install
npm run dev
```

> ⚠️ **Importante:** el componente llama a `https://api.anthropic.com/v1/messages` directamente desde el navegador y **sin clave de API**, porque se diseñó para ejecutarse como *artifact* dentro de Claude.ai. Para usarlo de forma independiente hace falta un **backend o proxy** que agregue la clave (`x-api-key`) del lado del servidor. Nunca pongas la clave en el código del frontend.

## Estructura

```
generateinvestmentportfolio/
├── portfolio-analyzer.jsx   # Componente principal: formulario, llamada a la IA y dashboard
├── main.jsx                 # Punto de entrada de React
├── index.html
├── vite.config.js
└── package.json
```

## Aviso

Proyecto educativo. Los análisis los genera un modelo de IA y **no constituyen asesoría financiera**.

## Créditos

- Componente original: [@josesastoquea23](https://github.com/josesastoquea23)
- Configuración del proyecto con Vite: [@yeimy07](https://github.com/yeimy07)
