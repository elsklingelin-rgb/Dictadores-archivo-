# Dictadores-archivo-
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dictadores del Mundo | Archivo Histórico Extenso</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@700&family=Inter:wght@300;400;600&display=swap');

        :root {
            --primary-red: #9b1c1c;
            --dark-bg: #0a0a0a;
            --card-bg: #141414;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--dark-bg);
            color: #d1d5db;
            scroll-behavior: smooth;
        }

        .title-font {
            font-family: 'Cinzel', serif;
        }

        .header-bg {
            background: linear-gradient(rgba(0,0,0,0.8), rgba(0,0,0,0.8)), 
                        url('https://images.unsplash.com/photo-1547049082-1a12c3bf2b7b?q=80&w=1470&auto=format&fit=crop');
            background-size: cover;
            background-position: center;
        }

        .dictator-card {
            background-color: var(--card-bg);
            border: 1px solid #262626;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .dictator-card:hover {
            border-color: var(--primary-red);
            transform: scale(1.02);
            box-shadow: 0 0 25px rgba(155, 28, 28, 0.3);
        }

        .category-btn {
            @apply px-5 py-2 rounded-full border border-zinc-700 text-sm transition-all duration-300;
        }

        .category-btn.active {
            @apply bg-red-800 border-red-800 text-white shadow-lg shadow-red-900/20;
        }

        .modal-overlay {
            display: none;
            background: rgba(0,0,0,0.95);
            backdrop-filter: blur(8px);
        }

        .stat-box {
            background: rgba(255,255,255,0.03);
            border-left: 3px solid var(--primary-red);
        }

        .section-title {
            @apply text-red-600 font-bold text-[10px] tracking-[0.2em] uppercase mb-2 block;
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #0a0a0a; }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #444; }
    </style>
</head>
<body class="antialiased">

    <!-- Hero Section -->
    <header class="header-bg h-[60vh] flex items-center justify-center relative border-b-2 border-red-900">
        <div class="text-center px-6 z-10">
            <h1 class="title-font text-5xl md:text-8xl text-white mb-4 tracking-tighter">TYRANNOS</h1>
            <p class="text-red-500 font-bold tracking-[0.3em] text-xs md:text-sm mb-8 uppercase">Crónica de la ambición, el control y el legado del poder absoluto</p>
            <div class="h-1 w-24 bg-red-700 mx-auto"></div>
        </div>
    </header>

    <!-- Filter Bar -->
    <nav class="sticky top-0 z-40 bg-zinc-950/90 backdrop-blur-md border-b border-zinc-800 py-6">
        <div class="container mx-auto px-4 overflow-x-auto no-scrollbar">
            <div class="flex items-center justify-center space-x-3 min-w-max">
                <button onclick="filter('all')" id="btn-all" class="category-btn active">Todos</button>
                <button onclick="filter('europa')" id="btn-europa" class="category-btn">Europa</button>
                <button onclick="filter('america')" id="btn-america" class="category-btn">América</button>
                <button onclick="filter('asia')" id="btn-asia" class="category-btn">Asia</button>
                <button onclick="filter('africa')" id="btn-africa" class="category-btn">África</button>
                <button onclick="filter('m-oriente')" id="btn-m-oriente" class="category-btn">Medio Oriente</button>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main class="container mx-auto px-6 py-12">
        <div class="flex flex-col md:flex-row justify-between items-end mb-12 gap-4">
            <div>
                <h2 class="text-3xl font-bold text-white mb-2">Expedientes Biográficos</h2>
                <p class="text-zinc-500">Haz clic en un perfil para leer la trayectoria completa y el perfil psicológico del régimen.</p>
            </div>
            <div class="relative w-full md:w-72">
                <i class="fas fa-search absolute left-3 top-1/2 -translate-y-1/2 text-zinc-500"></i>
                <input type="text" id="searchInput" onkeyup="search()" placeholder="Buscar dictador o país..." class="w-full bg-zinc-900 border border-zinc-800 rounded-lg py-2 pl-10 pr-4 text-white focus:outline-none focus:border-red-700">
            </div>
        </div>

        <div id="grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <!-- Dinámico -->
        </div>
    </main>

    <!-- Modal View -->
    <div id="modal" class="modal-overlay fixed inset-0 z-50 p-2 md:p-10 flex items-center justify-center">
        <div class="bg-zinc-900 w-full max-w-6xl h-full md:h-auto md:max-h-[90vh] rounded-2xl overflow-hidden shadow-2xl flex flex-col md:flex-row relative border border-zinc-800">
            <button onclick="closeModal()" class="absolute top-5 right-5 z-20 bg-black/50 p-2 rounded-full text-zinc-400 hover:text-white transition">
                <i class="fas fa-times text-xl"></i>
            </button>
            
            <div id="modal-img" class="w-full md:w-2/5 h-64 md:h-auto overflow-hidden">
                <!-- Foto -->
            </div>
            
            <div class="w-full md:w-3/5 p-6 md:p-12 overflow-y-auto">
                <div class="mb-8">
                    <span id="modal-region" class="section-title">Región</span>
                    <h3 id="modal-name" class="title-font text-4xl md:text-5xl text-white mb-1">Nombre</h3>
                    <p id="modal-period" class="text-zinc-400 font-medium text-lg italic">Periodo</p>
                </div>
                
                <div class="space-y-8">
                    <section>
                        <span class="section-title">Trayectoria y Orígenes</span>
                        <p id="modal-origins" class="text-zinc-300 leading-relaxed text-sm md:text-base"></p>
                    </section>

                    <section>
                        <span class="section-title">El Régimen y Métodos de Control</span>
                        <p id="modal-desc" class="text-zinc-300 leading-relaxed text-sm md:text-base"></p>
                    </section>

                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <div class="stat-box p-4">
                            <span class="text-zinc-500 text-[10px] uppercase font-bold block mb-1">Costo Humano</span>
                            <span id="modal-impact" class="text-red-500 font-bold text-sm"></span>
                        </div>
                        <div class="stat-box p-4">
                            <span class="text-zinc-500 text-[10px] uppercase font-bold block mb-1">Estructura Política</span>
                            <span id="modal-ideology" class="text-white font-bold text-sm"></span>
                        </div>
                        <div class="stat-box p-4">
                            <span class="text-zinc-500 text-[10px] uppercase font-bold block mb-1">Nacimiento/Muerte</span>
                            <span id="modal-dates" class="text-zinc-400 font-bold text-sm"></span>
                        </div>
                    </div>

                    <section class="bg-red-950/10 p-4 border border-red-900/30 rounded-lg">
                        <span class="section-title">Caída y Legado</span>
                        <p id="modal-end" class="text-zinc-300 text-sm"></p>
                    </section>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-zinc-950 py-12 border-t border-zinc-900 mt-20">
        <div class="container mx-auto px-6 text-center">
            <div class="title-font text-xl text-zinc-700 mb-4 tracking-widest uppercase">Tyrannos Archive v2.0</div>
            <p class="text-zinc-600 max-w-2xl mx-auto text-xs leading-relaxed">
                Este compendio biográfico utiliza datos de archivos históricos, organizaciones de derechos humanos y registros académicos. Su objetivo es documentar las violaciones a las libertades individuales y el desarrollo del poder totalitario a lo largo de la historia.
            </p>
        </div>
    </footer>

    <script>
        const data = [
            {
                id: 1, name: "Adolf Hitler", region: "europa", country: "Alemania", period: "1933-1945",
                ideology: "Totalitarismo Nazi", impact: "11-17 millones", dates: "1889 - 1945",
                origins: "Nacido en Austria, fue un cabo veterano de la IGM y artista frustrado. Explotó el resentimiento alemán tras el Tratado de Versalles y la crisis del 29 para ascender democráticamente antes de desmantelar la República de Weimar.",
                desc: "Implementó la 'Gleichschaltung' (sincronización) de la sociedad. Su control se basó en la propaganda de Goebbels, la Gestapo y las SS. Estableció campos de concentración para exterminar minorías, opositores y judíos bajo la 'Solución Final'.",
                end: "Se suicidó en su búnker bajo las ruinas de Berlín mientras el Ejército Rojo tomaba la ciudad. Su legado es el recordatorio más oscuro del mal institucionalizado.",
                img: "https://images.unsplash.com/photo-1590424765952-47402660d84c?q=80&w=600"
            },
            {
                id: 2, name: "Joseph Stalin", region: "europa", country: "Unión Soviética", period: "1924-1953",
                ideology: "Comunismo Estalinista", impact: "20-30 millones", dates: "1878 - 1953",
                origins: "Nacido Iósif Dzhugashvili en Georgia, de origen humilde y ex-seminarista. Escaló en el partido mediante la burocracia y la eliminación silenciosa de sus rivales tras la muerte de Lenin.",
                desc: "Transformó la URSS en una potencia industrial a costa de colectivizaciones forzosas que causaron hambrunas masivas (Holodomor). Gobernó mediante la 'Gran Purga', eliminando a casi toda la cúpula militar y civil original del partido.",
                end: "Murió de una hemorragia cerebral en su dacha. Tras su muerte, el país inició un proceso de 'desestalinización' para denunciar sus excesos y culto a la personalidad.",
                img: "https://images.unsplash.com/photo-1529156069898-49953e39b3ac?q=80&w=600"
            },
            {
                id: 3, name: "Mao Zedong", region: "asia", country: "China", period: "1949-1976",
                ideology: "Maoísmo", impact: "45-70 millones", dates: "1893 - 1976",
                origins: "Hijo de campesinos acomodados, fue bibliotecario y co-fundador del Partido Comunista Chino. Lideró la Larga Marcha y venció a los nacionalistas tras la ocupación japonesa.",
                desc: "Impulsó el 'Gran Salto Adelante', una campaña de industrialización rural que provocó la mayor hambruna de la historia humana. Más tarde lanzó la 'Revolución Cultural' para purgar elementos burgueses mediante el uso de los Guardias Rojos.",
                end: "Murió por problemas de salud derivados de la edad. Aunque su impacto humanitario fue devastador, sigue siendo la figura central del estado chino actual.",
                img: "https://images.unsplash.com/photo-1589182373726-e4f658ab50f0?q=80&w=600"
            },
            {
                id: 4, name: "Augusto Pinochet", region: "america", country: "Chile", period: "1973-1990",
                ideology: "Autoritarismo Militar", impact: "3,200 asesinados / 40,000 torturados", dates: "1915 - 2006",
                origins: "Militar de carrera que juró lealtad al presidente Allende antes de liderar el violento golpe de estado de 1973 con apoyo encubierto de la CIA en el marco de la Guerra Fría.",
                desc: "Clausuró el Congreso y proscribió partidos. Implementó un modelo económico neoliberal radical ('Chicago Boys') mientras la DINA perseguía sistemáticamente a disidentes en la 'Operación Cóndor'.",
                end: "Perdió un plebiscito en 1988 y entregó el poder en 1990, permaneciendo como comandante en jefe y senador vitalicio. Murió bajo arresto domiciliario y múltiples procesos judiciales.",
                img: "https://images.unsplash.com/photo-1544212515-99884577f884?q=80&w=600"
            },
            {
                id: 5, name: "Idi Amin Dada", region: "africa", country: "Uganda", period: "1971-1979",
                ideology: "Despotismo Militar", impact: "300,000 - 500,000", dates: "1925 - 2003",
                origins: "Ex-campeón de boxeo y oficial del ejército colonial británico. Tomó el poder mediante un golpe mientras el presidente Obote estaba fuera del país.",
                desc: "Su mandato fue una mezcla de brutalidad y excentricidad. Expulsó a la comunidad asiática, colapsando la economía, y utilizó escuadrones de la muerte (State Research Bureau) para ejecuciones arbitrarias públicas.",
                end: "Fue derrocado por fuerzas tanzanas y rebeldes ugandeses. Huyó a Libia y finalmente a Arabia Saudita, donde vivió con lujos hasta su muerte natural.",
                img: "https://images.unsplash.com/photo-1523805081326-78667ebfb601?q=80&w=600"
            },
            {
                id: 6, name: "Saddam Hussein", region: "m-oriente", country: "Irak", period: "1979-2003",
                ideology: "Nacionalismo Baazista", impact: "1-2 millones (incluyendo guerras)", dates: "1937 - 2006",
                origins: "Proveniente de una familia de campesinos pobres, se unió al Partido Baaz en su juventud. Participó en intentos de magnicidio antes de convertirse en el hombre fuerte del régimen.",
                desc: "Estableció un control total mediante un culto extremo a la personalidad. Libró una guerra de 8 años contra Irán y utilizó armas químicas contra su propia población kurda (Masacre de Halabja).",
                end: "Derrocado tras la invasión de la coalición liderada por EE.UU. en 2003. Fue capturado en un agujero bajo tierra y ejecutado en la horca tras un juicio por crímenes de lesa humanidad.",
                img: "https://images.unsplash.com/photo-1516733725897-1aa73b87c8e8?q=80&w=600"
            },
            {
                id: 7, name: "Pol Pot", region: "asia", country: "Camboya", period: "1975-1979",
                ideology: "Comunismo Agrario", impact: "1.7 - 2.2 millones", dates: "1925 - 1998",
                origins: "Nacido Saloth Sar, estudió electrónica en Francia donde se radicalizó. Regresó para liderar a la guerrilla de los Jemeres Rojos desde la selva.",
                desc: "Declaró el 'Año Cero'. Evacuó ciudades enteras hacia granjas colectivas, abolió el dinero, la religión y la propiedad privada. Quien hablara un idioma extranjero o usara anteojos era considerado intelectual y ejecutado.",
                end: "Derrocado por Vietnam. Se refugió en la selva liderando una resistencia guerrillera por décadas. Murió de causas naturales justo cuando iba a ser entregado a un tribunal internacional.",
                img: "https://images.unsplash.com/photo-1555436169-20e93ea9a7ff?q=80&w=600"
            },
            {
                id: 8, name: "Francisco Franco", region: "europa", country: "España", period: "1939-1975",
                ideology: "Franquismo / Nacionalcatolicismo", impact: "150,000+ (post-guerra)", dates: "1892 - 1975",
                origins: "Militar de carrera con éxito en la Guerra del Rif. Fue uno de los líderes del golpe de 1936 que desencadenó la Guerra Civil Española, emergiendo como único mando del bando sublevado.",
                desc: "Gobernó con el título de 'Caudillo'. Su régimen eliminó las libertades democráticas, prohibió las lenguas regionales y mantuvo un estricto control social apoyado por la Iglesia. Durante décadas mantuvo a España aislada internacionalmente.",
                end: "Falleció por causas naturales a los 82 años. Designó a Juan Carlos I como sucesor con la intención de continuar su régimen, pero el país inició rápidamente una transición hacia la democracia.",
                img: "https://images.unsplash.com/photo-1551009175-8a68da93d5f9?q=80&w=600"
            },
            {
                id: 9, name: "Rafael Trujillo", region: "america", country: "Rep. Dominicana", period: "1930-1961",
                ideology: "Autoritarismo Personalista", impact: "50,000+", dates: "1891 - 1961",
                origins: "Entrenado por marines estadounidenses durante la ocupación. Usó su posición como jefe de la Guardia Nacional para dar un golpe y mantenerse en el poder mediante el terror y la corrupción.",
                desc: "Cambió el nombre de la capital a Ciudad Trujillo. Controlaba el 60% de la economía nacional. Perpetró la 'Masacre del Perejil' contra haitianos y utilizó a su policía secreta (SIM) para torturar a la clase alta opositora.",
                end: "Fue emboscado y acribillado en su auto mientras se dirigía a una cita galante. Su familia fue expulsada del país poco después, poniendo fin a la 'Era de Trujillo'.",
                img: "https://images.unsplash.com/photo-1523438097201-512ae7d59c44?q=80&w=600"
            }
        ];

        function render(list) {
            const grid = document.getElementById('grid');
            grid.innerHTML = '';
            
            list.forEach(item => {
                grid.innerHTML += `
                    <div class="dictator-card rounded-xl overflow-hidden cursor-pointer" onclick="openModal(${item.id})">
                        <div class="h-56 bg-zinc-800 relative">
                            <img src="${item.img}" alt="${item.name}" class="w-full h-full object-cover grayscale opacity-70 group-hover:opacity-100 transition">
                            <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-transparent to-transparent"></div>
                            <div class="absolute bottom-4 left-4">
                                <span class="bg-red-800 text-[10px] text-white px-3 py-1 rounded font-black uppercase tracking-widest">${item.country}</span>
                            </div>
                        </div>
                        <div class="p-6">
                            <h3 class="title-font text-xl text-white mb-2">${item.name}</h3>
                            <p class="text-red-500 text-[10px] mb-3 font-bold uppercase tracking-widest">${item.period}</p>
                            <p class="text-zinc-500 text-xs leading-relaxed line-clamp-3">${item.origins}</p>
                        </div>
                    </div>
                `;
            });
        }

        function filter(region) {
            document.querySelectorAll('.category-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(`btn-${region}`).classList.add('active');
            const filtered = region === 'all' ? data : data.filter(d => d.region === region);
            render(filtered);
        }

        function search() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = data.filter(d => 
                d.name.toLowerCase().includes(query) || 
                d.country.toLowerCase().includes(query)
            );
            render(filtered);
        }

        function openModal(id) {
            const item = data.find(d => d.id === id);
            const modal = document.getElementById('modal');
            
            document.getElementById('modal-img').innerHTML = `<img src="${item.img}" class="w-full h-full object-cover grayscale opacity-40">`;
            document.getElementById('modal-region').innerText = item.region.replace('-', ' ');
            document.getElementById('modal-name').innerText = item.name;
            document.getElementById('modal-period').innerText = `${item.country} | ${item.period}`;
            document.getElementById('modal-origins').innerText = item.origins;
            document.getElementById('modal-desc').innerText = item.desc;
            document.getElementById('modal-impact').innerText = item.impact;
            document.getElementById('modal-ideology').innerText = item.ideology;
            document.getElementById('modal-dates').innerText = item.dates;
            document.getElementById('modal-end').innerText = item.end;

            modal.style.display = 'flex';
            document.body.style.overflow = 'hidden';
        }

        function closeModal() {
            document.getElementById('modal').style.display = 'none';
            document.body.style.overflow = 'auto';
        }

        window.onclick = function(e) {
            if (e.target == document.getElementById('modal')) closeModal();
        }

        // Carga inicial
        render(data);
    </script>
</body>
</html>

