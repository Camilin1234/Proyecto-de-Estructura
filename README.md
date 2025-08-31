# Proyecto-de-Estructura
Avance Módulo de Rutas
El módulo de rutas está enfocado en mostrar trayectos logísticos básicos entre puntos clave de distintas ciudades, usando coordenadas geográficas para calcular distancias aproximadas. En esta primera fase, trabajamos con Bogotá y Medellín como ejemplo para validar el funcionamiento del sistema y dejar una base escalable a más ubicaciones.
Información que maneja el código
•	Ciudades registradas con coordenadas de inicio y destino.
•	Nombres de puntos de referencia para facilitar la interpretación de la ruta.
•	Distancia aproximada entre los puntos calculada en kilómetros.
Operaciones
•	Consultar rutas por ciudad para conocer los puntos de inicio y fin.
•	Calcular la distancia entre coordenadas usando la fórmula de Haversine.
•	Mostrar resultados en consola para pruebas rápidas y validación.
Limitaciones actuales
•	El módulo solo incluye dos ciudades de ejemplo.
•	No hay integración con mapas en tiempo real, tráfico ni niveles de seguridad aún.
•	La información de coordenadas está precargada y no se actualiza automáticamente.
Cronograma
<img width="675" height="262" alt="image" src="https://github.com/user-attachments/assets/aae994bd-379d-40d7-bd8a-ad2fecfd87e4" />



const rutas = {
  "Bogotá": {
    inicio: { nombre: "Centro Bogotá", lat: 4.6097, lon: -74.0817 },
    destino: { nombre: "Funza", lat: 4.7169, lon: -74.2111 }
  },
  "Medellín": {
    inicio: { nombre: "Parque Berrío", lat: 6.2518, lon: -75.5636 },
    destino: { nombre: "Envigado", lat: 6.1759, lon: -75.5917 }
  }
};

function obtenerRuta(ciudad) {
  if (!rutas[ciudad]) {
    console.log(`No se encontró información para ${ciudad}.`);
    return null;
  }
  const datos = rutas[ciudad];
  console.log(`Ruta en ${ciudad}:`);
  console.log(`- Inicio: ${datos.inicio.nombre} (${datos.inicio.lat}, ${datos.inicio.lon})`);
  console.log(`- Destino: ${datos.destino.nombre} (${datos.destino.lat}, ${datos.destino.lon})`);
  return datos;
}

function calcularDistancia(lat1, lon1, lat2, lon2) {
  const R = 6371;
  const rad = Math.PI / 180;
  const dLat = (lat2 - lat1) * rad;
  const dLon = (lon2 - lon1) * rad;
  const a = Math.sin(dLat / 2) ** 2 +
            Math.cos(lat1 * rad) * Math.cos(lat2 * rad) *
            Math.sin(dLon / 2) ** 2;
  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
  return (R * c).toFixed(2);
}

const ciudad = "Bogotá";
const datosRuta = obtenerRuta(ciudad);

if (datosRuta) {
  const distancia = calcularDistancia(
    datosRuta.inicio.lat, datosRuta.inicio.lon,
    datosRuta.destino.lat, datosRuta.destino.lon
  );
  console.log(`Distancia aproximada: ${distancia} km`);
}




Este código define un objeto llamado rutas donde cada ciudad tiene un punto de inicio y uno de destino con sus coordenadas. Primero, se llama a la función obtenerRuta, que busca la ciudad que indiquemos y muestra la información de sus puntos en consola. Después, se usa calcularDistancia, que aplica la fórmula de Haversine para calcular la distancia aproximada en kilómetros entre dos coordenadas. Finalmente, imprime el resultado en consola.
En este avance se trabaja solo con Bogotá y Medellín, pero el sistema está hecho para crecer fácilmente y agregar más rutas, así como datos de tráfico y seguridad en próximas fases.


