# MartaDiaz.github.io
Musica i M.C
mi-proyecto-musica/
│── index.html      # Tu web principal
│── README.md       # Info del proyecto
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>La Música y los Medios de Comunicación</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Paleta de colores: Soft Earth -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #fdfaf6;
            color: #4a4a4a;
        }
        .nav-button {
            transition: all 0.3s ease;
            border-bottom: 4px solid transparent;
        }
        .nav-button.active {
            border-bottom-color: #c084fc; /* purple-400 */
            color: #581c87; /* purple-900 */
        }
        .timeline-item::before {
            content: '';
            position: absolute;
            left: -30px;
            top: 50%;
            transform: translateY(-50%);
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background-color: #c084fc; /* purple-400 */
            border: 4px solid #f3e8ff; /* purple-100 */
        }
        .timeline-line {
            position: absolute;
            left: -21px;
            top: 0;
            bottom: 0;
            width: 2px;
            background-color: #e9d5ff; /* purple-200 */
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
        /* Nueva clase para ocultar contenido sin usar display: none */
        .content-hidden {
            position: absolute;
            left: -9999px;
            opacity: 0;
        }
        .content-visible {
            position: static;
            opacity: 1;
        }
    </style>
</head>
<body class="antialiased">

    <div class="container mx-auto max-w-6xl p-4 sm:p-6 lg:p-8">
        
        <header class="text-center mb-10">
            <h1 class="text-4xl md:text-5xl font-bold text-purple-900">Un Viaje Sonoro</h1>
            <p class="text-lg text-stone-600 mt-2">La evolución de la música a través de los medios de comunicación</p>
        </header>

        <nav class="flex justify-center border-b border-stone-200 mb-8">
            <button id="btn-radio" class="nav-button active text-lg font-semibold py-4 px-6">📻 Radio</button>
            <button id="btn-tv" class="nav-button text-lg font-semibold py-4 px-6">📺 Televisión</button>
            <button id="btn-cine" class="nav-button text-lg font-semibold py-4 px-6">🎬 Cine</button>
            <button id="btn-redes" class="nav-button text-lg font-semibold py-4 px-6">📱 Redes Sociales</button>
        </nav>

        <main>
            <!-- CONTENEDOR PRINCIPAL QUE CAMBIA SU CONTENIDO -->
            <div id="main-content-container">
                <!-- SECCIÓN RADIO -->
                <section id="content-radio" class="content-visible space-y-12">
                    <div class="text-center">
                        <h2 class="text-3xl font-bold text-purple-800 mb-2">La Música en la Radio</h2>
                        <p class="max-w-3xl mx-auto text-stone-600">La radio fue el primer gran altavoz de la música, el primer medio masivo que llevó el sonido a los hogares. La figura clave en esta etapa fue el **DJ**, un prescriptor musical cuyo gusto influenciaba a millones de oyentes.</p>
                    </div>
                    <div class="grid md:grid-cols-2 gap-12 items-center">
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-6">Historia y Evolución</h3>
                            <div class="relative pl-8">
                                <div class="timeline-line"></div>
                                <div class="space-y-8">
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 20-30: Emisiones en Directo</h4>
                                        <p class="text-sm text-stone-600">Orquestas y cantantes se presentaban en los estudios para que la música llegara en vivo a las casas.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 50: La Radiofórmula</h4>
                                        <p class="text-sm text-stone-600">Nacen emisoras centradas en éxitos, impulsando el rock and roll y el pop. El DJ se convierte en un ídolo.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 70-80: Radios Temáticas</h4>
                                        <p class="text-sm text-stone-600">Surgen emisoras especializadas en rock, jazz o clásica, creando audiencias más específicas.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Actualidad: Era Digital</h4>
                                        <p class="text-sm text-stone-600">Los programas se convierten en podcasts y las emisoras se integran en redes sociales, manteniendo su influencia.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div>
                            <h3 id="chart-title" class="text-2xl font-semibold text-purple-700 mb-4 text-center">Formatos de Radio Hoy</h3>
                            <div class="chart-container">
                                <canvas id="mainChart"></canvas>
                            </div>
                        </div>
                    </div>
                </section>
                <!-- OTRAS SECCIONES (OCULTAS POR DEFECTO CON LA NUEVA CLASE) -->
                <section id="content-tv" class="content-hidden space-y-12">
                    <div class="text-center">
                        <h2 class="text-3xl font-bold text-purple-800 mb-2">La Música en la Televisión</h2>
                        <p class="max-w-3xl mx-auto text-stone-600">La televisión añadió un componente visual crucial a la música. Ya no solo se escuchaba a los artistas, sino que también se les **veía**, lo que cambió para siempre la industria.</p>
                    </div>
                    <div class="grid md:grid-cols-2 gap-12 items-center">
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-6">Historia y Evolución</h3>
                            <div class="relative pl-8">
                                <div class="timeline-line"></div>
                                <div class="space-y-8">
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 50-60: Programas de Variedades</h4>
                                        <p class="text-sm text-stone-600">Artistas como Elvis Presley o The Beatles se convierten en fenómenos globales gracias a su imagen en TV.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 80: Nace MTV</h4>
                                        <p class="text-sm text-stone-600">El videoclip se convierte en el formato principal. Artistas como Michael Jackson y Madonna se vuelven superestrellas.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 90-2000: Talent Shows</h4>
                                        <p class="text-sm text-stone-600">Programas como Operación Triunfo se vuelven inmensamente populares, sirviendo como vía de descubrimiento.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Actualidad: Streaming</h4>
                                        <p class="text-sm text-stone-600">La TV lineal pierde fuelle frente a YouTube, pero los talent shows siguen siendo una forma clave de descubrir artistas.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-4 text-center">Impacto de Formatos TV</h3>
                            <div class="chart-container">
                                <canvas></canvas>
                            </div>
                        </div>
                    </div>
                </section>
                <section id="content-cine" class="content-hidden space-y-12">
                    <div class="text-center">
                        <h2 class="text-3xl font-bold text-purple-800 mb-2">La Música en el Cine</h2>
                        <p class="max-w-3xl mx-auto text-stone-600">En el cine, la música es un elemento narrativo y emocional, tan importante como la fotografía o el guion, capaz de transformar por completo una escena.</p>
                    </div>
                    <div class="grid md:grid-cols-2 gap-12 items-center">
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-6">Historia y Evolución</h3>
                            <div class="relative pl-8">
                                <div class="timeline-line"></div>
                                <div class="space-y-8">
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">1895-1927: Cine Mudo</h4>
                                        <p class="text-sm text-stone-600">Un pianista o una orquesta tocaban en directo en el cine para crear atmósfera y generar emociones.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">1927 en adelante: Cine Sonoro</h4>
                                        <p class="text-sm text-stone-600">Compositores como Max Steiner crean el modelo de la banda sonora orquestal de Hollywood.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 60-70: Música Popular</h4>
                                        <p class="text-sm text-stone-600">Canciones de rock y pop se usan en películas, convirtiendo las bandas sonoras en grandes éxitos comerciales.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Actualidad: Era Digital</h4>
                                        <p class="text-sm text-stone-600">Se combina la orquesta con sintetizadores. Compositores como Hans Zimmer se vuelven tan famosos como los directores.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-4 text-center">Evolución Estilos de BSO</h3>
                            <div class="chart-container">
                                <canvas></canvas>
                            </div>
                        </div>
                    </div>
                </section>
                <section id="content-redes" class="content-hidden space-y-12">
                    <div class="text-center">
                        <h2 class="text-3xl font-bold text-purple-800 mb-2">La Música en las Redes Sociales</h2>
                        <p class="max-w-3xl mx-auto text-stone-600">Las redes sociales han democratizado la música, convirtiendo a cualquier persona en un potencial creador y distribuidor de contenido musical.</p>
                    </div>
                    <div class="grid md:grid-cols-2 gap-12 items-center">
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-6">Historia y Evolución</h3>
                            <div class="relative pl-8">
                                <div class="timeline-line"></div>
                                <div class="space-y-8">
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 90: Intercambio de Archivos</h4>
                                        <p class="text-sm text-stone-600">Napster populariza el formato MP3 y la descarga de música, cambiando la industria para siempre.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 2000: MySpace</h4>
                                        <p class="text-sm text-stone-600">Los artistas suben sus canciones y conectan con fans directamente, sin necesidad de un sello discográfico.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Años 2010: El Streaming</h4>
                                        <p class="text-sm text-stone-600">Spotify y YouTube dominan la industria, ofreciendo un catálogo musical casi infinito a los usuarios.</p>
                                    </div>
                                    <div class="timeline-item relative">
                                        <h4 class="font-bold">Actualidad: La Viralidad</h4>
                                        <p class="text-sm text-stone-600">Un artista puede hacerse viral en TikTok o Instagram con un solo fragmento, catapultando su carrera en días.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div>
                            <h3 class="text-2xl font-semibold text-purple-700 mb-4 text-center">Plataformas Virales (Cuota)</h3>
                            <div class="chart-container">
                                <canvas></canvas>
                            </div>
                        </div>
                    </div>
                </section>
            </div>
        </main>

        <footer class="text-center mt-16 border-t pt-6 border-stone-200">
            <p class="text-stone-500">Una exploración interactiva sobre la música y su evolución tecnológica.</p>
        </footer>

    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const chartColors = {
                purple: 'rgba(168, 85, 247, 0.7)',
                pink: 'rgba(236, 72, 153, 0.7)',
                amber: 'rgba(245, 158, 11, 0.7)',
                teal: 'rgba(20, 184, 166, 0.7)',
                sky: 'rgba(56, 189, 248, 0.7)',
            };
            
            const chartHoverColors = {
                purple: 'rgba(168, 85, 247, 1)',
                pink: 'rgba(236, 72, 153, 1)',
                amber: 'rgba(245, 158, 11, 1)',
                teal: 'rgba(20, 184, 166, 1)',
                sky: 'rgba(56, 189, 248, 1)',
            };

            // Datos y configuración para cada gráfico
            const chartData = {
                'btn-radio': {
                    type: 'pie',
                    title: 'Formatos de Radio Hoy',
                    data: {
                        labels: ['Radiofórmula', 'Podcast Musical', 'Radio Temática'],
                        datasets: [{
                            label: 'Distribución de Formatos',
                            data: [45, 35, 20],
                            backgroundColor: [chartColors.purple, chartColors.pink, chartColors.amber],
                            hoverBackgroundColor: [chartHoverColors.purple, chartHoverColors.pink, chartHoverColors.amber],
                            borderColor: '#fdfaf6',
                            borderWidth: 2
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { position: 'top' }
                        }
                    }
                },
                'btn-tv': {
                    type: 'bar',
                    title: 'Impacto de Formatos TV',
                    data: {
                        labels: ['Videoclips (Streaming)', 'Talent Shows', 'Premios Musicales'],
                        datasets: [{
                            label: 'Nivel de Influencia Actual',
                            data: [85, 65, 50],
                            backgroundColor: [chartColors.teal, chartColors.purple, chartColors.sky],
                            hoverBackgroundColor: [chartHoverColors.teal, chartHoverColors.purple, chartHoverColors.sky],
                            borderRadius: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { display: false } },
                        scales: { y: { beginAtZero: true } }
                    }
                },
                'btn-cine': {
                    type: 'line',
                    title: 'Evolución Estilos de BSO',
                    data: {
                        labels: ['1950', '1970', '1990', '2010', 'Hoy'],
                        datasets: [{
                            label: 'Orquestal',
                            data: [90, 70, 60, 50, 40],
                            borderColor: chartColors.purple,
                            backgroundColor: chartColors.purple,
                            fill: false,
                            tension: 0.4
                        }, {
                            label: 'Pop/Rock',
                            data: [5, 25, 30, 35, 30],
                            borderColor: chartColors.pink,
                            backgroundColor: chartColors.pink,
                            fill: false,
                            tension: 0.4
                        }, {
                            label: 'Electrónica/Digital',
                            data: [0, 5, 10, 15, 30],
                            borderColor: chartColors.teal,
                            backgroundColor: chartColors.teal,
                            fill: false,
                            tension: 0.4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { y: { beginAtZero: true } }
                    }
                },
                'btn-redes': {
                    type: 'doughnut',
                    title: 'Plataformas Virales (Cuota)',
                    data: {
                        labels: ['TikTok', 'Instagram', 'YouTube'],
                        datasets: [{
                            label: 'Cuota de Viralidad Musical',
                            data: [60, 25, 15],
                            backgroundColor: [chartColors.sky, chartColors.pink, chartColors.purple],
                            hoverBackgroundColor: [chartHoverColors.sky, chartHoverColors.pink, chartHoverColors.purple],
                            borderColor: '#fdfaf6',
                            borderWidth: 2
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { position: 'top' } }
                    }
                }
            };

            let currentChart = null;
            const navButtons = document.querySelectorAll('.nav-button');
            const contentSections = document.querySelectorAll('main section');
            const mainChartCanvas = document.getElementById('mainChart');
            const chartTitleElement = document.getElementById('chart-title');

            // Función para actualizar el gráfico
            const updateChart = (buttonId) => {
                // Si ya existe un gráfico, lo destruimos para limpiar
                if (currentChart) {
                    currentChart.destroy();
                }

                // Obtenemos los datos del gráfico para la pestaña seleccionada
                const chartInfo = chartData[buttonId];
                if (chartInfo) {
                    // Actualizamos el título del gráfico
                    chartTitleElement.textContent = chartInfo.title;

                    // Creamos el nuevo gráfico
                    currentChart = new Chart(mainChartCanvas, {
                        type: chartInfo.type,
                        data: chartInfo.data,
                        options: chartInfo.options
                    });
                }
            };

            // Función para cambiar de sección de contenido
            const switchContent = (buttonId) => {
                // Ocultamos todas las secciones de contenido
                contentSections.forEach(section => section.classList.add('content-hidden'));
                
                // Mostramos la sección de contenido correspondiente
                const selectedSection = document.getElementById(buttonId.replace('btn-', 'content-'));
                if (selectedSection) {
                    selectedSection.classList.remove('content-hidden');
                    selectedSection.classList.add('content-visible');
                }
            };

            // Agregamos los listeners a los botones de navegación
            navButtons.forEach(button => {
                button.addEventListener('click', () => {
                    // Quitamos la clase 'active' de todos los botones
                    navButtons.forEach(btn => btn.classList.remove('active'));
                    // Añadimos la clase 'active' al botón clickeado
                    button.classList.add('active');

                    // Llamamos a las funciones para actualizar el contenido y el gráfico
                    switchContent(button.id);
                    updateChart(button.id);
                });
            });
            
            // Configuración inicial al cargar la página: muestra la sección de radio
            updateChart('btn-radio');
        });
    </script>
</body>
</html>
