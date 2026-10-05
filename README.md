<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Styloan - What are you wearing next? เช่าลุคใหม่ ไม่ต้องซื้อซ้ำ</title>
  
  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  
  <!-- Lucide Minimal Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            brand: {
              blue: '#5B8DF0',
              blueDark: '#3B68C4',
              blueLight: '#EEF4FF',
              yellow: '#FACC15',
              yellowLight: '#FEF9C3',
              pink: '#F472B6',
              pinkLight: '#FDF2F8',
              lavender: '#C084FC',
              lavenderLight: '#F3E8FF'
            }
          },
          fontFamily: {
            sans: ['Prompt', 'sans-serif'],
            serif: ['Playfair Display', 'serif']
          }
        }
      }
    }
  </script>

  <style>
    body {
      font-family: 'Prompt', sans-serif;
      background-color: #FAFAFD;
      color: #1E293B;
      -webkit-tap-highlight-color: transparent;
      overflow-x: hidden;
    }
    .font-brand-logo { font-family: 'Playfair Display', serif; }
    .wavy-underline {
      text-decoration: underline wavy #FACC15 4px;
      text-underline-offset: 8px;
    }
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    @keyframes floatSlow {
      0%, 100% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-8px) rotate(6deg); }
    }
    .floating-star { animation: floatSlow 4s ease-in-out infinite; }
    @keyframes pulseRoute {
      0% { stroke-dashoffset: 20; }
      100% { stroke-dashoffset: 0; }
    }
    .route-line {
      stroke-dasharray: 6;
      animation: pulseRoute 1.5s linear infinite;
    }
  </style>
</head>
<body class="min-h-screen flex flex-col pb-20 md:pb-0">

  <!-- Header / Navigation Bar -->
  <header id="mainHeader" class="sticky top-0 z-40 bg-white/95 backdrop-blur border-b border-slate-100 shadow-sm transition-all duration-300">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 sm:h-20 flex items-center justify-between gap-4">
      
      <!-- Brand Logo -->
      <a href="javascript:void(0)" onclick="navigateTo('home')" class="flex items-center gap-2 group shrink-0">
        <div class="relative bg-brand-blue text-white w-8 h-10 sm:w-10 sm:h-12 rounded-t-lg rounded-b-xl flex items-center justify-center shadow-md shadow-brand-blue/30 group-hover:scale-105 transition-transform">
          <div class="w-2 h-2 sm:w-2.5 sm:h-2.5 bg-white rounded-full absolute top-1.5 shadow-inner"></div>
          <span class="font-brand-logo text-xl sm:text-2xl font-black text-brand-yellowLight mt-1 drop-shadow">S</span>
        </div>
        <div class="flex items-baseline">
          <span class="font-brand-logo text-2xl sm:text-3xl font-black tracking-tight text-slate-900">styloan</span>
          <span class="text-brand-pink text-2xl sm:text-3xl font-black leading-none">.</span>
        </div>
      </a>

      <!-- Sticky Search Bar on Scroll -->
      <div id="stickySearchContainer" class="hidden flex-1 max-w-md mx-2 transition-all opacity-0 translate-y-[-10px]">
        <div class="bg-slate-100 rounded-full px-3 py-1.5 border border-slate-200 flex items-center gap-2 text-xs">
          <i data-lucide="search" class="w-3.5 h-3.5 text-slate-400 shrink-0"></i>
          <input type="text" id="stickySearchInput" oninput="handleSearchFilter(this.value)" placeholder="ค้นหาชุดเดรส, สูท, คอสเพลย์..." class="w-full bg-transparent border-none focus:outline-none text-slate-700 placeholder:text-slate-400">
          <button type="button" onclick="openImageSearchModal()" class="text-brand-blue p-0.5 hover:opacity-80">
            <i data-lucide="camera" class="w-3.5 h-3.5"></i>
          </button>
          <button type="button" onclick="toggleSearchMenuModal()" class="text-slate-500 p-0.5 hover:opacity-80">
            <i data-lucide="sliders-horizontal" class="w-3.5 h-3.5"></i>
          </button>
        </div>
      </div>

      <!-- Desktop Nav Links -->
      <nav class="hidden md:flex items-center gap-5 text-xs font-medium text-slate-600">
        <button onclick="navigateTo('home')" class="hover:text-brand-blue transition">หน้าแรก</button>
        <button onclick="navigateTo('wishlist')" class="hover:text-brand-blue flex items-center gap-1.5 transition">
          <i data-lucide="heart" class="w-4 h-4 text-brand-pink"></i> รายการโปรด (<span id="navWishlistCount">0</span>)
        </button>
        <button onclick="navigateTo('bookings')" class="hover:text-brand-blue flex items-center gap-1.5 transition">
          <i data-lucide="calendar-check" class="w-4 h-4 text-brand-blue"></i> ออเดอร์ของฉัน
        </button>
        <button onclick="navigateTo('return-schedule')" class="hover:text-brand-blue flex items-center gap-1.5 transition">
          <i data-lucide="clock" class="w-4 h-4 text-amber-500"></i> ปฏิทินวันคืนชุด
        </button>
      </nav>

      <!-- Actions -->
      <div class="flex items-center gap-2 sm:gap-3 shrink-0">
        <!-- Notification Bell -->
        <button onclick="toggleNotificationsModal()" class="relative p-2 rounded-full hover:bg-slate-100 text-slate-600 transition">
          <i data-lucide="bell" class="w-5 h-5"></i>
          <span id="unreadNotifBadge" class="absolute top-1.5 right-1.5 w-2 h-2 bg-brand-pink rounded-full ring-2 ring-white"></span>
        </button>

        <!-- Coins Chip -->
        <button onclick="openCoinRewardsModal()" class="flex items-center gap-1.5 bg-brand-yellowLight hover:bg-yellow-200 border border-yellow-300 text-yellow-900 px-3 py-1.5 rounded-full text-xs font-bold transition-all shadow-sm active:scale-95">
          <span>🪙</span>
          <span id="navCoinCount">420</span>
          <span class="hidden sm:inline text-[10px] bg-white text-brand-pink px-1.5 py-0.5 rounded-full border border-brand-pink/30 font-semibold">โค้ด</span>
        </button>

        <!-- Profile Button -->
        <button onclick="navigateTo('profile')" class="flex items-center gap-1.5 bg-slate-100 hover:bg-slate-200 border border-slate-200 p-1.5 sm:px-3 sm:py-1.5 rounded-full text-xs font-semibold text-slate-700 transition">
          <div class="w-6 h-6 rounded-full bg-gradient-to-tr from-brand-pink to-brand-blue flex items-center justify-center text-white text-[10px] font-bold">
            <i data-lucide="user" class="w-3.5 h-3.5"></i>
          </div>
          <span class="hidden sm:inline">โปรไฟล์</span>
        </button>
      </div>

    </div>
  </header>

  <!-- Main Container -->
  <main class="flex-1 w-full mx-auto">

    <!-- ================= VIEW 1: HOME ================= -->
    <section id="view-home" class="space-y-6 sm:space-y-8">
      
      <!-- HERO SECTION -->
      <div class="relative overflow-hidden bg-gradient-to-b from-white via-blue-50/20 to-white pt-8 sm:pt-10 pb-10 sm:pb-12 px-4 sm:px-6 lg:px-8 text-center border-b border-slate-100/80">
        
        <!-- Pastel Floating Stars -->
        <div class="floating-star absolute top-3 sm:top-6 right-4 sm:right-16 text-yellow-300/80 text-3xl sm:text-5xl select-none pointer-events-none">★</div>
        <div class="floating-star absolute top-24 sm:top-24 left-3 sm:left-14 text-pink-300/70 text-2xl sm:text-4xl select-none pointer-events-none" style="animation-delay: 1.5s;">★</div>
        <div class="floating-star absolute bottom-3 right-6 sm:right-24 text-purple-300/60 text-2xl sm:text-4xl select-none pointer-events-none" style="animation-delay: 2.5s;">★</div>

        <div class="max-w-4xl mx-auto relative z-10 space-y-4 sm:space-y-5">
          <div class="inline-flex items-center gap-1.5 bg-amber-50 border border-amber-200/90 text-amber-900 px-3.5 py-1 rounded-full text-[11px] sm:text-xs font-medium shadow-sm">
            <span class="text-amber-500">⭐</span>
            <span>Hyperlocal Clothing Rental • เช่าลุคใหม่ ไม่ต้องซื้อซ้ำ</span>
          </div>

          <h1 class="text-3xl sm:text-5xl md:text-6xl font-black text-slate-900 tracking-tight leading-tight">
            <span class="font-serif">What are you</span> 
            <span class="font-serif italic text-brand-blue font-bold wavy-underline ml-1">wearing next?</span>
          </h1>

          <p class="text-slate-600 text-xs sm:text-sm md:text-base max-w-2xl mx-auto leading-relaxed px-2">
            เบื่อซื้อชุดใส่ครั้งเดียวแล้วล้นตู้? รวมร้านเช่าชุดสุดชิค สตรีทแวร์ คอสเพลย์ ชุดราตรี คาเฟ่ฮอปปิ้ง<br class="hidden sm:inline">
            พร้อมระบบคุ้มครองเงินมัดจำ Escrow ปลอดภัย 100%
          </p>

          <!-- Search Bar -->
          <div id="mainHeroSearchTrigger" class="pt-1 sm:pt-2 max-w-2xl mx-auto">
            <div class="bg-white rounded-2xl sm:rounded-full p-2 pl-3.5 sm:pl-5 shadow-lg shadow-slate-200/60 border border-slate-200/80 flex flex-col sm:flex-row items-center gap-2 transition-all focus-within:border-brand-blue">
              <div class="flex items-center gap-2 w-full flex-1">
                <i data-lucide="search" class="w-4 h-4 text-slate-400 shrink-0"></i>
                <input type="text" id="homeSearchInput" oninput="handleSearchFilter(this.value)" placeholder="ค้นหาชุดเดรส, สูท, แบรนด์ หรือคอสเพลย์..." 
                  class="w-full text-xs sm:text-sm bg-transparent border-none focus:outline-none text-slate-700 placeholder:text-slate-400 py-1">
                
                <button type="button" onclick="openImageSearchModal()" title="ค้นหาจากรูปภาพ" class="p-1.5 rounded-full hover:bg-slate-100 text-brand-blue transition">
                  <i data-lucide="camera" class="w-4 h-4"></i>
                </button>

                <button type="button" onclick="toggleSearchMenuModal()" title="เมนูค้นหา & ตัวกรอง" class="p-1.5 rounded-full hover:bg-slate-100 text-slate-500 transition">
                  <i data-lucide="sliders-horizontal" class="w-4 h-4"></i>
                </button>
              </div>

              <button onclick="triggerSearch()" class="w-full sm:w-auto bg-brand-blue hover:bg-brand-blueDark text-white px-6 py-2.5 rounded-xl sm:rounded-full text-xs sm:text-sm font-semibold shadow-md shadow-brand-blue/30 transition">
                ค้นหา
              </button>
            </div>
          </div>

          <!-- 4 Features Bar -->
          <div class="pt-3 sm:pt-4 flex flex-wrap items-center justify-center gap-y-2 gap-x-3 sm:gap-x-6 text-[10px] sm:text-xs text-slate-600 font-medium">
            <span class="flex items-center gap-1.5"><i data-lucide="shield-check" class="w-3.5 h-3.5 sm:w-4 sm:h-4 text-brand-blue"></i> บัญชี Escrow กักเงินมัดจำ</span>
            <span class="flex items-center gap-1.5"><i data-lucide="bike" class="w-3.5 h-3.5 sm:w-4 sm:h-4 text-brand-pink"></i> มีไรเดอร์ส่งด่วน Same-Day</span>
            <span class="flex items-center gap-1.5"><i data-lucide="calendar" class="w-3.5 h-3.5 sm:w-4 sm:h-4 text-emerald-500"></i> เว้น Buffer ซัก อบ รีด ก่อน-หลัง</span>
            <span class="flex items-center gap-1.5"><i data-lucide="recycle" class="w-3.5 h-3.5 sm:w-4 sm:h-4 text-emerald-600"></i> ลดขยะ Fast Fashion</span>
          </div>
        </div>
      </div>

      <!-- Main Home Content -->
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-6 sm:space-y-8">
        
        <!-- Explore Vibe Categories -->
        <div>
          <div class="flex items-center justify-between mb-3 px-1">
            <h2 class="text-sm sm:text-lg font-bold text-slate-900 flex items-center gap-1.5">
              <span>Explore your vibe</span>
              <span class="text-[10px] text-brand-pink bg-brand-pinkLight px-2 py-0.5 rounded-full font-medium">สไตล์เด่น</span>
            </h2>
            <span class="text-[11px] text-slate-400">เลือกสไตล์ชุด</span>
          </div>
          
          <div class="flex sm:grid sm:grid-cols-7 gap-2 sm:gap-2.5 overflow-x-auto no-scrollbar pb-1">
            <button onclick="filterVibe('all')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-brand-blue text-brand-blue font-semibold text-xs shadow-sm">
              <i data-lucide="sparkles" class="w-5 h-5 mb-1 text-brand-blue"></i>
              <span>ทั้งหมด</span>
            </button>
            <button onclick="filterVibe('Cosplay')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-slate-200 text-slate-700 font-semibold text-xs shadow-sm hover:border-brand-pink hover:text-brand-pink transition">
              <i data-lucide="wand-2" class="w-5 h-5 mb-1 text-slate-600"></i>
              <span>Cosplay</span>
            </button>
            <button onclick="filterVibe('Party')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-slate-200 text-slate-700 font-semibold text-xs shadow-sm hover:border-brand-pink hover:text-brand-pink transition">
              <i data-lucide="party-popper" class="w-5 h-5 mb-1 text-slate-600"></i>
              <span>Party</span>
            </button>
            <button onclick="filterVibe('Dinner')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-slate-200 text-slate-700 font-semibold text-xs shadow-sm hover:border-brand-yellow hover:text-amber-600 transition">
              <i data-lucide="wine" class="w-5 h-5 mb-1 text-slate-600"></i>
              <span>Dinner</span>
            </button>
            <button onclick="filterVibe('Wedding')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-slate-200 text-slate-700 font-semibold text-xs shadow-sm hover:border-brand-lavender hover:text-brand-lavender transition">
              <i data-lucide="heart-handshake" class="w-5 h-5 mb-1 text-slate-600"></i>
              <span>Wedding</span>
            </button>
            <button onclick="filterVibe('Y2K')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-slate-200 text-slate-700 font-semibold text-xs shadow-sm hover:border-brand-pink hover:text-brand-pink transition">
              <i data-lucide="glasses" class="w-5 h-5 mb-1 text-slate-600"></i>
              <span>Y2K</span>
            </button>
            <button onclick="filterVibe('Cafe')" class="vibe-btn shrink-0 min-w-[80px] sm:min-w-0 flex flex-col items-center justify-center p-3 rounded-2xl bg-white border border-slate-200 text-slate-700 font-semibold text-xs shadow-sm hover:border-emerald-400 hover:text-emerald-600 transition">
              <i data-lucide="coffee" class="w-5 h-5 mb-1 text-slate-600"></i>
              <span>Cafe</span>
            </button>
          </div>
        </div>

        <!-- Garment Catalog Section -->
        <div id="catalog-section" class="space-y-4">
          <div class="flex items-center justify-between border-b border-slate-200 pb-2 px-1">
            <div>
              <h2 class="text-sm sm:text-lg font-bold text-slate-900">Trending Garments</h2>
              <p class="text-[11px] text-slate-400">คอลเลกชันเสื้อผ้าให้เช่าทั้งหมด พร้อมระบบ Buffer ป้องกันวันชนกระชั้นชิด</p>
            </div>
            <div class="text-[11px] font-semibold text-brand-blue" id="garmentCountBadge">30 รายการ</div>
          </div>

          <div id="garmentGrid" class="grid grid-cols-2 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-3 sm:gap-6">
            <!-- Rendered via JS -->
          </div>
        </div>

      </div>

    </section>

    <!-- ================= VIEW 2: WISHLIST ================= -->
    <section id="view-wishlist" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 space-y-5">
      <div class="flex items-center justify-between">
        <button onclick="goBack()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 hover:text-brand-blue bg-white px-3 py-1.5 rounded-xl border border-slate-200 shadow-sm transition">
          <i data-lucide="arrow-left" class="w-4 h-4"></i> ย้อนกลับ
        </button>
        <span class="text-xs font-bold text-brand-pink bg-pink-50 px-2.5 py-1 rounded-full">
          <i data-lucide="heart" class="w-3.5 h-3.5 inline mr-1 text-brand-pink"></i> รายการโปรดของคุณ
        </span>
      </div>

      <div class="bg-white rounded-2xl sm:rounded-3xl p-5 border border-slate-100 shadow-sm space-y-4">
        <div class="border-b border-slate-100 pb-3 flex justify-between items-center">
          <div>
            <h1 class="text-base sm:text-xl font-bold text-slate-900">รายการโปรดของฉัน (My Wishlist)</h1>
            <p class="text-xs text-slate-400">ชุดเสื้อผ้าที่คุณกดถูกใจไว้ เช็คสถานะความพร้อมและกดจองได้ทันที</p>
          </div>
        </div>
        <div id="wishlistGrid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-3 sm:gap-6"></div>
      </div>
    </section>

    <!-- ================= VIEW 3: GARMENT DETAIL ================= -->
    <section id="view-garment-detail" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 space-y-5">
      <div class="flex items-center justify-between">
        <button onclick="goBack()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 hover:text-brand-blue bg-white px-3 py-1.5 rounded-xl border border-slate-200 shadow-sm transition">
          <i data-lucide="arrow-left" class="w-4 h-4"></i> ย้อนกลับ
        </button>
        <div class="flex items-center gap-2">
          <button id="detailWishlistBtn" onclick="toggleWishlistFromDetail()" class="p-2 rounded-xl bg-white border border-slate-200 text-slate-400 hover:text-brand-pink transition shadow-sm">
            <i data-lucide="heart" class="w-4 h-4"></i>
          </button>
          <span class="text-xs text-slate-400">รหัสชุด: <span id="detailGarmentCode">#STY-G01</span></span>
        </div>
      </div>

      <div class="bg-white rounded-2xl sm:rounded-3xl p-4 sm:p-8 border border-slate-100 shadow-sm grid grid-cols-1 md:grid-cols-2 gap-6 sm:gap-8">
        <div class="space-y-3">
          <div class="h-72 sm:h-96 rounded-2xl overflow-hidden bg-slate-100 shadow-inner">
            <img id="detailMainImg" src="" alt="garment" class="w-full h-full object-cover">
          </div>
          <div class="bg-slate-50 p-3 rounded-2xl border border-slate-200/80 space-y-1">
            <div class="flex items-center justify-between text-xs">
              <span class="font-bold text-slate-800 flex items-center gap-1.5">
                <i data-lucide="shield-check" class="w-4 h-4 text-emerald-500"></i> หลักฐานสภาพชุดก่อนส่ง (3 มุม)
              </span>
              <span class="text-[10px] text-emerald-700 bg-emerald-100 px-2 py-0.5 rounded-full font-semibold">ตรวจสอบแล้ว</span>
            </div>
            <p class="text-[11px] text-slate-500">ร้านค้าอัปโหลดภาพถ่ายสภาพชุดจริงในระบบ Escrow คืนเงินมัดจำ 100% เมื่อคืนชุดสมบูรณ์</p>
          </div>
        </div>

        <div class="flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div>
              <div class="flex items-center gap-2 mb-1">
                <span id="detailCategoryBadge" class="text-[10px] font-bold px-2.5 py-0.5 rounded-full bg-brand-pinkLight text-brand-pink">Party</span>
                <span id="detailColorBadge" class="text-[10px] font-bold px-2 py-0.5 rounded-full bg-slate-100 text-slate-600">สีชมพู</span>
                <span id="detailBrandName" class="text-xs text-slate-400 font-medium">Mitr</span>
              </div>
              <h1 id="detailTitle" class="text-xl sm:text-2xl font-bold text-slate-900">Mira Satin Maxi Dress</h1>
            </div>

            <div class="bg-blue-50/60 p-3.5 rounded-2xl border border-blue-100 flex items-center justify-between">
              <div>
                <span class="text-[10px] text-slate-500 block">ราคาค่าเช่าเริ่มต้น (ต่อวัน)</span>
                <span id="detailRentPrice" class="text-xl sm:text-2xl font-black text-brand-blue">฿250 <span class="text-xs font-normal text-slate-500">/วัน</span></span>
              </div>
              <div class="text-right">
                <span class="text-[10px] text-slate-500 block">เงินมัดจำประกันความเสียหาย</span>
                <span id="detailDepositPrice" class="text-sm sm:text-base font-bold text-amber-700">฿1,000</span>
                <span class="text-[9px] text-slate-400 block">(โอนคืนบัญชีที่คุณเลือกได้ 100%)</span>
              </div>
            </div>

            <div class="space-y-1.5">
              <h3 class="text-xs font-bold text-slate-800 flex items-center gap-1.5">
                <i data-lucide="ruler" class="w-4 h-4 text-brand-blue"></i> ขนาดสัดส่วนชุด (หน่วยเป็นนิ้ว)
              </h3>
              <div class="grid grid-cols-4 gap-2 text-center text-xs">
                <div class="bg-slate-50 p-2 rounded-xl border border-slate-200">
                  <span class="text-[9px] text-slate-400 block">รอบอก</span>
                  <span id="detailChest" class="font-bold text-slate-800">32-34"</span>
                </div>
                <div class="bg-slate-50 p-2 rounded-xl border border-slate-200">
                  <span class="text-[9px] text-slate-400 block">รอบเอว</span>
                  <span id="detailWaist" class="font-bold text-slate-800">25-27"</span>
                </div>
                <div class="bg-slate-50 p-2 rounded-xl border border-slate-200">
                  <span class="text-[9px] text-slate-400 block">สะโพก</span>
                  <span id="detailHips" class="font-bold text-slate-800">36"</span>
                </div>
                <div class="bg-slate-50 p-2 rounded-xl border border-slate-200">
                  <span class="text-[9px] text-slate-400 block">ความยาว</span>
                  <span id="detailLength" class="font-bold text-slate-800">48"</span>
                </div>
              </div>
            </div>

            <div class="p-3 rounded-2xl border border-slate-200 bg-white hover:border-brand-blue transition flex items-center justify-between">
              <div class="flex items-center gap-2">
                <div class="w-8 h-8 rounded-full bg-brand-pinkLight flex items-center justify-center text-brand-pink">
                  <i data-lucide="store" class="w-4 h-4"></i>
                </div>
                <div>
                  <h4 id="detailStoreName" class="font-bold text-xs text-slate-900">Studio Dress Up</h4>
                  <p id="detailStoreLocation" class="text-[10px] text-slate-500">ชลบุรี • ยืนยัน KYC แล้ว</p>
                </div>
              </div>
              <button onclick="openLenderFullProfile(currentDetailIndex)" class="text-[11px] font-semibold text-brand-blue hover:text-brand-blueDark bg-brand-blueLight px-2.5 py-1.5 rounded-xl">
                ดูร้านค้า
              </button>
            </div>
          </div>

          <div class="flex gap-2 pt-1">
            <button onclick="openChatFromDetail()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 px-3.5 py-2.5 rounded-xl text-xs font-semibold flex items-center gap-1.5 transition">
              <i data-lucide="message-circle" class="w-4 h-4 text-brand-blue"></i> ถามร้าน
            </button>
            <button onclick="proceedToBookingFromDetail()" class="flex-1 bg-brand-blue hover:bg-brand-blueDark text-white px-4 py-2.5 rounded-xl text-xs font-bold shadow-md transition flex items-center justify-center gap-1.5">
              <i data-lucide="calendar" class="w-4 h-4"></i> จองชุดนี้ (เลือกวัน)
            </button>
          </div>
        </div>
      </div>

      <!-- Reviews Section -->
      <div class="bg-white rounded-2xl sm:rounded-3xl p-4 sm:p-7 border border-slate-100 shadow-sm space-y-4">
        <div class="flex justify-between items-center border-b border-slate-100 pb-3">
          <h2 class="text-sm sm:text-base font-bold text-slate-900 flex items-center gap-1.5">
            <i data-lucide="star" class="w-4 h-4 text-brand-yellow"></i> รีวิวจากผู้เช่าจริง
          </h2>
          <button onclick="openWriteReviewModal(currentDetailIndex)" class="bg-brand-pinkLight text-brand-pink px-3 py-1.5 rounded-xl text-xs font-bold">
            เขียนรีวิว
          </button>
        </div>
        <div id="detailReviewsList" class="space-y-2.5"></div>
      </div>
    </section>

    <!-- ================= VIEW 4: MY BOOKINGS & ORDERS (พร้อมฟังก์ชันเรียกไรเดอร์รับชุดในหน้ารายการเช่า) ================= -->
    <section id="view-bookings" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 space-y-5">
      <button onclick="goBack()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 hover:text-brand-blue bg-white px-3 py-1.5 rounded-xl border border-slate-200 shadow-sm transition">
        <i data-lucide="arrow-left" class="w-4 h-4"></i> ย้อนกลับ
      </button>

      <div class="bg-white rounded-2xl sm:rounded-3xl p-4 sm:p-7 border border-slate-100 shadow-sm space-y-5">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 border-b border-slate-100 pb-4">
          <div>
            <h1 class="text-base sm:text-xl font-bold text-slate-900 flex items-center gap-2">
              <i data-lucide="calendar-check" class="w-5 h-5 text-brand-blue"></i> ออเดอร์ & การจองของฉัน
            </h1>
            <p class="text-xs text-slate-400">ตรวจสอบสถานะ เรียกไรเดอร์รับชุดคืน และดูประวัติที่คืนเสร็จสิ้น</p>
          </div>

          <div class="flex bg-slate-100 p-1 rounded-xl text-xs font-bold">
            <button onclick="switchBookingTab('active')" id="tabActiveBookingsBtn" class="px-4 py-1.5 rounded-lg bg-white text-brand-blue shadow-sm transition">
              กำลังดำเนินการ (<span id="activeOrdersBadge">1</span>)
            </button>
            <button onclick="switchBookingTab('history')" id="tabHistoryBookingsBtn" class="px-4 py-1.5 rounded-lg text-slate-500 hover:text-slate-800 transition">
              ประวัติที่คืนแล้ว (<span id="historyOrdersBadge">0</span>)
            </button>
          </div>
        </div>

        <!-- 1. รายการจองปัจจุบัน (Active Orders) -->
        <div id="activeBookingsContainer" class="space-y-4"></div>

        <!-- 2. ประวัติการเช่าที่เสร็จสิ้นแล้ว (Completed History) -->
        <div id="historyBookingsContainer" class="hidden space-y-4"></div>

        <!-- Embedded Grab-Style Live Rider Tracker Interface -->
        <div id="embeddedGrabTracker" class="hidden border border-emerald-200 rounded-3xl overflow-hidden bg-slate-50 shadow-md animate-in fade-in duration-200 space-y-0">
          <div class="bg-slate-900 text-white p-3 px-5 flex justify-between items-center">
            <div class="flex items-center gap-2">
              <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-ping"></span>
              <span class="font-bold text-xs sm:text-sm">ติดตามตำแหน่งไรเดอร์แบบสด (Grab Live View)</span>
            </div>
            <button onclick="closeEmbeddedTracker()" class="text-slate-400 hover:text-white text-xs">ปิดแผนที่</button>
          </div>

          <div class="relative h-64 sm:h-80 bg-slate-100 overflow-hidden flex items-center justify-center">
            <svg class="absolute inset-0 w-full h-full" xmlns="http://www.w3.org/2000/svg">
              <defs>
                <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
                  <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#E2E8F0" stroke-width="1"/>
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="#F8FAFC" />
              <rect width="100%" height="100%" fill="url(#grid)" />
              <path d="M 50 150 Q 200 80, 380 200 T 700 240" fill="none" stroke="#CBD5E1" stroke-width="12" stroke-linecap="round"/>
              <path d="M 50 150 Q 200 80, 380 200 T 700 240" fill="none" stroke="#5B8DF0" stroke-width="6" stroke-linecap="round" class="route-line"/>
            </svg>

            <div class="absolute left-10 top-24 flex flex-col items-center">
              <div class="bg-white p-1.5 rounded-full shadow-lg border border-slate-200">
                <div class="w-5 h-5 rounded-full bg-brand-blue text-white flex items-center justify-center text-[10px]">
                  <i data-lucide="store" class="w-3.5 h-3.5"></i>
                </div>
              </div>
              <span class="bg-slate-900 text-white text-[8px] font-bold px-1.5 py-0.5 rounded-full mt-0.5">ร้านค้า</span>
            </div>

            <div id="movingRiderPin" class="absolute left-1/2 top-36 -translate-x-1/2 flex flex-col items-center transition-all duration-1000">
              <div class="bg-white p-1.5 rounded-full shadow-2xl border-2 border-emerald-500 animate-bounce">
                <div class="w-6 h-6 rounded-full bg-emerald-500 text-white flex items-center justify-center text-xs">
                  <i data-lucide="bike" class="w-3.5 h-3.5"></i>
                </div>
              </div>
              <span class="bg-emerald-600 text-white text-[9px] font-bold px-2 py-0.5 rounded-full shadow-md mt-0.5">
                ไรเดอร์กำลังปฏิบัติงาน (~15 นาที)
              </span>
            </div>

            <div class="absolute right-10 bottom-14 flex flex-col items-center">
              <div class="bg-white p-1.5 rounded-full shadow-lg border border-slate-200">
                <div class="w-5 h-5 rounded-full bg-brand-pink text-white flex items-center justify-center text-[10px]">
                  <i data-lucide="home" class="w-3.5 h-3.5"></i>
                </div>
              </div>
              <span class="bg-slate-900 text-white text-[8px] font-bold px-1.5 py-0.5 rounded-full mt-0.5">ที่พักคุณ</span>
            </div>
          </div>

          <div class="p-3.5 sm:p-4 bg-white border-t border-slate-200 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-3">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-full bg-emerald-100 border-2 border-emerald-500 flex items-center justify-center text-emerald-700 font-bold">
                🛵
              </div>
              <div>
                <h4 class="font-bold text-slate-900 text-xs sm:text-sm">พี่วัฒนา ใจดี (Rider Same-Day)</h4>
                <p class="text-[10px] text-slate-500">Honda Click 150i • 1กข-8921 ชลบุรี • ⭐ 4.98</p>
              </div>
            </div>
            <div class="flex gap-2 w-full sm:w-auto">
              <a href="tel:0891234567" class="flex-1 sm:flex-none bg-slate-100 text-slate-700 px-3 py-1.5 rounded-xl text-xs font-semibold flex items-center justify-center gap-1">
                <i data-lucide="phone" class="w-3.5 h-3.5 text-emerald-600"></i> โทร
              </a>
              <button onclick="openChatModal('พี่วัฒนา (Rider)', 'สอบถามตำแหน่งจัดส่ง/เข้ารับ')" class="flex-1 sm:flex-none bg-brand-blue text-white px-3 py-1.5 rounded-xl text-xs font-bold">
                แชตกับไรเดอร์
              </button>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- ================= VIEW 5: RETURN SCHEDULE ================= -->
    <section id="view-return-schedule" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 space-y-5">
      <button onclick="goBack()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 hover:text-brand-blue bg-white px-3 py-1.5 rounded-xl border border-slate-200 shadow-sm transition">
        <i data-lucide="arrow-left" class="w-4 h-4"></i> ย้อนกลับ
      </button>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
        <div class="lg:col-span-2 bg-white rounded-3xl p-5 sm:p-7 border border-slate-100 shadow-sm space-y-4">
          <div class="border-b border-slate-100 pb-3 flex justify-between items-center">
            <h2 class="text-base font-bold text-slate-900 flex items-center gap-2">
              <i data-lucide="calendar" class="w-4 h-4 text-amber-500"></i> ปฏิทินแสดงวันที่ต้องส่งคืนชุด
            </h2>
            <span class="text-xs font-bold text-amber-800 bg-amber-100 px-3 py-1 rounded-full">ต.ค. 2026</span>
          </div>

          <div class="border border-slate-200 rounded-2xl p-4 bg-white">
            <div class="grid grid-cols-7 gap-1 text-center font-bold text-slate-400 text-xs mb-2">
              <div>อา.</div><div>จ.</div><div>อ.</div><div>พ.</div><div>พฤ.</div><div>ศ.</div><div>ส.</div>
            </div>
            <div id="returnCalendarDaysGrid" class="grid grid-cols-7 gap-1 text-center text-xs"></div>
          </div>

          <div class="bg-amber-50 border border-amber-200 text-amber-900 p-3 rounded-2xl text-xs space-y-1">
            <p class="font-bold">⚠️ กำหนดส่งคืนชุด: 12 ต.ค. 2026 (ก่อน 20:00 น.)</p>
            <p class="text-[11px]">เมื่อทำการคืนชุดเรียบร้อย เงินมัดจำ Escrow จะถูกโอนคืนเข้าช่องทางบัญชีที่คุณเลือกไว้โดยอัตโนมัติค่ะ</p>
          </div>
        </div>

        <div class="bg-white rounded-3xl p-5 border border-slate-100 shadow-sm space-y-4 flex flex-col justify-between">
          <div class="space-y-3 text-xs">
            <h3 class="font-bold text-slate-900 text-sm border-b border-slate-100 pb-2">เรียกไรเดอร์เข้ารับชุดคืน</h3>
            <label class="block font-semibold text-slate-700">จุดนัดรับชุด:</label>
            <textarea id="returnPickupAddress" rows="2" class="w-full p-2.5 rounded-xl border border-slate-200 text-xs focus:border-brand-blue focus:outline-none">หอพักสดใส คอนโด ซอยสดใส บางแสน ชลบุรี (โทร 082-XXX-8921)</textarea>
          </div>
          <button onclick="handleConfirmCourierPickup()" class="w-full bg-brand-blue hover:bg-brand-blueDark text-white font-bold text-xs py-3 rounded-xl shadow transition flex items-center justify-center gap-1.5">
            <i data-lucide="check" class="w-4 h-4"></i> ยืนยันเรียกรถรับชุดคืน
          </button>
        </div>
      </div>
    </section>

    <!-- ================= VIEW 6: LENDER PROFILE ================= -->
    <section id="view-lender-profile" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 space-y-5">
      <button onclick="goBack()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 hover:text-brand-blue bg-white px-3 py-1.5 rounded-xl border border-slate-200 shadow-sm transition">
        <i data-lucide="arrow-left" class="w-4 h-4"></i> ย้อนกลับ
      </button>

      <div class="bg-white rounded-2xl sm:rounded-3xl p-5 sm:p-7 border border-slate-100 shadow-sm space-y-3">
        <div class="flex items-center gap-4">
          <div class="w-16 h-16 rounded-2xl bg-gradient-to-tr from-brand-pink to-brand-blue flex items-center justify-center text-white text-2xl shadow">🏪</div>
          <div>
            <h1 id="lpStoreName" class="text-xl font-bold text-slate-900">Studio Dress Up</h1>
            <p id="lpStoreLocation" class="text-xs text-slate-500">ชลบุรี • Hyperlocal Verified Vendor</p>
          </div>
        </div>
      </div>

      <div class="space-y-3">
        <h2 class="text-base font-bold text-slate-900 border-b border-slate-200 pb-2">เสื้อผ้าทั้งหมดของร้านนี้</h2>
        <div id="lenderAllGarmentsGrid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-3"></div>
      </div>
    </section>

    <!-- ================= VIEW 7: USER PROFILE & SETTINGS ================= -->
    <section id="view-profile" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 space-y-5">
      <button onclick="goBack()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 hover:text-brand-blue bg-white px-3 py-1.5 rounded-xl border border-slate-200 shadow-sm transition">
        <i data-lucide="arrow-left" class="w-4 h-4"></i> ย้อนกลับ
      </button>

      <div class="bg-white rounded-2xl sm:rounded-3xl p-5 sm:p-7 border border-slate-100 shadow-sm relative overflow-hidden">
        <div class="flex flex-col sm:flex-row items-center sm:items-start gap-4 text-center sm:text-left">
          <div class="w-20 h-20 rounded-full bg-gradient-to-tr from-brand-pink to-brand-blue p-1 shadow-md">
            <div class="w-full h-full bg-white rounded-full flex items-center justify-center text-slate-800 text-2xl font-serif font-black">S</div>
          </div>
          <div class="flex-1 space-y-1.5">
            <h1 class="text-xl sm:text-2xl font-bold text-slate-900" id="userDisplayName">Salinee Sanai</h1>
            <p class="text-xs text-slate-500" id="userDisplayPhone">เบอร์โทรศัพท์: 082-XXX-8921 • Verified User</p>
            
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 pt-2 text-center sm:text-left">
              <div class="bg-slate-50 p-2 rounded-xl border border-slate-100">
                <span class="text-[10px] text-slate-400 block">Styloan Coins</span>
                <span class="text-sm sm:text-base font-black text-amber-600">🪙 <span id="profileCoinsDisplay">420</span></span>
              </div>
              <div class="bg-slate-50 p-2 rounded-xl border border-slate-100">
                <span class="text-[10px] text-slate-400 block">อัตราคืนตรงเวลา</span>
                <span class="text-sm sm:text-base font-bold text-emerald-600">100%</span>
              </div>
              <div class="bg-slate-50 p-2 rounded-xl border border-slate-100">
                <span class="text-[10px] text-slate-400 block">คะแนนรีวิว</span>
                <span class="text-sm sm:text-base font-bold text-slate-800">⭐ 4.9</span>
              </div>
              <div class="bg-slate-50 p-2 rounded-xl border border-slate-100">
                <span class="text-[10px] text-slate-400 block">มัดจำ Escrow</span>
                <span class="text-sm sm:text-base font-bold text-brand-blue">฿1,000</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Settings Panel -->
      <div class="bg-white rounded-2xl sm:rounded-3xl p-5 sm:p-7 border border-slate-100 shadow-sm space-y-5">
        <div class="border-b border-slate-100 pb-3 flex items-center gap-2">
          <i data-lucide="settings" class="w-5 h-5 text-slate-700"></i>
          <h2 class="text-base font-bold text-slate-900">ตั้งค่าบัญชี & ข้อมูลการโอนคืน (Settings)</h2>
        </div>

        <form onsubmit="handleSaveUserSettings(event)" class="space-y-4 text-xs">
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
              <label class="block font-semibold text-slate-700 mb-1">ชื่อผู้ใช้งาน</label>
              <input type="text" id="settingUserName" value="Salinee Sanai" class="w-full px-3 py-2 rounded-xl border border-slate-200 focus:border-brand-blue focus:outline-none">
            </div>
            <div>
              <label class="block font-semibold text-slate-700 mb-1">เบอร์โทรศัพท์ติดต่อ</label>
              <input type="text" id="settingUserPhone" value="082-XXX-8921" class="w-full px-3 py-2 rounded-xl border border-slate-200 focus:border-brand-blue focus:outline-none">
            </div>
            <div class="sm:col-span-2">
              <label class="block font-semibold text-slate-700 mb-1">ที่อยู่จัดส่งเริ่มต้น</label>
              <input type="text" id="settingUserAddress" value="หอพักสดใส คอนโด ซอยสดใส บางแสน ชลบุรี 20131" class="w-full px-3 py-2 rounded-xl border border-slate-200 focus:border-brand-blue focus:outline-none">
            </div>
            <div class="sm:col-span-2">
              <label class="block font-semibold text-slate-700 mb-1">หมายเลขพร้อมเพย์ / บัญชีรับเงินมัดจำคืนเริ่มต้น</label>
              <input type="text" id="settingDefaultRefundAccount" value="082-XXX-8921 (พร้อมเพย์)" class="w-full px-3 py-2 rounded-xl border border-slate-200 focus:border-brand-blue focus:outline-none">
            </div>
          </div>

          <div class="pt-3 flex justify-end gap-2">
            <button type="submit" class="bg-brand-blue hover:bg-brand-blueDark text-white font-bold py-2 px-5 rounded-xl shadow transition">
              บันทึกการตั้งค่า
            </button>
          </div>
        </form>
      </div>
    </section>

  </main>

  <!-- ================= MODAL 1: BOOKING & DATE RANGE PICKER (พร้อมระบบ Buffer ก่อน-หลัง) ================= -->
  <div id="bookingModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-end sm:items-center justify-center p-0 sm:p-4 hidden">
    <div class="bg-white w-full max-w-xl rounded-t-3xl sm:rounded-3xl shadow-2xl overflow-hidden flex flex-col max-h-[92vh] sm:max-h-[90vh]">
      
      <div class="bg-slate-900 text-white p-4 flex items-center justify-between">
        <div class="flex items-center gap-2">
          <div class="w-8 h-8 rounded-lg bg-brand-blue flex items-center justify-center text-white text-xs">
            <i data-lucide="calendar" class="w-4 h-4"></i>
          </div>
          <div>
            <h3 id="modalDressTitle" class="font-bold text-xs sm:text-sm">Mira Satin Maxi Dress</h3>
            <p id="modalStoreNameSubtitle" class="text-[10px] text-slate-300">ร้าน Studio Dress Up</p>
          </div>
        </div>
        <button onclick="closeBookingModal()" class="text-slate-400 hover:text-white">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <div class="p-4 sm:p-5 overflow-y-auto space-y-4 no-scrollbar text-xs">
        <div class="bg-blue-50/70 border border-blue-200/80 p-3 rounded-2xl flex items-center justify-between text-xs">
          <div>
            <span class="font-bold text-brand-blue block">ปฏิทิน Buffer ก่อน-หลัง:</span>
            <span class="text-[11px] text-slate-600">เว้นระยะ 1 วันก่อนหน้า (เตรียม/ส่ง) และ 2 วันหลังเช่า (ซัก/อบ/รีด) ป้องกันวันชนกระชั้นชิด</span>
          </div>
          <button onclick="resetDateRangeSelection()" class="text-[11px] text-slate-500 hover:text-brand-pink underline shrink-0 ml-2">ล้างวัน</button>
        </div>

        <div class="border border-slate-200 rounded-2xl p-3 bg-white shadow-inner">
          <div class="grid grid-cols-7 gap-1 text-center font-bold text-slate-400 text-[10px] mb-1">
            <div>อา.</div><div>จ.</div><div>อ.</div><div>พ.</div><div>พฤ.</div><div>ศ.</div><div>ส.</div>
          </div>
          <div id="calendarDaysGrid" class="grid grid-cols-7 gap-1 text-center text-xs"></div>
        </div>

        <!-- Indicator Guide -->
        <div class="flex flex-wrap items-center justify-between gap-1 text-[10px] text-slate-500 px-1">
          <span class="flex items-center gap-1"><span class="w-2.5 h-2.5 rounded-full bg-brand-blue"></span> วันเช่าที่เลือก</span>
          <span class="flex items-center gap-1"><span class="w-2.5 h-2.5 rounded-full bg-amber-200"></span> Buffer (ก่อน/หลัง)</span>
          <span class="flex items-center gap-1"><span class="w-2.5 h-2.5 rounded-full bg-slate-200"></span> ติดจอง/ผ่านแล้ว</span>
        </div>

        <div id="selectedPeriodBox" class="p-3 rounded-xl bg-blue-50 border border-blue-200 hidden space-y-1">
          <div class="flex justify-between items-center font-bold text-brand-blue text-xs">
            <span><i data-lucide="check-circle" class="w-3.5 h-3.5 inline mr-1"></i> ช่วงเวลาเช่าที่คุณเลือก:</span>
            <span id="selectedDatesText">16 ต.ค. - 18 ต.ค. 2026 (3 วัน)</span>
          </div>
          <p class="text-[10px] text-slate-500">
            ระบบล็อกวันพัก <strong class="text-amber-700">Pre-Buffer (1 วันก่อนหน้า)</strong> และ <strong class="text-amber-700">Post-Buffer (2 วันหลังรอบเช่า)</strong> เพื่อซัก อบ รีด อย่างสมบูรณ์
          </p>
        </div>

        <!-- รูปแบบการรับชุด -->
        <div class="border-t border-slate-100 pt-3 space-y-2">
          <label class="block font-bold text-slate-800 text-xs">รูปแบบการรับชุด:</label>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
            <label class="p-2.5 rounded-xl border border-slate-200 cursor-pointer hover:border-brand-blue bg-white flex items-center justify-between">
              <div class="flex items-center gap-1.5">
                <input type="radio" name="deliveryOption" value="pickup" checked onchange="handleDeliveryChange(0, 'รับที่หน้าร้าน', false)" class="text-brand-blue">
                <span class="font-bold text-slate-800 text-xs">รับหน้าร้าน</span>
              </div>
              <span class="text-[10px] font-bold text-emerald-600 bg-emerald-50 px-1 rounded">ฟรี</span>
            </label>
            <label class="p-2.5 rounded-xl border border-slate-200 cursor-pointer hover:border-brand-blue bg-white flex items-center justify-between">
              <div class="flex items-center gap-1.5">
                <input type="radio" name="deliveryOption" value="rider" onchange="handleDeliveryChange(120, 'ส่งด่วน Rider Same-day', true)" class="text-brand-blue">
                <span class="font-bold text-slate-800 text-xs">ส่งด่วน Rider</span>
              </div>
              <span class="text-[10px] font-bold text-brand-blue">฿120</span>
            </label>
            <label class="p-2.5 rounded-xl border border-slate-200 cursor-pointer hover:border-brand-blue bg-white flex items-center justify-between">
              <div class="flex items-center gap-1.5">
                <input type="radio" name="deliveryOption" value="standard" onchange="handleDeliveryChange(50, 'ส่งปกติ 1-2 วัน', true)" class="text-brand-blue">
                <span class="font-bold text-slate-800 text-xs">ส่งปกติ</span>
              </div>
              <span class="text-[10px] font-bold text-slate-700">฿50</span>
            </label>
          </div>
        </div>

        <div id="addressSection" class="hidden border-t border-slate-100 pt-3 space-y-1">
          <label class="block font-bold text-slate-800 text-xs">ที่อยู่จัดส่งพัสดุ / นัดรับ Rider *</label>
          <textarea id="inputRecipientAddress" rows="2" class="w-full px-3 py-2 rounded-xl border border-slate-200 text-xs focus:border-brand-blue focus:outline-none">หอพักสดใส คอนโด ซอยสดใส บางแสน ชลบุรี 20131</textarea>
        </div>

        <!-- โค้ดส่วนลด -->
        <div class="border-t border-slate-100 pt-3 space-y-2">
          <label class="block font-bold text-slate-800 text-xs">
            <i data-lucide="ticket" class="w-3.5 h-3.5 inline mr-1 text-brand-pink"></i> โค้ดส่วนลดค่าเช่า / ค่าส่ง:
          </label>
          <div class="flex gap-2">
            <input type="text" id="inputPromoCode" placeholder="พิมพ์รหัสโค้ด เช่น STY50, FREESHIP" class="flex-1 px-3 py-2 rounded-xl border border-slate-200 text-xs uppercase focus:border-brand-blue focus:outline-none">
            <button type="button" onclick="applyPromoCodeManual()" class="bg-slate-800 hover:bg-black text-white px-3.5 py-2 rounded-xl font-bold transition">
              ใช้โค้ด
            </button>
            <button type="button" onclick="openCoinRewardsModal()" class="bg-brand-pinkLight text-brand-pink px-3 py-2 rounded-xl font-bold hover:bg-pink-100 transition whitespace-nowrap">
              เลือกโค้ดของฉัน
            </button>
          </div>
          <div id="promoCodeStatusMsg" class="text-[10px] hidden font-medium"></div>
        </div>

        <!-- เลือกช่องทางรับเงินมัดจำคืน -->
        <div class="border-t border-slate-100 pt-3 space-y-2">
          <label class="block font-bold text-slate-800 text-xs flex items-center justify-between">
            <span><i data-lucide="wallet" class="w-3.5 h-3.5 inline mr-1 text-emerald-600"></i> ช่องทางรับเงินมัดจำคืน (Escrow Refund Account):</span>
            <span class="text-[10px] text-emerald-600 font-normal">คืน 100% หลังตรวจรับชุด</span>
          </label>
          <div class="grid grid-cols-2 gap-2">
            <label class="p-2 rounded-xl border border-slate-200 flex items-center gap-2 cursor-pointer bg-white">
              <input type="radio" name="refundMethod" value="promptpay" checked class="text-brand-blue">
              <span class="font-bold text-slate-700">พร้อมเพย์ (PromptPay)</span>
            </label>
            <label class="p-2 rounded-xl border border-slate-200 flex items-center gap-2 cursor-pointer bg-white">
              <input type="radio" name="refundMethod" value="bank" class="text-brand-blue">
              <span class="font-bold text-slate-700">โอนเข้าบัญชีธนาคาร</span>
            </label>
          </div>
          <input type="text" id="refundAccountInfo" placeholder="ระบุเบอร์พร้อมเพย์ หรือเลขที่บัญชี และชื่อธนาคาร" value="082-XXX-8921 (พร้อมเพย์)" class="w-full px-3 py-2 rounded-xl border border-slate-200 text-xs focus:border-brand-blue focus:outline-none">
        </div>

        <!-- Escrow Checkout Summary -->
        <div class="border-t border-slate-100 pt-3 space-y-1 text-slate-600 text-xs">
          <div class="flex justify-between">
            <span>ค่าเช่าชุด (<span id="calcDaysCountText">1</span> วัน)</span>
            <span id="summaryRentPrice" class="font-medium text-slate-800">฿250</span>
          </div>
          <div class="flex justify-between">
            <span>เงินมัดจำประกันชุด (ได้คืน 100%)</span>
            <span id="summaryDeposit" class="font-medium text-amber-700">฿1,000</span>
          </div>
          <div class="flex justify-between">
            <span>ค่าจัดส่ง (<span id="deliveryLabelText">รับที่หน้าร้าน</span>)</span>
            <span id="summaryShippingPrice" class="font-bold text-emerald-600">฿0 (ฟรี)</span>
          </div>
          <div class="flex justify-between items-center py-0.5 text-brand-pink font-semibold">
            <span id="appliedCouponText">ส่วนลดโค้ดโปรโมชัน:</span>
            <span id="appliedCouponAmount">-฿0</span>
          </div>
          <div class="border-t border-slate-200 pt-2 flex justify-between items-center font-bold text-slate-900 text-sm">
            <span>ยอดชำระสุทธิ (พักใน Escrow)</span>
            <span id="finalCheckoutTotal" class="text-base text-brand-blue">฿1,250</span>
          </div>
        </div>
      </div>

      <div class="bg-slate-50 p-4 border-t border-slate-100 flex items-center justify-between">
        <span class="text-[10px] text-slate-500">มัดจำพักใน Escrow ปลอดภัย 100%</span>
        <button onclick="openPaymentGatewayModal()" id="confirmBookBtn" disabled class="bg-brand-blue hover:bg-brand-blueDark disabled:bg-slate-300 disabled:cursor-not-allowed text-white font-bold text-xs px-5 py-2.5 rounded-xl shadow transition">
          ไปหน้าเลือกวิธีชำระเงิน ➔
        </button>
      </div>

    </div>
  </div>

  <!-- ================= MODAL 2: ORDER RIDER RETURN PICKUP (เรียกไรเดอร์รับชุดคืนจากหน้ารายการเช่า) ================= -->
  <div id="orderReturnPickupModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
    <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl overflow-hidden p-5 sm:p-6 space-y-4 text-xs animate-in zoom-in-95 duration-200">
      <div class="flex justify-between items-center border-b border-slate-100 pb-3">
        <div class="flex items-center gap-2">
          <div class="w-8 h-8 rounded-full bg-emerald-100 text-emerald-600 flex items-center justify-center">
            <i data-lucide="bike" class="w-4 h-4"></i>
          </div>
          <div>
            <h3 class="font-bold text-sm text-slate-900">เรียก Rider เข้ารับชุดคืน</h3>
            <p id="returnPickupOrderSubtitle" class="text-[10px] text-slate-400">ออเดอร์ #STY2610-0982</p>
          </div>
        </div>
        <button onclick="closeOrderReturnPickupModal()"><i data-lucide="x" class="w-5 h-5 text-slate-400"></i></button>
      </div>

      <div class="space-y-3">
        <div>
          <label class="block font-semibold text-slate-700 mb-1">จุดนัดรับชุดของไรเดอร์ *</label>
          <textarea id="orderReturnAddressInput" rows="2" class="w-full p-2.5 rounded-xl border border-slate-200 text-xs focus:border-brand-blue focus:outline-none">หอพักสดใส คอนโด ซอยสดใส บางแสน ชลบุรี (โทร 082-XXX-8921)</textarea>
        </div>

        <div>
          <label class="block font-semibold text-slate-700 mb-1">เวลานัดรับที่สะดวก *</label>
          <select id="orderReturnTimeSelect" class="w-full p-2.5 rounded-xl border border-slate-200 text-xs focus:border-brand-blue focus:outline-none">
            <option value="asap">ด่วนที่สุด (ไรเดอร์เข้ารับภายใน 30-45 นาที)</option>
            <option value="12:00">วันนี้ 12:00 - 13:00 น.</option>
            <option value="17:00">วันนี้ 17:00 - 18:00 น.</option>
            <option value="19:00">วันนี้ 19:00 - 20:00 น.</option>
          </select>
        </div>

        <!-- Condition Proof Outgoing Upload (FR-16) -->
        <div class="p-3 rounded-2xl bg-slate-50 border border-slate-200 space-y-1.5">
          <div class="flex justify-between items-center">
            <span class="font-bold text-slate-700"><i data-lucide="camera" class="w-3.5 h-3.5 inline mr-1 text-brand-blue"></i> ภาพถ่ายสภาพชุดก่อนส่งมอบ (Condition Proof)</span>
            <span class="text-[10px] text-brand-blue font-semibold">แนะนำ</span>
          </div>
          <p class="text-[10px] text-slate-400">ถ่ายรูปสภาพชุดและบรรจุลงถุงผ้า Styloan เพื่อเป็นหลักฐานการคืนเงินมัดจำ 100%</p>
          <input type="file" id="returnProofPhotoInput" class="w-full text-[11px] text-slate-500 file:mr-2 file:py-1 file:px-2.5 file:rounded-lg file:border-0 file:text-[10px] file:font-semibold file:bg-brand-blueLight file:text-brand-blue">
        </div>
      </div>

      <div class="pt-2 flex gap-2">
        <button onclick="confirmOrderRiderPickup()" class="flex-1 bg-emerald-500 hover:bg-emerald-600 text-white font-bold py-2.5 rounded-xl shadow transition flex items-center justify-center gap-1.5">
          <i data-lucide="check" class="w-4 h-4"></i> ยืนยันเรียกรถรับชุด
        </button>
        <button onclick="closeOrderReturnPickupModal()" class="px-4 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold py-2.5 rounded-xl transition">
          ยกเลิก
        </button>
      </div>
    </div>
  </div>

  <!-- ================= MODAL 3: PAYMENT METHOD SELECTION ================= -->
  <div id="paymentModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
    <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl overflow-hidden p-5 sm:p-6 space-y-4 text-xs">
      
      <div class="flex justify-between items-center border-b border-slate-100 pb-3">
        <div>
          <h3 class="font-bold text-sm text-slate-900">เลือกวิธีการชำระเงิน</h3>
          <p class="text-[10px] text-slate-400">คุ้มครองด้วยระบบพักเงิน Escrow 100%</p>
        </div>
        <button onclick="closePaymentModal()"><i data-lucide="x" class="w-5 h-5 text-slate-400"></i></button>
      </div>

      <div class="bg-blue-50/70 p-3 rounded-2xl border border-blue-100 flex justify-between items-center">
        <span class="text-slate-600">ยอดรวมที่ต้องชำระ (ค่าเช่า + มัดจำ):</span>
        <span id="paymentTotalDisplay" class="text-xl font-black text-brand-blue">฿1,250</span>
      </div>

      <!-- Payment Method Radio List -->
      <div class="space-y-2">
        <label class="p-3 rounded-2xl border border-brand-blue bg-blue-50/30 flex items-center justify-between cursor-pointer">
          <div class="flex items-center gap-2.5">
            <input type="radio" name="payMethod" value="promptpay" checked class="text-brand-blue">
            <div>
              <span class="font-bold text-slate-800 block">Thai QR PromptPay</span>
              <span class="text-[10px] text-slate-400">สแกนจ่ายผ่าน Mobile Banking ทุกธนาคาร</span>
            </div>
          </div>
          <span class="text-xs">📱</span>
        </label>

        <label class="p-3 rounded-2xl border border-slate-200 hover:border-slate-300 flex items-center justify-between cursor-pointer">
          <div class="flex items-center gap-2.5">
            <input type="radio" name="payMethod" value="card" class="text-brand-blue">
            <div>
              <span class="font-bold text-slate-800 block">บัตรเครดิต / เดบิต (Visa, Mastercard)</span>
              <span class="text-[10px] text-slate-400">ปลอดภัยมาตรฐาน PCI-DSS</span>
            </div>
          </div>
          <span class="text-xs">💳</span>
        </label>

        <label class="p-3 rounded-2xl border border-slate-200 hover:border-slate-300 flex items-center justify-between cursor-pointer">
          <div class="flex items-center gap-2.5">
            <input type="radio" name="payMethod" value="mobile" class="text-brand-blue">
            <div>
              <span class="font-bold text-slate-800 block">Mobile Banking (K PLUS / SCB EASY)</span>
              <span class="text-[10px] text-slate-400">ตัดบัญชีอัตโนมัติ</span>
            </div>
          </div>
          <span class="text-xs">🏦</span>
        </label>

        <label class="p-3 rounded-2xl border border-slate-200 hover:border-slate-300 flex items-center justify-between cursor-pointer">
          <div class="flex items-center gap-2.5">
            <input type="radio" name="payMethod" value="truemoney" class="text-brand-blue">
            <div>
              <span class="font-bold text-slate-800 block">TrueMoney Wallet</span>
              <span class="text-[10px] text-slate-400">ชำระผ่านกระเป๋าเงินวอลเล็ท</span>
            </div>
          </div>
          <span class="text-xs">👛</span>
        </label>
      </div>

      <button onclick="simulateSuccessfulPayment()" class="w-full bg-emerald-500 hover:bg-emerald-600 text-white font-bold py-3 rounded-2xl shadow transition text-xs flex items-center justify-center gap-1.5">
        <i data-lucide="check-circle" class="w-4 h-4"></i> ยืนยันการชำระเงินเข้าสู่ระบบ Escrow
      </button>

    </div>
  </div>

  <!-- ================= MODAL 4: SEARCH ADVANCED MENU DRAWER ================= -->
  <div id="searchMenuModal" class="fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-sm flex justify-start hidden">
    <div class="bg-white w-full max-w-xs h-full shadow-2xl flex flex-col p-5 space-y-4 animate-in slide-in-from-left duration-200 text-xs">
      <div class="flex justify-between items-center border-b border-slate-100 pb-3">
        <h3 class="font-bold text-sm text-slate-900 flex items-center gap-1.5">
          <i data-lucide="sliders-horizontal" class="w-4 h-4 text-brand-blue"></i> ตัวกรอง & เมนูค้นหา
        </h3>
        <button onclick="toggleSearchMenuModal()"><i data-lucide="x" class="w-5 h-5 text-slate-400"></i></button>
      </div>

      <div class="space-y-3.5 flex-1 overflow-y-auto no-scrollbar">
        <div>
          <label class="font-bold text-slate-700 block mb-1">หมวดหมู่สไตล์</label>
          <select id="filterCategorySelect" class="w-full p-2.5 rounded-xl border border-slate-200">
            <option value="all">ทั้งหมด (All Styles)</option>
            <option value="Cosplay">Cosplay (คอสเพลย์)</option>
            <option value="Party">Party (ปาร์ตี้/ออกงาน)</option>
            <option value="Dinner">Dinner (ดินเนอร์/สูท)</option>
            <option value="Wedding">Wedding (งานแต่งงาน)</option>
            <option value="Y2K">Y2K (สตรีท/วินเทจ)</option>
            <option value="Cafe">Cafe (คาเฟ่ฮอปปิ้ง)</option>
          </select>
        </div>

        <div>
          <label class="font-bold text-slate-700 block mb-1.5">โทนสีชุด (Color Palette)</label>
          <div class="grid grid-cols-4 gap-1.5 text-center text-[10px]" id="colorFilterContainer">
            <button type="button" onclick="selectColorFilter('all')" class="color-btn p-1.5 rounded-xl border border-brand-blue bg-blue-50 text-brand-blue font-bold">ทั้งหมด</button>
            <button type="button" onclick="selectColorFilter('ชมพู')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-brand-pink">ชมพู</button>
            <button type="button" onclick="selectColorFilter('ฟ้า')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-brand-blue">ฟ้า</button>
            <button type="button" onclick="selectColorFilter('ขาว')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-slate-400">ขาว</button>
            <button type="button" onclick="selectColorFilter('ดำ')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-slate-800">ดำ</button>
            <button type="button" onclick="selectColorFilter('ทอง/ครีม')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-amber-400">ทอง/ครีม</button>
            <button type="button" onclick="selectColorFilter('เขียว')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-emerald-500">เขียว</button>
            <button type="button" onclick="selectColorFilter('ม่วง')" class="color-btn p-1.5 rounded-xl border border-slate-200 hover:border-purple-400">ม่วง</button>
          </div>
        </div>

        <div>
          <label class="font-bold text-slate-700 block mb-1">ช่วงราคาค่าเช่าต่อวัน</label>
          <div class="flex gap-2 items-center">
            <input type="number" id="filterMinPrice" placeholder="ต่ำสุด (฿)" class="w-full p-2 rounded-xl border border-slate-200">
            <span>-</span>
            <input type="number" id="filterMaxPrice" placeholder="สูงสุด (฿)" class="w-full p-2 rounded-xl border border-slate-200">
          </div>
        </div>
      </div>

      <div class="pt-2 border-t border-slate-100 flex gap-2">
        <button onclick="applySearchFilters()" class="flex-1 bg-brand-blue text-white py-2.5 rounded-xl font-bold">ใช้ตัวกรอง</button>
        <button onclick="resetSearchFilters()" class="px-3 bg-slate-100 text-slate-600 py-2.5 rounded-xl font-medium">รีเซ็ต</button>
      </div>
    </div>
  </div>

  <!-- ================= MODAL 5: IMAGE VISUAL SEARCH ================= -->
  <div id="imageSearchModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
    <div class="bg-white w-full max-w-sm rounded-3xl shadow-2xl p-5 space-y-4 text-xs text-center">
      <div class="flex justify-between items-center border-b border-slate-100 pb-2">
        <h3 class="font-bold text-sm text-slate-900 flex items-center gap-1.5">
          <i data-lucide="camera" class="w-4 h-4 text-brand-pink"></i> ค้นหาชุดจากรูปภาพ
        </h3>
        <button onclick="closeImageSearchModal()"><i data-lucide="x" class="w-5 h-5 text-slate-400"></i></button>
      </div>

      <div class="border-2 border-dashed border-slate-200 p-6 rounded-2xl hover:border-brand-blue transition cursor-pointer" onclick="document.getElementById('imgUploadInput').click()">
        <i data-lucide="upload-cloud" class="w-8 h-8 mx-auto text-brand-blue mb-2"></i>
        <p class="font-bold text-slate-700">อัปโหลดรูปภาพชุดที่คุณต้องการ</p>
        <p class="text-[10px] text-slate-400 mt-1">รองรับไฟล์ JPG, PNG หรือภาพแคปจากโซเชียล</p>
        <input type="file" id="imgUploadInput" accept="image/*" class="hidden" onchange="handleImageUploaded(event)">
      </div>

      <div class="text-[10px] text-slate-400">ระบบจะวิเคราะห์รูปทรงและโทนสีเพื่อค้นหาชุดที่ใกล้เคียงที่สุดค่ะ</div>
    </div>
  </div>

  <!-- ================= MODAL 6: COINS & VOUCHERS ================= -->
  <div id="coinRewardsModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
    <div class="bg-white w-full max-w-md rounded-3xl shadow-2xl overflow-hidden flex flex-col max-h-[85vh]">
      <div class="p-4 border-b border-slate-100 flex items-center justify-between">
        <h3 class="font-bold text-sm text-slate-900">🪙 Styloan Coins & Vouchers</h3>
        <button onclick="closeCoinRewardsModal()" class="text-slate-400 hover:text-black"><i data-lucide="x" class="w-5 h-5"></i></button>
      </div>

      <div class="p-3 bg-amber-50 flex items-center justify-between text-xs">
        <span class="text-amber-900 font-medium">ยอดคอยน์สะสม:</span>
        <span class="font-black text-amber-600">🪙 <span id="rewardModalCoinCount">420</span> Coins</span>
      </div>

      <div class="flex border-b border-slate-200 text-xs font-bold">
        <button onclick="switchVoucherTab('redeem')" id="tabRedeemBtn" class="flex-1 py-3 border-b-2 border-brand-blue text-brand-blue">แลกโค้ด</button>
        <button onclick="switchVoucherTab('my')" id="tabMyVouchersBtn" class="flex-1 py-3 border-b-2 border-transparent text-slate-500">โค้ดของฉัน (<span id="myVouchersCountBadge">1</span>)</button>
      </div>

      <div class="p-4 overflow-y-auto space-y-2.5 no-scrollbar text-xs flex-1">
        <div id="tabRedeemContent" class="space-y-2">
          <div class="p-3 rounded-2xl border border-slate-200 flex items-center justify-between">
            <div>
              <span class="font-bold text-slate-800 block">โค้ดส่งฟรี Rider (ลด ฿60)</span>
              <span class="text-[10px] text-slate-400">ใช้ได้กับทุกออเดอร์</span>
            </div>
            <button onclick="redeemCoupon('FREE_SHIP', 50, 'โค้ดส่งฟรี Rider (ลด ฿60)', 60, 'FREESHIP')" class="bg-brand-pink text-white font-bold text-[11px] px-3 py-1.5 rounded-xl">แลก 50 Coins</button>
          </div>
          <div class="p-3 rounded-2xl border border-slate-200 flex items-center justify-between">
            <div>
              <span class="font-bold text-slate-800 block">โค้ดส่วนลดค่าเช่า ฿100</span>
              <span class="text-[10px] text-slate-400">ลดทันทีจากยอดค่าเช่า</span>
            </div>
            <button onclick="redeemCoupon('DISCOUNT_100', 100, 'โค้ดลดค่าเช่า ฿100', 100, 'STY100')" class="bg-brand-blue text-white font-bold text-[11px] px-3 py-1.5 rounded-xl">แลก 100 Coins</button>
          </div>
        </div>
        <div id="tabMyVouchersContent" class="hidden space-y-2">
          <div id="myVouchersListContainer" class="space-y-2"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- ================= MODAL 7: NOTIFICATIONS PANEL ================= -->
  <div id="notificationsModal" class="fixed inset-0 z-50 bg-slate-900/40 backdrop-blur-sm flex justify-end hidden">
    <div class="bg-white w-full max-w-sm h-full shadow-2xl flex flex-col animate-in slide-in-from-right duration-200">
      <div class="p-4 border-b border-slate-100 flex items-center justify-between">
        <div class="flex items-center gap-2">
          <div class="w-2 h-2 rounded-full bg-brand-blue"></div>
          <h3 class="font-bold text-sm text-slate-800">การแจ้งเตือน</h3>
        </div>
        <button onclick="toggleNotificationsModal()" class="text-slate-400 hover:text-black"><i data-lucide="x" class="w-5 h-5"></i></button>
      </div>

      <div class="flex-1 overflow-y-auto p-4 space-y-2.5 no-scrollbar text-xs">
        <div class="p-3 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
          <div class="flex justify-between items-center text-slate-800 font-semibold">
            <span class="flex items-center gap-1.5"><i data-lucide="bike" class="w-3.5 h-3.5 text-brand-blue"></i> ไรเดอร์กำลังไปรับชุด</span>
            <span class="text-[10px] text-slate-400 font-normal">เรียลไทม์</span>
          </div>
          <p class="text-slate-500 text-[11px]">พี่วัฒนา (Rider) กำลังมุ่งหน้าไปรับชุดจากร้านเพื่อจัดส่งให้คุณค่ะ</p>
        </div>

        <div class="p-3 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
          <div class="flex justify-between items-center text-slate-800 font-semibold">
            <span class="flex items-center gap-1.5"><i data-lucide="clock" class="w-3.5 h-3.5 text-amber-500"></i> เตือนวันคืนชุด</span>
            <span class="text-[10px] text-slate-400 font-normal">วันนี้</span>
          </div>
          <p class="text-slate-500 text-[11px]">กำหนดส่งคืน 12 ต.ค. สามารถกดเรียกรถรับชุดคืนได้เลยค่ะ</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Mobile Bottom Nav -->
  <div class="md:hidden fixed bottom-0 left-0 right-0 z-40 bg-white border-t border-slate-200 flex items-center justify-around py-2 px-1 text-[10px] text-slate-500 shadow-lg">
    <button onclick="navigateTo('home')" class="flex flex-col items-center gap-0.5 text-brand-blue font-bold">
      <i data-lucide="home" class="w-4 h-4"></i><span>หน้าแรก</span>
    </button>
    <button onclick="navigateTo('wishlist')" class="flex flex-col items-center gap-0.5 hover:text-brand-blue">
      <i data-lucide="heart" class="w-4 h-4 text-brand-pink"></i><span>ถูกใจ</span>
    </button>
    <button onclick="navigateTo('bookings')" class="flex flex-col items-center gap-0.5 hover:text-brand-blue">
      <i data-lucide="calendar-check" class="w-4 h-4"></i><span>ออเดอร์</span>
    </button>
    <button onclick="navigateTo('return-schedule')" class="flex flex-col items-center gap-0.5 hover:text-brand-blue">
      <i data-lucide="truck" class="w-4 h-4 text-amber-500"></i><span>คืนชุด</span>
    </button>
    <button onclick="navigateTo('profile')" class="flex flex-col items-center gap-0.5 hover:text-brand-blue">
      <i data-lucide="user" class="w-4 h-4"></i><span>โปรไฟล์</span>
    </button>
  </div>

  <!-- ================= SCRIPT & DATABASE (30 ITEMS WITH PRE/POST BUFFER) ================= -->
  <script>
    // 30 Garments Database
    const garmentsData = [
      { id: 'STY-G01', title: 'Mira Satin Maxi Dress', brand: 'Mitr', category: 'Party', color: 'ชมพู', rentPricePerDay: 250, deposit: 1000, image: 'https://images.unsplash.com/photo-1595777457583-95e059d581b8?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: '36"', length: '48"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี (ซอยสดใส)', storeRating: 4.9, reviews: [{ author: 'Selena K.', rating: 5, date: '2 วันก่อน', comment: 'ชุดตรงปก สวยมากค่ะ' }] },
      { id: 'STY-G02', title: 'Ethereal Tulle Lilac Gown', brand: 'Pastel Wardrobe', category: 'Wedding', color: 'ม่วง', rentPricePerDay: 350, deposit: 1500, image: 'https://images.unsplash.com/photo-1566174053879-31528523f8ae?w=600&auto=format&fit=crop&q=80', chest: '33-35"', waist: '26-28"', hips: 'ฟรีไซส์', length: '52"', storeName: 'Pastel Wardrobe', storeAddress: 'พัทยาเหนือ', storeRating: 4.8, reviews: [{ author: 'Mild S.', rating: 5, date: '3 วันก่อน', comment: 'ฟีลเจ้าหญิงสุดๆ' }] },
      { id: 'STY-G03', title: 'Genshin Electro Archon Kimono', brand: 'Cosplay Studio', category: 'Cosplay', color: 'ม่วง', rentPricePerDay: 280, deposit: 1200, image: 'https://images.unsplash.com/photo-1578632767115-351597cf2477?w=600&auto=format&fit=crop&q=80', chest: '32-35"', waist: '25-28"', hips: '38"', length: '50"', storeName: 'Aniverse Cosplay', storeAddress: 'บางแสน ชลบุรี', storeRating: 5.0, reviews: [] },
      { id: 'STY-G04', title: 'Cyberpunk Neon Maid Costume', brand: 'Anime Vibe', category: 'Cosplay', color: 'ดำ', rentPricePerDay: 220, deposit: 900, image: 'https://images.unsplash.com/photo-1534447677768-be436bb09401?w=600&auto=format&fit=crop&q=80', chest: '31-34"', waist: '24-27"', hips: '36"', length: '35"', storeName: 'Aniverse Cosplay', storeAddress: 'บางแสน ชลบุรี', storeRating: 5.0, reviews: [] },
      { id: 'STY-G05', title: 'Japanese Seifuku High School Set', brand: 'Harajuku Wardrobe', category: 'Cosplay', color: 'ฟ้า', rentPricePerDay: 160, deposit: 600, image: 'https://images.unsplash.com/photo-1520006403909-838d6b92c22e?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: 'ฟรีไซส์', length: '40"', storeName: 'Aniverse Cosplay', storeAddress: 'บางแสน ชลบุรี', storeRating: 5.0, reviews: [] },
      { id: 'STY-G06', title: 'Cyber Metallic Set', brand: 'Street Vibe', category: 'Y2K', color: 'ฟ้า', rentPricePerDay: 180, deposit: 800, image: 'https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?w=600&auto=format&fit=crop&q=80', chest: '30-34"', waist: '24-28"', hips: '37"', length: '40"', storeName: 'คุณฟ้า (Lender)', storeAddress: 'บางแสน', storeRating: 5.0, reviews: [] },
      { id: 'STY-G07', title: 'Structured Blazer Suit', brand: 'The Suit Lounge', category: 'Dinner', color: 'ดำ', rentPricePerDay: 290, deposit: 1200, image: 'https://images.unsplash.com/photo-1539109136881-3be0616acf4b?w=600&auto=format&fit=crop&q=80', chest: '36-38"', waist: '28-30"', hips: '38"', length: '29"', storeName: 'The Suit Lounge', storeAddress: 'เซ็นทรัล ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G08', title: 'Cottagecore Midi Dress', brand: 'Vintage Romance', category: 'Cafe', color: 'ทอง/ครีม', rentPricePerDay: 150, deposit: 600, image: 'https://images.unsplash.com/photo-1550639525-c97d455acf70?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: 'ฟรีไซส์', length: '42"', storeName: 'คุณริน (Lender)', storeAddress: 'ศรีราชา', storeRating: 4.7, reviews: [] },
      { id: 'STY-G09', title: 'Sequin Mini Cocktail', brand: 'Glitz & Glam', category: 'Party', color: 'ทอง/ครีม', rentPricePerDay: 220, deposit: 1000, image: 'https://images.unsplash.com/photo-1572804013309-59a88b7e92f1?w=600&auto=format&fit=crop&q=80', chest: '32-35"', waist: '26-28"', hips: '37"', length: '33"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G10', title: 'Emerald Velvet Slip Dress', brand: 'Silk & Chic', category: 'Dinner', color: 'เขียว', rentPricePerDay: 280, deposit: 1100, image: 'https://images.unsplash.com/photo-1518895949257-7621c3c786d7?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '26-28"', hips: '36"', length: '46"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G11', title: 'Chiffon Off-Shoulder Gown', brand: 'Pastel Wardrobe', category: 'Wedding', color: 'ขาว', rentPricePerDay: 390, deposit: 1500, image: 'https://images.unsplash.com/photo-1502716119720-b23a93e5fe1b?w=600&auto=format&fit=crop&q=80', chest: '33-35"', waist: '25-27"', hips: 'ฟรีไซส์', length: '54"', storeName: 'Pastel Wardrobe', storeAddress: 'พัทยาเหนือ', storeRating: 4.8, reviews: [] },
      { id: 'STY-G12', title: 'Neon Crop & Low-Rise Skirt', brand: 'Y2K Club', category: 'Y2K', color: 'ชมพู', rentPricePerDay: 190, deposit: 750, image: 'https://images.unsplash.com/photo-1509631179647-0177331693ae?w=600&auto=format&fit=crop&q=80', chest: '30-33"', waist: '24-26"', hips: '35"', length: '36"', storeName: 'คุณฟ้า (Lender)', storeAddress: 'บางแสน', storeRating: 5.0, reviews: [] },
      { id: 'STY-G13', title: 'French Puff Sleeve Dress', brand: 'Maison Cafe', category: 'Cafe', color: 'ขาว', rentPricePerDay: 170, deposit: 700, image: 'https://images.unsplash.com/photo-1496747611176-843222e1e57c?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '26-28"', hips: '37"', length: '41"', storeName: 'คุณริน (Lender)', storeAddress: 'ศรีราชา', storeRating: 4.7, reviews: [] },
      { id: 'STY-G14', title: 'Champagne Glitter Gown', brand: 'Luxe Rental', category: 'Party', color: 'ทอง/ครีม', rentPricePerDay: 320, deposit: 1300, image: 'https://images.unsplash.com/photo-1490481651871-ab68de25d43d?w=600&auto=format&fit=crop&q=80', chest: '33-35"', waist: '26-28"', hips: '37"', length: '50"', storeName: 'The Suit Lounge', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G15', title: 'Classic Double-Breasted Suit', brand: 'The Suit Lounge', category: 'Dinner', color: 'ดำ', rentPricePerDay: 310, deposit: 1250, image: 'https://images.unsplash.com/photo-1507679799987-c73779587ccf?w=600&auto=format&fit=crop&q=80', chest: '38-40"', waist: '30-32"', hips: '39"', length: '30"', storeName: 'The Suit Lounge', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G16', title: 'Floral Corset Fairy Dress', brand: 'Pastel Wardrobe', category: 'Wedding', color: 'ชมพู', rentPricePerDay: 340, deposit: 1400, image: 'https://images.unsplash.com/photo-1485230895905-ec40ba36b9bc?w=600&auto=format&fit=crop&q=80', chest: '31-33"', waist: '24-26"', hips: 'ฟรีไซส์', length: '47"', storeName: 'Pastel Wardrobe', storeAddress: 'พัทยาเหนือ', storeRating: 4.8, reviews: [] },
      { id: 'STY-G17', title: 'Denim Halter Patchwork Set', brand: 'Retro Wave', category: 'Y2K', color: 'ฟ้า', rentPricePerDay: 180, deposit: 800, image: 'https://images.unsplash.com/photo-1529139574466-a303027c1d8b?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: '36"', length: '38"', storeName: 'คุณฟ้า (Lender)', storeAddress: 'บางแสน', storeRating: 5.0, reviews: [] },
      { id: 'STY-G18', title: 'Linen Brunch Two-Piece', brand: 'Cafe Vibe', category: 'Cafe', color: 'ขาว', rentPricePerDay: 160, deposit: 650, image: 'https://images.unsplash.com/photo-1515372039744-b8f02a3ae446?w=600&auto=format&fit=crop&q=80', chest: '33-35"', waist: '26-28"', hips: '38"', length: '40"', storeName: 'คุณริน (Lender)', storeAddress: 'ศรีราชา', storeRating: 4.7, reviews: [] },
      { id: 'STY-G19', title: 'Burgundy Bodycon Mini', brand: 'Mitr', category: 'Party', color: 'ชมพู', rentPricePerDay: 230, deposit: 950, image: 'https://images.unsplash.com/photo-1544441893-675973e31985?w=600&auto=format&fit=crop&q=80', chest: '31-34"', waist: '24-27"', hips: '35"', length: '34"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G20', title: 'Minimalist Silk Slip Gown', brand: 'Pure Silk', category: 'Dinner', color: 'ดำ', rentPricePerDay: 270, deposit: 1100, image: 'https://images.unsplash.com/photo-1469334031218-e382a71b716b?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: '36"', length: '49"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G21', title: 'Lavender Tiered Princess Dress', brand: 'Pastel Wardrobe', category: 'Wedding', color: 'ม่วง', rentPricePerDay: 380, deposit: 1500, image: 'https://images.unsplash.com/photo-1509551388413-e18d0ac5d495?w=600&auto=format&fit=crop&q=80', chest: '32-35"', waist: '25-28"', hips: 'ฟรีไซส์', length: '53"', storeName: 'Pastel Wardrobe', storeAddress: 'พัทยาเหนือ', storeRating: 4.8, reviews: [] },
      { id: 'STY-G22', title: 'Silver Hologram Cargo Set', brand: 'Cyber Chic', category: 'Y2K', color: 'ฟ้า', rentPricePerDay: 200, deposit: 850, image: 'https://images.unsplash.com/photo-1512436991641-6745cdb1723f?w=600&auto=format&fit=crop&q=80', chest: '32-36"', waist: '25-28"', hips: '38"', length: '41"', storeName: 'คุณฟ้า (Lender)', storeAddress: 'บางแสน', storeRating: 5.0, reviews: [] },
      { id: 'STY-G23', title: 'White Eyelet Lace Midi', brand: 'Vintage Romance', category: 'Cafe', color: 'ขาว', rentPricePerDay: 180, deposit: 700, image: 'https://images.unsplash.com/photo-1487222477894-8943e31ef7b2?w=600&auto=format&fit=crop&q=80', chest: '33-35"', waist: '26-28"', hips: '37"', length: '43"', storeName: 'คุณริน (Lender)', storeAddress: 'ศรีราชา', storeRating: 4.7, reviews: [] },
      { id: 'STY-G24', title: 'Golden Glam Backless Dress', brand: 'Luxe Rental', category: 'Party', color: 'ทอง/ครีม', rentPricePerDay: 300, deposit: 1200, image: 'https://images.unsplash.com/photo-1534126511673-b6899657816a?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: '36"', length: '45"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G25', title: 'Midnight Navy Tuxedo Suit', brand: 'The Suit Lounge', category: 'Dinner', color: 'ฟ้า', rentPricePerDay: 330, deposit: 1300, image: 'https://images.unsplash.com/photo-1508427953056-b00b8d78ebf5?w=600&auto=format&fit=crop&q=80', chest: '38-40"', waist: '30-32"', hips: '39"', length: '31"', storeName: 'The Suit Lounge', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G26', title: 'Rose Gold Sequin Ballgown', brand: 'Pastel Wardrobe', category: 'Wedding', color: 'ชมพู', rentPricePerDay: 420, deposit: 1700, image: 'https://images.unsplash.com/photo-1518049362265-d5b2a6467637?w=600&auto=format&fit=crop&q=80', chest: '33-35"', waist: '26-28"', hips: 'ฟรีไซส์', length: '55"', storeName: 'Pastel Wardrobe', storeAddress: 'พัทยาเหนือ', storeRating: 4.8, reviews: [] },
      { id: 'STY-G27', title: 'Hot Pink Feather Cocktail', brand: 'Glitz & Glam', category: 'Party', color: 'ชมพู', rentPricePerDay: 260, deposit: 1050, image: 'https://images.unsplash.com/photo-1523381294911-8d3cead13475?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: '36"', length: '33"', storeName: 'Studio Dress Up', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G28', title: 'Charcoal Pinstripe Tailored Suit', brand: 'The Suit Lounge', category: 'Dinner', color: 'ดำ', rentPricePerDay: 290, deposit: 1200, image: 'https://images.unsplash.com/photo-1492447273231-0f8fecec1e3a?w=600&auto=format&fit=crop&q=80', chest: '37-39"', waist: '29-31"', hips: '38"', length: '29"', storeName: 'The Suit Lounge', storeAddress: 'ชลบุรี', storeRating: 4.9, reviews: [] },
      { id: 'STY-G29', title: 'Peach Satin Mermaid Dress', brand: 'Pastel Wardrobe', category: 'Wedding', color: 'ชมพู', rentPricePerDay: 370, deposit: 1450, image: 'https://images.unsplash.com/photo-1502716119720-b23a93e5fe1b?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: '36"', length: '52"', storeName: 'Pastel Wardrobe', storeAddress: 'พัทยาเหนือ', storeRating: 4.8, reviews: [] },
      { id: 'STY-G30', title: 'Pastel Yellow Gingham Dress', brand: 'Vintage Romance', category: 'Cafe', color: 'ทอง/ครีม', rentPricePerDay: 160, deposit: 650, image: 'https://images.unsplash.com/photo-1496747611176-843222e1e57c?w=600&auto=format&fit=crop&q=80', chest: '32-34"', waist: '25-27"', hips: 'ฟรีไซส์', length: '41"', storeName: 'คุณริน (Lender)', storeAddress: 'ศรีราชา', storeRating: 4.7, reviews: [] }
    ];

    // Global State
    let userCoins = 420;
    let currentDetailIndex = 0;
    let navigationHistory = ['home'];
    let currentDeliveryCost = 0;
    let currentDeliveryText = 'รับที่หน้าร้าน';
    let currentDiscountAmount = 0;
    let appliedVoucherTitle = 'ไม่มี';
    let rangeStartDay = null;
    let rangeEndDay = null;
    let selectedColorFilter = 'all';

    let currentOrderActionIdx = null;

    // Wishlist Database State
    let wishlistIds = ['STY-G01', 'STY-G03'];

    // Real-time Dates
    const today = new Date();
    const currentRealDay = today.getDate(); // ล็อกวันย้อนหลัง

    // รอบการเช่าตัวอย่างในระบบ: เช่าวันที่ 11-13
    // Pre-Buffer (1 วันก่อนหน้า): วันที่ 10
    // Post-Buffer (2 วันหลังเช่า): วันที่ 14-15
    const bookedDays = [11, 12, 13];
    const preBufferDays = [10]; // Buffer ก่อนหน้า
    const postBufferDays = [14, 15]; // Buffer หลังเช่า

    // Orders Database
    let activeOrders = [
      {
        id: 'STY2610-0982',
        title: 'Mira Satin Maxi Dress',
        storeName: 'Studio Dress Up',
        dates: '10 ต.ค. - 12 ต.ค. 2026',
        deposit: 1000,
        rentPrice: 590,
        refundAccount: '082-XXX-8921 (พร้อมเพย์)',
        delivery: 'ส่งด่วน Rider Same-day',
        image: 'https://images.unsplash.com/photo-1595777457583-95e059d581b8?w=200&auto=format&fit=crop&q=80',
        status: 'ได้รับชุดแล้ว (อยู่ระหว่างการใช้งาน)',
        hasReceived: true
      }
    ];

    let historyOrders = [];

    // Vouchers Database
    let myVouchers = [
      { id: 'V-WELCOME', code: 'WELCOME50', title: 'โค้ดต้อนรับสมาชิกใหม่ ลด ฿50', discount: 50, isUsed: false },
      { id: 'V-PROMO', code: 'STY100', title: 'โค้ดโปรโมชันพิเศษ ลด ฿100', discount: 100, isUsed: false }
    ];

    // Sticky Search Bar on Scroll
    window.addEventListener('scroll', () => {
      const heroTrigger = document.getElementById('mainHeroSearchTrigger');
      const stickyBox = document.getElementById('stickySearchContainer');
      if (!heroTrigger || !stickyBox) return;

      const rect = heroTrigger.getBoundingClientRect();
      if (rect.bottom < 60) {
        stickyBox.classList.remove('hidden');
        setTimeout(() => {
          stickyBox.classList.remove('opacity-0', 'translate-y-[-10px]');
        }, 10);
      } else {
        stickyBox.classList.add('opacity-0', 'translate-y-[-10px]');
        setTimeout(() => {
          stickyBox.classList.add('hidden');
        }, 200);
      }
    });

    // Navigation System
    function navigateTo(viewName, addToHistory = true) {
      const views = ['home', 'wishlist', 'garment-detail', 'lender-profile', 'bookings', 'return-schedule', 'profile'];
      views.forEach(v => {
        const el = document.getElementById(`view-${v}`);
        if (el) el.classList.add('hidden');
      });

      const target = document.getElementById(`view-${viewName}`);
      if (target) target.classList.remove('hidden');

      if (viewName === 'wishlist') renderWishlistItems();
      if (viewName === 'bookings') renderOrdersList();

      if (addToHistory && navigationHistory[navigationHistory.length - 1] !== viewName) {
        navigationHistory.push(viewName);
      }

      window.scrollTo({ top: 0, behavior: 'smooth' });
      lucide.createIcons();
    }

    function goBack() {
      if (navigationHistory.length > 1) {
        navigationHistory.pop();
        navigateTo(navigationHistory[navigationHistory.length - 1], false);
      } else {
        navigateTo('home', false);
      }
    }

    // Wishlist Toggle Functions
    function toggleWishlist(garmentId, e) {
      if (e) e.stopPropagation();
      const idx = wishlistIds.indexOf(garmentId);
      if (idx > -1) {
        wishlistIds.splice(idx, 1);
      } else {
        wishlistIds.push(garmentId);
      }
      updateWishlistCounters();
      renderGarments();
      if (!document.getElementById('view-wishlist').classList.contains('hidden')) {
        renderWishlistItems();
      }
      updateDetailWishlistButton();
    }

    function updateWishlistCounters() {
      document.getElementById('navWishlistCount').innerText = wishlistIds.length;
    }

    function updateDetailWishlistButton() {
      const btn = document.getElementById('detailWishlistBtn');
      if (!btn) return;
      const curId = garmentsData[currentDetailIndex].id;
      if (wishlistIds.includes(curId)) {
        btn.className = 'p-2 rounded-xl bg-pink-50 border border-brand-pink text-brand-pink transition shadow-sm';
      } else {
        btn.className = 'p-2 rounded-xl bg-white border border-slate-200 text-slate-400 hover:text-brand-pink transition shadow-sm';
      }
    }

    function toggleWishlistFromDetail() {
      const curId = garmentsData[currentDetailIndex].id;
      toggleWishlist(curId);
      updateDetailWishlistButton();
    }

    function renderWishlistItems() {
      const grid = document.getElementById('wishlistGrid');
      grid.innerHTML = '';
      const list = garmentsData.filter(g => wishlistIds.includes(g.id));

      if (list.length === 0) {
        grid.innerHTML = '<div class="col-span-full py-12 text-center text-slate-400 text-xs">คุณยังไม่มีชุดในรายการโปรด แตะหัวใจเพื่อบันทึกชุดที่ชอบได้เลยค่ะ ✨</div>';
        return;
      }

      list.forEach(item => {
        const origIdx = garmentsData.findIndex(g => g.id === item.id);
        grid.innerHTML += `
          <div class="bg-white rounded-2xl border border-slate-100 overflow-hidden shadow-sm hover:shadow-md transition flex flex-col">
            <div class="relative h-44 sm:h-56 bg-slate-100 overflow-hidden cursor-pointer" onclick="openGarmentDetail(${origIdx})">
              <img src="${item.image}" class="w-full h-full object-cover">
              <button onclick="toggleWishlist('${item.id}', event)" class="absolute top-2 right-2 p-1.5 rounded-full bg-white/90 text-brand-pink shadow">
                <i data-lucide="heart" class="w-4 h-4 fill-current"></i>
              </button>
            </div>
            <div class="p-3 flex-1 flex flex-col justify-between text-xs">
              <div>
                <h3 class="font-bold text-slate-800 truncate">${item.title}</h3>
                <span class="text-brand-blue font-black">฿${item.rentPricePerDay} /วัน</span>
              </div>
              <button onclick="openBookingFromCard(${origIdx})" class="mt-2 w-full bg-brand-blue text-white py-1.5 rounded-xl font-bold text-[11px]">จองชุดนี้</button>
            </div>
          </div>
        `;
      });
      lucide.createIcons();
    }

    // Render 30 Garments
    function renderGarments(filteredList = garmentsData) {
      const grid = document.getElementById('garmentGrid');
      grid.innerHTML = '';
      document.getElementById('garmentCountBadge').innerText = `${filteredList.length} รายการ`;

      filteredList.forEach((item) => {
        const originalIndex = garmentsData.findIndex(g => g.id === item.id);
        const isFav = wishlistIds.includes(item.id);

        const card = document.createElement('div');
        card.className = 'bg-white rounded-2xl border border-slate-100 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col relative';
        card.innerHTML = `
          <div class="relative h-48 sm:h-64 bg-slate-100 overflow-hidden cursor-pointer" onclick="openGarmentDetail(${originalIndex})">
            <img src="${item.image}" class="w-full h-full object-cover hover:scale-105 transition-transform duration-300">
            <span class="absolute top-2 left-2 bg-white/90 text-[9px] font-bold px-2 py-0.5 rounded-full text-slate-700">${item.category}</span>
            <button onclick="toggleWishlist('${item.id}', event)" class="absolute top-2 right-2 p-1.5 rounded-full bg-white/90 shadow text-slate-400 hover:text-brand-pink transition">
              <i data-lucide="heart" class="w-3.5 h-3.5 ${isFav ? 'text-brand-pink fill-current' : ''}"></i>
            </button>
          </div>
          <div class="p-3 sm:p-4 flex-1 flex flex-col justify-between">
            <div>
              <div class="flex justify-between items-start mb-1 cursor-pointer" onclick="openGarmentDetail(${originalIndex})">
                <h3 class="font-bold text-slate-800 text-xs sm:text-sm truncate pr-1">${item.title}</h3>
              </div>
              <div class="flex items-center gap-1.5">
                <span class="text-brand-blue font-black text-xs sm:text-sm">฿${item.rentPricePerDay} <span class="text-[9px] text-slate-400 font-normal">/วัน</span></span>
                <span class="text-[9px] bg-slate-100 text-slate-600 px-1.5 py-0.2 rounded font-medium">${item.color}</span>
              </div>
              <p class="text-[10px] text-slate-400 truncate mt-0.5">${item.storeName}</p>
            </div>
            <div class="flex gap-1.5 pt-2">
              <button onclick="openGarmentDetail(${originalIndex})" class="flex-1 bg-slate-100 text-slate-700 py-1.5 rounded-lg text-[10px] font-semibold">ดูชุด</button>
              <button onclick="openBookingFromCard(${originalIndex})" class="flex-1 bg-brand-blue text-white py-1.5 rounded-lg text-[10px] font-semibold">จอง</button>
            </div>
          </div>
        `;
        grid.appendChild(card);
      });
      lucide.createIcons();
    }

    function handleSearchFilter(query) {
      const q = query.toLowerCase().trim();
      const filtered = garmentsData.filter(g => 
        g.title.toLowerCase().includes(q) || g.brand.toLowerCase().includes(q) || g.category.toLowerCase().includes(q) || g.color.toLowerCase().includes(q)
      );
      renderGarments(filtered);
    }

    function triggerSearch() {
      handleSearchFilter(document.getElementById('homeSearchInput').value);
      document.getElementById('catalog-section').scrollIntoView({ behavior: 'smooth' });
    }

    function filterVibe(category) {
      if (category === 'all') renderGarments(garmentsData);
      else renderGarments(garmentsData.filter(g => g.category.toLowerCase() === category.toLowerCase()));
    }

    // Color Filter Selection
    function selectColorFilter(color) {
      selectedColorFilter = color;
      document.querySelectorAll('.color-btn').forEach(btn => {
        if (btn.innerText === color || (color === 'all' && btn.innerText === 'ทั้งหมด')) {
          btn.className = 'color-btn p-1.5 rounded-xl border border-brand-blue bg-blue-50 text-brand-blue font-bold';
        } else {
          btn.className = 'color-btn p-1.5 rounded-xl border border-slate-200 hover:border-slate-300';
        }
      });
    }

    function toggleSearchMenuModal() { document.getElementById('searchMenuModal').classList.toggle('hidden'); }

    function applySearchFilters() {
      const cat = document.getElementById('filterCategorySelect').value;
      const min = parseFloat(document.getElementById('filterMinPrice').value) || 0;
      const max = parseFloat(document.getElementById('filterMaxPrice').value) || Infinity;

      let filtered = garmentsData.filter(g => {
        const matchCat = (cat === 'all' || g.category.toLowerCase() === cat.toLowerCase());
        const matchColor = (selectedColorFilter === 'all' || g.color.includes(selectedColorFilter));
        const matchPrice = (g.rentPricePerDay >= min && g.rentPricePerDay <= max);
        return matchCat && matchColor && matchPrice;
      });

      renderGarments(filtered);
      toggleSearchMenuModal();
      document.getElementById('catalog-section').scrollIntoView({ behavior: 'smooth' });
    }

    function resetSearchFilters() {
      document.getElementById('filterCategorySelect').value = 'all';
      document.getElementById('filterMinPrice').value = '';
      document.getElementById('filterMaxPrice').value = '';
      selectColorFilter('all');
      renderGarments(garmentsData);
      toggleSearchMenuModal();
    }

    function openImageSearchModal() { document.getElementById('imageSearchModal').classList.remove('hidden'); }
    function closeImageSearchModal() { document.getElementById('imageSearchModal').classList.add('hidden'); }

    function handleImageUploaded(e) {
      if (e.target.files && e.target.files[0]) {
        closeImageSearchModal();
        alert('ระบบวิเคราะห์รูปทรงและโทนสีเรียบร้อยค่ะ ✨');
        renderGarments(garmentsData.filter(g => g.category === 'Cosplay' || g.category === 'Party'));
        document.getElementById('catalog-section').scrollIntoView({ behavior: 'smooth' });
      }
    }

    // Detail View
    function openGarmentDetail(index) {
      currentDetailIndex = index;
      const item = garmentsData[index];
      document.getElementById('detailGarmentCode').innerText = `#${item.id}`;
      document.getElementById('detailCategoryBadge').innerText = item.category;
      document.getElementById('detailColorBadge').innerText = item.color;
      document.getElementById('detailBrandName').innerText = item.brand;
      document.getElementById('detailTitle').innerText = item.title;
      document.getElementById('detailMainImg').src = item.image;
      document.getElementById('detailRentPrice').innerHTML = `฿${item.rentPricePerDay} <span class="text-xs font-normal text-slate-500">/วัน</span>`;
      document.getElementById('detailDepositPrice').innerText = `฿${item.deposit.toLocaleString()}`;
      document.getElementById('detailChest').innerText = item.chest;
      document.getElementById('detailWaist').innerText = item.waist;
      document.getElementById('detailHips').innerText = item.hips;
      document.getElementById('detailLength').innerText = item.length;
      document.getElementById('detailStoreName').innerText = item.storeName;
      document.getElementById('detailStoreLocation').innerText = `${item.storeAddress} • Verified`;
      renderGarmentReviews(item);
      updateDetailWishlistButton();
      navigateTo('garment-detail');
    }

    function renderGarmentReviews(item) {
      const container = document.getElementById('detailReviewsList');
      container.innerHTML = '';
      if (!item.reviews || item.reviews.length === 0) {
        container.innerHTML = '<p class="text-xs text-slate-400 py-3 text-center">ยังไม่มีรีวิวสำหรับชุดนี้ค่ะ ✨</p>';
        return;
      }
      item.reviews.forEach(rev => {
        container.innerHTML += `
          <div class="p-2.5 rounded-xl bg-slate-50 border border-slate-200 text-xs space-y-1">
            <div class="flex justify-between font-bold"><span>${rev.author}</span><span class="text-amber-500">★ ${rev.rating}</span></div>
            <p class="text-slate-600 text-[11px]">${rev.comment}</p>
          </div>
        `;
      });
    }

    // ================= BOOKING ENGINE พร้อม BUFFER ก่อนหน้า-หลัง =================
    function openBookingFromCard(index) {
      currentDetailIndex = index;
      openBookingModalDirect(garmentsData[index]);
    }

    function proceedToBookingFromDetail() {
      openBookingModalDirect(garmentsData[currentDetailIndex]);
    }

    function openBookingModalDirect(item) {
      rangeStartDay = null;
      rangeEndDay = null;
      currentDiscountAmount = 0;
      appliedVoucherTitle = 'ไม่มี';

      document.getElementById('modalDressTitle').innerText = item.title;
      document.getElementById('modalStoreNameSubtitle').innerText = item.storeName;
      document.getElementById('summaryDeposit').innerText = `฿${item.deposit.toLocaleString()}`;
      document.getElementById('selectedPeriodBox').classList.add('hidden');
      document.getElementById('confirmBookBtn').setAttribute('disabled', 'true');
      document.getElementById('inputPromoCode').value = '';
      document.getElementById('promoCodeStatusMsg').classList.add('hidden');

      buildCalendarGrid();
      calculateFinalTotal();
      document.getElementById('bookingModal').classList.remove('hidden');
      lucide.createIcons();
    }

    function closeBookingModal() { document.getElementById('bookingModal').classList.add('hidden'); }

    function resetDateRangeSelection() {
      rangeStartDay = null;
      rangeEndDay = null;
      document.getElementById('selectedPeriodBox').classList.add('hidden');
      document.getElementById('confirmBookBtn').setAttribute('disabled', 'true');
      buildCalendarGrid();
      calculateFinalTotal();
    }

    function buildCalendarGrid() {
      const grid = document.getElementById('calendarDaysGrid');
      grid.innerHTML = '';
      for (let empty = 0; empty < 4; empty++) grid.appendChild(document.createElement('div'));

      for (let day = 1; day <= 31; day++) {
        const cell = document.createElement('button');
        cell.className = 'calendar-day-btn py-2 rounded-lg font-medium transition flex flex-col items-center justify-center relative text-xs ';

        // 1. วันย้อนหลัง
        if (day < currentRealDay) {
          cell.className += 'bg-slate-100 text-slate-300 cursor-not-allowed';
          cell.innerHTML = `<span>${day}</span><span class="text-[7px]">ผ่านแล้ว</span>`;
          cell.disabled = true;
        } 
        // 2. ติดจอง (Booked)
        else if (bookedDays.includes(day)) {
          cell.className += 'bg-slate-200 text-slate-400 cursor-not-allowed';
          cell.innerHTML = `<span>${day}</span><span class="text-[7px]">ติดจอง</span>`;
          cell.disabled = true;
        } 
        // 3. Pre-Buffer ก่อนหน้า (เตรียมชุด/ส่งพัสดุล่วงหน้า)
        else if (preBufferDays.includes(day)) {
          cell.className += 'bg-amber-100 text-amber-900 cursor-not-allowed';
          cell.innerHTML = `<span>${day}</span><span class="text-[7px] font-bold">Pre-Buffer</span>`;
          cell.disabled = true;
        }
        // 4. Post-Buffer หลังเช่า (ซัก/อบ/รีด)
        else if (postBufferDays.includes(day)) {
          cell.className += 'bg-amber-100 text-amber-900 cursor-not-allowed';
          cell.innerHTML = `<span>${day}</span><span class="text-[7px] font-bold">Post-Buffer</span>`;
          cell.disabled = true;
        } 
        // 5. วันว่างที่เลือกได้
        else {
          if (rangeStartDay === day && !rangeEndDay) {
            cell.className += 'bg-brand-blue text-white font-bold shadow';
            cell.innerHTML = `<span>${day}</span><span class="text-[7px]">เริ่ม</span>`;
          } else if (rangeStartDay && rangeEndDay && day >= rangeStartDay && day <= rangeEndDay) {
            if (day === rangeStartDay) {
              cell.className += 'bg-brand-blue text-white font-bold shadow';
              cell.innerHTML = `<span>${day}</span><span class="text-[7px]">เริ่ม</span>`;
            } else if (day === rangeEndDay) {
              cell.className += 'bg-brand-pink text-white font-bold shadow';
              cell.innerHTML = `<span>${day}</span><span class="text-[7px]">คืน</span>`;
            } else {
              cell.className += 'bg-blue-100 text-brand-blue font-bold';
              cell.innerHTML = `<span>${day}</span><span class="text-[7px]">เช่า</span>`;
            }
          } else {
            cell.className += 'bg-slate-50 hover:bg-brand-blueLight text-slate-700';
            cell.innerHTML = `<span>${day}</span><span class="text-[7px] text-emerald-600">ว่าง</span>`;
          }

          cell.onclick = () => handleDayClick(day);
        }

        grid.appendChild(cell);
      }
    }

    function handleDayClick(day) {
      if (!rangeStartDay || (rangeStartDay && rangeEndDay)) {
        rangeStartDay = day;
        rangeEndDay = null;
        document.getElementById('selectedPeriodBox').classList.add('hidden');
        document.getElementById('confirmBookBtn').setAttribute('disabled', 'true');
        buildCalendarGrid();
      } else if (rangeStartDay && !rangeEndDay) {
        if (day < rangeStartDay) {
          rangeStartDay = day;
          buildCalendarGrid();
          return;
        }

        // ตรวจสอบว่าช่วงที่เลือกชนกับวันจอง หรือ Buffer ก่อนหน้า-หลัง หรือไม่
        for (let d = rangeStartDay; d <= day; d++) {
          if (bookedDays.includes(d) || preBufferDays.includes(d) || postBufferDays.includes(d)) {
            alert('ช่วงเวลาที่คุณเลือกชนกับคิวจองหรือช่วง Buffer ก่อนหน้า/หลังการเช่า กรุณาเลือกช่วงวันอื่นเพื่อเว้นระยะเวลาจัดเตรียมชุดค่ะ');
            resetDateRangeSelection();
            return;
          }
        }

        rangeEndDay = day;
        const totalDays = rangeEndDay - rangeStartDay + 1;
        document.getElementById('selectedPeriodBox').classList.remove('hidden');
        document.getElementById('selectedDatesText').innerText = (totalDays === 1) 
          ? `${rangeStartDay} ต.ค. 2026 (1 วัน)` 
          : `${rangeStartDay} ต.ค. - ${rangeEndDay} ต.ค. 2026 (${totalDays} วัน)`;

        document.getElementById('confirmBookBtn').removeAttribute('disabled');
        buildCalendarGrid();
        calculateFinalTotal();
      }
    }

    function handleDeliveryChange(cost, labelText, requiresAddress) {
      currentDeliveryCost = cost;
      currentDeliveryText = labelText;
      document.getElementById('deliveryLabelText').innerText = labelText;
      document.getElementById('summaryShippingPrice').innerText = (cost === 0) ? '฿0 (ฟรี)' : `฿${cost}`;
      const addr = document.getElementById('addressSection');
      if (requiresAddress) addr.classList.remove('hidden'); else addr.classList.add('hidden');
      calculateFinalTotal();
    }

    // Promo Code
    function applyPromoCodeManual() {
      const code = document.getElementById('inputPromoCode').value.trim().toUpperCase();
      const statusMsg = document.getElementById('promoCodeStatusMsg');
      statusMsg.classList.remove('hidden');

      if (!code) {
        statusMsg.className = 'text-[10px] text-red-500 font-medium';
        statusMsg.innerText = 'กรุณากรอกรหัสโค้ดส่วนลดค่ะ';
        return;
      }

      const found = myVouchers.find(v => v.code === code && !v.isUsed);
      if (found) {
        currentDiscountAmount = found.discount;
        appliedVoucherTitle = found.title;
        found.isUsed = true;
        statusMsg.className = 'text-[10px] text-emerald-600 font-medium';
        statusMsg.innerText = `✓ ใช้โค้ด "${code}" สำเร็จ ลด ฿${found.discount}`;
      } else if (code === 'FREESHIP') {
        currentDiscountAmount = 60;
        appliedVoucherTitle = 'โค้ดส่งฟรี (ลด ฿60)';
        statusMsg.className = 'text-[10px] text-emerald-600 font-medium';
        statusMsg.innerText = '✓ ใช้โค้ดส่งฟรีสำเร็จ ลด ฿60';
      } else {
        statusMsg.className = 'text-[10px] text-red-500 font-medium';
        statusMsg.innerText = 'รหัสโค้ดไม่ถูกต้อง หรือถูกใช้งานไปแล้วค่ะ';
        currentDiscountAmount = 0;
        appliedVoucherTitle = 'ไม่มี';
      }

      calculateFinalTotal();
    }

    function calculateFinalTotal() {
      const item = garmentsData[currentDetailIndex];
      const days = (rangeStartDay && rangeEndDay) ? (rangeEndDay - rangeStartDay + 1) : 1;
      document.getElementById('calcDaysCountText').innerText = days;
      const rentTotal = item.rentPricePerDay * days;
      document.getElementById('summaryRentPrice').innerText = `฿${rentTotal.toLocaleString()}`;

      document.getElementById('appliedCouponText').innerText = `ส่วนลด (${appliedVoucherTitle}):`;
      document.getElementById('appliedCouponAmount').innerText = `-฿${currentDiscountAmount}`;

      let total = rentTotal + item.deposit + currentDeliveryCost - currentDiscountAmount;
      if (total < item.deposit) total = item.deposit;

      document.getElementById('finalCheckoutTotal').innerText = `฿${total.toLocaleString()}`;
      return total;
    }

    function openPaymentGatewayModal() {
      const refundAcc = document.getElementById('refundAccountInfo').value.trim();
      if (!refundAcc) {
        alert('กรุณาระบุช่องทางบัญชีสำหรับรับเงินมัดจำคืน เพื่อความปลอดภัยในระบบ Escrow ค่ะ');
        return;
      }
      document.getElementById('paymentTotalDisplay').innerText = `฿${calculateFinalTotal().toLocaleString()}`;
      document.getElementById('paymentModal').classList.remove('hidden');
    }

    function closePaymentModal() { document.getElementById('paymentModal').classList.add('hidden'); }

    function simulateSuccessfulPayment() {
      const item = garmentsData[currentDetailIndex];
      const selectedMethod = document.querySelector('input[name="payMethod"]:checked').value;
      const refundAcc = document.getElementById('refundAccountInfo').value;

      const newOrder = {
        id: `STY2610-${Math.floor(1000 + Math.random() * 9000)}`,
        title: item.title,
        storeName: item.storeName,
        dates: `${rangeStartDay} ต.ค. - ${rangeEndDay} ต.ค. 2026`,
        deposit: item.deposit,
        rentPrice: calculateFinalTotal() - item.deposit,
        refundAccount: refundAcc,
        delivery: currentDeliveryText,
        image: item.image,
        status: 'ได้รับชุดแล้ว (อยู่ระหว่างการใช้งาน)',
        hasReceived: true
      };

      activeOrders.unshift(newOrder);

      closePaymentModal();
      closeBookingModal();
      alert(`ชำระเงินผ่าน ${selectedMethod.toUpperCase()} สำเร็จ!\nระบบได้บันทึกช่องทางคืนมัดจำ: ${refundAcc}\nเงินมัดจำพักใน Escrow ปลอดภัย 100% ค่ะ ✨`);
      navigateTo('bookings');
    }

    // ================= ORDERS TAB & ACTION (เรียกไรเดอร์รับชุดในหน้าออเดอร์) =================
    function switchBookingTab(tab) {
      const activeBtn = document.getElementById('tabActiveBookingsBtn');
      const historyBtn = document.getElementById('tabHistoryBookingsBtn');
      const activeBox = document.getElementById('activeBookingsContainer');
      const historyBox = document.getElementById('historyBookingsContainer');

      if (tab === 'active') {
        activeBtn.className = 'px-4 py-1.5 rounded-lg bg-white text-brand-blue shadow-sm transition';
        historyBtn.className = 'px-4 py-1.5 rounded-lg text-slate-500 hover:text-slate-800 transition';
        activeBox.classList.remove('hidden');
        historyBox.classList.add('hidden');
      } else {
        historyBtn.className = 'px-4 py-1.5 rounded-lg bg-white text-brand-blue shadow-sm transition';
        activeBtn.className = 'px-4 py-1.5 rounded-lg text-slate-500 hover:text-slate-800 transition';
        historyBox.classList.remove('hidden');
        activeBox.classList.add('hidden');
      }
    }

    function renderOrdersList() {
      const activeBox = document.getElementById('activeBookingsContainer');
      const historyBox = document.getElementById('historyBookingsContainer');
      
      document.getElementById('activeOrdersBadge').innerText = activeOrders.length;
      document.getElementById('historyOrdersBadge').innerText = historyOrders.length;

      activeBox.innerHTML = '';
      if (activeOrders.length === 0) {
        activeBox.innerHTML = '<p class="text-xs text-slate-400 py-6 text-center">ไม่มีคำสั่งเช่าที่กำลังดำเนินการค่ะ</p>';
      } else {
        activeOrders.forEach((order, idx) => {
          activeBox.innerHTML += `
            <div class="border border-slate-200 rounded-2xl p-4 space-y-3 bg-slate-50/50">
              <div class="flex justify-between items-center text-xs border-b border-slate-200 pb-2">
                <span class="font-mono text-slate-500 font-bold">#${order.id} • ${order.storeName}</span>
                <span class="bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded-full text-[10px] font-bold">${order.status}</span>
              </div>
              <div class="flex flex-col sm:flex-row gap-3 items-start sm:items-center">
                <img src="${order.image}" class="w-16 h-20 object-cover rounded-xl">
                <div class="flex-1 space-y-1 text-xs">
                  <h3 class="font-bold text-slate-900">${order.title}</h3>
                  <p class="text-slate-500">ช่วงเวลาเช่า: ${order.dates}</p>
                  <p class="text-slate-600">เงินมัดจำ Escrow: <strong class="text-brand-blue">฿${order.deposit.toLocaleString()}</strong></p>
                  <p class="text-[10px] text-emerald-600">บัญชีรับคืนมัดจำ: ${order.refundAccount}</p>
                </div>
                <div class="flex flex-wrap gap-2 w-full sm:w-auto">
                  <!-- ปุ่มเรียกไรเดอร์รับชุดคืน (ฟังก์ชันใหม่ในหน้าเช่า) -->
                  <button onclick="openOrderReturnPickupModal(${idx})" class="flex-1 sm:flex-none bg-emerald-500 hover:bg-emerald-600 text-white text-xs font-semibold px-3 py-2 rounded-xl transition flex items-center justify-center gap-1 shadow-sm">
                    <i data-lucide="bike" class="w-3.5 h-3.5"></i> เรียก Rider รับชุดคืน
                  </button>
                  <button onclick="openEmbeddedTracker()" class="flex-1 sm:flex-none bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold px-3 py-2 rounded-xl transition flex items-center justify-center gap-1">
                    <i data-lucide="map-pin" class="w-3.5 h-3.5 text-brand-blue"></i> ดูตำแหน่ง
                  </button>
                  <button onclick="handleCompleteOrderReturn(${idx})" class="flex-1 sm:flex-none bg-brand-blue hover:bg-brand-blueDark text-white text-xs font-semibold px-3 py-2 rounded-xl transition flex items-center justify-center gap-1">
                    <i data-lucide="check" class="w-3.5 h-3.5"></i> คืนชุดเสร็จสิ้น
                  </button>
                </div>
              </div>
            </div>
          `;
        });
      }

      historyBox.innerHTML = '';
      if (historyOrders.length === 0) {
        historyBox.innerHTML = '<p class="text-xs text-slate-400 py-6 text-center">ยังไม่มีประวัติการเช่าที่เสร็จสิ้นค่ะ</p>';
      } else {
        historyOrders.forEach(order => {
          historyBox.innerHTML += `
            <div class="border border-slate-200 rounded-2xl p-4 space-y-3 bg-white opacity-90">
              <div class="flex justify-between items-center text-xs border-b border-slate-100 pb-2">
                <span class="font-mono text-slate-400 font-bold">#${order.id} • ${order.storeName}</span>
                <span class="bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded-full text-[10px] font-bold">✓ คืนชุดและโอนคืนมัดจำแล้ว</span>
              </div>
              <div class="flex flex-col sm:flex-row gap-3 items-start sm:items-center">
                <img src="${order.image}" class="w-16 h-20 object-cover rounded-xl grayscale">
                <div class="flex-1 space-y-1 text-xs">
                  <h3 class="font-bold text-slate-800">${order.title}</h3>
                  <p class="text-slate-400">รอบการเช่า: ${order.dates}</p>
                  <p class="text-emerald-600 font-medium">เงินมัดจำ ฿${order.deposit.toLocaleString()} โอนคืนเข้า ${order.refundAccount} เรียบร้อย</p>
                </div>
                <button onclick="alert('ใบเสร็จรับเงิน Escrow สมบูรณ์ โอนเงินมัดจำคืนเรียบร้อยค่ะ')" class="w-full sm:w-auto bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs px-3 py-2 rounded-xl font-semibold">
                  ดูสลิปโอนคืน
                </button>
              </div>
            </div>
          `;
        });
      }
      lucide.createIcons();
    }

    // Modal เรียกไรเดอร์รับชุดในหน้าออเดอร์
    function openOrderReturnPickupModal(idx) {
      currentOrderActionIdx = idx;
      const order = activeOrders[idx];
      document.getElementById('returnPickupOrderSubtitle').innerText = `ออเดอร์ #${order.id} (${order.title})`;
      document.getElementById('orderReturnPickupModal').classList.remove('hidden');
      lucide.createIcons();
    }

    function closeOrderReturnPickupModal() {
      document.getElementById('orderReturnPickupModal').classList.add('hidden');
    }

    function confirmOrderRiderPickup() {
      const order = activeOrders[currentOrderActionIdx];
      const timeVal = document.getElementById('orderReturnTimeSelect').value;
      const addr = document.getElementById('orderReturnAddressInput').value;
      
      closeOrderReturnPickupModal();
      openEmbeddedTracker();

      alert(`เรียก Rider มารับชุดเรียบร้อยแล้วค่ะ!\nเวลานัดรับ: ${timeVal}\nจุดนัดรับ: ${addr}\nไรเดอร์จะเดินทางมาถึงในไม่ช้า และเมื่อร้านค้าตรวจรับชุดสมบูรณ์ เงินมัดจำ Escrow ฿${order.deposit.toLocaleString()} จะโอนคืนเข้า ${order.refundAccount} ทันทีค่ะ 🛵✨`);
    }

    function handleCompleteOrderReturn(index) {
      const order = activeOrders[index];
      activeOrders.splice(index, 1);
      historyOrders.unshift(order);
      closeEmbeddedTracker();
      renderOrdersList();
      alert(`ส่งคืนชุด "${order.title}" เรียบร้อยแล้ว!\nระบบ Escrow ได้โอนเงินมัดจำ ฿${order.deposit.toLocaleString()} คืนเข้า ${order.refundAccount} เรียบร้อยแล้วค่ะ 💸✨`);
    }

    function openEmbeddedTracker() {
      const box = document.getElementById('embeddedGrabTracker');
      box.classList.remove('hidden');
      box.scrollIntoView({ behavior: 'smooth' });
    }

    function closeEmbeddedTracker() { document.getElementById('embeddedGrabTracker').classList.add('hidden'); }

    // Settings
    function handleSaveUserSettings(e) {
      e.preventDefault();
      const name = document.getElementById('settingUserName').value;
      const phone = document.getElementById('settingUserPhone').value;
      document.getElementById('userDisplayName').innerText = name;
      document.getElementById('userDisplayPhone').innerText = `เบอร์โทรศัพท์: ${phone} • Verified User`;
      alert('บันทึกการตั้งค่าเรียบร้อยแล้วค่ะ ✨');
    }

    // Notifications & Vouchers
    function toggleNotificationsModal() {
      document.getElementById('notificationsModal').classList.toggle('hidden');
      document.getElementById('unreadNotifBadge').classList.add('hidden');
    }

    function openCoinRewardsModal() {
      document.getElementById('rewardModalCoinCount').innerText = userCoins;
      renderMyVouchers();
      document.getElementById('coinRewardsModal').classList.remove('hidden');
    }

    function closeCoinRewardsModal() { document.getElementById('coinRewardsModal').classList.add('hidden'); }

    function switchVoucherTab(tab) {
      if (tab === 'redeem') {
        document.getElementById('tabRedeemContent').classList.remove('hidden');
        document.getElementById('tabMyVouchersContent').classList.add('hidden');
      } else {
        document.getElementById('tabRedeemContent').classList.add('hidden');
        document.getElementById('tabMyVouchersContent').classList.remove('hidden');
        renderMyVouchers();
      }
    }

    function redeemCoupon(type, cost, title, discount, code) {
      if (userCoins < cost) { alert('Coins ไม่พอค่ะ'); return; }
      userCoins -= cost;
      document.getElementById('navCoinCount').innerText = userCoins;
      document.getElementById('rewardModalCoinCount').innerText = userCoins;
      myVouchers.push({ id: `V-${Date.now()}`, code, title, discount, isUsed: false });
      alert(`แลก ${title} สำเร็จ! โค้ดของคุณคือ "${code}"`);
      switchVoucherTab('my');
    }

    function renderMyVouchers() {
      const container = document.getElementById('myVouchersListContainer');
      container.innerHTML = '';
      document.getElementById('myVouchersCountBadge').innerText = myVouchers.filter(v => !v.isUsed).length;
      myVouchers.forEach(v => {
        container.innerHTML += `
          <div class="p-2.5 rounded-xl border border-slate-200 flex justify-between items-center text-xs">
            <div>
              <span class="font-bold block">${v.title}</span>
              <span class="text-[10px] text-brand-blue font-mono">รหัส: ${v.code}</span>
            </div>
            <button onclick="applyVoucher('${v.id}')" ${v.isUsed ? 'disabled' : ''} class="${v.isUsed ? 'bg-slate-200 text-slate-400' : 'bg-brand-blue text-white'} px-2.5 py-1 rounded-lg font-bold">
              ${v.isUsed ? 'ใช้แล้ว' : 'ใช้โค้ดนี้'}
            </button>
          </div>
        `;
      });
    }

    function applyVoucher(id) {
      const v = myVouchers.find(x => x.id === id);
      if (!v || v.isUsed) return;
      v.isUsed = true;
      currentDiscountAmount = v.discount;
      appliedVoucherTitle = v.title;
      alert(`ใช้ ${v.title} สำเร็จ! นำไปหักจากยอดจองทันทีค่ะ`);
      closeCoinRewardsModal();
      calculateFinalTotal();
    }

    function buildReturnCalendar() {
      const grid = document.getElementById('returnCalendarDaysGrid');
      if (!grid) return;
      grid.innerHTML = '';
      for (let empty = 0; empty < 4; empty++) grid.appendChild(document.createElement('div'));
      for (let day = 1; day <= 31; day++) {
        const cell = document.createElement('div');
        cell.className = 'py-2 rounded-lg text-xs font-medium ' + (day === 12 ? 'bg-red-500 text-white font-bold animate-pulse' : 'bg-slate-50 text-slate-700');
        cell.innerHTML = `<span>${day}</span>` + (day === 12 ? '<span class="text-[7px] block">คืน</span>' : '');
        grid.appendChild(cell);
      }
    }

    function handleConfirmCourierPickup() {
      alert('เรียกรถรับชุดคืนเรียบร้อย ไรเดอร์จะโทรติดต่อก่อนเข้ารับค่ะ 🛵');
      navigateTo('bookings');
    }

    // Init App
    window.addEventListener('DOMContentLoaded', () => {
      renderGarments();
      updateWishlistCounters();
      buildReturnCalendar();
      renderOrdersList();
      lucide.createIcons();
    });
  </script>
</body>
</html>
