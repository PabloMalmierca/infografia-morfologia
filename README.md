# infografia-morfologia
Infografía morfología para bachillerato con analizador de palabras
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Morfología del Español: La Arquitectura de las Palabras</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f0f4f8;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 350px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
                max-height: 400px;
            }
        }
        .flow-line {
            position: relative;
            padding-left: 30px;
        }
        .flow-line::before {
            content: '';
            position: absolute;
            left: 10px;
            top: 0;
            bottom: 0;
            width: 2px;
            background-color: #009FFD;
        }
         .flow-line::after {
            content: '►';
            position: absolute;
            left: 3px;
            top: 50%;
            transform: translateY(-50%);
            color: #009FFD;
            font-size: 1.2rem;
        }
        .card-shadow {
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
        }
        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #009FFD;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-800">

    <div class="container mx-auto p-4 md:p-8">

        <header class="text-center mb-12">
            <h1 class="text-4xl md:text-5xl font-bold text-[#004AAD]">Morfología del Español</h1>
            <p class="text-xl md:text-2xl text-[#009FFD] mt-2">La Arquitectura de las Palabras</p>
        </header>

        <main class="space-y-12">

            <section class="bg-white rounded-lg card-shadow p-6 text-center">
                <h2 class="text-2xl font-bold text-[#004AAD] mb-2">¿Qué es la Morfología? 🏗️</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">Es la parte de la gramática que estudia la estructura interna de las palabras, analizando cómo se forman y las variaciones que presentan. Nos permite entender que las palabras son como edificios construidos con piezas más pequeñas llamadas morfemas.</p>
            </section>

            <section class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start">
                <div class="bg-white rounded-lg card-shadow p-6">
                    <h2 class="text-2xl font-bold text-[#004AAD] mb-4 text-center">La Estructura de la Palabra</h2>
                    <p class="mb-6 text-gray-600">Toda palabra se puede descomponer en unidades mínimas con significado. La base es el lexema o raíz, que contiene el significado principal, y a ella se unen los morfemas o afijos para añadir matices gramaticales o crear nuevas palabras.</p>
                    <div class="space-y-4">
                         <div class="text-center p-3 bg-blue-50 rounded-lg">
                            <span class="font-bold text-lg text-[#004AAD]">IN-UTIL-IZ-A-BLE-S</span>
                        </div>
                        <div class="flow-line ml-4">
                            <div class="p-3 bg-green-100 rounded-lg">
                                <span class="font-bold text-green-800">Lexema (Raíz):</span> <span class="text-green-700">-UTIL-</span> (Aporta el significado básico)
                            </div>
                        </div>
                        <div class="flow-line ml-4">
                            <div class="p-3 bg-yellow-100 rounded-lg">
                                <span class="font-bold text-yellow-800">Morfemas (Afijos):</span>
                                <ul class="list-disc list-inside mt-2 text-yellow-700">
                                    <li><span class="font-semibold">Prefijo:</span> IN- (negación)</li>
                                    <li><span class="font-semibold">Sufijos:</span> -IZ, -A, -BLE (forman el verbo y luego el adjetivo)</li>
                                    <li><span class="font-semibold">Flexivo:</span> -S (indica número plural)</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="bg-white rounded-lg card-shadow p-6">
                     <h2 class="text-2xl font-bold text-[#004AAD] mb-4 text-center">Clases de Palabras</h2>
                     <p class="mb-6 text-gray-600">Las palabras se clasifican en variables, que admiten cambios de género, número o conjugación, e invariables, que no los admiten. Esta distinción es fundamental en la gramática española.</p>
                    <div class="chart-container">
                        <canvas id="wordClassesChart"></canvas>
                    </div>
                </div>
            </section>

            <section class="bg-white rounded-lg card-shadow p-6 text-center">
                <h2 class="text-2xl font-bold text-[#004AAD] mb-4">Analizador de Palabras Interactivo ✨</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto mb-6">Introduce una palabra y deja que la IA de Gemini la analice morfológicamente por ti.</p>
                <div class="flex flex-col sm:flex-row gap-2 max-w-lg mx-auto">
                    <input type="text" id="wordInput" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-[#009FFD]" placeholder="Ej: indestructibles">
                    <button id="analyzeButton" class="w-full sm:w-auto bg-[#004AAD] text-white font-bold py-2 px-6 rounded-lg hover:bg-[#003B8A] transition-colors flex items-center justify-center">
                        Analizar Palabra
                    </button>
                </div>
                <div id="analysisResult" class="mt-6 text-left max-w-lg mx-auto min-h-[100px]">
                     <div id="loader" class="hidden mx-auto loader"></div>
                     <p id="initialMessage" class="text-gray-500 text-center">El resultado del análisis aparecerá aquí.</p>
                </div>
            </section>

            <section class="bg-white rounded-lg card-shadow p-6 md:col-span-2">
                 <h2 class="text-3xl font-bold text-[#004AAD] mb-6 text-center">Procesos de Formación de Palabras</h2>
                 <p class="text-lg text-gray-600 max-w-4xl mx-auto mb-8 text-center">El español es una lengua viva que crea nuevo léxico constantemente a través de tres mecanismos principales: la flexión, la derivación y la composición.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-xl font-bold text-[#009FFD] mb-4">1. Flexión: Género y Número</h3>
                        <p class="mb-4 text-gray-600">La flexión no crea palabras nuevas, sino que aporta información gramatical a una palabra ya existente. Los cambios de género y número son los más comunes en sustantivos y adjetivos.</p>
                        <div class="chart-container h-64 max-h-72">
                            <canvas id="flexionChart"></canvas>
                        </div>
                    </div>
                     <div>
                        <h3 class="text-xl font-bold text-[#009FFD] mb-4">2. Derivación: Prefijos y Sufijos</h3>
                         <p class="mb-4 text-gray-600">Es el proceso más productivo. Se añaden afijos (prefijos o sufijos) a una raíz para crear una palabra nueva, a menudo cambiando su categoría gramatical o su significado.</p>
                        <div class="chart-container h-64 max-h-72">
                            <canvas id="derivacionChart"></canvas>
                        </div>
                    </div>
                    <div class="md:col-span-2">
                         <h3 class="text-xl font-bold text-[#009FFD] mb-4 text-center">3. Composición y Parasíntesis</h3>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-4">
                            <div class="bg-blue-50 p-4 rounded-lg text-center">
                                <h4 class="font-bold text-lg text-[#004AAD]">Composición</h4>
                                <p class="text-gray-600 mt-2">Unión de dos o más raíces.</p>
                                <p class="mt-2 font-mono text-lg bg-white p-2 rounded">Lexema + Lexema</p>
                                <p class="mt-2 text-gray-700">Ej: <span class="font-bold">saca</span> + <span class="font-bold">puntas</span> → sacapuntas</p>
                            </div>
                            <div class="bg-blue-50 p-4 rounded-lg text-center">
                                <h4 class="font-bold text-lg text-[#004AAD]">Parasíntesis</h4>
                                <p class="text-gray-600 mt-2">Prefijación y sufijación simultáneas.</p>
                                <p class="mt-2 font-mono text-lg bg-white p-2 rounded">Prefijo + Lexema + Sufijo</p>
                                <p class="mt-2 text-gray-700">Ej: <span class="font-bold">a</span> + <span class="font-bold">naranj</span> + <span class="font-bold">ado</span> → anaranjado</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
            
            <section>
                 <h2 class="text-3xl font-bold text-[#004AAD] mb-6 text-center">Otros Mecanismos de Creación Léxica</h2>
                 <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white rounded-lg card-shadow p-6 text-center">
                        <p class="text-4xl mb-2">✂️</p>
                        <h3 class="text-xl font-bold text-[#004AAD]">Acortamiento</h3>
                        <p class="text-gray-600 mt-2">Se elimina parte de una palabra para crear una forma más corta. Ej: <span class="font-semibold">bici</span> (bicicleta), <span class="font-semibold">cine</span> (cinematógrafo).</p>
                    </div>
                    <div class="bg-white rounded-lg card-shadow p-6 text-center">
                        <p class="text-4xl mb-2">🔠</p>
                        <h3 class="text-xl font-bold text-[#004AAD]">Siglas</h3>
                        <p class="text-gray-600 mt-2">Se forman con las letras iniciales de un grupo de palabras. Se deletrean. Ej: <span class="font-semibold">DNI</span> (Documento Nacional de Identidad).</p>
                    </div>
                     <div class="bg-white rounded-lg card-shadow p-6 text-center">
                        <p class="text-4xl mb-2">🗣️</p>
                        <h3 class="text-xl font-bold text-[#004AAD]">Acrónimos</h3>
                        <p class="text-gray-600 mt-2">Se forman con iniciales o sílabas, pero se leen como una palabra. Ej: <span class="font-semibold">ovni</span> (Objeto Volador No Identificado).</p>
                    </div>
                 </div>
            </section>

        </main>

        <footer class="text-center mt-12 py-4 border-t border-gray-300">
            <p class="text-gray-500">Infografía basada en la "Nueva gramática básica de la lengua española" (RAE).</p>
        </footer>

    </div>

    <script>
        const brilliantBlues = ['#004AAD', '#009FFD', '#24CCFF', '#80FFDB'];
        
        function wrapLabel(label) {
            if (typeof label !== 'string' || label.length <= 16) {
                return label;
            }
            const words = label.split(' ');
            const lines = [];
            let currentLine = '';
            for (const word of words) {
                if ((currentLine + ' ' + word).trim().length > 16) {
                    lines.push(currentLine.trim());
                    currentLine = word;
                } else {
                    currentLine = (currentLine + ' ' + word).trim();
                }
            }
            if (currentLine) {
                lines.push(currentLine.trim());
            }
            return lines;
        }

        const tooltipTitleCallback = (tooltipItems) => {
            const item = tooltipItems[0];
            let label = item.chart.data.labels[item.dataIndex];
            return Array.isArray(label) ? label.join(' ') : label;
        };

        const defaultChartOptions = {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    position: 'bottom',
                    labels: {
                        font: {
                            size: 14,
                        }
                    }
                },
                tooltip: {
                    callbacks: {
                        title: tooltipTitleCallback
                    }
                }
            }
        };

        new Chart(document.getElementById('wordClassesChart'), {
            type: 'doughnut',
            data: {
                labels: ['Palabras Variables', 'Palabras Invariables'],
                datasets: [{
                    label: 'Clases de Palabras',
                    data: [65, 35],
                    backgroundColor: [brilliantBlues[0], brilliantBlues[2]],
                    borderColor: '#ffffff',
                    borderWidth: 2
                }]
            },
            options: { ...defaultChartOptions }
        });

        new Chart(document.getElementById('flexionChart'), {
            type: 'bar',
            data: {
                labels: ['Género (o/a)', 'Número (s/es)'],
                datasets: [{
                    label: 'Variaciones por Flexión',
                    data: [85, 95],
                    backgroundColor: [brilliantBlues[1], brilliantBlues[3]],
                    borderColor: [brilliantBlues[0], brilliantBlues[2]],
                    borderWidth: 1
                }]
            },
            options: {
                ...defaultChartOptions,
                scales: {
                    y: {
                        beginAtZero: true,
                        ticks: {
                            callback: function(value) {
                                return value + '%'
                            }
                        },
                         title: {
                             display: true,
                             text: 'Frecuencia de Uso'
                         }
                    }
                },
                plugins: {
                    ...defaultChartOptions.plugins,
                    legend: { display: false }
                }
            }
        });
        
        const derivacionLabels = ['Sufijación (Crea o cambia categoría)', 'Prefijación (Modifica significado)'].map(wrapLabel);
        new Chart(document.getElementById('derivacionChart'), {
            type: 'bar',
            data: {
                labels: derivacionLabels,
                datasets: [{
                    label: 'Impacto en la Palabra',
                    data: [70, 30],
                    backgroundColor: [brilliantBlues[0], brilliantBlues[2]],
                    borderColor: [brilliantBlues[1], brilliantBlues[3]],
                    borderWidth: 1
                }]
            },
            options: {
                 ...defaultChartOptions,
                 indexAxis: 'y',
                 scales: {
                    x: {
                        beginAtZero: true,
                        ticks: {
                            callback: function(value) {
                                return value + '%'
                            }
                        },
                         title: {
                             display: true,
                             text: 'Productividad Relativa'
                         }
                    }
                },
                plugins: {
                    ...defaultChartOptions.plugins,
                    legend: { display: false }
                }
            }
        });

        const analyzeButton = document.getElementById('analyzeButton');
        const wordInput = document.getElementById('wordInput');
        const analysisResult = document.getElementById('analysisResult');
        const loader = document.getElementById('loader');
        const initialMessage = document.getElementById('initialMessage');

        analyzeButton.addEventListener('click', async () => {
            const word = wordInput.value.trim();
            if (!word) {
                analysisResult.innerHTML = '<p class="text-red-500 text-center">Por favor, introduce una palabra.</p>';
                return;
            }

            initialMessage.style.display = 'none';
            analysisResult.innerHTML = '';
            loader.style.display = 'block';
            analysisResult.appendChild(loader);

            const apiKey = "";
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;

            const systemPrompt = `Eres un experto lingüista especializado en morfología del español. Tu tarea es analizar una palabra y descomponerla en sus componentes morfológicos. Debes identificar la raíz (lexema), los prefijos, los sufijos derivativos y los morfemas flexivos (género, número, etc.). Proporciona una explicación breve y clara para cada componente.`;
            
            const userQuery = `Analiza la siguiente palabra: '${word}'`;

            const payload = {
                systemInstruction: {
                    parts: [{ text: systemPrompt }]
                },
                contents: [{
                    parts: [{ text: userQuery }]
                }],
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            palabra: { type: "STRING" },
                            analisis: {
                                type: "OBJECT",
                                properties: {
                                    lexema: {
                                        type: "OBJECT",
                                        properties: {
                                            forma: { type: "STRING" },
                                            significado: { type: "STRING" }
                                        }
                                    },
                                    prefijos: {
                                        type: "ARRAY",
                                        items: {
                                            type: "OBJECT",
                                            properties: {
                                                forma: { type: "STRING" },
                                                significado: { type: "STRING" }
                                            }
                                        }
                                    },
                                    sufijos: {
                                        type: "ARRAY",
                                        items: {
                                            type: "OBJECT",
                                            properties: {
                                                forma: { type: "STRING" },
                                                significado: { type: "STRING" }
                                            }
                                        }
                                    },
                                    morfemas_flexivos: {
                                        type: "ARRAY",
                                        items: {
                                            type: "OBJECT",
                                            properties: {
                                                forma: { type: "STRING" },
                                                significado: { type: "STRING" }
                                            }
                                        }
                                    }
                                }
                            },
                            resumen: { type: "STRING" }
                        }
                    }
                }
            };
            
            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    throw new Error(`Error en la API: ${response.statusText}`);
                }

                const result = await response.json();
                loader.style.display = 'none';

                if (result.candidates && result.candidates[0].content.parts[0].text) {
                    const data = JSON.parse(result.candidates[0].content.parts[0].text);
                    displayAnalysis(data);
                } else {
                    throw new Error("No se recibió un análisis válido.");
                }

            } catch (error) {
                console.error("Error:", error);
                loader.style.display = 'none';
                analysisResult.innerHTML = '<p class="text-red-500 text-center">Lo sentimos, no se pudo completar el análisis. Inténtalo de nuevo.</p>';
            }
        });

        function displayAnalysis(data) {
            let html = `<h3 class="text-xl font-bold text-center text-[#004AAD] mb-4">Análisis de: <span class="font-mono bg-gray-200 px-2 py-1 rounded">${data.palabra}</span></h3>`;
            html += `<div class="space-y-3">`;

            if (data.analisis.lexema && data.analisis.lexema.forma) {
                html += `<div class="p-3 bg-green-100 rounded-lg">
                            <p><span class="font-bold text-green-800">Lexema (Raíz):</span> <span class="font-mono text-green-700">${data.analisis.lexema.forma}</span></p>
                            <p class="text-sm text-green-600">${data.analisis.lexema.significado}</p>
                         </div>`;
            }

            if (data.analisis.prefijos && data.analisis.prefijos.length > 0) {
                 html += `<div class="p-3 bg-yellow-100 rounded-lg">
                            <p class="font-bold text-yellow-800">Prefijos:</p>
                            <ul class="list-disc list-inside mt-1 space-y-1">`;
                data.analisis.prefijos.forEach(p => {
                    html += `<li><span class="font-mono text-yellow-700">${p.forma}</span>: <span class="text-sm text-yellow-600">${p.significado}</span></li>`;
                });
                html += `</ul></div>`;
            }
            
            if (data.analisis.sufijos && data.analisis.sufijos.length > 0) {
                 html += `<div class="p-3 bg-yellow-100 rounded-lg">
                            <p class="font-bold text-yellow-800">Sufijos Derivativos:</p>
                            <ul class="list-disc list-inside mt-1 space-y-1">`;
                data.analisis.sufijos.forEach(s => {
                    html += `<li><span class="font-mono text-yellow-700">${s.forma}</span>: <span class="text-sm text-yellow-600">${s.significado}</span></li>`;
                });
                html += `</ul></div>`;
            }
            
            if (data.analisis.morfemas_flexivos && data.analisis.morfemas_flexivos.length > 0) {
                 html += `<div class="p-3 bg-blue-100 rounded-lg">
                            <p class="font-bold text-blue-800">Morfemas Flexivos:</p>
                            <ul class="list-disc list-inside mt-1 space-y-1">`;
                data.analisis.morfemas_flexivos.forEach(m => {
                    html += `<li><span class="font-mono text-blue-700">${m.forma}</span>: <span class="text-sm text-blue-600">${m.significado}</span></li>`;
                });
                html += `</ul></div>`;
            }

            html += `</div>`;
            html += `<p class="mt-4 p-3 bg-gray-100 rounded-lg text-gray-700">${data.resumen}</p>`;

            analysisResult.innerHTML = html;
        }

    </script>
</body>
</html>

