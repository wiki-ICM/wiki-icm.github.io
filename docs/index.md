#  :material-book: Wiki-ICM 

<p align="center">
  <img src="assets/imagen.png" alt="Logo Wiki-ICM" width="400">
</p>

<style>
  /* Estilos para embellecer y hacer responsiva la interfaz */
  .bienvenida-icm {
    text-align: center;
    max-width: 800px;
    margin: 0 auto 40px auto;
    font-size: 1.1em;
    color: #444;
  }
  .form-aportes {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
    align-items: flex-start;
    margin-bottom: 30px;
  }
  .campo-aporte {
    display: flex;
    flex-direction: column;
    text-align: left;
    min-width: 200px;
    flex: 1;
    max-width: 250px;
  }
  .campo-aporte label {
    font-weight: 600;
    font-size: 0.9em;
    color: #333;
    margin-bottom: 6px;
  }
  .campo-aporte select, .campo-aporte input {
    padding: 10px 12px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 1em;
    background-color: #fff;
    transition: all 0.3s ease;
  }
  .campo-aporte select:focus, .campo-aporte input:focus {
    border-color: #4051b5;
    outline: none;
    box-shadow: 0 0 8px rgba(64, 81, 181, 0.3);
  }
  #zona-arrastre {
    border: 3px dashed #4051b5; 
    border-radius: 12px; 
    padding: 50px 20px; 
    text-align: center; 
    background-color: rgba(64, 81, 181, 0.03); 
    margin: 20px auto; 
    cursor: pointer; 
    max-width: 700px;
    transition: all 0.3s ease;
  }
  #zona-arrastre:hover {
    background-color: rgba(64, 81, 181, 0.08);
  }
  .icono-subida {
    width: 48px; 
    height: 48px; 
    color: #4051b5; 
    margin-bottom: 10px;
  }
</style>

<div class="bienvenida-icm">
  Bienvenido a <strong>Wiki-ICM</strong>, un proyecto que busca recopilar material de estudio de la carrera <strong>Ingeniería Civil Matemática</strong>.
</div>

<!--
---

## 📂 Contenido

Los recursos están organizados siguiendo la malla curricular de la carrera:

* :material-school: **Malla Ingeniería Civil Matemática:** Apuntes, guías, certámenes pasados y libros  🛠 
* :material-plus-box: **Recursos Adicionales:** Otros ramos electivos o de otras carreras relacionadas.
## 🤝 ¿Cómo puedo ser parte?

Si tienes material para aportar puedes subirlo [aqui](https://drive.google.com/drive/folders/1DJBW6QvXpCti3Z_lFaO2_y4eFNrsqQ3G?usp=sharing), si tienes sugerencias o quieres ser parte del equipo de trabajo, puedes contactarnos a:

* :material-email: [jjunemann2024@udec.cl](mailto:jjunemann2024@udec.cl)
* :material-email: [bsandoval2018@udec.cl](mailto:bsandoval2018@udec.cl)
* :material-email: [pnahuelquin2024@udec.cl](mailto:pnahuelquin2024@udec.cl)
* :material-email: [femunoz2022@udec.cl](mailto:femunoz2022@udec.cl) -->

## Aportes 

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

  <!-- Ramo o Área ahora va primero -->
  <div class="campo-aporte">
    <label for="select-ramo">Ramo / Área:</label>
    <select id="select-ramo" disabled>
      <option value="">Primero elige un año...</option>
    </select>
  </div>

  <!-- Se despliega después de elegir Área (y se oculta si es Libre) -->
  <div class="campo-aporte" id="container-tipo-electivo" style="display: none;">
    <label for="select-tipo-electivo">Tipo de Electivo:</label>
    <select id="select-tipo-electivo">
      <option value="">Selecciona...</option>
      <option value="Obligatorio">Obligatorio</option>
      <option value="Opcional">Opcional</option>
    </select>
  </div>

  <!-- Se despliega para escribir el nombre de cualquier electivo u Otro -->
  <div class="campo-aporte" id="container-nombre-ramo" style="display: none;">
    <label for="input-nombre-ramo">Nombre del Ramo:</label>
    <input type="text" id="input-nombre-ramo" placeholder="Ej: Machine Learning">
  </div>

  <div class="campo-aporte">
    <label for="input-ano-material">Año Material:</label>
    <input type="number" id="input-ano-material" placeholder="Ej: 2024">
  </div>
</div>

<div id="zona-arrastre" onclick="document.getElementById('input-archivo').click();">
  <svg class="icono-subida" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path></svg><br>
  <strong>Arrastra el material nuevo aquí o haz clic para buscarlo</strong><br>
  <span style="font-size: 0.9em; color: #666;">(Llena todos los datos arriba primero)</span>
</div>

<input type="file" id="input-archivo" style="display: none;">

<script>
  const zonaArrastre = document.getElementById('zona-arrastre');
  const selectAno = document.getElementById('select-ano');
  const selectRamo = document.getElementById('select-ramo');
  const inputAnoMaterial = document.getElementById('input-ano-material');
  const inputArchivo = document.getElementById('input-archivo');
  
  const containerTipoElectivo = document.getElementById('container-tipo-electivo');
  const selectTipoElectivo = document.getElementById('select-tipo-electivo');
  const containerNombreRamo = document.getElementById('container-nombre-ramo');
  const inputNombreRamo = document.getElementById('input-nombre-ramo');
  
  const anoActual = new Date().getFullYear();
  inputAnoMaterial.placeholder = "Ej: " + anoActual;
  
  const ramosPorAno = {
    "1er Año": ["Calculo I","Calculo II","Algebra I","Algebra II","Fisica I","Fisica II","Quimica I","Quimica II","TRM I","Introduccion a la Innovacion"],
    "2do Año": ["Algebra III","Calculo III","Calculo IV","EDO","Programacion","ED2","Termodinamica"],
    "3er Año": ["Analisis Real I", "Optimiazacion I","Probabilidades","Mecanica de Fluidos","Analisis Numerico II","Analisis Real II","Electromagnetismo","Mecanica de Materiales","Optimizacion II","Inferencia Estadistica"],
    "4to Año": ["Analisis Funcional I","Analisis Numerico III","Regresion","Algebra IV","Formulacion y Evaluacion de Proyectos","Transferencia de Calor","Taller II"],
    "5to Año": ["Elementos Finitos","Procesos Estocasticos","Optimizacion III","Sistemas de Computacion","Principios de Ingeneria de Software","Taller III"],
    "6to Año": ["Sistemas Lineales Dinamicos","Introduccion aCiencias Ambientales","Gestion de Empresas"],
    "Electivos": ["Numerico","Discreta","Optimizacion","Estadistica","Libre"],
    "Otros": ["Licenciatura en Matematicas","Informatica","Extra"]
  };

  // Función para estandarizar textos (eliminar tildes, quitar espacios múltiples y capitalizar)
  function normalizarTexto(texto) {
    return texto.trim()
                .normalize("NFD")
                .replace(/[\u0300-\u036f]/g, "") // Remueve tildes
                .replace(/\s+/g, " ")            // Normaliza espacios
                .toLowerCase()
                .replace(/\b\w/g, l => l.toUpperCase()); // Mayúscula inicial por palabra
  }

  // Función que controla qué campos adicionales se muestran según el Año y Área seleccionados
  function actualizarVisibilidadCampos() {
    const ano = selectAno.value;
    const ramo = selectRamo.value;

    // Tipo de Electivo (Obligatorio/Opcional) se muestra si es Electivo, ya eligió un área, y NO es Libre
    if (ano === "Electivos" && ramo !== "" && ramo !== "Libre") {
      containerTipoElectivo.style.display = 'flex';
    } else {
      containerTipoElectivo.style.display = 'none';
      selectTipoElectivo.value = ''; // Limpiar
    }

    // Nombre del Ramo de ingreso manual: se muestra para CUALQUIER electivo y para OTROS (si ya eligieron Área)
    if ((ano === "Electivos" && ramo !== "") || (ano === "Otros" && ramo !== "")) {
      containerNombreRamo.style.display = 'flex';
    } else {
      containerNombreRamo.style.display = 'none';
      inputNombreRamo.value = ''; // Limpiar
    }
  }

  selectAno.addEventListener('change', (e) => {
    const anoSeleccionado = e.target.value;
    selectRamo.innerHTML = '<option value="">Selecciona ramo...</option>';

    if (anoSeleccionado && ramosPorAno[anoSeleccionado]) {
      selectRamo.disabled = false;
      ramosPorAno[anoSeleccionado].forEach(ramo => {
        const opcion = document.createElement('option');
        opcion.value = ramo;
        opcion.textContent = ramo;
        selectRamo.appendChild(opcion);
      });
    } else {
      selectRamo.disabled = true;
      selectRamo.innerHTML = '<option value="">Primero elige un año...</option>';
    }
    actualizarVisibilidadCampos();
  });

  selectRamo.addEventListener('change', actualizarVisibilidadCampos);

  zonaArrastre.addEventListener('dragover', (e) => {
    e.preventDefault();
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.15)';
  });

  zonaArrastre.addEventListener('dragleave', () => {
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.03)';
  });

  zonaArrastre.addEventListener('drop', (e) => {
    e.preventDefault();
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.03)';
    const file = e.dataTransfer.files[0];
    if (file) procesarArchivo(file);
  });

  inputArchivo.addEventListener('change', (e) => {
    const file = e.target.files[0];
    if (file) procesarArchivo(file);
    inputArchivo.value = ''; 
  });

  function procesarArchivo(file) {
    const anoMatValue = parseInt(inputAnoMaterial.value);
    
    // Validación de campos básicos
    if (!selectAno.value || !selectRamo.value || !inputAnoMaterial.value) {
      mostrarError('Faltan datos por llenar.');
      return;
    }

    // Validación si se muestra el campo "Obligatorio u Opcional"
    if (containerTipoElectivo.style.display === 'flex' && !selectTipoElectivo.value) {
      mostrarError('Falta seleccionar si el electivo es Obligatorio u Opcional.');
      return;
    }

    // Validación si se muestra el campo "Nombre del Ramo" manual
    if (containerNombreRamo.style.display === 'flex' && !inputNombreRamo.value.trim()) {
      mostrarError('Falta ingresar el nombre del ramo.');
      return;
    }

    if (anoMatValue < 2010 || anoMatValue > anoActual) {
      mostrarError('El año del material debe ser entre 2010 y ' + anoActual + '.');
      return;
    }

    // Preparar el nombre final del ramo (Normalizado si fue ingreso manual)
    let ramoFinal = selectRamo.value;
    if (containerNombreRamo.style.display === 'flex') {
      ramoFinal = normalizarTexto(inputNombreRamo.value);
    }

    zonaArrastre.innerHTML = '<svg class="icono-subida" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path></svg><br><strong>Subiendo archivo...</strong>';

    const reader = new FileReader();
    reader.onload = function(event) {
      const base64Data = event.target.result.split(',')[1];
      
      const formData = new URLSearchParams();
      formData.append('fileName', file.name);
      formData.append('mimeType', file.type);
      formData.append('fileData', base64Data);
      formData.append('ano', selectAno.value);
      
      // Enviamos el ramo estandarizado (si lo introdujo manualmente, irá estandarizado)
      formData.append('ramo', ramoFinal); 
      
      // Enviamos también el área (ej. "Numerico", "Libre") por si necesitas el dato base en tu Apps Script
      formData.append('areaElectivo', selectRamo.value); 
      
      // Enviamos el tipo de electivo si corresponde, de lo contrario enviamos vacío
      formData.append('tipoElectivo', selectTipoElectivo.value || ""); 
      formData.append('anoMaterial', anoMatValue.toString());

      const scriptURL = 'https://script.google.com/macros/s/AKfycbysVOvQhQe6XaAUCVJXImhsEdQlHfxOcZyj127yYlxI_vMX4MKCEsiNLNf79HawwZ6eNg/exec';

      fetch(scriptURL, {
        method: 'POST',
        body: formData,
        mode: 'no-cors'
      }).then(() => {
        zonaArrastre.innerHTML = '<svg class="icono-subida" style="color: #388e3c;" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg><br><strong style="color: #388e3c;">¡Archivo subido exitosamente!</strong>';
        
        // Reset de Formulario
        selectAno.value = ''; 
        selectRamo.innerHTML = '<option value="">Primero elige un año...</option>';
        selectRamo.disabled = true;
        inputAnoMaterial.value = '';
        actualizarVisibilidadCampos();
        
        setTimeout(() => resetZona(), 4000);
      }).catch(error => {
        mostrarError('Hubo un error de conexión. Intenta de nuevo.');
      });
    };
    
    reader.readAsDataURL(file);
  }

  function mostrarError(mensaje) {
    zonaArrastre.innerHTML = '<strong style="color: #d32f2f;">' + mensaje + '</strong>';
    setTimeout(() => resetZona(), 3500);
  }

  function resetZona() {
    zonaArrastre.innerHTML = '<svg class="icono-subida" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path></svg><br><strong>Arrastra el material nuevo aquí o haz clic para buscarlo</strong><br><span style="font-size: 0.9em; color: #666;">(Llena todos los datos arriba primero)</span>';
  }
</script>
