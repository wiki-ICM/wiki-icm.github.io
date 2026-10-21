# Aportar material

Comparte apuntes, guías, evaluaciones o resúmenes para ayudar a otros estudiantes de Ingeniería Civil Matemática. Puedes usar este formulario sin una cuenta de GitHub.

[Ir al formulario](#enviar-un-archivo){ .md-button .md-button--primary }
[Explorar el material existente](material.md){ .md-button }

## Antes de enviar

- Revisa la carpeta de la asignatura para evitar duplicados.
- Comparte material propio o que tengas permiso para distribuir. No incluyas datos personales de otras personas.
- Usa un nombre descriptivo, por ejemplo: `Calculo-I_Guia-03_2024.pdf`. Si incluye soluciones, indícalo en el nombre.
- Comprueba que el archivo se abra y sea legible.

## Cómo completar el aporte

1. **Año de la carrera:** el nivel al que corresponde el ramo, no el año del documento. También puedes elegir «Electivos» u «Otros».
2. **Ramo / área:** selecciona la asignatura o el área correspondiente.
3. **Datos adicionales:** para electivos, indica si es obligatorio u opcional cuando se solicite y escribe el nombre del ramo. Para «Otros», escribe también el nombre del ramo.
4. **Año del material:** el año en que se elaboró o utilizó el documento, por ejemplo, 2024. El formulario admite desde 2010 hasta el año actual.
5. **Archivo:** arrástralo a la zona de envío o selecciónalo haciendo clic. Envía un archivo a la vez y espera el mensaje antes de continuar.

Por ejemplo, para una guía de Cálculo I de 2024, elige **1er Año → Calculo I** y escribe **2024** en «Año Material».

## Enviar un archivo

El envío comienza al seleccionar o soltar el archivo, una vez completados los datos.

<div class="form-aportes">
  <div class="campo-aporte">
    <label for="select-ano">Año Carrera:</label>
    <select id="select-ano">
      <option value="">Selecciona...</option>
      <option value="1er Año">1er Año</option>
      <option value="2do Año">2do Año</option>
      <option value="3er Año">3er Año</option>
      <option value="4to Año">4to Año</option>
      <option value="5to Año">5to Año</option>
      <option value="6to Año">6to Año</option>
      <option value="Electivos">Electivos</option>
      <option value="Otros">Otros</option>
    </select>
  </div>

  <div class="campo-aporte">
    <label for="select-ramo">Ramo / Área:</label>
    <select id="select-ramo" disabled>
      <option value="">Primero elige un año...</option>
    </select>
  </div>

  <!-- Desplegable Obligatorio / Opcional -->
  <div class="campo-aporte" id="container-tipo-electivo" style="display: none;">
    <label for="select-tipo-electivo">Tipo de Electivo:</label>
    <select id="select-tipo-electivo">
      <option value="">Selecciona...</option>
      <option value="Obligatorio">Obligatorio</option>
      <option value="Opcional">Opcional</option>
    </select>
  </div>

  <!-- Campo para ingresar nombre libre -->
  <div class="campo-aporte" id="container-nombre-ramo" style="display: none;">
    <label for="input-nombre-ramo">Nombre del Ramo:</label>
    <input type="text" id="input-nombre-ramo" placeholder="Ej: Elementos Finitos">
  </div>

  <div class="campo-aporte">
    <label for="input-ano-material">Año Material:</label>
    <input type="number" id="input-ano-material" placeholder="Ej: 2024">
  </div>
</div>

<div id="zona-arrastre" role="button" tabindex="0" aria-label="Seleccionar archivo para aportar" aria-describedby="estado-aporte">
  <svg class="icono-subida" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path></svg><br>
  <strong>Arrastra el material nuevo aquí o haz clic para buscarlo</strong><br>
  <span style="font-size: 0.9em; color: #666;">(Llena todos los datos arriba primero)</span>
</div>

<input type="file" id="input-archivo" style="display: none;">
<p id="estado-aporte" role="status" aria-live="polite"></p>
<noscript>Activa JavaScript para usar el formulario de aportes.</noscript>


## Después del envío

El formulario envía el archivo al servicio de Google usado por el proyecto. El mensaje de envío **no confirma que el archivo se haya guardado ni publicado**: el navegador no puede leer la respuesta de ese servicio.

Si aparece un error de conexión, conserva tu archivo y vuelve a intentarlo cuando recuperes la conexión. Si ya viste el mensaje de envío, revisa la carpeta de la asignatura antes de repetirlo para evitar duplicados.

## ¿No encuentras tu ramo o quieres corregir un enlace?

Puedes [abrir una propuesta o reportar un problema en GitHub](https://github.com/wiki-ICM/wiki-icm.github.io/issues). Necesitas una cuenta de GitHub para hacerlo. Indica la página, la asignatura y qué falta o debe corregirse; evita incluir datos personales.
