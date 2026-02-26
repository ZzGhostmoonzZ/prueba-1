<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Garaje Central - Reserva tu puesto</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gye: {
                            celeste: '#74C3E9', // Azul claro de la bandera de Guayaquil
                            light: '#E6F4FB',
                            dark: '#4AA6D4'
                        },
                        ios: {
                            bg: '#F2F2F7', // Fondo gris claro de iOS
                            card: '#FFFFFF',
                            text: '#1C1C1E',
                            gray: '#8E8E93'
                        }
                    },
                    fontFamily: {
                        sans: ['-apple-system', 'BlinkMacSystemFont', '"Segoe UI"', 'Roboto', 'Helvetica', 'Arial', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        /* Estilos iOS personalizados */
        body {
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            background-color: #F2F2F7;
        }
        
        /* Ocultar scrollbars para un look más limpio */
        ::-webkit-scrollbar {
            width: 0px;
            background: transparent;
        }

        .ios-shadow {
            box-shadow: 0 4px 24px rgba(0, 0, 0, 0.04);
        }

        .spot-btn {
            transition: all 0.2s cubic-bezier(0.25, 0.1, 0.25, 1);
        }
        
        .spot-btn:active {
            transform: scale(0.95);
        }

        /* Inputs nativos limpios */
        input[type="datetime-local"], input[type="text"] {
            -webkit-appearance: none;
            background: transparent;
        }
    </style>
</head>
<body class="text-ios-text font-sans pb-24">

    <!-- Navbar estilo iOS (Efecto Glass) -->
    <nav class="sticky top-0 z-40 bg-white/80 backdrop-blur-md border-b border-gray-200/80">
        <div class="max-w-5xl mx-auto px-4 sm:px-6">
            <div class="flex items-center justify-between h-14">
                <div class="flex items-center gap-2 text-gye-dark">
                    <i data-lucide="car-front" class="h-6 w-6"></i>
                    <span class="font-semibold text-[17px] tracking-tight text-ios-text">Garaje Central</span>
                </div>
                <div class="flex items-center gap-4">
                    <div class="text-[13px] font-medium bg-gye-light text-gye-dark px-3 py-1 rounded-full">
                        $1.25 / hr
                    </div>
                    <!-- Botón de Admin (Dueño) -->
                    <button id="btn-admin" class="text-ios-gray hover:text-gye-dark transition-colors">
                        <i data-lucide="lock" class="h-5 w-5"></i>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Contenido Principal -->
    <main class="max-w-5xl mx-auto px-4 sm:px-6 py-6">
        
        <!-- Header de sección -->
        <div class="mb-6 px-2">
            <h1 class="text-[28px] font-bold tracking-tight">Nueva Reserva</h1>
            <p class="text-[15px] text-ios-gray mt-1">Completa tus datos y elige un puesto.</p>
        </div>

        <div class="flex flex-col md:flex-row gap-6">
            
            <!-- Columna Izquierda: Formulario iOS -->
            <div class="w-full md:w-1/2 space-y-6">
                
                <!-- IA Magic Input -->
                <div class="bg-white rounded-[20px] p-4 ios-shadow relative overflow-hidden group">
                    <div class="absolute top-0 left-0 w-1 h-full bg-gye-celeste"></div>
                    <label class="block text-[13px] font-semibold text-gye-dark mb-1 uppercase tracking-wider flex items-center gap-1">
                        <i data-lucide="sparkles" class="h-3 w-3"></i> Asistente Inteligente
                    </label>
                    <p class="text-[14px] text-ios-gray mb-3">¿Cuándo vienes? Escríbelo y lo llenaremos por ti.</p>
                    <div class="flex gap-2">
                        <input type="text" id="magic-input" placeholder="Ej: Hoy a las 3pm por 2 horas" 
                            class="flex-1 bg-ios-bg px-3 py-2.5 rounded-xl outline-none text-[15px] focus:ring-2 focus:ring-gye-celeste/50 transition-all">
                        <button id="btn-magic" class="bg-gye-celeste text-white px-4 py-2.5 rounded-xl font-medium text-[15px] active:bg-gye-dark transition-colors">
                            Auto
                        </button>
                    </div>
                    <p id="magic-status" class="text-[12px] mt-2 hidden font-medium"></p>
                </div>

                <!-- Lista Agrupada estilo iOS -->
                <div class="bg-white rounded-[20px] ios-shadow overflow-hidden">
                    <!-- Fila: Nombre -->
                    <div class="flex items-center justify-between px-4 py-3 border-b border-gray-100">
                        <span class="text-[16px] text-ios-text w-1/3">Nombre</span>
                        <input type="text" id="user-name" placeholder="Juan Pérez" class="w-2/3 text-right text-[16px] text-ios-gray outline-none focus:text-ios-text">
                    </div>
                    
                    <!-- Fila: Placa -->
                    <div class="flex items-center justify-between px-4 py-3 border-b border-gray-100">
                        <span class="text-[16px] text-ios-text w-1/3">Placa</span>
                        <input type="text" id="user-plate" placeholder="GSQ-1234" class="w-2/3 text-right text-[16px] text-ios-gray outline-none focus:text-ios-text uppercase">
                    </div>

                    <!-- Fila: Entrada -->
                    <div class="flex items-center justify-between px-4 py-3 border-b border-gray-100">
                        <span class="text-[16px] text-ios-text w-1/3">Entrada</span>
                        <input type="datetime-local" id="start-time" class="w-2/3 text-right text-[16px] text-gye-dark font-medium outline-none">
                    </div>
                    
                    <!-- Fila: Salida -->
                    <div class="flex items-center justify-between px-4 py-3">
                        <span class="text-[16px] text-ios-text w-1/3">Salida</span>
                        <input type="datetime-local" id="end-time" class="w-2/3 text-right text-[16px] text-gye-dark font-medium outline-none">
                    </div>
                </div>

                <!-- IA Sugerencias (Oculto por defecto) -->
                <div id="ai-suggestions-panel" class="bg-white rounded-[20px] p-5 ios-shadow hidden">
                    <div class="flex items-center justify-between mb-2">
                        <h3 class="text-[16px] font-semibold text-ios-text flex items-center gap-2">
                            <span class="w-6 h-6 rounded-full bg-gye-light text-gye-dark flex items-center justify-center">
                                <i data-lucide="map" class="h-3 w-3"></i>
                            </span>
                            Ideas Locales
                        </h3>
                        <button id="btn-get-suggestions" class="text-[13px] text-gye-dark font-medium px-2 py-1 bg-gye-light rounded-lg">
                            Sugerir
                        </button>
                    </div>
                    <p class="text-[14px] text-ios-gray mb-3">Tienes <span id="suggestion-hours-text" class="font-medium text-ios-text"></span> libres. ¿Qué hacemos en Guayaquil?</p>
                    <div id="ai-suggestions-content" class="text-[14px] text-ios-text space-y-2 hidden bg-ios-bg p-3 rounded-xl"></div>
                </div>

            </div>

            <!-- Columna Derecha: Mapa y Resumen -->
            <div class="w-full md:w-1/2 space-y-6">
                
                <!-- Mapa Interactivo -->
                <div class="bg-white rounded-[20px] p-5 ios-shadow">
                    <div class="flex justify-between items-center mb-4">
                        <h2 class="text-[17px] font-semibold">Selecciona Puesto</h2>
                        <span id="spot-badge" class="px-2 py-1 bg-gray-100 text-ios-gray text-[12px] font-bold rounded-md">Ninguno</span>
                    </div>

                    <!-- Cuadrícula -->
                    <div class="bg-ios-bg p-3 rounded-2xl">
                        <div class="w-full text-center mb-3">
                            <span class="text-[10px] font-bold text-ios-gray uppercase tracking-widest bg-gray-200/60 px-4 py-1 rounded-full">Puerta / Calle</span>
                        </div>
                        <div id="parking-map" class="grid grid-cols-5 gap-2">
                            <!-- JS inyecta puestos aquí -->
                        </div>
                    </div>

                    <!-- Leyenda minimalista -->
                    <div class="flex justify-center gap-5 mt-4">
                        <div class="flex items-center gap-1.5"><div class="w-3 h-3 rounded-full bg-white border border-gray-300"></div><span class="text-[12px] text-ios-gray">Libre</span></div>
                        <div class="flex items-center gap-1.5"><div class="w-3 h-3 rounded-full bg-gye-celeste"></div><span class="text-[12px] text-ios-gray">Tu Puesto</span></div>
                        <div class="flex items-center gap-1.5"><div class="w-3 h-3 rounded-full bg-gray-300"></div><span class="text-[12px] text-ios-gray">Ocupado</span></div>
                    </div>
                </div>

                <!-- Total a Pagar / Sticky inferior en móvil -->
                <div class="fixed bottom-0 left-0 w-full bg-white/90 backdrop-blur-lg border-t border-gray-200 p-4 pb-8 md:pb-4 md:relative md:bg-transparent md:backdrop-blur-none md:border-none md:p-0 z-30 ios-shadow md:shadow-none">
                    <div class="max-w-5xl mx-auto flex items-center justify-between mb-3 md:bg-white md:p-5 md:rounded-[20px] md:mb-0">
                        <div>
                            <p class="text-[13px] text-ios-gray">Total a pagar</p>
                            <p id="summary-price" class="text-[28px] font-bold text-ios-text leading-tight">$0.00</p>
                            <p id="summary-time" class="text-[12px] text-ios-gray">0 horas</p>
                        </div>
                        <button id="btn-reserve" class="bg-gye-celeste hover:bg-gye-dark text-white font-semibold text-[17px] py-3.5 px-8 rounded-full shadow-lg shadow-gye-celeste/30 transition-all disabled:opacity-50 disabled:shadow-none disabled:cursor-not-allowed">
                            Reservar
                        </button>
                    </div>
                </div>
                
            </div>
        </div>
    </main>

    <!-- Modal Admin (Panel de Dueño) -->
    <div id="admin-modal" class="fixed inset-0 bg-ios-bg z-50 flex flex-col hidden transition-transform translate-y-full duration-300 ease-in-out">
        <div class="bg-white px-4 py-3 border-b border-gray-200 flex justify-between items-center sticky top-0">
            <h2 class="text-[17px] font-semibold">Panel de Administración</h2>
            <button id="btn-close-admin" class="text-gye-dark font-medium text-[17px]">Cerrar</button>
        </div>
        <div class="flex-1 overflow-y-auto p-4">
            <div class="flex justify-between items-end mb-4 px-1">
                <div>
                    <h3 class="text-[22px] font-bold">Reservas Activas</h3>
                    <p class="text-[14px] text-ios-gray">Datos registrados en el sistema.</p>
                </div>
                <button id="btn-clear-db" class="text-[13px] text-red-500 font-medium px-3 py-1 bg-red-50 rounded-lg">Borrar Todo</button>
            </div>
            
            <div id="admin-list" class="space-y-3">
                <!-- Se inyectan items aquí -->
            </div>
        </div>
    </div>

    <!-- Modal de Confirmación iOS (Alert) -->
    <div id="ios-alert" class="fixed inset-0 bg-black/40 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4 opacity-0 transition-opacity duration-200">
        <div class="bg-white/90 backdrop-blur-xl rounded-[14px] w-full max-w-[270px] text-center overflow-hidden transform scale-95 transition-transform duration-200" id="ios-alert-content">
            <div class="p-5 pt-6">
                <h3 id="alert-title" class="text-[17px] font-semibold text-ios-text mb-1">Título</h3>
                <p id="alert-message" class="text-[13px] text-ios-text leading-tight"></p>
            </div>
            <div class="border-t border-gray-300/50 flex">
                <button id="btn-alert-ok" class="w-full py-3 text-[17px] font-semibold text-gye-celeste active:bg-gray-200/50 transition-colors">
                    OK
                </button>
            </div>
        </div>
    </div>

    <script>
        // Inicializar iconos
        lucide.createIcons();

        // Configuración Global
        const TOTAL_SPOTS = 25;
        const PRICE_PER_HOUR = 1.25;
        const DB_KEY = 'garaje_reservations'; // Clave para LocalStorage

        // Variables de estado
        let selectedSpot = null;
        let totalHoursCalculated = 0;
        let totalPriceCalculated = 0;

        // Referencias DOM
        const formName = document.getElementById('user-name');
        const formPlate = document.getElementById('user-plate');
        const inputStart = document.getElementById('start-time');
        const inputEnd = document.getElementById('end-time');
        
        const summaryPrice = document.getElementById('summary-price');
        const summaryTime = document.getElementById('summary-time');
        const spotBadge = document.getElementById('spot-badge');
        const btnReserve = document.getElementById('btn-reserve');
        const mapContainer = document.getElementById('parking-map');

        // Modales
        const iosAlert = document.getElementById('ios-alert');
        const iosAlertContent = document.getElementById('ios-alert-content');
        const alertTitle = document.getElementById('alert-title');
        const alertMessage = document.getElementById('alert-message');
        const btnAlertOk = document.getElementById('btn-alert-ok');

        const adminModal = document.getElementById('admin-modal');
        const btnAdmin = document.getElementById('btn-admin');
        const btnCloseAdmin = document.getElementById('btn-close-admin');
        const adminList = document.getElementById('admin-list');
        const btnClearDb = document.getElementById('btn-clear-db');

        // Gemeni API Elements
        const apiKey = ""; 
        const magicInput = document.getElementById('magic-input');
        const btnMagic = document.getElementById('btn-magic');
        const magicStatus = document.getElementById('magic-status');
        
        const aiSuggestionsPanel = document.getElementById('ai-suggestions-panel');
        const suggestionHoursText = document.getElementById('suggestion-hours-text');
        const btnGetSuggestions = document.getElementById('btn-get-suggestions');
        const aiSuggestionsContent = document.getElementById('ai-suggestions-content');

        // --- MANEJO DE BASE DE DATOS LOCAL (localStorage) ---
        
        function getReservations() {
            return JSON.parse(localStorage.getItem(DB_KEY) || '[]');
        }

        function saveReservation(data) {
            const current = getReservations();
            current.push(data);
            localStorage.setItem(DB_KEY, JSON.stringify(current));
        }

        function getOccupiedSpots() {
            const reservations = getReservations();
            const now = new Date();
            let occupied = [];
            
            reservations.forEach(res => {
                const end = new Date(res.end);
                // Si la fecha de salida es en el futuro, el puesto sigue ocupado
                if (end > now) {
                    occupied.push(parseInt(res.spot));
                }
            });
            return occupied;
        }

        // --- UI ESTILO iOS ---

        function showAlert(title, message, callback = null) {
            alertTitle.textContent = title;
            alertMessage.innerHTML = message;
            
            iosAlert.classList.remove('hidden');
            setTimeout(() => {
                iosAlert.classList.remove('opacity-0');
                iosAlertContent.classList.remove('scale-95');
                iosAlertContent.classList.add('scale-100');
            }, 10);

            btnAlertOk.onclick = () => {
                iosAlert.classList.add('opacity-0');
                iosAlertContent.classList.remove('scale-100');
                iosAlertContent.classList.add('scale-95');
                setTimeout(() => { iosAlert.classList.add('hidden'); if(callback) callback(); }, 200);
            };
        }

        // --- LÓGICA DE TIEMPO Y CÁLCULOS ---

        function formatDateTimeLocal(date) {
            const pad = (n) => n.toString().padStart(2, '0');
            return `${date.getFullYear()}-${pad(date.getMonth() + 1)}-${pad(date.getDate())}T${pad(date.getHours())}:${pad(date.getMinutes())}`;
        }

        function setupDefaultTimes() {
            const now = new Date();
            const ms = 1000 * 60 * 15;
            const roundedNow = new Date(Math.ceil(now.getTime() / ms) * ms);
            const later = new Date(roundedNow.getTime() + (2 * 60 * 60 * 1000));

            const nowFormatted = formatDateTimeLocal(roundedNow);
            inputStart.min = nowFormatted;
            inputStart.value = nowFormatted;
            inputEnd.min = nowFormatted;
            inputEnd.value = formatDateTimeLocal(later);
            calculatePrice();
        }

        function calculatePrice() {
            const startVal = inputStart.value;
            const endVal = inputEnd.value;

            if (!startVal || !endVal) return updatePriceDisplay(0, 0);

            const startTime = new Date(startVal);
            const endTime = new Date(endVal);
            
            if (endTime <= startTime) {
                updatePriceDisplay(0, 0);
                inputEnd.value = '';
                return showAlert('Hora Inválida', 'La salida debe ser posterior a la entrada.');
            }

            const diffMinutes = (endTime - startTime) / (1000 * 60);
            const hoursToCharge = Math.ceil(diffMinutes / 60);
            const totalCost = hoursToCharge * PRICE_PER_HOUR;

            totalHoursCalculated = hoursToCharge;
            totalPriceCalculated = totalCost;

            let timeStr = `${Math.floor(diffMinutes/60)}h ${Math.floor(diffMinutes%60)}m`;
            updatePriceDisplay(timeStr, totalCost);
            validateForm();

            // Sugerencias IA UI
            if (hoursToCharge > 0) {
                aiSuggestionsPanel.classList.remove('hidden');
                suggestionHoursText.textContent = hoursToCharge === 1 ? '1 hr' : `${hoursToCharge} hrs`;
                aiSuggestionsContent.classList.add('hidden');
                aiSuggestionsContent.innerHTML = '';
            } else {
                aiSuggestionsPanel.classList.add('hidden');
            }
        }

        function updatePriceDisplay(timeStr, price) {
            summaryTime.textContent = timeStr === 0 ? '0 horas' : timeStr;
            summaryPrice.textContent = `$${price.toFixed(2)}`;
        }

        // --- LÓGICA DEL MAPA ---

        function renderMap() {
            mapContainer.innerHTML = '';
            const occupiedSpots = getOccupiedSpots();
            
            for (let i = 1; i <= TOTAL_SPOTS; i++) {
                const isOccupied = occupiedSpots.includes(i);
                
                const spotEl = document.createElement('div');
                spotEl.className = `
                    relative aspect-square rounded-[10px] flex items-center justify-center
                    text-[14px] font-bold spot-btn select-none
                    ${isOccupied 
                        ? 'bg-gray-200 text-gray-400 cursor-not-allowed' 
                        : 'bg-white text-ios-gray cursor-pointer border border-gray-200 shadow-sm'}
                `;
                spotEl.dataset.spotNumber = i;
                spotEl.textContent = `${i}`;

                if (!isOccupied) {
                    spotEl.addEventListener('click', () => selectSpot(i, spotEl));
                }
                
                mapContainer.appendChild(spotEl);
            }
        }

        function selectSpot(spotNumber, element) {
            // Limpiar anterior
            if (selectedSpot) {
                const prevEl = document.querySelector(`[data-spot-number="${selectedSpot}"]`);
                if (prevEl) {
                    prevEl.className = 'relative aspect-square rounded-[10px] flex items-center justify-center text-[14px] font-bold spot-btn select-none bg-white text-ios-gray cursor-pointer border border-gray-200 shadow-sm';
                }
            }

            // Toggle logic
            if (selectedSpot === spotNumber) {
                selectedSpot = null;
                spotBadge.textContent = 'Ninguno';
                spotBadge.className = 'px-2 py-1 bg-gray-100 text-ios-gray text-[12px] font-bold rounded-md';
            } else {
                selectedSpot = spotNumber;
                element.className = 'relative aspect-square rounded-[10px] flex items-center justify-center text-[14px] font-bold spot-btn select-none bg-gye-celeste text-white cursor-pointer shadow-md shadow-gye-celeste/40 transform scale-105';
                
                spotBadge.textContent = `Puesto ${spotNumber}`;
                spotBadge.className = 'px-2 py-1 bg-gye-light text-gye-dark text-[12px] font-bold rounded-md';
            }
            validateForm();
        }

        function validateForm() {
            const hasName = formName.value.trim().length > 0;
            const hasPlate = formPlate.value.trim().length > 0;
            
            if (selectedSpot !== null && totalPriceCalculated > 0 && hasName && hasPlate) {
                btnReserve.disabled = false;
            } else {
                btnReserve.disabled = true;
            }
        }

        // --- PROCESAR RESERVA ---

        function processReservation() {
            const reservationData = {
                id: Date.now().toString(36),
                name: formName.value.trim(),
                plate: formPlate.value.trim().toUpperCase(),
                spot: selectedSpot,
                start: inputStart.value,
                end: inputEnd.value,
                cost: totalPriceCalculated,
                timestamp: new Date().toISOString()
            };

            // Guardar en la base de datos local
            saveReservation(reservationData);

            showAlert('Reserva Exitosa', `<b>Puesto ${selectedSpot}</b> confirmado para <b>${reservationData.plate}</b>.<br><br>Total cobrado: $${totalPriceCalculated.toFixed(2)}`, () => {
                // Reset UI
                selectedSpot = null;
                spotBadge.textContent = 'Ninguno';
                spotBadge.className = 'px-2 py-1 bg-gray-100 text-ios-gray text-[12px] font-bold rounded-md';
                formName.value = '';
                formPlate.value = '';
                setupDefaultTimes();
                renderMap(); // Volver a dibujar mapa (el puesto ahora estará bloqueado)
                validateForm();
            });
        }

        // --- PANEL DE ADMINISTRACIÓN ---
        
        btnAdmin.addEventListener('click', () => {
            renderAdminList();
            adminModal.classList.remove('hidden');
            // Timeout para animar la entrada
            setTimeout(() => {
                adminModal.classList.remove('translate-y-full');
            }, 10);
        });

        btnCloseAdmin.addEventListener('click', () => {
            adminModal.classList.add('translate-y-full');
            setTimeout(() => {
                adminModal.classList.add('hidden');
            }, 300);
        });

        btnClearDb.addEventListener('click', () => {
            if(confirm('¿Estás seguro de borrar toda la base de datos de reservas?')) {
                localStorage.removeItem(DB_KEY);
                renderAdminList();
                renderMap(); // Actualiza el mapa para liberar puestos
            }
        });

        function renderAdminList() {
            const reservations = getReservations().reverse(); // Más recientes primero
            adminList.innerHTML = '';

            if(reservations.length === 0) {
                adminList.innerHTML = '<p class="text-center text-ios-gray mt-10">No hay reservas registradas.</p>';
                return;
            }

            reservations.forEach(r => {
                const sDate = new Date(r.start).toLocaleString('es-EC', {day:'2-digit', month:'short', hour:'2-digit', minute:'2-digit'});
                const eDate = new Date(r.end).toLocaleString('es-EC', {hour:'2-digit', minute:'2-digit'});
                
                const card = document.createElement('div');
                card.className = 'bg-white p-4 rounded-[16px] ios-shadow border border-gray-100 flex justify-between items-center';
                card.innerHTML = `
                    <div>
                        <div class="flex items-center gap-2 mb-1">
                            <span class="font-bold text-[16px]">${r.plate}</span>
                            <span class="bg-gye-light text-gye-dark text-[10px] px-2 py-0.5 rounded uppercase font-bold">P-${r.spot}</span>
                        </div>
                        <p class="text-[14px] text-ios-text">${r.name}</p>
                        <p class="text-[12px] text-ios-gray">${sDate} - ${eDate}</p>
                    </div>
                    <div class="text-right">
                        <span class="text-[18px] font-bold text-gye-celeste">$${r.cost.toFixed(2)}</span>
                    </div>
                `;
                adminList.appendChild(card);
            });
        }

        // --- FUNCIONALIDADES GEMINI API ---

        async function fetchGeminiWithRetry(prompt, systemInstruction, isJson = false, retries = 5) {
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                systemInstruction: { parts: [{ text: systemInstruction }] }
            };
            if (isJson) {
                payload.generationConfig = {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            start: { type: "STRING" }, end: { type: "STRING" },
                            name: { type: "STRING" }, plate: { type: "STRING" }
                        },
                        required: ["start", "end"]
                    }
                };
            }
            let delay = 1000;
            for (let i = 0; i < retries; i++) {
                try {
                    const response = await fetch(url, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload) });
                    if (!response.ok) throw new Error(response.status);
                    const data = await response.json();
                    return data.candidates?.[0]?.content?.parts?.[0]?.text;
                } catch (error) {
                    if (i === retries - 1) throw error;
                    await new Promise(res => setTimeout(res, delay));
                    delay *= 2;
                }
            }
        }

        // Reserva Mágica 
        btnMagic.addEventListener('click', async () => {
            const text = magicInput.value.trim();
            if (!text) return;

            btnMagic.disabled = true;
            btnMagic.textContent = '...';
            magicStatus.classList.remove('hidden', 'text-red-500');
            magicStatus.classList.add('text-gye-celeste');
            magicStatus.textContent = 'Interpretando...';

            try {
                const now = new Date();
                const context = `Hoy es ${now.toLocaleDateString('es-ES', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' })}`;
                const sysPrompt = `Eres asistente de un garaje en Guayaquil. Extrae fechas, nombre del cliente y placa del vehículo. Retorna JSON "start" y "end" (YYYY-MM-DDTHH:mm). Si no hay salida, asume 2h extra. "name" y "plate" son opcionales. Contexto: ${context}`;
                
                const response = await fetchGeminiWithRetry(text, sysPrompt, true);
                const result = JSON.parse(response);
                
                if (result.start && result.end) {
                    inputStart.value = result.start;
                    inputEnd.value = result.end;
                    if(result.name) formName.value = result.name;
                    if(result.plate) formPlate.value = result.plate.toUpperCase();
                    
                    calculatePrice();
                    magicStatus.classList.replace('text-gye-celeste', 'text-green-500');
                    magicStatus.textContent = '¡Datos llenados con éxito!';
                    setTimeout(() => magicStatus.classList.add('hidden'), 3000);
                }
            } catch (e) {
                magicStatus.classList.replace('text-gye-celeste', 'text-red-500');
                magicStatus.textContent = 'No entendimos el formato. Intenta ser más claro.';
            } finally {
                btnMagic.disabled = false;
                btnMagic.textContent = 'Auto';
            }
        });

        // Sugerencias IA
        btnGetSuggestions.addEventListener('click', async () => {
            btnGetSuggestions.disabled = true;
            btnGetSuggestions.textContent = '...';
            aiSuggestionsContent.classList.remove('hidden');
            aiSuggestionsContent.innerHTML = '<p class="text-ios-gray animate-pulse">Buscando planes...</p>';

            try {
                const sysPrompt = `Eres un guía turístico guayaco. Recomienda 3 actividades cerca del garaje (centro de Guayaquil) que se ajusten estrictamente al tiempo disponible. Usa un tono fresco, viñetas HTML <ul><li> y emojis. Retorna SOLO HTML sin bloques de markdown.`;
                const userPrompt = `Tengo ${totalHoursCalculated} hora(s) libre(s).`;
                const response = await fetchGeminiWithRetry(userPrompt, sysPrompt, false);
                aiSuggestionsContent.innerHTML = response.replace(/```html/g, '').replace(/```/g, '');
            } catch (e) {
                aiSuggestionsContent.innerHTML = '<p class="text-red-500">Error conectando con la guía.</p>';
            } finally {
                btnGetSuggestions.disabled = false;
                btnGetSuggestions.textContent = 'Sugerir';
            }
        });

        // Eventos
        inputStart.addEventListener('change', calculatePrice);
        inputEnd.addEventListener('change', calculatePrice);
        formName.addEventListener('input', validateForm);
        formPlate.addEventListener('input', validateForm);
        btnReserve.addEventListener('click', processReservation);

        // Inicializar
        setupDefaultTimes();
        renderMap();
        validateForm();

    </script>
</body>
</html>
