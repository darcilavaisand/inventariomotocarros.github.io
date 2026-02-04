[index.html](https://github.com/user-attachments/files/25060354/index.html)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🚛 Inventario Motocarros - Trazabilidad</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #2c3e50);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
            max-width: 900px;
            width: 100%;
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #2c3e50, #4a6491);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 32px;
            margin-bottom: 10px;
        }
        
        .header p {
            opacity: 0.9;
            font-size: 16px;
        }
        
        .content {
            padding: 30px;
        }
        
        .setup-section {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            border: 1px solid #e0e6ed;
            display: none;
        }
        
        .setup-section.active {
            display: block;
        }
        
        .form-group {
            margin-bottom: 24px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: #2c3e50;
            font-size: 16px;
        }
        
        .form-control {
            width: 100%;
            padding: 14px;
            border: 2px solid #ddd;
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s;
        }
        
        .form-control:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }
        
        textarea.form-control {
            min-height: 100px;
            resize: vertical;
        }
        
        .checkbox-group {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 12px;
            margin-top: 12px;
        }
        
        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .checkbox-item input {
            width: auto;
            margin: 0;
            cursor: pointer;
        }
        
        .btn-group {
            display: flex;
            gap: 15px;
            margin-top: 25px;
            flex-wrap: wrap;
        }
        
        .btn {
            padding: 16px 28px;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            flex: 1;
            min-width: 180px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(52, 152, 219, 0.4);
        }
        
        .btn-secondary {
            background: #e0e6ed;
            color: #2c3e50;
        }
        
        .btn-secondary:hover {
            background: #d1d9e6;
            transform: translateY(-2px);
        }
        
        .status {
            padding: 18px;
            border-radius: 12px;
            margin: 25px 0;
            text-align: center;
            font-weight: 600;
            font-size: 18px;
            display: none;
            animation: fadeIn 0.4s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .status.success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            display: block;
        }
        
        .status.error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
            display: block;
        }
        
        .status.loading {
            background: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
            display: block;
        }
        
        .table-container {
            margin-top: 35px;
            overflow-x: auto;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            display: none;
        }
        
        .table-container.active {
            display: block;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }
        
        table th {
            background: #2c3e50;
            color: white;
            padding: 16px;
            text-align: left;
            font-weight: 600;
        }
        
        table td {
            padding: 14px;
            border-bottom: 1px solid #eee;
        }
        
        table tr:hover {
            background: #f8f9fa;
        }
        
        .ref-CC200 { color: #3498db; font-weight: 700; }
        .ref-CC250 { color: #27ae60; font-weight: 700; }
        .ref-CC300 { color: #e67e22; font-weight: 700; }
        
        .badge {
            display: inline-block;
            padding: 5px 14px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 600;
        }
        
        .badge-incompleto { background: #fff3cd; color: #856404; }
        .badge-calidad { background: #f8d7da; color: #721c24; }
        .badge-bueno { background: #d4edda; color: #155724; }
        
        .instructions {
            background: #e3f2fd;
            padding: 20px;
            border-radius: 12px;
            margin: 25px 0;
            border-left: 4px solid #3498db;
        }
        
        .instructions h3 {
            color: #2c3e50;
            margin-bottom: 12px;
        }
        
        .instructions ol {
            padding-left: 20px;
            margin-top: 10px;
            color: #2c3e50;
        }
        
        .instructions li {
            margin-bottom: 8px;
            line-height: 1.5;
        }
        
        @media (max-width: 768px) {
            .content { padding: 20px; }
            .btn-group { flex-direction: column; }
            .btn { width: 100%; }
            .header h1 { font-size: 26px; }
            .checkbox-group { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🚛 Inventario Motocarros</h1>
            <p>Trazabilidad en Tiempo Real - CC200 • CC250 • CC300</p>
        </div>

        <div class="content">
            <!-- SECCIÓN DE CONFIGURACIÓN INICIAL -->
            <div id="setupSection" class="setup-section active">
                <div class="instructions">
                    <h3>📋 Configuración Inicial</h3>
                    <ol>
                        <li>Crea tu Google Sheet con encabezados: Fecha/Hora, Referencia, Estado, Novedades Calidad, Unidades, Observaciones, Usuario</li>
                        <li>Ve a Extensiones → Apps Script y pega el código proporcionado</li>
                        <li>Despliega como Aplicación Web y copia la URL (termina en /exec)</li>
                        <li>Pega esa URL aquí abajo y haz clic en "Guardar Configuración"</li>
                    </ol>
                </div>
                
                <div class="form-group">
                    <label>🔗 URL de Apps Script</label>
                    <input type="text" id="scriptUrl" class="form-control" placeholder="https://script.google.com/macros/s/.../exec">
                </div>
                
                <div class="btn-group">
                    <button class="btn btn-primary" onclick="saveConfig()">💾 Guardar Configuración</button>
                </div>
                
                <div id="setupStatus" class="status"></div>
            </div>

            <!-- FORMULARIO PRINCIPAL -->
            <div id="formSection" style="display: none;">
                <h2 style="color: #2c3e50; margin-bottom: 25px; font-size: 26px;">
                    📝 Registrar Unidad
                </h2>

                <div class="form-group">
                    <label>🏷️ Referencia del Motocarro</label>
                    <select id="reference" class="form-control" required>
                        <option value="">Selecciona una referencia</option>
                        <option value="CC200">CC200</option>
                        <option value="CC250">CC250</option>
                        <option value="CC300">CC300</option>
                    </select>
                </div>

                <div class="form-group">
                    <label>📊 Estado de la Unidad</label>
                    <select id="status" class="form-control" required onchange="toggleQualitySection()">
                        <option value="">Selecciona el estado</option>
                        <option value="incompleto">🔧 Ensamblada Incompleta</option>
                        <option value="calidad">🎨 Novedades por Calidad</option>
                        <option value="bueno">✅ Producto en Buen Estado</option>
                    </select>
                </div>

                <div id="qualitySection" class="form-group" style="display: none;">
                    <label>🎨 Novedades de Calidad (selecciona todas las que apliquen)</label>
                    <div class="checkbox-group">
                        <div class="checkbox-item">
                            <input type="checkbox" id="issue1" value="Pintura defectuosa">
                            <label for="issue1">Pintura defectuosa</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="issue2" value="Rayaduras">
                            <label for="issue2">Rayaduras en pintura</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="issue3" value="Componentes faltantes">
                            <label for="issue3">Componentes faltantes</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="issue4" value="Alineación incorrecta">
                            <label for="issue4">Alineación incorrecta</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="issue5" value="Problemas eléctricos">
                            <label for="issue5">Problemas eléctricos</label>
                        </div>
                        <div class="checkbox-item">
                            <input type="checkbox" id="issue6" value="Otro">
                            <label for="issue6">Otro</label>
                        </div>
                    </div>
                </div>

                <div class="form-group">
                    <label>🔢 Cantidad de Unidades</label>
                    <input type="number" id="units" class="form-control" min="1" value="1" required>
                </div>

                <div class="form-group">
                    <label>📝 Observaciones Adicionales</label>
                    <textarea id="observations" class="form-control" placeholder="Ej: Falta tapa de motor, necesita revisión final..."></textarea>
                </div>

                <div class="btn-group">
                    <button class="btn btn-secondary" onclick="clearForm()">
                        🧹 Limpiar
                    </button>
                    <button class="btn btn-primary" onclick="submitInventory()">
                        💾 Guardar Registro
                    </button>
                </div>

                <div id="statusMessage" class="status"></div>

                <!-- TABLA DE REGISTROS -->
                <div class="table-container" id="recordsContainer">
                    <h3 style="color: #2c3e50; margin: 25px 0 20px 0; padding-left: 10px; border-left: 4px solid #3498db; font-size: 22px;">
                        📊 Últimos Registros
                    </h3>
                    <table>
                        <thead>
                            <tr>
                                <th>Fecha/Hora</th>
                                <th>Referencia</th>
                                <th>Estado</th>
                                <th>Unidades</th>
                                <th>Observaciones</th>
                            </tr>
                        </thead>
                        <tbody id="recordsBody">
                            <tr>
                                <td colspan="5" style="text-align: center; padding: 30px; color: #7f8c8d; font-style: italic;">
                                    Tus registros aparecerán aquí después de guardar
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Configuración
        const CONFIG_KEY = 'inventario_script_url';
        
        // Cargar configuración al inicio
        document.addEventListener('DOMContentLoaded', () => {
            const savedUrl = localStorage.getItem(CONFIG_KEY);
            if (savedUrl) {
                showForm();
            }
        });
        
        // Guardar configuración
        function saveConfig() {
            const url = document.getElementById('scriptUrl').value.trim();
            const statusDiv = document.getElementById('setupStatus');
            
            if (!url) {
                statusDiv.textContent = '⚠️ Por favor ingresa la URL';
                statusDiv.className = 'status error';
                return;
            }
            
            if (!url.includes('script.google.com') || !url.includes('/exec')) {
                statusDiv.textContent = '⚠️ URL inválida. Debe ser de Google Apps Script y terminar en /exec';
                statusDiv.className = 'status error';
                return;
            }
            
            localStorage.setItem(CONFIG_KEY, url);
            statusDiv.textContent = '✅ Configuración guardada exitosamente';
            statusDiv.className = 'status success';
            
            // Mostrar formulario después de 1 segundo
            setTimeout(showForm, 1000);
        }
        
        // Mostrar formulario principal
        function showForm() {
            document.getElementById('setupSection').classList.remove('active');
            document.getElementById('formSection').style.display = 'block';
        }
        
        // Mostrar/ocultar sección de calidad
        function toggleQualitySection() {
            const status = document.getElementById('status').value;
            document.getElementById('qualitySection').style.display = 
                status === 'calidad' ? 'block' : 'none';
        }
        
        // Obtener novedades seleccionadas
        function getQualityIssues() {
            return Array.from(document.querySelectorAll('#qualitySection input[type="checkbox"]:checked'))
                .map(cb => cb.value);
        }
        
        // Enviar registro
        async function submitInventory() {
            const scriptUrl = localStorage.getItem(CONFIG_KEY);
            const statusDiv = document.getElementById('statusMessage');
            
            if (!scriptUrl) {
                statusDiv.textContent = '⚠️ Configura primero la URL de Apps Script';
                statusDiv.className = 'status error';
                return;
            }
            
            const reference = document.getElementById('reference').value;
            const status = document.getElementById('status').value;
            const units = document.getElementById('units').value;
            const observations = document.getElementById('observations').value;
            
            // Validaciones
            if (!reference || !status || !units) {
                statusDiv.textContent = '⚠️ Completa todos los campos requeridos';
                statusDiv.className = 'status error';
                return;
            }
            
            if (status === 'calidad' && getQualityIssues().length === 0) {
                statusDiv.textContent = '⚠️ Selecciona al menos una novedad de calidad';
                statusDiv.className = 'status error';
                return;
            }
            
            // Mostrar loading
            statusDiv.textContent = 'Guardando registro...';
            statusDiv.className = 'status loading';
            
            try {
                const response = await fetch(scriptUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        reference: reference,
                        status: status,
                        qualityIssues: getQualityIssues(),
                        units: units,
                        observations: observations,
                        user: 'Operador'
                    })
                });
                
                const result = await response.json();
                
                if (result.success) {
                    statusDiv.textContent = '✅ ¡Registro guardado exitosamente!';
                    statusDiv.className = 'status success';
                    
                    // Agregar a tabla visual
                    addRecordToTable({
                        fecha: new Date().toLocaleString('es-ES'),
                        referencia: reference,
                        estado: status,
                        unidades: units,
                        observaciones: observations || '-'
                    });
                    
                    // Limpiar formulario después de 1.5s
                    setTimeout(clearForm, 1500);
                } else {
                    throw new Error(result.error || 'Error desconocido');
                }
            } catch (error) {
                console.error('Error:', error);
                statusDiv.textContent = `❌ Error: ${error.message || 'No se pudo guardar'}`;
                statusDiv.className = 'status error';
            }
        }
        
        // Agregar registro visualmente a la tabla
        function addRecordToTable(record) {
            const body = document.getElementById('recordsBody');
            const container = document.getElementById('recordsContainer');
            
            // Si es el primer registro, limpiar el mensaje de "sin registros"
            if (body.children.length === 1 && body.children[0].children[0].colSpan === 5) {
                body.innerHTML = '';
            }
            
            // Crear fila
            const row = document.createElement('tr');
            
            // Mapear estado a badge
            const estadoMap = {
                'incompleto': 'Incompleto',
                'calidad': 'Novedades Calidad',
                'bueno': 'Buen Estado'
            };
            const badgeClass = {
                'incompleto': 'badge-incompleto',
                'calidad': 'badge-calidad',
                'bueno': 'badge-bueno'
            };
            
            row.innerHTML = `
                <td style="font-size: 14px; color: #7f8c8d;">${record.fecha}</td>
                <td><span class="ref-${record.referencia}">${record.referencia}</span></td>
                <td><span class="badge ${badgeClass[record.estado]}">${estadoMap[record.estado]}</span></td>
                <td style="font-weight: 700; color: #2c3e50;">${record.unidades}</td>
                <td style="font-size: 14px; color: #555;">${record.observaciones}</td>
            `;
            
            // Insertar al inicio
            body.insertBefore(row, body.firstChild);
            
            // Mostrar tabla
            container.classList.add('active');
            
            // Limitar a 10 registros
            if (body.children.length > 10) {
                body.removeChild(body.lastChild);
            }
        }
        
        // Limpiar formulario
        function clearForm() {
            document.getElementById('reference').value = '';
            document.getElementById('status').value = '';
            document.getElementById('qualitySection').style.display = 'none';
            document.querySelectorAll('#qualitySection input[type="checkbox"]').forEach(cb => cb.checked = false);
            document.getElementById('units').value = '1';
            document.getElementById('observations').value = '';
            document.getElementById('statusMessage').className = 'status';
            document.getElementById('statusMessage').style.display = 'none';
        }
    </script>
</body>
</html>
