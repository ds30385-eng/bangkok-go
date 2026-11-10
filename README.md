<!DOCTYPE html>
<html lang="th" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bangkok Miracle Journey - สำรวจสุดยอดสถานที่ท่องเที่ยวกรุงเทพมหานคร</title>

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        bkk: {
                            gold: '#F59E0B',
                            goldLight: '#FBBF24',
                            goldGlow: '#D97706',
                            dark: '#070A10',
                            navy: '#0F172A',
                            card: '#111827',
                            cardHover: '#1F2937',
                            pinkNeon: '#EC4899',
                            cyanNeon: '#06B6D4'
                        }
                    },
                    fontFamily: {
                        sans: ['Kanit', 'Inter', 'sans-serif'],
                    },
                    animation: {
                        'pulse-glow': 'pulseGlow 2s infinite alternate',
                        'float': 'float 3s ease-in-out infinite',
                        'shimmer': 'shimmer 2.5s infinite'
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%': { boxShadow: '0 0 15px rgba(245, 158, 11, 0.2)' },
                            '100%': { boxShadow: '0 0 35px rgba(245, 158, 11, 0.6)' }
                        },
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-8px)' }
                        },
                        shimmer: {
                            '100%': { transform: 'translateX(100%)' }
                        }
                    }
                }
            }
        }
    </script>

    <!-- Google Fonts: Kanit & Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Alpine.js CDN -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

    <!-- Lucide Icons CDN -->
    <script src="https://unpkg.com/lucide@latest"></script>

    <style>
        body { font-family: 'Kanit', 'Inter', sans-serif; }
        .glass-header {
            background: rgba(7, 10, 16, 0.88);
            backdrop-filter: blur(16px);
        }
        .glass-card {
            background: rgba(17, 24, 39, 0.7);
            backdrop-filter: blur(12px);
        }
        .hide-scrollbar::-webkit-scrollbar { display: none; }
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        @media print {
            .no-print { display: none !important; }
            .print-only { display: block !important; }
        }
    </style>
</head>
<body class="bg-bkk-dark text-slate-100 min-h-screen flex flex-col selection:bg-amber-400 selection:text-slate-950 overflow-x-hidden"
      x-data="bkkTourismApp()" 
      x-init="initApp()">

    <!-- ================= 0. WELCOME OVERLAY (สวัสดีค่ะ เริ่ดๆ ปังๆ) ================= -->
    <div x-show="showWelcomeOverlay"
         x-transition:leave="transition ease-in duration-500 transform"
         x-transition:leave-start="opacity-100 scale-100"
         x-transition:leave-end="opacity-0 scale-105"
         class="fixed inset-0 z-50 flex items-center justify-center bg-slate-950/95 backdrop-blur-2xl px-4 no-print">
        
        <div class="max-w-2xl w-full text-center space-y-8 relative">
            <!-- Glow background effect -->
            <div class="absolute -top-20 left-1/2 -translate-x-1/2 w-72 h-72 bg-amber-500/20 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute -bottom-20 left-1/2 -translate-x-1/2 w-72 h-72 bg-pink-500/20 rounded-full blur-3xl pointer-events-none"></div>

            <!-- Greeting Badge -->
            <div class="inline-flex items-center gap-2 px-5 py-2 rounded-full border border-amber-500/40 bg-amber-500/10 text-amber-300 text-sm font-semibold tracking-wider animate-bounce shadow-lg shadow-amber-500/10">
                <span class="text-lg">🌸</span>
                <span x-text="lang === 'th' ? 'สวัสดีค่ะ ยินดีต้อนรับสู่กรุงเทพฯ' : 'Sawasdee Ka! Welcome to Bangkok'"></span>
            </div>

            <!-- Main Heading with Neon Glow -->
            <div class="space-y-4">
                <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight text-white leading-tight">
                    BANGKOK <br/>
                    <span class="bg-gradient-to-r from-amber-300 via-yellow-200 to-amber-500 bg-clip-text text-transparent drop-shadow-[0_0_25px_rgba(245,158,11,0.5)]">
                        MIRACLE JOURNEY
                    </span>
                </h1>
                <p class="text-base sm:text-lg text-slate-300 max-w-lg mx-auto font-light leading-relaxed" 
                   x-text="lang === 'th' ? 'เปิดประสบการณ์ท่องเที่ยวกรุงเทพฯ รูปแบบใหม่ สวยปัง ครบทุกย่าน สถานที่ฮิต รถไฟฟ้า BTS/MRT พร้อมจัดทริปสุดพิเศษ' : 'Discover iconic landmarks, secret spots, street food, and seamless metro routes in Thailand\'s vibrant capital.'">
                </p>
            </div>

            <!-- Action Button with Sound & Animation -->
            <div class="pt-4 flex flex-col sm:flex-row items-center justify-center gap-4">
                <button @click="enterWebsite()" 
                        class="px-8 py-4 rounded-2xl bg-gradient-to-r from-amber-400 via-amber-500 to-yellow-500 text-slate-950 font-extrabold text-lg shadow-xl shadow-amber-500/25 hover:scale-105 active:scale-95 transition-all duration-300 flex items-center gap-3 group">
                    <span x-text="lang === 'th' ? 'เริ่มต้นออกเดินทาง 🚀' : 'Explore Miracle Bangkok 🚀'"></span>
                    <i data-lucide="sparkles" class="w-5 h-5 group-hover:rotate-12 transition"></i>
                </button>
            </div>

            <!-- Author Credit Badge in Welcome Screen -->
            <div class="pt-2">
                <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-slate-900/90 border border-amber-500/30 text-xs text-slate-300 backdrop-blur-md">
                    <i data-lucide="award" class="w-3.5 h-3.5 text-amber-400"></i>
                    <span>พัฒนาและจัดทำโดย: <strong class="text-amber-300 font-bold">ณัฐธิดา สุระเสียง ม.6/6</strong></span>
                </div>
            </div>
        </div>
    </div>

    <!-- ================= 1. HEADER & NAVIGATION ================= -->
    <header class="sticky top-0 z-40 glass-header border-b border-slate-800/80 transition-all">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Brand Logo -->
            <div class="flex items-center space-x-3 cursor-pointer" @click="activeTab = 'explore'; scrollToTop()">
                <div class="w-11 h-11 rounded-2xl bg-gradient-to-tr from-amber-500 via-amber-400 to-yellow-300 flex items-center justify-center text-slate-950 font-bold shadow-lg shadow-amber-500/20 animate-pulse-glow">
                    <i data-lucide="compass" class="w-6 h-6"></i>
                </div>
                <div>
                    <span class="text-xl font-extrabold tracking-tight bg-gradient-to-r from-amber-300 via-yellow-200 to-white bg-clip-text text-transparent block leading-tight">
                        BANGKOK MIRACLE
                    </span>
                    <span class="text-[10px] text-amber-400 font-semibold tracking-widest uppercase block" x-text="lang === 'th' ? 'เที่ยวกรุงเทพฯ เริ่ดๆ ปังๆ' : 'Official Luxury Guide'"></span>
                </div>
            </div>

            <!-- Credit Badge Header (Desktop) -->
            <div class="hidden lg:flex items-center gap-2 px-3 py-1.5 rounded-xl bg-slate-900/80 border border-slate-800 text-xs text-slate-300">
                <i data-lucide="user-check" class="w-3.5 h-3.5 text-amber-400"></i>
                <span>ผู้จัดทำ: <strong class="text-amber-300 font-bold">ณัฐธิดา สุระเสียง ม.6/6</strong></span>
            </div>

            <!-- Navigation Links (Desktop) -->
            <nav class="hidden md:flex items-center space-x-2">
                <button @click="activeTab = 'explore'" 
                        :class="activeTab === 'explore' ? 'bg-amber-500/10 text-amber-400 border-amber-500/40 shadow-lg shadow-amber-500/5' : 'text-slate-300 hover:text-white hover:bg-slate-800/60 border-transparent'"
                        class="px-4 py-2 rounded-xl font-medium text-sm transition border flex items-center gap-2">
                    <i data-lucide="map-pin" class="w-4 h-4"></i>
                    <span x-text="t('navExplore')"></span>
                </button>
                
                <button @click="activeTab = 'transit'" 
                        :class="activeTab === 'transit' ? 'bg-amber-500/10 text-amber-400 border-amber-500/40 shadow-lg shadow-amber-500/5' : 'text-slate-300 hover:text-white hover:bg-slate-800/60 border-transparent'"
                        class="px-4 py-2 rounded-xl font-medium text-sm transition border flex items-center gap-2">
                    <i data-lucide="train" class="w-4 h-4"></i>
                    <span x-text="t('navTransit')"></span>
                </button>

                <button @click="activeTab = 'itinerary'" 
                        :class="activeTab === 'itinerary' ? 'bg-amber-500/10 text-amber-400 border-amber-500/40 shadow-lg shadow-amber-500/5' : 'text-slate-300 hover:text-white hover:bg-slate-800/60 border-transparent'"
                        class="px-4 py-2 rounded-xl font-medium text-sm transition border flex items-center gap-2 relative">
                    <i data-lucide="calendar" class="w-4 h-4"></i>
                    <span x-text="t('navItinerary')"></span>
                    <span x-show="itinerary.length > 0" 
                          x-text="itinerary.length" 
                          class="bg-amber-400 text-slate-950 font-extrabold text-xs rounded-full w-5 h-5 flex items-center justify-center animate-pulse"></span>
                </button>
            </nav>

            <!-- Audio Toggle & Language Switcher -->
            <div class="flex items-center space-x-3">
                <!-- Audio Greeting Toggle -->
                <button @click="playAudioGreeting()" 
                        title="ฟังเสียงสวัสดีค่ะ"
                        class="p-2 rounded-xl border border-slate-700 bg-slate-800/80 hover:bg-amber-500/20 hover:border-amber-500/40 text-amber-400 transition">
                    <i data-lucide="volume-2" class="w-4 h-4"></i>
                </button>

                <!-- Language Switcher -->
                <button @click="toggleLang()" 
                        class="px-3.5 py-2 rounded-xl border border-slate-700 bg-slate-800/80 hover:bg-slate-700 text-xs font-semibold tracking-wider flex items-center gap-1.5 text-slate-200 transition">
                    <i data-lucide="globe" class="w-3.5 h-3.5 text-amber-400"></i>
                    <span x-text="lang === 'th' ? 'EN' : 'TH'"></span>
                </button>

                <!-- Mobile Saved Itinerary Count -->
                <button @click="activeTab = 'itinerary'" 
                        class="md:hidden relative p-2 text-slate-300 hover:text-white bg-slate-800 rounded-lg">
                    <i data-lucide="bookmark" class="w-5 h-5"></i>
                    <span x-show="itinerary.length > 0" 
                          x-text="itinerary.length" 
                          class="absolute -top-1 -right-1 bg-amber-400 text-slate-950 font-bold text-xs rounded-full w-4 h-4 flex items-center justify-center"></span>
                </button>
            </div>
        </div>

        <!-- Mobile Navigation Bottom Bar -->
        <div class="md:hidden border-t border-slate-800 bg-bkk-dark/95 px-4 py-2.5 flex justify-around no-print">
            <button @click="activeTab = 'explore'" :class="activeTab === 'explore' ? 'text-amber-400 font-bold' : 'text-slate-400'" class="flex flex-col items-center gap-1 text-xs">
                <i data-lucide="map-pin" class="w-5 h-5"></i>
                <span x-text="t('navExplore')"></span>
            </button>
            <button @click="activeTab = 'transit'" :class="activeTab === 'transit' ? 'text-amber-400 font-bold' : 'text-slate-400'" class="flex flex-col items-center gap-1 text-xs">
                <i data-lucide="train" class="w-5 h-5"></i>
                <span x-text="t('navTransit')"></span>
            </button>
            <button @click="activeTab = 'itinerary'" :class="activeTab === 'itinerary' ? 'text-amber-400 font-bold' : 'text-slate-400'" class="flex flex-col items-center gap-1 text-xs relative">
                <i data-lucide="calendar" class="w-5 h-5"></i>
                <span x-text="t('navItinerary')"></span>
            </button>
        </div>
    </header>

    <!-- ================= MAIN CONTENT AREA ================= -->
    <main class="flex-grow">

        <!-- TAB 1: EXPLORE PLACES & HERO -->
        <section x-show="activeTab === 'explore'" class="space-y-10 pb-16">
            <!-- HERO BANNER -->
            <div class="relative overflow-hidden bg-slate-950 border-b border-slate-800/80 py-16 lg:py-24 px-4 sm:px-6 lg:px-8">
                <div class="absolute inset-0 opacity-25 bg-[radial-gradient(#f59e0b_1px,transparent_1px)] [background-size:28px_28px]"></div>
                <div class="absolute -top-40 -right-40 w-96 h-96 bg-amber-500/15 rounded-full blur-3xl pointer-events-none"></div>
                <div class="absolute -bottom-40 -left-40 w-96 h-96 bg-cyan-500/10 rounded-full blur-3xl pointer-events-none"></div>

                <div class="relative max-w-5xl mx-auto text-center space-y-6">
                    <!-- Dynamic Sawasdee Greeting Banner -->
                    <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full border border-amber-500/30 bg-amber-500/10 text-amber-300 text-xs sm:text-sm font-semibold tracking-wide animate-float">
                        <span>✨</span>
                        <span x-text="t('heroBadge')"></span>
                    </div>
                    
                    <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight text-white leading-tight">
                        <span x-text="t('heroTitle1')"></span> <br class="hidden sm:inline"/>
                        <span class="bg-gradient-to-r from-amber-400 via-amber-200 to-yellow-400 bg-clip-text text-transparent" x-text="t('heroTitle2')"></span>
                    </h1>
                    <p class="text-base sm:text-xl text-slate-300 max-w-2xl mx-auto font-light leading-relaxed" x-text="t('heroDesc')"></p>

                    <!-- SEARCH BAR & DISTRICT FILTER -->
                    <div class="pt-4 max-w-3xl mx-auto space-y-4">
                        <div class="relative flex items-center">
                            <i data-lucide="search" class="absolute left-4 w-5 h-5 text-amber-400"></i>
                            <input type="text" 
                                   x-model="searchQuery" 
                                   :placeholder="t('searchPlaceholder')" 
                                   class="w-full pl-12 pr-10 py-4 bg-slate-900/90 border border-slate-700/80 rounded-2xl text-white placeholder-slate-500 focus:outline-none focus:border-amber-400 focus:ring-2 focus:ring-amber-400/20 shadow-2xl transition">
                            <button x-show="searchQuery.length > 0" 
                                    @click="searchQuery = ''" 
                                    class="absolute right-4 text-slate-400 hover:text-white">
                                <i data-lucide="x" class="w-5 h-5"></i>
                            </button>
                        </div>

                        <!-- District Quick Filters -->
                        <div class="flex items-center gap-2 overflow-x-auto hide-scrollbar py-2 text-xs">
                            <span class="text-slate-400 whitespace-nowrap font-semibold" x-text="t('districtLabel') + ':'"></span>
                            <button @click="selectedDistrict = 'all'" 
                                    :class="selectedDistrict === 'all' ? 'bg-amber-400 text-slate-950 font-bold' : 'bg-slate-800 text-slate-300 hover:bg-slate-700'"
                                    class="px-3.5 py-1.5 rounded-xl whitespace-nowrap transition">
                                <span x-text="t('allDistricts')"></span>
                            </button>
                            <template x-for="district in districts" :key="district.id">
                                <button @click="selectedDistrict = district.id" 
                                        :class="selectedDistrict === district.id ? 'bg-amber-400 text-slate-950 font-bold' : 'bg-slate-800 text-slate-300 hover:bg-slate-700'"
                                        class="px-3.5 py-1.5 rounded-xl whitespace-nowrap transition">
                                    <span x-text="lang === 'th' ? district.nameTh : district.nameEn"></span>
                                </button>
                            </template>
                        </div>
                    </div>
                </div>
            </div>

            <!-- CATEGORY FILTER TABS -->
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex items-center gap-2.5 overflow-x-auto hide-scrollbar pb-4 border-b border-slate-800">
                    <template x-for="cat in categories" :key="cat.id">
                        <button @click="selectedCategory = cat.id" 
                                :class="selectedCategory === cat.id ? 'bg-amber-500/10 text-amber-400 border-amber-500/40 font-semibold shadow-lg shadow-amber-500/5' : 'bg-slate-800/60 text-slate-400 border-transparent hover:text-slate-200 hover:bg-slate-800'"
                                class="px-5 py-3 rounded-2xl border transition-all duration-200 flex items-center gap-2.5 whitespace-nowrap text-sm">
                            <i :data-lucide="cat.icon" class="w-4 h-4"></i>
                            <span x-text="lang === 'th' ? cat.nameTh : cat.nameEn"></span>
                            <span class="text-xs px-2.5 py-0.5 rounded-full bg-slate-900 border border-slate-700 text-slate-400"
                                  x-text="getCategoryCount(cat.id)"></span>
                        </button>
                    </template>
                </div>
            </div>

            <!-- ATTRACTIONS CARDS GRID -->
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <!-- Header Stats & Sorting -->
                <div class="flex justify-between items-center mb-6">
                    <p class="text-sm text-slate-400">
                        <span x-text="t('showingResults')"></span> 
                        <span class="font-extrabold text-amber-400 text-base" x-text="filteredPlaces.length"></span> 
                        <span x-text="t('placesCount')"></span>
                    </p>
                    <div class="flex items-center gap-2 text-xs text-slate-400">
                        <i data-lucide="arrow-up-down" class="w-3.5 h-3.5"></i>
                        <span x-text="t('sortBy')"></span>
                        <select x-model="sortBy" class="bg-slate-800 text-white rounded-xl px-3 py-1.5 border border-slate-700 focus:outline-none">
                            <option value="rating" x-text="t('sortRating')"></option>
                            <option value="reviews" x-text="t('sortPopular')"></option>
                        </select>
                    </div>
                </div>

                <!-- Places Grid -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <template x-for="place in filteredPlaces" :key="place.id">
                        <div class="group bg-bkk-card rounded-3xl border border-slate-800 hover:border-amber-500/40 overflow-hidden flex flex-col justify-between transition-all duration-300 hover:-translate-y-1.5 hover:shadow-2xl hover:shadow-amber-500/10">
                            <div>
                                <!-- Image Banner -->
                                <div class="relative aspect-video overflow-hidden bg-slate-950">
                                    <img :src="place.image" 
                                         :alt="place.nameTh" 
                                         class="w-full h-full object-cover transition duration-700 group-hover:scale-110"
                                         onerror="this.onerror=null; this.src='https://images.unsplash.com/photo-1508009603885-50cf7c579365?auto=format&fit=crop&w=800&q=80';">
                                    <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-slate-950/20 to-transparent"></div>
                                    
                                    <!-- Category Badge -->
                                    <span class="absolute top-3 left-3 px-3 py-1 rounded-xl text-xs font-semibold bg-slate-950/80 backdrop-blur-md text-amber-300 border border-amber-500/30">
                                        <span x-text="getCategoryName(place.category)"></span>
                                    </span>

                                    <!-- Rating Tag -->
                                    <div class="absolute bottom-3 left-3 flex items-center gap-1 px-3 py-1 rounded-xl bg-slate-950/80 backdrop-blur-md text-xs font-bold text-white border border-slate-700">
                                        <i data-lucide="star" class="w-3.5 h-3.5 fill-amber-400 text-amber-400"></i>
                                        <span x-text="place.rating"></span>
                                        <span class="text-slate-400 font-normal">
                                            (<span x-text="place.reviewCount"></span>)
                                        </span>
                                    </div>

                                    <!-- Quick Add Button -->
                                    <button @click.stop="toggleItinerary(place)" 
                                            :class="isInItinerary(place.id) ? 'bg-amber-400 text-slate-950' : 'bg-slate-950/80 text-white hover:bg-amber-400 hover:text-slate-950'"
                                            class="absolute top-3 right-3 p-2.5 rounded-2xl backdrop-blur-md border border-slate-700 transition duration-200">
                                        <i :data-lucide="isInItinerary(place.id) ? 'check' : 'plus'" class="w-4 h-4"></i>
                                    </button>
                                </div>

                                <!-- Information Body -->
                                <div class="p-6 space-y-3">
                                    <div>
                                        <h3 class="text-lg font-bold text-white group-hover:text-amber-300 transition" x-text="lang === 'th' ? place.nameTh : place.nameEn"></h3>
                                        <p class="text-xs text-slate-400 mt-1 flex items-center gap-1">
                                            <i data-lucide="map-pin" class="w-3.5 h-3.5 text-amber-400"></i>
                                            <span x-text="getDistrictName(place.district)"></span>
                                        </p>
                                    </div>

                                    <p class="text-xs text-slate-300 line-clamp-2 leading-relaxed" x-text="lang === 'th' ? place.descTh : place.descEn"></p>

                                    <!-- Station & Opening Hours -->
                                    <div class="pt-3 border-t border-slate-800 space-y-2 text-xs">
                                        <div class="flex items-center text-slate-300 gap-2">
                                            <i data-lucide="subway" class="w-3.5 h-3.5 text-cyan-400 flex-shrink-0"></i>
                                            <span class="truncate" x-text="place.transit"></span>
                                        </div>
                                        <div class="flex items-center text-slate-400 gap-2">
                                            <i data-lucide="clock" class="w-3.5 h-3.5 text-amber-400 flex-shrink-0"></i>
                                            <span x-text="place.hours"></span>
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <!-- Card Footer Action Buttons -->
                            <div class="p-6 pt-0 flex gap-2.5">
                                <button @click="openModal(place)" 
                                        class="flex-1 py-3 px-3 rounded-2xl bg-slate-800 hover:bg-slate-700 text-white text-xs font-semibold flex items-center justify-center gap-1.5 transition">
                                    <i data-lucide="info" class="w-4 h-4 text-amber-400"></i>
                                    <span x-text="t('viewDetails')"></span>
                                </button>
                                <button @click="toggleItinerary(place)" 
                                        :class="isInItinerary(place.id) ? 'bg-amber-500/20 text-amber-300 border border-amber-500/40' : 'bg-gradient-to-r from-amber-400 to-yellow-400 hover:from-amber-300 hover:to-yellow-300 text-slate-950 font-bold'"
                                        class="py-3 px-4 rounded-2xl text-xs transition flex items-center gap-1.5">
                                    <i :data-lucide="isInItinerary(place.id) ? 'check' : 'calendar-plus'" class="w-4 h-4"></i>
                                    <span x-text="isInItinerary(place.id) ? t('added') : t('addToPlan')"></span>
                                </button>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </section>

        <!-- TAB 2: BTS/MRT ROUTE & FARE CALCULATOR -->
        <section x-show="activeTab === 'transit'" class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-8">
            <div class="text-center space-y-3">
                <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-cyan-500/10 border border-cyan-500/30 text-cyan-400 text-xs font-semibold">
                    <i data-lucide="train" class="w-3.5 h-3.5"></i>
                    <span x-text="t('transitTitleBadge')"></span>
                </span>
                <h2 class="text-3xl font-extrabold text-white" x-text="t('transitHeader')"></h2>
                <p class="text-slate-400 text-sm max-w-xl mx-auto" x-text="t('transitSub')"></p>
            </div>

            <!-- Transit Calculator Card -->
            <div class="bg-bkk-card rounded-3xl border border-slate-800 p-6 sm:p-8 shadow-2xl space-y-8">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <!-- Origin Station -->
                    <div class="space-y-2">
                        <label class="text-xs font-semibold text-slate-400 uppercase tracking-wider flex items-center gap-2">
                            <span class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span>
                            <span x-text="t('originStation')"></span>
                        </label>
                        <select x-model="transitStart" class="w-full bg-slate-900 border border-slate-700/80 rounded-2xl p-4 text-white focus:outline-none focus:border-amber-400 text-sm">
                            <template x-for="st in metroStations" :key="st.id">
                                <option :value="st.id" x-text="st.line + ' - ' + (lang === 'th' ? st.nameTh : st.nameEn)"></option>
                            </template>
                        </select>
                    </div>

                    <!-- Destination Station -->
                    <div class="space-y-2">
                        <label class="text-xs font-semibold text-slate-400 uppercase tracking-wider flex items-center gap-2">
                            <span class="w-2.5 h-2.5 rounded-full bg-rose-400"></span>
                            <span x-text="t('destinationStation')"></span>
                        </label>
                        <select x-model="transitEnd" class="w-full bg-slate-900 border border-slate-700/80 rounded-2xl p-4 text-white focus:outline-none focus:border-amber-400 text-sm">
                            <template x-for="st in metroStations" :key="st.id">
                                <option :value="st.id" x-text="st.line + ' - ' + (lang === 'th' ? st.nameTh : st.nameEn)"></option>
                            </template>
                        </select>
                    </div>
                </div>

                <!-- Route Calculation Results Banner -->
                <div class="bg-slate-900/90 rounded-2xl p-6 border border-slate-800 flex flex-col md:flex-row items-center justify-between gap-6">
                    <div class="flex items-center gap-4">
                        <div class="w-14 h-14 rounded-2xl bg-amber-500/10 border border-amber-500/30 flex items-center justify-center text-amber-400">
                            <i data-lucide="ticket" class="w-8 h-8"></i>
                        </div>
                        <div>
                            <span class="text-xs text-slate-400 block font-medium" x-text="t('estFare')"></span>
                            <div class="text-3xl font-extrabold text-amber-400">
                                ฿<span x-text="calculateTransit().fare"></span>
                                <span class="text-xs font-normal text-slate-400">/ คน (THB)</span>
                            </div>
                        </div>
                    </div>

                    <div class="flex items-center gap-8 border-t md:border-t-0 md:border-l border-slate-800 pt-4 md:pt-0 md:pl-8">
                        <div>
                            <span class="text-xs text-slate-400 block font-medium" x-text="t('estTime')"></span>
                            <span class="text-xl font-bold text-white" x-text="calculateTransit().time + ' ' + t('mins')"></span>
                        </div>
                        <div>
                            <span class="text-xs text-slate-400 block font-medium" x-text="t('transfers')"></span>
                            <span class="text-xl font-bold text-white" x-text="calculateTransit().transfers + ' ' + t('times')"></span>
                        </div>
                    </div>
                </div>

                <!-- Suggested Metro Route Timeline -->
                <div class="space-y-4">
                    <h3 class="text-base font-bold text-slate-200 flex items-center gap-2">
                        <i data-lucide="route" class="w-4 h-4 text-amber-400"></i>
                        <span x-text="t('suggestedRoute')"></span>
                    </h3>
                    <div class="p-5 bg-slate-900/50 rounded-2xl border border-slate-800 space-y-3">
                        <div class="flex items-center gap-3 text-sm">
                            <span class="w-3.5 h-3.5 rounded-full bg-emerald-500"></span>
                            <span class="font-bold text-white" x-text="getStationName(transitStart)"></span>
                        </div>
                        <div class="pl-6 border-l-2 border-dashed border-slate-700 ml-1.5 py-2 text-xs text-slate-400">
                            <span x-text="calculateTransit().transfers > 0 ? t('transitTransferMsg') : t('directLineMsg')"></span>
                        </div>
                        <div class="flex items-center gap-3 text-sm">
                            <span class="w-3.5 h-3.5 rounded-full bg-rose-500"></span>
                            <span class="font-bold text-white" x-text="getStationName(transitEnd)"></span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 3: ITINERARY BUILDER -->
        <section x-show="activeTab === 'itinerary'" class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-8">
            <!-- Header Actions -->
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 no-print">
                <div>
                    <h2 class="text-3xl font-extrabold text-white flex items-center gap-3">
                        <i data-lucide="map" class="w-8 h-8 text-amber-400"></i>
                        <span x-text="t('myItineraryTitle')"></span>
                    </h2>
                    <p class="text-slate-400 text-sm mt-1" x-text="t('myItinerarySub')"></p>
                </div>
                <div class="flex items-center gap-3" x-show="itinerary.length > 0">
                    <button @click="clearItinerary()" class="px-4 py-2.5 rounded-2xl bg-slate-800 hover:bg-rose-500/20 hover:text-rose-400 text-slate-400 text-xs font-semibold transition border border-slate-700">
                        <span x-text="t('clearAll')"></span>
                    </button>
                    <button @click="window.print()" class="px-5 py-2.5 rounded-2xl bg-amber-400 hover:bg-amber-300 text-slate-950 text-xs font-extrabold transition flex items-center gap-2 shadow-lg shadow-amber-400/10">
                        <i data-lucide="printer" class="w-4 h-4"></i>
                        <span x-text="t('exportPdf')"></span>
                    </button>
                </div>
            </div>

            <!-- Active Itinerary Content -->
            <div x-show="itinerary.length > 0" class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <!-- Timeline Items -->
                <div class="lg:col-span-2 space-y-4">
                    <template x-for="(item, index) in itinerary" :key="item.id">
                        <div class="relative bg-bkk-card rounded-3xl border border-slate-800 p-5 flex items-start gap-4 transition hover:border-slate-700">
                            <!-- Step Number -->
                            <div class="w-9 h-9 rounded-2xl bg-gradient-to-tr from-amber-400 to-yellow-300 text-slate-950 font-extrabold text-sm flex items-center justify-center flex-shrink-0 mt-1 shadow-md">
                                <span x-text="index + 1"></span>
                            </div>

                            <!-- Place Details -->
                            <div class="flex-grow space-y-2">
                                <div class="flex justify-between items-start">
                                    <h4 class="font-bold text-base text-white" x-text="lang === 'th' ? item.nameTh : item.nameEn"></h4>
                                    <button @click="removeFromItinerary(item.id)" class="text-slate-500 hover:text-rose-400 p-1 transition no-print">
                                        <i data-lucide="trash-2" class="w-4 h-4"></i>
                                    </button>
                                </div>
                                <div class="flex flex-wrap items-center gap-3 text-xs text-slate-400">
                                    <span class="flex items-center gap-1 text-amber-300">
                                        <i data-lucide="tag" class="w-3.5 h-3.5"></i>
                                        <span x-text="getCategoryName(item.category)"></span>
                                    </span>
                                    <span class="flex items-center gap-1">
                                        <i data-lucide="clock" class="w-3.5 h-3.5 text-slate-500"></i>
                                        <span x-text="item.hours"></span>
                                    </span>
                                </div>
                            </div>

                            <!-- Reorder Controls -->
                            <div class="flex flex-col gap-1 no-print">
                                <button @click="moveItineraryItem(index, -1)" :disabled="index === 0" class="p-1 text-slate-400 hover:text-white disabled:opacity-30">
                                    <i data-lucide="chevron-up" class="w-4 h-4"></i>
                                </button>
                                <button @click="moveItineraryItem(index, 1)" :disabled="index === itinerary.length - 1" class="p-1 text-slate-400 hover:text-white disabled:opacity-30">
                                    <i data-lucide="chevron-down" class="w-4 h-4"></i>
                                </button>
                            </div>
                        </div>
                    </template>
                </div>

                <!-- Summary Sidebar -->
                <div class="bg-bkk-card rounded-3xl border border-slate-800 p-6 h-fit space-y-6">
                    <h3 class="text-lg font-bold text-white border-b border-slate-800 pb-3" x-text="t('tripSummary')"></h3>
                    
                    <div class="space-y-4">
                        <div class="flex justify-between items-center text-sm">
                            <span class="text-slate-400" x-text="t('totalPlaces')"></span>
                            <span class="font-bold text-white" x-text="itinerary.length"></span>
                        </div>
                        <div class="flex justify-between items-center text-sm">
                            <span class="text-slate-400" x-text="t('estTravelTime')"></span>
                            <span class="font-bold text-amber-400" x-text="(itinerary.length * 1.5).toFixed(1) + ' ' + t('hours')"></span>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- ================= FOOTER & CREDIT SECTION ================= -->
    <footer class="bg-slate-950 border-t border-slate-800 py-10 px-4 sm:px-6 lg:px-8 no-print">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-6 text-center md:text-left">
            <div class="space-y-2">
                <div class="flex items-center justify-center md:justify-start gap-2">
                    <div class="w-7 h-7 rounded-xl bg-amber-400 flex items-center justify-center text-slate-950 font-bold">
                        <i data-lucide="sparkles" class="w-4 h-4"></i>
                    </div>
                    <span class="text-lg font-bold text-white">BANGKOK MIRACLE JOURNEY</span>
                </div>
                <p class="text-xs text-slate-400">รวบรวมสุดยอดสถานที่ท่องเที่ยว สถานีรถไฟฟ้า และระบบจัดทริปเดินทางในกรุงเทพมหานคร</p>
            </div>

            <!-- Author Credit Box -->
            <div class="p-4 rounded-2xl bg-slate-900/90 border border-amber-500/30 text-xs space-y-1 shadow-lg shadow-amber-500/5">
                <div class="text-slate-400 font-light">ออกแบบและพัฒนาเว็บไซต์โดย</div>
                <div class="text-sm font-extrabold text-amber-300 flex items-center justify-center md:justify-start gap-1.5">
                    <i data-lucide="heart" class="w-3.5 h-3.5 text-rose-500 fill-rose-500 animate-pulse"></i>
                    <span>ณัฐธิดา สุระเสียง ม.6/6</span>
                </div>
            </div>
        </div>
    </footer>

    <!-- ================= ATTRACTION MODAL DETAIL ================= -->
    <div x-show="modalOpen" 
         x-transition:enter="transition ease-out duration-300"
         x-transition:enter-start="opacity-0 scale-95"
         x-transition:enter-end="opacity-100 scale-100"
         x-transition:leave="transition ease-in duration-200"
         x-transition:leave-start="opacity-100 scale-100"
         x-transition:leave-end="opacity-0 scale-95"
         class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-950/85 backdrop-blur-md overflow-y-auto"
         @click.self="closeModal()" 
         style="display: none;">
        
        <template x-if="selectedPlace">
            <div class="bg-bkk-card border border-slate-800 rounded-3xl max-w-3xl w-full overflow-hidden shadow-2xl relative my-8">
                <!-- Modal Close -->
                <button @click="closeModal()" class="absolute top-4 right-4 z-10 p-2.5 rounded-full bg-slate-950/80 hover:bg-slate-800 text-white transition backdrop-blur-md border border-slate-700">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>

                <!-- Modal Banner Header -->
                <div class="relative h-72 sm:h-80 bg-slate-950">
                    <img :src="selectedPlace.image" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-slate-950/40 to-transparent"></div>
                    <div class="absolute bottom-6 left-6 right-6 space-y-2">
                        <span class="px-3 py-1 rounded-xl text-xs font-bold bg-amber-400 text-slate-950" x-text="getCategoryName(selectedPlace.category)"></span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-white" x-text="lang === 'th' ? selectedPlace.nameTh : selectedPlace.nameEn"></h2>
                    </div>
                </div>

                <!-- Modal Content Details -->
                <div class="p-6 sm:p-8 space-y-6 max-h-[60vh] overflow-y-auto hide-scrollbar">
                    <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 p-4 bg-slate-900/80 rounded-2xl border border-slate-800 text-xs">
                        <div>
                            <span class="text-slate-400 block" x-text="t('rating')"></span>
                            <span class="font-bold text-amber-400 text-sm flex items-center gap-1 mt-0.5">
                                <i data-lucide="star" class="w-3.5 h-3.5 fill-amber-400"></i>
                                <span x-text="selectedPlace.rating"></span>
                            </span>
                        </div>
                        <div>
                            <span class="text-slate-400 block" x-text="t('district')"></span>
                            <span class="font-semibold text-white mt-0.5 block truncate" x-text="getDistrictName(selectedPlace.district)"></span>
                        </div>
                        <div class="col-span-2 sm:col-span-2">
                            <span class="text-slate-400 block" x-text="t('transit')"></span>
                            <span class="font-semibold text-white mt-0.5 block truncate" x-text="selectedPlace.transit"></span>
                        </div>
                    </div>

                    <div class="space-y-2">
                        <h3 class="text-sm font-bold text-slate-300 uppercase tracking-wider" x-text="t('aboutPlace')"></h3>
                        <p class="text-sm text-slate-300 leading-relaxed" x-text="lang === 'th' ? selectedPlace.descTh : selectedPlace.descEn"></p>
                    </div>

                    <!-- External Map Integration -->
                    <div class="space-y-3">
                        <h3 class="text-sm font-bold text-slate-300 uppercase tracking-wider flex items-center gap-2">
                            <i data-lucide="map-pin" class="w-4 h-4 text-amber-400"></i>
                            <span x-text="t('locationMap')"></span>
                        </h3>
                        <div class="relative h-48 bg-slate-950 rounded-2xl border border-slate-800 overflow-hidden flex items-center justify-center text-center p-4">
                            <div class="absolute inset-0 opacity-30 bg-[radial-gradient(#f59e0b_1px,transparent_1px)] [background-size:16px_16px]"></div>
                            <div class="relative space-y-2">
                                <div class="w-10 h-10 rounded-full bg-amber-500/20 text-amber-400 mx-auto flex items-center justify-center animate-bounce">
                                    <i data-lucide="map-pin" class="w-6 h-6"></i>
                                </div>
                                <p class="text-xs font-semibold text-white" x-text="lang === 'th' ? selectedPlace.nameTh : selectedPlace.nameEn"></p>
                                <a :href="'https://www.google.com/maps/search/?api=1&query=' + encodeURIComponent(selectedPlace.nameTh)" 
                                   target="_blank" 
                                   class="inline-flex items-center gap-1.5 px-4 py-2 rounded-xl bg-amber-400 hover:bg-amber-300 text-slate-950 font-extrabold text-xs transition">
                                    <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                                    <span x-text="t('openGoogleMaps')"></span>
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </template>
    </div>

    <!-- ================= ALPINE.JS CORE LOGIC ================= -->
    <script>
        function bkkTourismApp() {
            return {
                lang: 'th',
                activeTab: 'explore',
                searchQuery: '',
                selectedCategory: 'all',
                selectedDistrict: 'all',
                sortBy: 'rating',
                modalOpen: false,
                selectedPlace: null,
                showWelcomeOverlay: true,
                newReviewText: '',
                newReviewRating: 5,
                transitStart: 'siam',
                transitEnd: 'watmangkon',
                itinerary: [],

                // Enter Site Logic with Audio Greeting Synth
                enterWebsite() {
                    this.showWelcomeOverlay = false;
                    this.playAudioGreeting();
                    this.$nextTick(() => lucide.createIcons());
                },

                playAudioGreeting() {
                    try {
                        const ctx = new (window.AudioContext || window.webkitAudioContext)();
                        const notes = [523.25, 659.25, 783.99, 1046.50]; // C5, E5, G5, C6 (Bright Melody)
                        notes.forEach((freq, index) => {
                            const osc = ctx.createOscillator();
                            const gain = ctx.createGain();
                            osc.type = 'sine';
                            osc.frequency.value = freq;
                            gain.gain.setValueAtTime(0.08, ctx.currentTime + index * 0.12);
                            gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + index * 0.12 + 0.4);
                            osc.connect(gain);
                            gain.connect(ctx.destination);
                            osc.start(ctx.currentTime + index * 0.12);
                            osc.stop(ctx.currentTime + index * 0.12 + 0.45);
                        });
                    } catch(e) {
                        console.log('Audio synth playback unavailable');
                    }
                },

                // Translations
                dict: {
                    th: {
                        navExplore: 'สถานที่ท่องเที่ยว',
                        navTransit: 'คำนวณรถไฟฟ้า BTS/MRT',
                        navItinerary: 'จัดทริปเดินทาง',
                        heroBadge: 'สวัสดีค่ะ 👋 ยินดีต้อนรับสู่คู่มือท่องเที่ยวกรุงเทพฯ 2026',
                        heroTitle1: 'สัมผัสเสน่ห์มหานคร',
                        heroTitle2: 'กรุงเทพฯ ที่ไม่เคยหลับใหล',
                        heroDesc: 'รวบรวมวัดวาอาราม ย่านอาหารสตรีทฟู้ด ตลาดกลางคืน ห้างสรรพสินค้าชั้นนำ และสถานที่ยอดฮิตพร้อมเส้นทาง BTS/MRT',
                        searchPlaceholder: 'ค้นหาชื่อสถานที่, ย่าน, BTS/MRT...',
                        districtLabel: 'เลือกย่านยอดนิยม',
                        allDistricts: 'ทุกย่าน',
                        showingResults: 'แสดงผลลัพธ์',
                        placesCount: 'สถานที่',
                        sortBy: 'เรียงตาม:',
                        sortRating: 'คะแนนรีวิวสูงสุด',
                        sortPopular: 'จำนวนรีวิวมากที่สุด',
                        viewDetails: 'ดูรายละเอียด',
                        addToPlan: 'เพิ่มลงทริป',
                        added: 'เพิ่มแล้ว',
                        rating: 'คะแนน',
                        district: 'ย่าน',
                        transit: 'สถานีใกล้เคียง',
                        aboutPlace: 'เกี่ยวกับสถานที่นี้',
                        locationMap: 'ตำแหน่งที่ตั้งและแผนที่',
                        openGoogleMaps: 'เปิดใน Google Maps',
                        transitTitleBadge: 'ระบบคำนวณการเดินทาง',
                        transitHeader: 'คำนวณเส้นทาง & ค่าโดยสาร BTS / MRT',
                        transitSub: 'เลือกสถานีต้นทางและปลายทางเพื่อประเมินค่าโดยสารและเวลาเดินทางโดยประมาณ',
                        originStation: 'สถานีต้นทาง',
                        destinationStation: 'สถานีปลายทาง',
                        estFare: 'ค่าโดยสารประมาณการ',
                        estTime: 'ระยะเวลาเดินทาง',
                        transfers: 'การเปลี่ยนสาย',
                        suggestedRoute: 'แนะนำเส้นทางเดินทาง',
                        directLineMsg: 'เดินทางด้วยสายตรง ไม่ต้องเปลี่ยนขบวน',
                        transitTransferMsg: 'มีจุดเปลี่ยนขบวน 1 ครั้ง (สยาม / อโศก / สีลม / เตาปูน / สำโรง)',
                        mins: 'นาที',
                        times: 'ครั้ง',
                        myItineraryTitle: 'แผนการท่องเที่ยวของคุณ',
                        myItinerarySub: 'รายการสถานที่ที่คุณเลือกไว้ สามารถจัดลำดับการเดินทางได้ตามต้องการ',
                        clearAll: 'ลบทั้งหมด',
                        exportPdf: 'พิมพ์ / บันทึก PDF',
                        tripSummary: 'สรุปข้อมูลทริป',
                        totalPlaces: 'จำนวนสถานที่ทั้งหมด',
                        estTravelTime: 'เวลารวมท่องเที่ยวโดยประมาณ',
                        hours: 'ชั่วโมง'
                    },
                    en: {
                        navExplore: 'Explore Attractions',
                        navTransit: 'BTS/MRT Calculator',
                        navItinerary: 'Trip Planner',
                        heroBadge: 'Sawasdee Ka 👋 Welcome to Miracle Bangkok 2026',
                        heroTitle1: 'Discover The Charm Of',
                        heroTitle2: 'Vibrant Bangkok City',
                        heroDesc: 'Explore iconic temples, legendary street food, night markets, modern malls, and easy BTS/MRT navigation.',
                        searchPlaceholder: 'Search places, districts, metro lines...',
                        districtLabel: 'Popular Districts',
                        allDistricts: 'All Districts',
                        showingResults: 'Showing',
                        placesCount: 'attractions',
                        sortBy: 'Sort by:',
                        sortRating: 'Highest Rating',
                        sortPopular: 'Most Reviewed',
                        viewDetails: 'Details',
                        addToPlan: 'Add to Trip',
                        added: 'Added',
                        rating: 'Rating',
                        district: 'District',
                        transit: 'Nearest Transit',
                        aboutPlace: 'About Destination',
                        locationMap: 'Location & Map',
                        openGoogleMaps: 'Open in Google Maps',
                        transitTitleBadge: 'Transit Navigation',
                        transitHeader: 'BTS / MRT Route & Fare Calculator',
                        transitSub: 'Select origin and destination stations to estimate ticket fare and duration.',
                        originStation: 'Origin Station',
                        destinationStation: 'Destination Station',
                        estFare: 'Estimated Fare',
                        estTime: 'Travel Time',
                        transfers: 'Line Transfers',
                        suggestedRoute: 'Suggested Route',
                        directLineMsg: 'Direct line - No transfer needed',
                        transitTransferMsg: 'Requires 1 transfer (Siam / Asok / Silom / Tao Poon / Samrong)',
                        mins: 'mins',
                        times: 'transfer(s)',
                        myItineraryTitle: 'My Travel Itinerary',
                        myItinerarySub: 'Manage and reorder your customized Bangkok day trip plan.',
                        clearAll: 'Clear All',
                        exportPdf: 'Print / Save PDF',
                        tripSummary: 'Trip Overview',
                        totalPlaces: 'Total Attractions',
                        estTravelTime: 'Estimated Total Time',
                        hours: 'hours'
                    }
                },

                // Master Districts
                districts: [
                    { id: 'rattanakosin', nameTh: 'เกาะรัตนโกสินทร์', nameEn: 'Rattanakosin' },
                    { id: 'siam', nameTh: 'สยาม / ราชประสงค์', nameEn: 'Siam & Ratchaprasong' },
                    { id: 'yaowarat', nameTh: 'เยาวราช / ตลาดน้อย', nameEn: 'Yaowarat & Talat Noi' },
                    { id: 'sukhumvit', nameTh: 'สุขุมวิท / อโศก', nameEn: 'Sukhumvit & Asok' },
                    { id: 'riverside', nameTh: 'ริมแม่น้ำเจ้าพระยา', nameEn: 'Chao Phraya Riverside' }
                ],

                // Categories
                categories: [
                    { id: 'all', nameTh: 'ทั้งหมด', nameEn: 'All', icon: 'grid' },
                    { id: 'temple', nameTh: 'วัด & วัฒนธรรม', nameEn: 'Culture & Temples', icon: 'landmark' },
                    { id: 'food', nameTh: 'สตรีทฟู้ด & ร้านอาหาร', nameEn: 'Food & Dining', icon: 'utensils' },
                    { id: 'shopping', nameTh: 'ช้อปปิ้ง & ตลาด', nameEn: 'Shopping & Markets', icon: 'shopping-bag' },
                    { id: 'nightlife', nameTh: 'ไนท์ไลฟ์ & บาร์', nameEn: 'Nightlife & Views', icon: 'moon' }
                ],

                // Metro Stations Database (BTS & MRT Lines)
                metroStations: [
                    { id: 'siam', line: 'BTS Green (Sukhumvit)', nameTh: 'สยาม (Siam)', nameEn: 'Siam' },
                    { id: 'asok', line: 'BTS Green (Sukhumvit)', nameTh: 'อโศก (Asok)', nameEn: 'Asok' },
                    { id: 'mochit', line: 'BTS Green (Sukhumvit)', nameTh: 'หมอชิต (Mo Chit)', nameEn: 'Mo Chit' },
                    { id: 'national_stadium', line: 'BTS Silom Line', nameTh: 'สนามกีฬาแห่งชาติ', nameEn: 'National Stadium' },
                    { id: 'saphan_taksin', line: 'BTS Silom Line', nameTh: 'สะพานตากสิน (Saphan Taksin)', nameEn: 'Saphan Taksin' },
                    { id: 'charoen_nakhon', line: 'BTS Gold Line', nameTh: 'เจริญนคร (ICONSIAM)', nameEn: 'Charoen Nakhon' },
                    { id: 'sanambhai', line: 'MRT Blue Line', nameTh: 'สนามไชย (Sanam Chai)', nameEn: 'Sanam Chai' },
                    { id: 'watmangkon', line: 'MRT Blue Line', nameTh: 'วัดมังกร (Wat Mangkon)', nameEn: 'Wat Mangkon' },
                    { id: 'hua_lamphong', line: 'MRT Blue Line', nameTh: 'หัวลำโพง (Hua Lamphong)', nameEn: 'Hua Lamphong' },
                    { id: 'sukhumvit_mrt', line: 'MRT Blue Line', nameTh: 'สุขุมวิท (Sukhumvit MRT)', nameEn: 'Sukhumvit MRT' },
                    { id: 'taopoon', line: 'MRT Purple Line', nameTh: 'เตาปูน (Tao Poon)', nameEn: 'Tao Poon' },
                    { id: 'yellow_samrong', line: 'MRT Yellow Line', nameTh: 'สำโรง (Yellow Line)', nameEn: 'Samrong (Yellow)' },
                    { id: 'pink_minburi', line: 'MRT Pink Line', nameTh: 'มีนบุรี (Pink Line)', nameEn: 'Min Buri (Pink)' }
                ],

                // Expanded Attractions Database (12 Places)
                places: [
                    {
                        id: 1,
                        nameTh: 'พระบรมมหาราชวัง และ วัดพระแก้ว',
                        nameEn: 'Grand Palace & Wat Phra Kaew',
                        category: 'temple',
                        district: 'rattanakosin',
                        rating: 4.9,
                        reviewCount: 2450,
                        hours: '08:30 - 15:30 น.',
                        transit: 'MRT สนามไชย (ทางออก 1) / เรือด่วนเจ้าพระยา',
                        image: 'https://images.unsplash.com/photo-1563492065599-3520f775eeed?auto=format&fit=crop&w=800&q=80',
                        descTh: 'พระบรมมหาราชวังและวัดพระศรีรัตนศาสดาราม สถาปัตยกรรมไทยอันวิจิตรงดงาม ประดิษฐานพระแก้วมรกตซึ่งเป็นศูนย์รวมจิตใจของคนไทย',
                        descEn: 'The majestic Grand Palace and Temple of the Emerald Buddha, showcasing world-famous Thai architecture.'
                    },
                    {
                        id: 2,
                        nameTh: 'วัดอรุณราชวราราม (วัดแจ้ง)',
                        nameEn: 'Wat Arun (Temple of Dawn)',
                        category: 'temple',
                        district: 'riverside',
                        rating: 4.9,
                        reviewCount: 1980,
                        hours: '08:00 - 18:00 น.',
                        transit: 'MRT อิสรภาพ / เรือข้ามฟากท่าเตียน',
                        image: 'https://images.unsplash.com/photo-1508009603885-50cf7c579365?auto=format&fit=crop&w=800&q=80',
                        descTh: 'วัดโบราณสัญลักษณ์ริมแม่น้ำเจ้าพระยา โดดเด่นด้วยพระปรางค์ประดับด้วยกระเบื้องเคลือบโบราณงดงาม สดใสยามสะท้อนแสงอาทิตย์',
                        descEn: 'Iconic riverside temple famous for its towering prang decorated with colorful porcelain pieces.'
                    },
                    {
                        id: 3,
                        nameTh: 'สตรีทฟู้ดเยาวราช',
                        nameEn: 'Yaowarat Street Food',
                        category: 'food',
                        district: 'yaowarat',
                        rating: 4.8,
                        reviewCount: 3100,
                        hours: '17:00 - 24:00 น.',
                        transit: 'MRT วัดมังกร (ทางออก 1)',
                        image: 'https://images.unsplash.com/photo-1555396273-367ea4eb4db5?auto=format&fit=crop&w=800&q=80',
                        descTh: 'สวรรค์ของคนรักอาหารยามค่ำคืน รวบรวมสตรีทฟู้ดระดับตำนาน ก๋วยจั๊บ ซีฟู้ด ขนมหวาน และร้านมิชลินไกด์มากมาย',
                        descEn: 'World-renowned Chinatown street food hub offering legendary local food, desserts, and Michelin stalls.'
                    },
                    {
                        id: 4,
                        nameTh: 'ไอคอนสยาม (ICONSIAM)',
                        nameEn: 'ICONSIAM & SookSiam',
                        category: 'shopping',
                        district: 'riverside',
                        rating: 4.9,
                        reviewCount: 2890,
                        hours: '10:00 - 22:00 น.',
                        transit: 'BTS เจริญนคร (สายสีทอง) / เรือรับส่ง',
                        image: 'https://images.unsplash.com/photo-1583491470869-bc984240aee0?auto=format&fit=crop&w=800&q=80',
                        descTh: 'อภิมหาโครงการเมืองริมแม่น้ำเจ้าพระยา รวมแบรนด์เนมระดับโลก พร้อมโซนสุขสยามจำลองตลาดน้ำและภูมิปัญญาไทย 4 ภาค',
                        descEn: 'World-class landmark shopping complex featuring high-end retail and SookSiam indoor floating market.'
                    },
                    {
                        id: 5,
                        nameTh: 'ตลาดนัดจตุจักร',
                        nameEn: 'Chatuchak Weekend Market',
                        category: 'shopping',
                        district: 'siam',
                        rating: 4.7,
                        reviewCount: 4200,
                        hours: 'ส.-อา. 09:00 - 18:00 น.',
                        transit: 'BTS หมอชิต / MRT กำแพงเพชร',
                        image: 'https://images.unsplash.com/photo-1513151233558-d860c5398176?auto=format&fit=crop&w=800&q=80',
                        descTh: 'ตลาดนัดกลางแจ้งที่ใหญ่ที่สุดแห่งหนึ่งของโลก รวมสินค้ามากกว่า 15,000 แผง ทั้งเสื้อผ้า ของแต่งบ้าน และของโบราณ',
                        descEn: 'One of the largest outdoor markets in the world with over 15,000 stalls selling fashion, handicrafts, and local food.'
                    },
                    {
                        id: 6,
                        nameTh: 'ตึกมหานคร สกายวอล์ค',
                        nameEn: 'Mahanakhon SkyWalk',
                        category: 'nightlife',
                        district: 'sukhumvit',
                        rating: 4.8,
                        reviewCount: 1420,
                        hours: '10:00 - 24:00 น.',
                        transit: 'BTS ช่องนนทรี (ทางออก 3)',
                        image: 'https://images.unsplash.com/photo-1540555700478-4be289fbecef?auto=format&fit=crop&w=800&q=80',
                        descTh: 'จุดชมวิวพื้นกระจกใสลอยฟ้าที่สูงที่สุดในประเทศไทย ณ ชั้น 78 ชมทัศนียภาพกรุงเทพฯ แบบ 360 องศา',
                        descEn: 'Thailand’s highest 360-degree observation deck with a glass-bottom floor on the 78th floor.'
                    },
                    {
                        id: 7,
                        nameTh: 'ตลาดน้อย & สตรีทอาร์ตเจริญกรุง',
                        nameEn: 'Talat Noi & Charoenkrung Creative District',
                        category: 'food',
                        district: 'yaowarat',
                        rating: 4.7,
                        reviewCount: 880,
                        hours: '09:00 - 19:00 น.',
                        transit: 'MRT หัวลำโพง / เรือด่วนกรมเจ้าท่า',
                        image: 'https://images.unsplash.com/photo-1513584684374-8bab748fbf90?auto=format&fit=crop&w=800&q=80',
                        descTh: 'ย่านชุมชนจีนโบราณริมแม่น้ำเจ้าพระยา โดดเด่นด้วยคาเฟ่วินเทจ สตรีทอาร์ตเก๋ๆ และเซียงกงในตำนาน',
                        descEn: 'Historic Chinese neighborhood turned creative district filled with vintage cafes, street art, and heritage alleyways.'
                    },
                    {
                        id: 8,
                        nameTh: 'หอศิลปวัฒนธรรมแห่งกรุงเทพมหานคร (BACC)',
                        nameEn: 'Bangkok Art and Culture Centre',
                        category: 'temple',
                        district: 'siam',
                        rating: 4.6,
                        reviewCount: 1650,
                        hours: '10:00 - 20:00 น. (ปิดวันจันทร์)',
                        transit: 'BTS สนามกีฬาแห่งชาติ (ทางออก 3)',
                        image: 'https://images.unsplash.com/photo-1561214115-f2f134cc4912?auto=format&fit=crop&w=800&q=80',
                        descTh: 'ศูนย์กลางจัดแสดงงานศิลปะร่วมสมัย นิทรรศการระดับชาติและนานาชาติ ดีไซน์ตึกรูปทรงก้นหอยสุดชิคใจกลางสยาม',
                        descEn: 'Contemporary art center hosting national and international exhibitions, design shops, and art cafes.'
                    },
                    {
                        id: 9,
                        nameTh: 'สวนป่าเบญจกิติ',
                        nameEn: 'Benchakitti Forest Park',
                        category: 'nightlife',
                        district: 'sukhumvit',
                        rating: 4.9,
                        reviewCount: 1350,
                        hours: '05:00 - 21:00 น.',
                        transit: 'BTS อโศก / MRT สุขุมวิท / MRT ศูนย์การประชุมแห่งชาติสิริกิติ์',
                        image: 'https://images.unsplash.com/photo-1500382017468-9049fed747ef?auto=format&fit=crop&w=800&q=80',
                        descTh: 'ปอดแห่งใหม่ใจกลางกรุงเทพฯ มี Skywalk ทางเดินลอยฟ้า สวนน้ำธรรมชาติ และลู่วิ่งปั่นจักรยานสุดร่มรื่น',
                        descEn: 'Vast urban forest park featuring elevated skywalks, wetland ecosystems, and scenic cycling tracks.'
                    },
                    {
                        id: 10,
                        nameTh: 'คลองโอ่งอ่าง (Street Art Canal)',
                        nameEn: 'Ong Ang Canal Street Art',
                        category: 'food',
                        district: 'rattanakosin',
                        rating: 4.6,
                        reviewCount: 790,
                        hours: '16:00 - 22:00 น.',
                        transit: 'MRT สามยอด (ทางออก 1)',
                        image: 'https://images.unsplash.com/photo-1526481280693-3bfa7568e0f3?auto=format&fit=crop&w=800&q=80',
                        descTh: 'ถนนคนเดินริมคลองประวัติศาสตร์ ปรับปรุงภูมิทัศน์สวยงาม เต็มไปด้วยภาพวาดสตรีทอาร์ต พายเรือคายัค และสตรีทฟู้ด',
                        descEn: 'Revitalized canal promenade featuring vibrant street art wall murals, kayaking, and street food stalls.'
                    },
                    {
                        id: 11,
                        nameTh: 'เอเชียทีค เดอะ ริเวอร์ฟรอนท์',
                        nameEn: 'Asiatique The Riverfront',
                        category: 'nightlife',
                        district: 'riverside',
                        rating: 4.7,
                        reviewCount: 2300,
                        hours: '16:00 - 24:00 น.',
                        transit: 'BTS สะพานตากสิน แล้วต่อเรือรับส่งเอเชียทีค',
                        image: 'https://images.unsplash.com/photo-1519671482749-fd09be7ccebf?auto=format&fit=crop&w=800&q=80',
                        descTh: 'แหล่งช้อปปิ้งและไลฟ์สไตล์ริมแม่น้ำเจ้าพระยา โดดเด่นด้วยชิงช้าสวรรค์ยักษ์ ASIATIQUE Sky และบ้านผีสิง',
                        descEn: 'Open-air night mall by the Chao Phraya River featuring the giant Ferris wheel and waterfront dining.'
                    },
                    {
                        id: 12,
                        nameTh: 'วัดไตรมิตรวิทยารามวรวิหาร',
                        nameEn: 'Wat Traimit (Temple of Golden Buddha)',
                        category: 'temple',
                        district: 'yaowarat',
                        rating: 4.8,
                        reviewCount: 1120,
                        hours: '08:00 - 17:00 น.',
                        transit: 'MRT หัวลำโพง (ทางออก 1)',
                        image: 'https://images.unsplash.com/photo-1563492065599-3520f775eeed?auto=format&fit=crop&w=800&q=80',
                        descTh: 'ประดิษฐาน "พระพุทธมหาสุวรรณปฏิมากร" พระพุทธรูปทองคำแท้ที่ใหญ่ที่สุดในโลก น้ำหนักกว่า 5.5 ตัน',
                        descEn: 'Home to the world\'s largest solid gold Buddha statue, weighing over 5.5 tons.'
                    }
                ],

                // Methods
                initApp() {
                    this.$nextTick(() => {
                        lucide.createIcons();
                    });
                },

                toggleLang() {
                    this.lang = this.lang === 'th' ? 'en' : 'th';
                    this.$nextTick(() => lucide.createIcons());
                },

                t(key) {
                    return this.dict[this.lang][key] || key;
                },

                scrollToTop() {
                    window.scrollTo({ top: 0, behavior: 'smooth' });
                },

                get filteredPlaces() {
                    let list = this.places.filter(p => {
                        const matchCat = this.selectedCategory === 'all' || p.category === this.selectedCategory;
                        const matchDist = this.selectedDistrict === 'all' || p.district === this.selectedDistrict;
                        const q = this.searchQuery.toLowerCase();
                        const matchSearch = !q || 
                            p.nameTh.toLowerCase().includes(q) || 
                            p.nameEn.toLowerCase().includes(q) || 
                            p.descTh.toLowerCase().includes(q) ||
                            p.transit.toLowerCase().includes(q);
                        
                        return matchCat && matchDist && matchSearch;
                    });

                    if (this.sortBy === 'rating') {
                        list.sort((a, b) => b.rating - a.rating);
                    } else if (this.sortBy === 'reviews') {
                        list.sort((a, b) => b.reviewCount - a.reviewCount);
                    }

                    return list;
                },

                getCategoryCount(catId) {
                    if (catId === 'all') return this.places.length;
                    return this.places.filter(p => p.category === catId).length;
                },

                getCategoryName(catId) {
                    const c = this.categories.find(item => item.id === catId);
                    return c ? (this.lang === 'th' ? c.nameTh : c.nameEn) : catId;
                },

                getDistrictName(distId) {
                    const d = this.districts.find(item => item.id === distId);
                    return d ? (this.lang === 'th' ? d.nameTh : d.nameEn) : distId;
                },

                openModal(place) {
                    this.selectedPlace = place;
                    this.modalOpen = true;
                    this.$nextTick(() => lucide.createIcons());
                },

                closeModal() {
                    this.modalOpen = false;
                    this.selectedPlace = null;
                },

                toggleItinerary(place) {
                    const exists = this.itinerary.some(item => item.id === place.id);
                    if (exists) {
                        this.itinerary = this.itinerary.filter(item => item.id !== place.id);
                    } else {
                        this.itinerary.push(place);
                    }
                },

                isInItinerary(placeId) {
                    return this.itinerary.some(item => item.id === placeId);
                },

                removeFromItinerary(placeId) {
                    this.itinerary = this.itinerary.filter(item => item.id !== placeId);
                },

                clearItinerary() {
                    this.itinerary = [];
                },

                moveItineraryItem(index, direction) {
                    const newIndex = index + direction;
                    if (newIndex < 0 || newIndex >= this.itinerary.length) return;
                    const temp = this.itinerary[index];
                    this.itinerary[index] = this.itinerary[newIndex];
                    this.itinerary[newIndex] = temp;
                },

                getStationName(stId) {
                    const st = this.metroStations.find(s => s.id === stId);
                    return st ? (this.lang === 'th' ? st.nameTh : st.nameEn) : stId;
                },

                calculateTransit() {
                    if (this.transitStart === this.transitEnd) {
                        return { fare: 0, time: 0, transfers: 0 };
                    }
                    const st1 = this.metroStations.find(s => s.id === this.transitStart);
                    const st2 = this.metroStations.find(s => s.id === this.transitEnd);

                    const sameLine = st1 && st2 && st1.line === st2.line;
                    const transfers = sameLine ? 0 : 1;
                    const fare = sameLine ? 35 : 52;
                    const time = sameLine ? 15 : 30;

                    return { fare, time, transfers };
                }
            }
        }
    </script>
</body>
</html>
