# Bitácora de auditoría
Estudiante: Marlon Stiven Ramos Vásquez
Repositorio: https://github.com/stivenramos31/astro-performance-MarlonRamos
URL publicada: [https://astro-performance-marlon-ramos.vercel.app/]
Fecha: 1 de octubre de 2026

## 1. Medición inicial
| Indicador | Resultado inicial | Observación |
| :--- | :--- | :--- |
| Desempeño | [Puntaje general] 
| LCP | [Valor en segundos] 
| CLS | [Valor de CLS] 
| INP | [Valor en ms] 
| Bytes transferidos / peso total | [Peso total] 

### Tres hallazgos principales
1. **Hallazgo:** El JavaScript bloquea el renderizado principal.[cite: 4]
   **Evidencia:** Lighthouse sugiere "Elimina los recursos que bloqueen el renderizado".[cite: 4]
   **Recurso o archivo relacionado:** `script.js` en el `<head>` del `index.html`.[cite: 4, 8]
2. **Hallazgo:** Cambios acumulativos de diseño (CLS) por imágenes sin tamaño.[cite: 4]
   **Evidencia:** Elementos de imagen marcados en el diagnóstico de CLS.[cite: 4]
   **Recurso o archivo relacionado:** Las etiquetas `<img>` no tienen `width` ni `height`.[cite: 4, 8]
3. **Hallazgo:** Carga de imágenes fuera de pantalla y formatos no optimizados.[cite: 4]
   **Evidencia:** Lighthouse recomienda "Aplazar la carga de imágenes ocultas" y mejorar el formato.[cite: 4]
   **Recurso o archivo relacionado:** Las imágenes de Cloudinary en la sección archivo cargan de inmediato y en JPEG.[cite: 4, 10]

## 2. Hipótesis antes de modificar
1. **Si cambio** la etiqueta del script agregando `defer` **espero mejorar** el LCP **porque** el navegador no detendrá el análisis del HTML para ejecutar JS.[cite: 4]
2. **Si cambio** las etiquetas `<img>` agregando atributos `width` y `height` **espero mejorar** el CLS **porque** el navegador reservará el espacio exacto antes de la descarga.[cite: 4]
3. **Si cambio** las imágenes de las tarjetas añadiendo `loading="lazy"` y parámetros de Cloudinary (`f_auto,q_auto`) **espero mejorar** los bytes iniciales transferidos **porque** serviremos formatos modernos (WebP) y solo cuando entren al viewport.