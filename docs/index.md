#  :material-book: Wiki-ICM 

<p align="center">
  <img src="assets/imagen.png" alt="Logo Wiki-ICM" width="400">
</p>


Bienvenido a **Wiki-ICM**, un proyecto que busca recopilar apuntes, listados y material de la carrera **Ingeniería Civil Matemática UdeC**.

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

<div style="margin-bottom: 15px; text-align: center;">
  <label for="select-ano"><strong>Año Carrera:</strong></label>
  <select id="select-ano" style="padding: 5px; margin-right: 15px; border-radius: 5px;">
    <option value="">Selecciona...</option>
    <option value="1er Año">1er Año</option>
    <option value="2do Año">2do Año</option>
    <option value="3er Año">3er Año</option>
    <option value="4to Año">4to Año</option>
    <option value="5to Año">5to Año</option>
    <option value="6to Año">6to Año</option>
    <option value="Otro">Otro / General</option>
  </select>

  <label for="select-ramo"><strong>Ramo:</strong></label>
  <!-- Partimos con el selector bloqueado hasta que elijan un año -->
  <select id="select-ramo" style="padding: 5px; border-radius: 5px; width: 150px; margin-right: 15px;" disabled>
    <option value="">Primero elige un año...</option>
  </select>

  <label for="input-ano-material"><strong>Año Material:</strong></label>
  <input type="number" id="input-ano-material" placeholder="Ej: 2025" style="padding: 5px; border-radius: 5px; width: 90px;">
</div>

<div id="zona-arrastre" onclick="document.getElementById('input-archivo').click();" style="border: 3px dashed #4051b5; border-radius: 10px; padding: 60px; text-align: center; background-color: rgba(64, 81, 181, 0.05); margin: 20px 0; cursor: pointer;">
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

  // AQUÍ ESTÁ LA MAGIA: El diccionario de ramos por año. 
  // Edita esto con la malla de tu carrera para agregar o quitar los que necesites.
  const ramosPorAno = {
    "1er Año": ["Calculo I","Calculo II","Algebra I","Algebra II","Fisica I","Fisica II","Quimica I","Quimica II","TRM I","Introduccion a la Innovacion"],
    "2do Año": ["Algebra III","Calculo III","Calculo IV","EDO","Programacion","ED2","Termodinamica"],
    "3er Año": ["CÁLCULO III", "ÁLGEBRA ABSTRACTA", "PROBABILIDADES", "ANÁLISIS NUMÉRICO"],
    "4to Año": ["GEOMETRÍA ALGEBRAICA", "ANÁLISIS REAL", "OPTIMIZACIÓN"],
    "5to Año": ["TEORÍA DE GALOIS", "ANÁLISIS COMPLEJO", "TEORÍA DE NÚMEROS"],
    "6to Año": ["PROYECTO DE TÍTULO", "ELECTIVO I", "ELECTIVO II"],
    "Otro": ["MATERIAL GENERAL", "TALLERES", "OTROS"]
  };

  // Evento que actualiza la lista de ramos cuando cambian el año
  selectAno.addEventListener('change', (e) => {
    const anoSeleccionado = e.target.value;
    
    // Limpiamos la lista de ramos
    selectRamo.innerHTML = '<option value="">Selecciona ramo...</option>';

    if (anoSeleccionado && ramosPorAno[anoSeleccionado]) {
      selectRamo.disabled = false; // Desbloqueamos el selector
      ramosPorAno[anoSeleccionado].forEach(ramo => {
        const opcion = document.createElement('option');
        opcion.value = ramo;
        opcion.textContent = ramo;
        selectRamo.appendChild(opcion);
      });
    } else {
      // Si vuelven a poner "Selecciona...", bloqueamos de nuevo
      selectRamo.disabled = true;
      selectRamo.innerHTML = '<option value="">Primero elige un año...</option>';
    }
  });

  zonaArrastre.addEventListener('dragover', (e) => {
    e.preventDefault();
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.2)';
  });

  zonaArrastre.addEventListener('dragleave', () => {
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.05)';
  });

  zonaArrastre.addEventListener('drop', (e) => {
    e.preventDefault();
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.05)';
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
    const anoActual = new Date().getFullYear();

    // Ahora validamos con selectRamo en vez del input de texto
    if (!selectAno.value || !selectRamo.value || !inputAnoMaterial.value) {
      zonaArrastre.innerHTML = '<strong style="color: red;">¡Oye! Faltan datos por llenar arriba.</strong>';
      setTimeout(() => resetZona(), 3500);
      return;
    }

    if (anoMatValue < 2010 || anoMatValue > anoActual) {
      zonaArrastre.innerHTML = '<strong style="color: red;">El año del material debe ser entre 2010 y ' + anoActual + '.</strong>';
      setTimeout(() => resetZona(), 4000);
      return;
    }

    zonaArrastre.innerHTML = '<strong>Subiendo archivo... aguanta un rato.</strong>';

    const reader = new FileReader();
    reader.onload = function(event) {
      const base64Data = event.target.result.split(',')[1];
      
      const formData = new URLSearchParams();
      formData.append('fileName', file.name);
      formData.append('mimeType', file.type);
      formData.append('fileData', base64Data);
      formData.append('ano', selectAno.value);
      formData.append('ramo', selectRamo.value);
      formData.append('anoMaterial', anoMatValue.toString());

      // ¡RECUERDA PONER TU URL ACÁ!
      const scriptURL = 'https://script.google.com/macros/s/AKfycbxAnaYDfZ3435EV632hUkHend8cIILkETye9-Vol_wKt1sWTzEC2OLZeS6nGxBSoPLKmg/exec';

      fetch(scriptURL, {
        method: 'POST',
        body: formData,
        mode: 'no-cors'
      }).then(() => {
        zonaArrastre.innerHTML = '<strong style="color: green;">¡Archivo subido al tiro! Gracias por apañar.</strong>';
        
        // Reseteamos todo para el siguiente archivo
        selectAno.value = ''; 
        selectRamo.innerHTML = '<option value="">Primero elige un año...</option>';
        selectRamo.disabled = true;
        inputAnoMaterial.value = '';
        
        setTimeout(() => resetZona(), 3500);
      }).catch(error => {
        zonaArrastre.innerHTML = '<strong style="color: red;">Chuta, hubo un error. Intenta de nuevo.</strong>';
      });
    };
    
    reader.readAsDataURL(file);
  }

  function resetZona() {
    zonaArrastre.innerHTML = '<strong>Arrastra el material nuevo aquí o haz clic para buscarlo</strong><br><span style="font-size: 0.9em; color: #666;">(Llena todos los datos arriba primero)</span>';
  }
</script>











