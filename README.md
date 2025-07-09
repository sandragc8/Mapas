# 🗺️ Generador y Visualizador de Mapas de Direcciones Madrid

Este proyecto permite generar direcciones aleatorias en Madrid usando OpenAI y visualizarlas en un mapa interactivo usando MapTiler. El sistema consta de dos partes principales: un notebook de Jupyter para generar las direcciones y un visualizador web para mostrarlas en el mapa.

## 🚀 ¿Cómo funciona?

1. **Generación de direcciones**: El notebook `peticiones.ipynb` utiliza la API de OpenAI para generar direcciones aleatorias en Madrid
2. **Geocodificación y filtrado**: Las direcciones se validan y se excluyen automáticamente aquellas que se salen del radio de 20 km del centro de Madrid
3. **Visualización**: El archivo `index.html` muestra las direcciones en un mapa interactivo con mapa de calor

## 📋 Requisitos previos

- Python 3.7 o superior
- Navegador web moderno
- API Key de OpenAI
- API Key de MapTiler

## 🔧 Configuración

### 1. Claves API necesarias

#### OpenAI API Key
1. Obtén tu API key en [OpenAI Platform](https://platform.openai.com/api-keys)
2. Crea un archivo `template.env` en la carpeta del proyecto
3. Añade tu clave:
```
OPENAI_API_KEY=tu_clave_aqui
```

#### MapTiler API Key
1. Obtén tu API key gratuita en [MapTiler](https://www.maptiler.com/cloud/)
2. Edita el archivo `index.html` y reemplaza `TU_API_KEY_AQUI` con tu clave en la línea 204:
```javascript
const MAPTILER_API_KEY = 'tu_clave_maptiler_aqui';
```

### 2. Instalación de dependencias

Instala las librerías de Python necesarias:

```bash
pip install pandas openai python-dotenv tqdm openpyxl
```

## 🏃‍♂️ Cómo ejecutar el proyecto

### Paso 1: Generar direcciones

1. Abre `peticiones.ipynb` en Jupyter Notebook o VS Code
2. Ejecuta todas las celdas del notebook
3. El sistema generará automáticamente un archivo Excel con direcciones aleatorias de Madrid
4. Las direcciones se obtienen mediante peticiones a OpenAI con prompts optimizados para generar direcciones reales y variadas

### Paso 2: Visualizar en el mapa

1. Inicia un servidor web local en la carpeta del proyecto:

```bash
# Usando Python 3
python -m http.server 8000

# O usando Python 2
python -m SimpleHTTPServer 8000

# O usando Node.js (si tienes npx instalado)
npx http-server

# O usando PHP (si tienes PHP instalado)
php -S localhost:8000
```

2. Abre tu navegador y ve a: `http://localhost:8000`
3. El mapa se cargará automáticamente y mostrará las direcciones generadas

## 📊 Archivos incluidos

- **`peticiones.ipynb`**: Notebook para generar direcciones usando OpenAI
- **`index.html`**: Visualizador de mapa interactivo
- **`direcciones_madrid_100.xlsx`**: Ejemplo con 100 direcciones
- **`direcciones_madrid_1000.xlsx`**: Ejemplo con 1000 direcciones

## 🎛️ Personalización

### Cambiar el archivo Excel
Para usar un archivo Excel diferente, edita la línea 208 en `index.html`:
```javascript
const EXCEL_FILE_PATH = 'tu_archivo.xlsx';
```

### Ajustar el número de direcciones
En el notebook `peticiones.ipynb`, modifica la variable:
```python
NUMERO_DIRECCIONES = 1000  # Cambia este número
```

### Modificar el radio de exclusión
Las direcciones que se encuentren a más de 20 km del centro de Madrid se excluyen automáticamente. Para cambiar este radio, edita la línea 214 en `index.html`:
```javascript
const MAX_RADIUS_KM = 20;  // Cambia el radio en kilómetros
```

## 🌟 Características

- ✅ Generación paralela de direcciones con control de hilos
- ✅ Filtrado automático por radio geográfico (20 km)
- ✅ Mapa de calor interactivo
- ✅ Geocodificación automática
- ✅ Panel lateral con lista de direcciones
- ✅ Captura de pantalla del mapa
- ✅ Diseño responsive para móviles
- ✅ Manejo de errores y reintentos automáticos

## 🔍 Detalles técnicos

### Sistema de filtrado geográfico
El sistema utiliza la fórmula de Haversine para calcular la distancia entre cada dirección geocodificada y el centro de Madrid. Las direcciones que excedan los 20 km de radio se excluyen automáticamente para mantener la coherencia geográfica.

### Optimización de peticiones
- Máximo 5 hilos concurrentes para evitar límites de la API
- Sistema de reintentos automáticos (hasta 5 intentos)
- Delays configurables entre peticiones
- Temperatura alta (0.9) para mayor variabilidad en las direcciones

## 🐛 Solución de problemas

### Error: "No se pudo cargar el archivo Excel"
- Verifica que el archivo Excel esté en la misma carpeta que `index.html`
- Asegúrate de estar ejecutando un servidor web local

### Error: "API Key no válida"
- Verifica que las API keys estén correctamente configuradas
- Para OpenAI: revisa el archivo `template.env`
- Para MapTiler: revisa la línea 204 en `index.html`

### El mapa no se carga
- Verifica tu conexión a internet
- Revisa la consola del navegador para errores
- Asegúrate de que la API key de MapTiler sea válida
