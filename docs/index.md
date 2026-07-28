#  :material-book: Wiki-ICM 

<p align="center">
  <img src="assets/imagen.png" alt="Logo Wiki-ICM" width="400">
</p>

---

Bienvenido a **Wiki-ICM**, un proyecto que busca recopilar apuntes, listados y material de la carrera **Ingeniería Civil Matemática UdeC**.

---

## 📂 Contenido

Los recursos están organizados siguiendo la malla curricular de la carrera:

* :material-school: **Malla Ingeniería Civil Matemática:** Apuntes, guías, certámenes pasados y libros  🛠 
* :material-plus-box: **Recursos Adicionales:** Otros ramos electivos o de otras carreras relacionadas.

---
## Aportes

<div style="margin-bottom: 15px; text-align: center;">
  <label for="select-ano"><strong>Año:</strong></label>
  <select id="select-ano" style="padding: 5px; margin-right: 15px; border-radius: 5px;">
    <option value="">Selecciona...</option>
    <option value="1er Año">1er Año</option>
    <option value="2do Año">2do Año</option>
    <option value="3er Año">3er Año</option>
    <option value="4to Año">4to Año</option>
    <option value="5to Año">5to Año</option>
    <option value="Electivo"> Electivos </option>
    <option value="Otro">Otro </option>
  </select>

  <label for="input-ramo"><strong>Ramo:</strong></label>
  <input type="text" id="input-ramo" placeholder="Ej: Álgebra 1, Cálculo 1..." style="padding: 5px; border-radius: 5px; width: 200px;">
</div>

<div id="zona-arrastre" style="border: 3px dashed #4051b5; border-radius: 10px; padding: 60px; text-align: center; background-color: rgba(64, 81, 181, 0.05); margin: 20px 0; cursor: pointer;">
  <strong>Arrastra el material nuevo aquí</strong><br>
  <span style="font-size: 0.9em; color: #666;">(Asegúrate de poner el Año y el Ramo arriba primero)</span>
</div>

<script>
  const zonaArrastre = document.getElementById('zona-arrastre');
  const selectAno = document.getElementById('select-ano');
  const inputRamo = document.getElementById('input-ramo');

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
    if (!file) return;

    if (!selectAno.value || !inputRamo.value.trim()) {
      zonaArrastre.innerHTML = '<strong style="color: red;">Llena el Año y el Ramo primero.</strong>';
      setTimeout(() => {
        zonaArrastre.innerHTML = '<strong>Arrastra el material nuevo aquí</strong><br><span style="font-size: 0.9em; color: #666;">(Asegúrate de poner el Año y el Ramo arriba primero)</span>';
      }, 3500);
      return;
    }

    zonaArrastre.innerHTML = '<strong>Subiendo archivo...</strong>';

    const reader = new FileReader();
    reader.onload = function(event) {
      const base64Data = event.target.result.split(',')[1];
      
      const formData = new URLSearchParams();
      formData.append('fileName', file.name);
      formData.append('mimeType', file.type);
      formData.append('fileData', base64Data);
      formData.append('ano', selectAno.value);
      formData.append('ramo', inputRamo.value.trim());

      const scriptURL = 'https://script.google.com/macros/s/AKfycbz4KPGgJ_IwS0UCFn6_JtEkMBSrR7lAvwxw8NzIlhEQAw2T7tsPABaQtdNunOXyToy5BQ/exec';

      fetch(scriptURL, {
        method: 'POST',
        body: formData,
        mode: 'no-cors'
      }).then(() => {
        zonaArrastre.innerHTML = '<strong style="color: green;">Archivo subido.</strong>';
        selectAno.value = ''; 
        inputRamo.value = '';
        setTimeout(() => {
          zonaArrastre.innerHTML = '<strong>Arrastra más material aquí</strong>';
        }, 3500);
      }).catch(error => {
        zonaArrastre.innerHTML = '<strong style="color: red;">Hubo un error. Intenta de nuevo.</strong>';
      });
    };
    
    reader.readAsDataURL(file);
  });
</script>



<!-- ## 🤝 ¿Cómo puedo ser parte?



Si tienes material para aportar puedes subirlo [aqui](https://drive.google.com/drive/folders/1DJBW6QvXpCti3Z_lFaO2_y4eFNrsqQ3G?usp=sharing), si tienes sugerencias o quieres ser parte del equipo de trabajo, puedes contactarnos a:

* :material-email: [jjunemann2024@udec.cl](mailto:jjunemann2024@udec.cl)
* :material-email: [bsandoval2018@udec.cl](mailto:bsandoval2018@udec.cl)
* :material-email: [pnahuelquin2024@udec.cl](mailto:pnahuelquin2024@udec.cl)
* :material-email: [femunoz2022@udec.cl](mailto:femunoz2022@udec.cl) -->



