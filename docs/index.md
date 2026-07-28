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
  <label for="select-ano"><strong>Año:</strong></label>
  <select id="select-ano" style="padding: 5px; margin-right: 15px; border-radius: 5px;">
    <option value="">Seleccione un año...</option>
    <option value="1er Año">1er Año</option>
    <option value="2do Año">2do Año</option>
    <option value="3er Año">3er Año</option>
    <option value="4to Año">4to Año</option>
    <option value="5to Año">5to Año</option>
    <option value="6to Año">6to Año</option>
    <option value="Electivos">Electivos</option>
    <option value="Otro">Otro / General</option>
  </select>

  <label for="select-ramo"><strong>Ramo:</strong></label>
  <select id="select-ramo" style="padding: 5px; border-radius: 5px; width: 200px;" disabled>
    <option value="">Seleccione un ramo...</option>
  </select>
</div>

<!-- Zona de arrastre que ahora también es clickeable -->
<div id="zona-arrastre" style="border: 3px dashed #4051b5; border-radius: 10px; padding: 60px; text-align: center; background-color: rgba(64, 81, 181, 0.05); margin: 20px 0; cursor: pointer;">
  <strong>Arrastre el material nuevo aquí o haga clic para seleccionar un archivo</strong><br>
  <span style="font-size: 0.9em; color: #666;">(Asegúrese de seleccionar el Año y el Ramo previamente)</span>
</div>

<!-- Input oculto para abrir el explorador de archivos -->
<input type="file" id="input-archivo" style="display: none;">

<script>
  // DICCIONARIO DE RAMOS: Modifica esta lista con los ramos reales
  const ramosPorAno = {
    "1er Año": ["Álgebra I", "Cálculo I", "Física I", "Quimica I","TRM I"],
    "2do Año": ["Calculo III", "EDO", "Algebra III","Calculo IV"],
    "3er Año": ["Optimizacion I", "Analisis Real I", "Analisis Real 2","a"],
    "4to Año": ["test", "aa"],
    "5to Año": ["test", "Economía"],
    "6to Año": ["test", ""],
    "Electivos": ["test", "test", "test"],
    "Otro": ["test", "test"]
  };

  const zonaArrastre = document.getElementById('zona-arrastre');
  const selectAno = document.getElementById('select-ano');
  const selectRamo = document.getElementById('select-ramo');
  const inputArchivo = document.getElementById('input-archivo');

  // Lógica de los menús desplegables
  selectAno.addEventListener('change', function() {
    const añoSeleccionado = this.value;
    selectRamo.innerHTML = '<option value="">Seleccione un ramo...</option>';
    
    if (añoSeleccionado && ramosPorAno[añoSeleccionado]) {
      ramosPorAno[añoSeleccionado].forEach(ramo => {
        const option = document.createElement('option');
        option.value = ramo;
        option.textContent = ramo;
        selectRamo.appendChild(option);
      });
      selectRamo.disabled = false;
    } else {
      selectRamo.disabled = true;
    }
  });

  // --- EVENTOS DE LA ZONA DE ARRASTRE Y CLIC ---

  // Abrir ventana de archivos al hacer clic en la zona
  zonaArrastre.addEventListener('click', () => {
    inputArchivo.click();
  });

  // Capturar el archivo si lo seleccionan con la ventana
  inputArchivo.addEventListener('change', (e) => {
    if (e.target.files.length > 0) {
      procesarArchivo(e.target.files[0]);
    }
  });

  zonaArrastre.addEventListener('dragover', (e) => {
    e.preventDefault();
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.2)';
  });

  zonaArrastre.addEventListener('dragleave', () => {
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.05)';
  });

  // Capturar el archivo si lo arrastran
  zonaArrastre.addEventListener('drop', (e) => {
    e.preventDefault();
    zonaArrastre.style.backgroundColor = 'rgba(64, 81, 181, 0.05)';
    
    if (e.dataTransfer.files.length > 0) {
      procesarArchivo(e.dataTransfer.files[0]);
    }
  });

  // --- LÓGICA PRINCIPAL DE SUBIDA ---
  function procesarArchivo(file) {
    if (!selectAno.value || !selectRamo.value) {
      zonaArrastre.innerHTML = '<strong style="color: red;">Error: Por favor, seleccione el Año y el Ramo antes de subir el archivo.</strong>';
      setTimeout(() => {
        zonaArrastre.innerHTML = '<strong>Arrastre el material nuevo aquí o haga clic para seleccionar un archivo</strong><br><span style="font-size: 0.9em; color: #666;">(Asegúrese de seleccionar el Año y el Ramo previamente)</span>';
      }, 4000);
      inputArchivo.value = ''; // Limpiar input
      return;
    }

    zonaArrastre.innerHTML = '<strong>Subiendo archivo, por favor espere...</strong>';

    const reader = new FileReader();
    reader.onload = function(event) {
      const base64Data = event.target.result.split(',')[1];
      
      const formData = new URLSearchParams();
      formData.append('fileName', file.name);
      formData.append('mimeType', file.type);
      formData.append('fileData', base64Data);
      formData.append('ano', selectAno.value);
      formData.append('ramo', selectRamo.value);

      // ¡RECUERDA PONER TU URL DE APPS SCRIPT AQUÍ!
      const scriptURL = 'https://script.google.com/macros/s/AKfycbz4KPGgJ_IwS0UCFn6_JtEkMBSrR7lAvwxw8NzIlhEQAw2T7tsPABaQtdNunOXyToy5BQ/exec';

      fetch(scriptURL, {
        method: 'POST',
        body: formData,
        mode: 'no-cors'
      }).then(() => {
        zonaArrastre.innerHTML = '<strong style="color: green;">Archivo subido exitosamente. Gracias por su contribución.</strong>';
        selectAno.value = ''; 
        selectRamo.innerHTML = '<option value="">Seleccione un ramo...</option>';
        selectRamo.disabled = true;
        inputArchivo.value = ''; // Limpiar input para futuras subidas
        
        setTimeout(() => {
          zonaArrastre.innerHTML = '<strong>Arrastre el material nuevo aquí o haga clic para seleccionar un archivo</strong><br><span style="font-size: 0.9em; color: #666;">(Asegúrese de seleccionar el Año y el Ramo previamente)</span>';
        }, 4000);
      }).catch(error => {
        zonaArrastre.innerHTML = '<strong style="color: red;">Ha ocurrido un error durante la subida. Por favor, intente nuevamente.</strong>';
        inputArchivo.value = '';
      });
    };
    
    reader.readAsDataURL(file);
  }
</script>















