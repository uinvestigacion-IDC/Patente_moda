# Maniquí 3D de patronaje básico

Aplicativo web de un solo archivo HTML (`maniqui-patronaje.html`) que traza patrones de prendas a partir de medidas corporales, los muestra sobre un maniquí 3D articulado de mujer, hombre o niño, simula la caída de la tela en movimiento y exporta los moldes a escala 1:1 en PDF y DXF.

- Versión: 14 de octubre de 2026
- Autor: Mg. Mario Rafael Quiroz Martínez · IDC Diseño & Comunicación, Unidad de Investigación
- Base de trazo: SENA (2011), *Manual de patronaje básico e interpretación de diseños*; *Transformación de patrones básicos* (2014)

## Uso

1. Abra `maniqui-patronaje.html` en un navegador de escritorio actualizado (Chrome, Edge, Firefox o Safari). Requiere conexión a internet para cargar las bibliotecas desde jsDelivr.
2. Elija cuerpo, rango de edad y talla, o escriba estatura, peso y medidas propias.
3. Elija prenda superior e inferior, escote, cuello, manga y tela en el panel «2 · Prendas».
4. Revise la prenda en reposo, marcha, giro, sentado y brazos arriba.
5. Ajuste largo, ancho, vuelo, holgura o desahogo por pieza en la mesa de patronaje.
6. Exporte el PDF 1:1, el DXF o la ficha JSON.

La guía de 12 pasos de la sección «Guía» recorre la interfaz con resaltado de cada control.

## Prendas disponibles

| Cuerpo | Superior | Inferior |
| --- | --- | --- |
| Mujer | Blusa base (corpiño), chaqueta, vestido, vestido corte imperio, de talle alto, de cintura baja y evasé | Falda de una pinza, de dos pinzas, circular, circular, semicircular y doble circular (Guzmán), pantalón base |
| Hombre | Camisa clásica, chaqueta | Pantalón base, bóxer |
| Infantil | Patrón básico | Pantalón base, falda circular, falda semicircular, bóxer |

Con cualquier cuerpo se puede agregar un calcetín.

## Transformaciones de diseño

Tomadas de *Transformación de patrones básicos* (2014). Los valores con * son criterio del modelo porque el manual no da una cifra; la interfaz los marca igual.

| Elemento | Opciones | Páginas | Aplicación |
| --- | --- | --- | --- |
| Escote | Redondo, cuadrado, en V, ojal | 3–4 | Solo en prendas de base corpiño |
| Cuello | Sport, chino, camisero con pie | 6–8 | Prendas superiores |
| Manga | Corta*, fruncida arriba, fruncida abajo, campana* | 13–16 | Prendas con manga |

Valores de escote: redondo, espalda +1 cm sobre el hombro y −2 cm de profundidad, delantero +1 cm* y −4 cm; cuadrado, igual con esquina a 5 cm del centro delantero; en V, delantero −7 cm en línea recta; ojal, 7 cm sobre el hombro, espalda −2 cm y delantero −3 cm.

## Funciones

- Holgura por pieza y desahogo en cinco niveles por tipo de prenda: blusa de 2 a 10 cm, vestido y chaqueta de 4 a 12 cm, falda de 0 a 8 cm, pantalón de 0 a 6 cm. Se suma un ajuste por grosor de tela de −2 a +4 cm.
- Deducción de medidas de largo desde la estatura (solo cuerpo de mujer).
- Consumo de tela para anchos de 80 a 280 cm, por área y por acomodo de piezas en franjas, con desperdicio configurable y piezas al bies giradas 45°.
- Secciones de color por pieza (canesú, cortes, vivos) visibles en el plano, en 3D y en el PDF.
- Procedimiento de trazo paso a paso según el manual SENA.
- Interfaz en español, inglés, portugués, francés, alemán e italiano. Los pasos del procedimiento SENA se mantienen en español.
- Tema claro y oscuro con botones en la cabecera; la elección se guarda en el navegador.

## Simulación de la tela

| Parámetro | Valor |
| --- | --- |
| Integración | Verlet a 1/60 s, máximo 2 subpasos por fotograma, gravedad 9.81 m/s² |
| Malla | Filas cada 1 cm; 64 columnas (32 en mangas y perneras) |
| Unión al esqueleto | Dos huesos por vértice; peso al muslo × (0.35 + 0.65·s(θ)), s de 0 en 20° a 1 en 70° de flexión |
| Colisión | Esferas con el perfil de muslos y piernas, margen 0.012 m; salida hacia la posición sobre el cuerpo |
| Pliegues | A = (λ/π)·√c, desplazados hacia afuera del cuerpo |
| Telas | Popelina 115 g/m², gasa 60 g/m², jersey 180 g/m², denim 340 g/m² |
| Rendimiento medido | Unos 10 ms por fotograma en navegador de escritorio |

La física y la intensidad de los pliegues se pueden desactivar o regular en el panel de prendas.

## Salidas

| Formato | Contenido |
| --- | --- |
| PDF | Moldes a escala 1:1 en hojas A4, Carta, A3 o A0, con cuadro de control de 5 × 5 cm, datos del desarrollador y armado por hojas |
| DXF | AutoCAD R12 (AC1009) en milímetros, entregado dentro de un ZIP con un archivo LEEME. Capas: CORTE, COSTURA, PINZAS, REFERENCIAS, HILO, DOBLEZ, PIQUETES, TALADROS (círculos de 2.5 mm de radio) y TEXTO |
| JSON | Ficha técnica del boceto: cuerpo, talla, medidas, prendas, opciones de diseño, modificaciones por pieza y datos del desarrollador |

Antes de cortar, mida el cuadro de control del PDF impreso: debe medir 5 × 5 cm.

## Ficha JSON

Ejemplo mínimo:

```json
{
  "version": 1,
  "nombre": "Boceto 01 · Blusa con canesú y falda en A",
  "desarrollador": {
    "nombre": "Mg. Mario Rafael Quiroz Martínez",
    "institucion": "IDC Diseño & Comunicación · Unidad de Investigación",
    "rol": "Desarrollador del proyecto y autor de la ficha",
    "fecha": "2026-10-14"
  },
  "cuerpo": "mujer",
  "rango": "18–29",
  "talla": 10,
  "medidas": { "estatura": 162, "peso": 56, "busto": 93, "cintura": 69, "cadera": 97 },
  "prendas": {
    "superior": "corpino",
    "inferior": "falda1",
    "manga": true,
    "escote": "v",
    "cuello": "ninguno",
    "manga_tipo": "base"
  },
  "piezas": {
    "delantero": {
      "color": "#2E5E8C",
      "secciones": [{ "nombre": "Canesú", "tipo": "banda-h", "desde": 0, "hasta": 13, "color": "#E8D9B5" }]
    },
    "delantero-falda": { "color": "#B5523B", "vuelo": 10, "largo": -6 }
  }
}
```

Valores admitidos:

- `prendas.escote`: `base`, `redondo`, `cuadrado`, `v`, `ojal`.
- `prendas.cuello`: `ninguno`, `sport`, `chino`, `camisero`.
- `prendas.manga_tipo`: `base`, `corta`, `fruncidaArriba`, `fruncidaAbajo`, `campana`.
- Claves de `piezas`: `delantero`, `espalda`, `manga`, `puno`, `delantero-falda`, `posterior`, `delantero-pant`, `posterior-pant`, `circular`, `calcetin`, `cuello`, `pie-cuello`.
- Colores: hexadecimal de seis dígitos (`#RRGGBB`).

## Estructura del código fuente

El archivo publicado se genera con `build.py`, que inserta en `pagina.html` los módulos y el logotipo:

| Archivo | Contenido |
| --- | --- |
| `pagina.html` | Interfaz, estado, maniquí 3D, plano, PDF, ficha JSON y tema |
| `patrones.js` | Trazo de piezas (SENA y transformaciones de 2014), holgura, marcas técnicas y consumo de tela |
| `tela3d.js` | Malla de la prenda, unión al esqueleto, simulación, colisiones, pliegues, escote y cuello 3D |
| `i18n.js` | Textos en seis idiomas |
| `extras.js` | Consumo, exportación DXF y ZIP, guía de uso e idioma |
| `build.py` | Ensambla `maniqui-patronaje.html` y una copia de prueba con bibliotecas locales |

Bibliotecas, con versión fija: Three.js 0.170 (OrbitControls, CSS2DRenderer), anime.js 4.5 y jsPDF 2.5.1.

## Pruebas realizadas

- 38 combinaciones de cuerpo y prenda con exportación a PDF, DXF y acomodo de piezas: sin errores de consola.
- DXF abierto con `ezdxf` en modo de recuperación: 0 errores.
- Interfaz en inglés y alemán; tema claro y oscuro.

## Limitaciones

- El escote solo se aplica a prendas de base corpiño.
- El cuello 3D sigue la base del cuello aunque el escote esté bajado; la pieza plana sí corresponde al escote elegido.
- Los nombres compuestos de las mangas de diseño quedan en español en los otros idiomas.
- No incluye mangas kimono, raglán ni de dos piezas, vestido princesa ni traslado de pinzas.
- Los módulos de LED y material reflectante quedan fuera del alcance del patronaje básico.

## Propiedad intelectual

El procedimiento implementado en este aplicativo es objeto de una solicitud de patente de invención en preparación ante Indecopi. No publique el código, el archivo ni el enlace del aplicativo antes de presentar la solicitud. Todos los derechos reservados.

## Fuentes

- SENA (2011). *Manual de patronaje básico e interpretación de diseños*. Centro de Manufactura en Textiles y Cuero, Bogotá.
- *Transformación de patrones básicos* (2014), pp. 3–8 y 13–16.
- Jakobsen, T. (2001). *Advanced Character Physics*. Game Developers Conference.
- Repositorio Blackmvmba88/Patronaje (licencia MIT): fórmula de la falda circular r = cintura/2π y consumo por área.
