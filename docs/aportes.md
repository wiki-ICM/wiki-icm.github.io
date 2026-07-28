<div style="margin-bottom: 15px; text-align: center;">
  <label for="select-ano"><strong>Año:</strong></label>
  <select id="select-ano" style="padding: 5px; margin-right: 15px; border-radius: 5px;">
    <option value="">Selecciona...</option>
    <option value="1er Año">1er Año</option>
    <option value="2do Año">2do Año</option>
    <option value="3er Año">3er Año</option>
    <option value="4to Año">4to Año</option>
    <option value="5to Año">5to Año</option>
    <option value="Otro">Otro / General</option>
  </select>

  <label for="input-ramo"><strong>Ramo:</strong></label>
  <input type="text" id="input-ramo" placeholder="Ej: Álgebra, Cálculo..." style="padding: 5px; border-radius: 5px; width: 200px;">
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

    // Validación para que no suban hueás sin etiquetar
    if (!selectAno.value || !inputRamo.value.trim()) {
      zonaArrastre.innerHTML = '<strong style="color: red;">¡Oye! Llena el Año y el Ramo primero.</strong>';
      setTimeout(() => {
        zonaArrastre.innerHTML = '<strong>Arrastra el material nuevo aquí</strong><br><span style="font-size: 0.9em; color: #666;">(Asegúrate de poner el Año y el Ramo arriba primero)</span>';
      }, 3500);
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
      formData.append('ramo', inputRamo.value.trim());

      const scriptURL = 'https://script.google.com/macros/s/AKfycbz4KPGgJ_IwS0UCFn6_JtEkMBSrR7lAvwxw8NzIlhEQAw2T7tsPABaQtdNunOXyToy5BQ/exec';

      fetch(scriptURL, {
        method: 'POST',
        body: formData,
        mode: 'no-cors'
      }).then(() => {
        zonaArrastre.innerHTML = '<strong style="color: green;">¡Archivo subido al tiro! Gracias por apañar.</strong>';
        selectAno.value = ''; 
        inputRamo.value = '';
        setTimeout(() => {
          zonaArrastre.innerHTML = '<strong>Arrastra más material aquí</strong>';
        }, 3500);
      }).catch(error => {
        zonaArrastre.innerHTML = '<strong style="color: red;">Chuta, hubo un error. Intenta de nuevo.</strong>';
      });
    };
    
    reader.readAsDataURL(file);
  });
</script>
