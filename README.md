# -```html
<!DOCTYPE html>
<html lang="uk" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Космічний Сад — Рослини, які ростуть навіть на Марсі</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        space: {
                            dark: '#0B1C2C',
                            card: '#132A42',
                            border: '#1F3F60'
                        },
                        mint: {
                            DEFAULT: '#7CDBA8',
                            dark: '#5ab885'
                        },
                        beige: {
                            DEFAULT: '#F5F0E6',
                            muted: '#E5DFD3'
                        },
                        coral: {
                            DEFAULT: '#FF6B6B',
                            hover: '#e05252'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0B1C2C;
            color: #F5F0E6;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0B1C2C;
        }
        ::-webkit-scrollbar-thumb {
            background: #1F3F60;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #7CDBA8;
        }
        .glow-mint {
            box-shadow: 0 0 25px rgba(124, 219, 168, 0.25);
        }
        .glow-coral {
            box-shadow: 0 0 25px rgba(255, 107, 107, 0.25);
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(2deg); }
        }
        .floating-mascot {
            animation: float 4s ease-in-out infinite;
        }
    </style>
</head>
<body class="bg-space-dark text-beige min-h-screen flex flex-col selection:bg-mint selection:text-space-dark">

    <!-- Top Notification Banner -->
    <div class="bg-gradient-to-r from-space-card via-mint/20 to-space-card text-beige text-xs sm:text-sm py-2 px-4 text-center border-b border-space-border flex items-center justify-center gap-2">
        <i class="fa-solid fa-satellite text-mint animate-pulse"></i>
        <span>Доставка по всій галактиці (і Україні) від 1000 ₴ — <strong>безкоштовна!</strong> Код купону: <span class="text-mint font-bold">MARS2026</span></span>
    </div>

    <!-- Header & Navigation -->
    <header class="sticky top-0 z-50 bg-space-dark/90 backdrop-blur-md border-b border-space-border shadow-lg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Logo & Title -->
            <a href="#home" onclick="switchTab('home')" class="flex items-center gap-3 group cursor-pointer">
                <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-mint to-space-card flex items-center justify-center border border-mint/40 shadow-md group-hover:scale-105 transition-transform">
                    <i class="fa-solid fa-seedling text-space-dark text-2xl"></i>
                </div>
                <div>
                    <span class="text-xl sm:text-2xl font-extrabold tracking-wider bg-gradient-to-r from-mint via-beige to-coral bg-clip-text text-transparent">Космічний Сад</span>
                    <p class="text-[10px] text-beige/70 tracking-widest uppercase font-medium">Рослини з іншої галактики</p>
                </div>
            </a>

            <!-- Desktop Navigation Menu -->
            <nav class="hidden lg:flex items-center gap-1 xl:gap-2">
                <button onclick="switchTab('home')" id="nav-home" class="nav-btn px-4 py-2 rounded-xl text-sm font-semibold transition-all bg-mint/10 text-mint border border-mint/30">Головна</button>
                <button onclick="switchTab('catalog')" id="nav-catalog" class="nav-btn px-4 py-2 rounded-xl text-sm font-medium text-beige/80 hover:text-mint hover:bg-space-card transition-all">Каталог</button>
                <button onclick="switchTab('about')" id="nav-about" class="nav-btn px-4 py-2 rounded-xl text-sm font-medium text-beige/80 hover:text-mint hover:bg-space-card transition-all">Про нас</button>
                <button onclick="switchTab('delivery')" id="nav-delivery" class="nav-btn px-4 py-2 rounded-xl text-sm font-medium text-beige/80 hover:text-mint hover:bg-space-card transition-all">Доставка та оплата</button>
                <button onclick="switchTab('contacts')" id="nav-contacts" class="nav-btn px-4 py-2 rounded-xl text-sm font-medium text-beige/80 hover:text-mint hover:bg-space-card transition-all">Контакти</button>
            </nav>

            <!-- Right Actions: Cart & Mobile Menu Toggle -->
            <div class="flex items-center gap-3">
                <button onclick="switchTab('cart')" class="relative bg-space-card border border-space-border hover:border-mint px-4 py-2.5 rounded-xl flex items-center gap-2 transition-all group">
                    <i class="fa-solid fa-cart-shopping text-mint group-hover:scale-110 transition-transform"></i>
                    <span class="hidden sm:inline text-sm font-semibold">Кошик</span>
                    <span id="cart-badge" class="absolute -top-2 -right-2 bg-coral text-space-dark font-bold text-xs w-6 h-6 rounded-full flex items-center justify-center shadow-md animate-bounce">0</span>
                </button>

                <button onclick="toggleMobileMenu()" class="lg:hidden text-beige hover:text-mint p-2 text-2xl focus:outline-none">
                    <i id="mobile-menu-icon" class="fa-solid fa-bars"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Menu Drawer -->
        <div id="mobile-menu" class="hidden lg:hidden bg-space-card border-b border-space-border px-4 py-5 space-y-3">
            <button onclick="switchTab('home'); toggleMobileMenu();" class="block w-full text-left px-4 py-3 rounded-xl font-semibold bg-mint/10 text-mint">Головна</button>
            <button onclick="switchTab('catalog'); toggleMobileMenu();" class="block w-full text-left px-4 py-3 rounded-xl font-medium text-beige hover:bg-space-dark">Каталог</button>
            <button onclick="switchTab('about'); toggleMobileMenu();" class="block w-full text-left px-4 py-3 rounded-xl font-medium text-beige hover:bg-space-dark">Про нас</button>
            <button onclick="switchTab('delivery'); toggleMobileMenu();" class="block w-full text-left px-4 py-3 rounded-xl font-medium text-beige hover:bg-space-dark">Доставка та оплата</button>
            <button onclick="switchTab('contacts'); toggleMobileMenu();" class="block w-full text-left px-4 py-3 rounded-xl font-medium text-beige hover:bg-space-dark">Контакти</button>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-grow">

        <!-- ==================== TAB 1: ГОЛОВНА (HOME) ==================== -->
        <section id="tab-home" class="tab-content py-8 sm:py-12">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-16">
                
                <!-- Hero Section -->
                <div class="relative bg-gradient-to-br from-space-card via-space-dark to-space-card border border-space-border rounded-3xl p-6 sm:p-12 overflow-hidden shadow-2xl">
                    <div class="absolute -right-20 -bottom-20 w-96 h-96 bg-mint/10 rounded-full blur-3xl pointer-events-none"></div>
                    <div class="absolute -left-20 -top-20 w-96 h-96 bg-coral/10 rounded-full blur-3xl pointer-events-none"></div>

                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center relative z-10">
                        <div class="lg:col-span-7 space-y-6 text-center lg:text-left">
                            <div class="inline-flex items-center gap-2 bg-mint/10 border border-mint/30 px-4 py-1.5 rounded-full text-mint text-xs font-semibold tracking-wide">
                                <i class="fa-solid fa-meteor"></i> Нова галактична колекція 2026
                            </div>
                            <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight leading-tight">
                                Рослини, які ростуть <span class="bg-gradient-to-r from-mint to-coral bg-clip-text text-transparent">навіть на Марсі</span>
                            </h1>
                            <p class="text-beige/80 text-base sm:text-lg max-w-xl mx-auto lg:mx-0 font-light">
                                Ласкаво просимо до «Космічного Саду»! Це не звичайний квітковий маркет. Кожна рослина привезена з далеких орбіт, має власний характер та унікальну історію виживання в умовах глибокого космосу.
                            </p>
                            <div class="flex flex-wrap justify-center lg:justify-start gap-4 pt-4">
                                <button onclick="switchTab('catalog')" class="bg-mint text-space-dark font-bold px-8 py-4 rounded-2xl shadow-lg hover:bg-mint-dark transition-all transform hover:-translate-y-0.5 flex items-center gap-3">
                                    <i class="fa-solid fa-rocket"></i> До каталогу рослин
                                </button>
                                <button onclick="scrollToQuiz()" class="bg-space-dark border border-mint/50 text-mint font-semibold px-8 py-4 rounded-2xl hover:bg-mint/10 transition-all flex items-center gap-2">
                                    <i class="fa-solid fa-wand-magic-sparkles"></i> Тест: Обери свій сукулент
                                </button>
                            </div>
                        </div>

                        <!-- Hero Mascot Visual -->
                        <div class="lg:col-span-5 flex flex-col items-center justify-center">
                            <div class="relative w-64 h-64 sm:w-80 sm:h-80 rounded-3xl bg-space-dark border-2 border-mint/40 flex items-center justify-center p-6 glow-mint floating-mascot">
                                <div class="absolute inset-0 bg-gradient-to-t from-space-card/80 to-transparent rounded-3xl"></div>
                                <img src="1000028811.webp" alt="Гавортія смугаста та Космос" class="w-48 h-48 sm:w-56 sm:h-56 object-cover rounded-2xl border border-space-border relative z-10 shadow-xl" onerror="this.src='https://placehold.co/400x400/0B1C2C/7CDBA8?text=Космос'">
                                <div class="absolute bottom-4 right-4 bg-space-dark/90 border border-mint px-3 py-1.5 rounded-xl text-xs font-bold text-mint flex items-center gap-1.5 z-20 shadow-lg">
                                    <i class="fa-solid fa-robot"></i> Талісман Космос
                                </div>
                            </div>
                            <p class="text-xs text-beige/60 mt-4 text-center italic">«Поливати раз на тиждень — як підтримувати життєзабезпечення шлюзу!»</p>
                        </div>
                    </div>
                </div>

                <!-- Why We're Different -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="bg-space-card border border-space-border p-8 rounded-3xl hover:border-mint/50 transition-all">
                        <div class="w-14 h-14 rounded-2xl bg-mint/10 border border-mint/30 flex items-center justify-center text-mint text-2xl mb-6">
                            <i class="fa-solid fa-meteor"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-3">Космічні легенди</h3>
                        <p class="text-beige/70 text-sm leading-relaxed">
                            Усі наші екземпляри мають бортові щоденники експедицій. Ви знаєте точну траєкторію та характер кожного зеленого мешканця.
                        </p>
                    </div>

                    <div class="bg-space-card border border-space-border p-8 rounded-3xl hover:border-mint/50 transition-all">
                        <div class="w-14 h-14 rounded-2xl bg-coral/10 border border-coral/30 flex items-center justify-center text-coral text-2xl mb-6">
                            <i class="fa-solid fa-shield-halved"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-3">Витривалість Марса</h3>
                        <p class="text-beige/70 text-sm leading-relaxed">
                            Наші рослини створені для зайнятих людей і мінімалістів. Вони спокійно прощають пропущений полив під час міжгалактичних подорожей.
                        </p>
                    </div>

                    <div class="bg-space-card border border-space-border p-8 rounded-3xl hover:border-mint/50 transition-all">
                        <div class="w-14 h-14 rounded-2xl bg-mint/10 border border-mint/30 flex items-center justify-center text-mint text-2xl mb-6">
                            <i class="fa-solid fa-gift"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-3">Естетичні набори</h3>
                        <p class="text-beige/70 text-sm leading-relaxed">
                            Повні комплекти «Життя на Марсі» з унікальними крафтовими горщиками, метеоритним ґрунтом та інструкцією пілота.
                        </p>
                    </div>
                </div>

                <!-- Featured Recommendations (4 items) -->
                <div>
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-end mb-8 gap-4">
                        <div>
                            <span class="text-mint text-xs font-bold uppercase tracking-wider">Хіти продажу</span>
                            <h2 class="text-3xl font-extrabold mt-1">Рекомендовані з орбіти</h2>
                        </div>
                        <button onclick="switchTab('catalog')" class="text-mint hover:underline text-sm font-semibold flex items-center gap-2">
                            Дивитись увесь каталог <i class="fa-solid fa-arrow-right"></i>
                        </button>
                    </div>

                    <div id="featured-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                        <!-- Populated via JavaScript -->
                    </div>
                </div>

                <!-- Challenge 1: Storytelling Snippet Banner -->
                <div class="bg-gradient-to-r from-space-card via-space-dark to-space-card border border-space-border rounded-3xl p-8 shadow-xl relative overflow-hidden">
                    <div class="max-w-3xl space-y-4">
                        <div class="inline-flex items-center gap-2 bg-coral/10 border border-coral/30 px-3 py-1 rounded-full text-coral text-xs font-bold">
                            <i class="fa-solid fa-book-open"></i> Сторітелінг з експедиції №42
                        </div>
                        <h3 class="text-2xl font-bold">Щоденник команди: «Як ми знайшли першу Альбуку»</h3>
                        <p class="text-beige/80 text-sm leading-relaxed">
                            «Коли наш зонд сів на незвідану ділянку плато, ми помітили дивні спіралі, що нагадували смарагдові пружини часу. Це виявилася Альбука спіральна сорту 'Frizzle Sizzle'. Вона закручується щоразу, коли відчуває наближення космічної бурі або дефіцит вологи...»
                        </p>
                        <button onclick="switchTab('catalog')" class="inline-block bg-mint/10 border border-mint text-mint font-semibold px-6 py-2.5 rounded-xl hover:bg-mint hover:space-dark transition-all text-sm">
                            Читати всі бортові щоденники
                        </button>
                    </div>
                </div>

                <!-- Challenge 2: Interactive Quiz Section -->
                <div id="quiz-section" class="bg-space-card border-2 border-mint/40 rounded-3xl p-6 sm:p-10 shadow-2xl relative">
                    <div class="absolute -top-4 right-8 bg-mint text-space-dark font-extrabold text-xs px-4 py-1.5 rounded-full shadow-md uppercase tracking-wider">
                        Інтерактивний квіз
                    </div>
                    
                    <div class="max-w-2xl mx-auto text-center space-y-6">
                        <div class="space-y-2">
                            <h3 class="text-2xl sm:text-3xl font-extrabold">Яка рослина підійде саме тобі?</h3>
                            <p class="text-beige/70 text-sm">Пройдіть міні-тест з 3 запитань і дізнайтеся свій ідеальний космічний сукулент.</p>
                        </div>

                        <div id="quiz-container" class="bg-space-dark border border-space-border rounded-2xl p-6 text-left space-y-6">
                            <!-- Quiz content injected by JS -->
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- ==================== TAB 2: КАТАЛОГ (CATALOG) ==================== -->
        <section id="tab-catalog" class="tab-content hidden py-8 sm:py-12">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-8">
                
                <div class="text-center max-w-2xl mx-auto space-y-3">
                    <h1 class="text-3xl sm:text-5xl font-extrabold">Галактичний Каталог</h1>
                    <p class="text-beige/80 text-sm sm:text-base">Усі 13 унікальних рослин та аксесуарів із повними досьє експедицій, історіями та рекомендаціями догляду.</p>
                </div>

                <!-- Category Filters -->
                <div class="flex flex-wrap items-center justify-center gap-2 sm:gap-3 pb-4">
                    <button onclick="filterCatalog('all')" id="filter-all" class="filter-btn px-5 py-2.5 rounded-xl text-sm font-semibold transition-all bg-mint text-space-dark shadow-md">Всі товари (13)</button>
                    <button onclick="filterCatalog('Космічні сукуленти')" id="filter-Космічні сукуленти" class="filter-btn px-5 py-2.5 rounded-xl text-sm font-medium bg-space-card border border-space-border text-beige hover:border-mint transition-all">Космічні сукуленти</button>
                    <button onclick="filterCatalog('Рослини-мандрівники')" id="filter-Рослини-мандрівники" class="filter-btn px-5 py-2.5 rounded-xl text-sm font-medium bg-space-card border border-space-border text-beige hover:border-mint transition-all">Рослини-мандрівники</button>
                    <button onclick="filterCatalog('Набори Життя на Марсі')" id="filter-Набори Життя на Марсі" class="filter-btn px-5 py-2.5 rounded-xl text-sm font-medium bg-space-card border border-space-border text-beige hover:border-mint transition-all">Набори «Життя на Марсі»</button>
                    <button onclick="filterCatalog('Аксесуари')" id="filter-Аксесуари" class="filter-btn px-5 py-2.5 rounded-xl text-sm font-medium bg-space-card border border-space-border text-beige hover:border-mint transition-all">Аксесуари</button>
                </div>

                <!-- Catalog Grid -->
                <div id="catalog-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
                    <!-- Populated via JavaScript -->
                </div>

     
