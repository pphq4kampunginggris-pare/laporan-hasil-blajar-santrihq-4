<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Tahfidz Al Karima - HQ Putri 4</title>
    
    <link rel="icon" type="image/x-icon" href="logohq.ico">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter & Amiri (Islamic Style) -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=Amiri:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- html2pdf.js CDN for Direct Premium PDF Download -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js" defer></script>
    <!-- Supabase JS Client CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <!-- canvas-confetti CDN for Premium Celebrations -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .arabic-text {
            font-family: 'Amiri', serif;
        }
        /* Custom scrollbar for premium aesthetic */
        ::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 8px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #059669;
        }

        /* Premium fade-in workspace transition */
        .fade-in-workspace {
            animation: fadeInWorkspace 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        @keyframes fadeInWorkspace {
            from {
                opacity: 0;
                transform: translateY(12px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Force background colors & gradients to print in full color in Portrait format */
        @media print {
            body {
                -webkit-print-color-adjust: exact !important;
                print-color-adjust: exact !important;
                background-color: #ffffff !important;
            }
            .no-print {
                display: none !important;
            }
            /* Reset shadow and layout scaling for print */
            #print-receipt-area, #wali-khs-card {
                border: none !important;
                box-shadow: none !important;
                width: 100% !important;
                max-width: 100% !important;
                padding: 0 !important;
                margin: 0 !important;
            }
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col antialiased">

    <!-- GATE LOGIN (INITIAL SCREEN) -->
    <div id="gate-screen" class="fixed inset-0 z-50 min-h-screen flex flex-col lg:flex-row bg-slate-50">
        <!-- Left Side: Branding and Islamic Theme Card -->
        <div class="hidden lg:flex lg:w-1/2 bg-gradient-to-tr from-emerald-950 via-emerald-900 to-slate-900 text-white p-16 flex-col justify-between relative overflow-hidden">
            <div class="absolute inset-0 bg-[radial-gradient(circle_at_top_right,rgba(16,185,129,0.15),transparent)] pointer-events-none"></div>
            
            <div class="flex items-center gap-3 z-10">
                <div class="bg-white/10 p-2.5 rounded-2xl border border-white/10 backdrop-blur-md">
                    <svg class="w-7 h-7 text-emerald-300" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
                    </svg>
                </div>

                <div>
                    <h1 class="text-base font-black tracking-tight bg-gradient-to-r from-white to-emerald-100 bg-clip-text text-transparent leading-none">YAYASAN INSAN BUDI MULIA DARUSSOLIKHIN</h1>
                    <p class="text-[9px] text-emerald-300/80 font-bold uppercase tracking-widest mt-1">PP Hamalatul Qur'an Putri 4</p>
                </div>
            </div>

            <div class="space-y-6 z-10">
                <span class="bg-emerald-500/20 text-emerald-300 border border-emerald-500/30 px-3.5 py-1.5 rounded-full text-xs font-bold tracking-wide uppercase inline-block">
                    E-Tahfidz Portal v5.0 (Steril)
                </span>
                <h2 class="text-4xl font-black leading-tight tracking-tight">
                    Sistem Laporan Real-Time<br/>dan Perkembangan Santri.
                </h2>
                <p class="text-slate-300/90 text-sm leading-relaxed max-w-lg">
                    Laporan pencatatan terpadu administrasi, laporan tahfidz harian, monitoring habit, serta visualisasi rekam jejak hafalan 30 Juz bagi santriwati secara instan lintas-perangkat.
                </p>
            </div>
            
            <!-- Real-time visual stats counter inside Gate Screen -->
            <div class="z-10 bg-white/5 border border-white/10 p-4 rounded-2xl flex items-center justify-between text-xs backdrop-blur-md">
                <div class="flex items-center gap-2">
                    <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-pulse"></span>
                    <span class="font-extrabold text-slate-200">Total Pengunjung Terdaftar:</span>
                </div>
                <div class="flex items-center gap-3">
                    <span class="font-mono text-emerald-300 font-bold" id="gate-visitor-count">156</span>
                    <span class="bg-white/15 px-2 py-0.5 rounded text-[10px] font-bold text-white" id="gate-online-count">6 Online</span>
                </div>
            </div>
        </div>

        <!-- Right Side: Interactive Login Portal Selection -->
        <div class="flex-1 flex items-center justify-center p-6 md:p-12">

            <div class="max-w-md w-full bg-white rounded-3xl p-8 border border-slate-200/60 shadow-2xl shadow-emerald-100/30">
                <div class="mb-6 text-center lg:text-left">
                    <div class="w-full max-w-md mb-4 bg-slate-900 text-amber-400 text-xs py-2 px-3 rounded-2xl shadow-md border-b border-green-500/20">
            <marquee behavior="scroll" direction="left" scrollamount="1" onmouseover="this.stop();" onmouseout="this.start();">
                <span class="font-bold"> E-Tahfidz PPHQ PUTRI 4: Mari pantau bersama rekam jejak perjuangan suci Ananda dalam menjaga kalamullah. Selamat menikmati laporan hasil studi (KHS) tahfidz Ananda.Trimakasih banyak telah mempercayai kami. no hp 085706399238</span>
            </marquee>
        </div>
                    <h3 class="text-2xl font-black text-slate-900 tracking-tight">E-TAHFIDZ PPHQ PUTRI 4 AL-KARIMA</h3>
                    <p class="text-[11px] text-slate-400 font-semibold mt-1">Pilih peran Anda di bawah ini untuk mengelola data</p>
                </div>

                <!-- Gate Sub-Navigation Selector -->
                <div class="bg-slate-100 p-1.5 rounded-2xl grid grid-cols-3 gap-1 mb-6">
                    <button id="role-btn-wali" onclick="setGateRole('wali')" class="py-2.5 rounded-xl text-xs font-black transition-all bg-white text-emerald-900 shadow-xs">
                        Wali Santri
                    </button>
                    <button id="role-btn-ustazah" onclick="setGateRole('ustazah')" class="py-2.5 rounded-xl text-xs font-bold text-slate-500 transition-all">
                        Ustazah
                    </button>
                    <button id="role-btn-admin" onclick="setGateRole('admin')" class="py-2.5 rounded-xl text-xs font-bold text-slate-500 transition-all">
                        Admin
                    </button>
                </div>

                <form id="gate-auth-form" onsubmit="handleGateLogin(event)" class="space-y-4">
                    <input type="hidden" id="selected-gate-role" value="wali">


                    <!-- WALI SANTRI FIELD: Name Search Input -->
                    <div id="gate-input-wrapper-wali" class="">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-2">Nama Lengkap Putri Anda</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                                <i class="fa-solid fa-magnifying-glass text-xs"></i>
                            </span>
                            <input type="text" id="gate-wali-student-name" oninput="handleWaliSearch()" placeholder="Contoh: Aisyah Humaira" class="w-full bg-slate-50 border border-slate-200 text-slate-800 rounded-2xl text-xs pl-10 pr-4 py-3.5 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold transition-all">
                        </div>


                        
                        <!-- Search matches dropdown suggestion -->
                        <div id="gate-wali-matches-box" class="hidden mt-2 bg-slate-50 border border-slate-150 rounded-2xl p-2 max-h-40 overflow-y-auto space-y-1.5">
                            <p class="text-[9px] font-black uppercase text-slate-400 px-2 tracking-widest mb-1">Hasil Pencarian:</p>
                            <div id="gate-wali-matches-list" class="space-y-1"></div>
                        </div>
                    </div>

                    <!-- USTAZAH SELECTOR FIELD -->
                    <div id="gate-input-wrapper-ustazah" class="hidden">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-2">Pilih Pembina Halaqah</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                                <i class="fa-solid fa-circle-user"></i>
                            </span>
                            <select id="gate-ustazah-select" class="w-full bg-slate-50 border border-slate-200 text-slate-800 rounded-2xl text-xs pl-10 pr-4 py-3.5 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold transition-all cursor-pointer">
                                <option value="Ayu">Ustazah Ayu (Halaqah Al-Mulk)</option>
                                <option value="Ayuniz">Ustazah Ayuniz (Halaqah Ar-Rahman)</option>
                                <option value="Rima">Ustazah Rima (Halaqah Ya-Sin)</option>
                                <option value="Nafis">Ustazah Nafis (Halaqah Al-Waqi'ah)</option>
                            </select>
                        </div>
                    </div>

                    <!-- PASSWORD / PIN FIELD -->
                    <div id="gate-input-wrapper-pin" class="hidden">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-2">Sandi Otoritas (PIN)</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                                <i class="fa-solid fa-lock-open text-xs"></i>
                            </span>
                            <input type="password" id="gate-pin" placeholder="••••" class="w-full bg-slate-50 border border-slate-200 text-slate-800 rounded-2xl text-xs pl-10 pr-4 py-3.5 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-extrabold tracking-widest transition-all">
                        </div>
                    </div>

                    <button type="submit" class="w-full bg-emerald-700 hover:bg-emerald-855 text-white font-extrabold text-xs py-3.5 rounded-2xl shadow-xl shadow-emerald-700/20 transition-all flex items-center justify-center gap-2">
                        <i class="fa-solid fa-right-to-bracket"></i> Masuk Ruangan
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- MAIN WORKSPACE HEADER -->
    <header class="bg-gradient-to-r from-emerald-950 to-slate-900 text-white shadow-lg sticky top-0 z-40 hidden no-print" id="main-app-header">
        <div class="max-w-7xl mx-auto px-4 py-3.5 flex items-center justify-between gap-3">
            <div class="flex items-center gap-3">
                <button onclick="handleLogout()" class="bg-white/10 hover:bg-white/20 text-emerald-300 border border-white/10 text-[10px] font-black px-3.5 py-2 rounded-xl transition-all flex items-center gap-1.5 shadow-sm">
                    <i class="fa-solid fa-arrow-left"></i> Keluar Portal
                </button>
                
                <div class="hidden sm:flex items-center gap-3 border-l border-white/10 pl-3">
                    <div class="bg-white/10 border border-white/20 p-2 rounded-2xl text-emerald-300 shadow-inner backdrop-blur-md">
                        <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                            <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
                        </svg>
                    </div>
                    <div>
                        <h1 class="text-base font-black tracking-tight leading-none bg-gradient-to-r from-white to-emerald-100 bg-clip-text text-transparent">E-Tahfidz Al Karima</h1>
                        <p class="text-[9px] text-emerald-300/90 font-extrabold uppercase tracking-widest mt-1" id="active-user-badge">Panel Pengguna</p>
                    </div>
                </div>
            </div>
            
            <div class="flex items-center gap-2.5">
                <!-- Header Live Sync Badge (Suppressed: Simple, clean and constant look) -->
                <div id="header-sync-badge" class="hidden flex items-center gap-1.5 bg-emerald-500/10 border border-emerald-500/20 px-3 py-1.5 rounded-xl text-[10px] font-bold text-emerald-300/90 tracking-wider">
                    <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
                    <span id="sync-time-label">TERHUBUNG</span>
                </div>

                <!-- Header Live Visitor Badge -->
                <div id="header-visitor-badge" class="flex items-center gap-2 bg-white/10 border border-white/10 px-3 py-1.5 rounded-xl text-[10px] font-bold text-emerald-300 tracking-wider hidden">
                    <i class="fa-solid fa-user text-amber-400"></i>
                    <span>PENGUNJUNG: <strong class="text-white" id="header-visitor-count">1</strong></span>
                </div>
                <button onclick="exportDashboardToPDF()" class="bg-emerald-700 hover:bg-emerald-600 text-white border border-emerald-500/30 text-[10px] font-black px-3.5 py-2 rounded-xl transition-all flex items-center gap-1.5 shadow-sm">
                    <i class="fa-solid fa-file-pdf text-amber-400"></i> Unduh PDF
                </button>
            </div>
        </div>
   </header>
<div class="sticky top-[68px] z-40 no-print bg-slate-900 text-amber-400 text-xs py-2 px-2 shadow-inner border-b border-green-500/20">
    <marquee behavior="scroll" direction="left" scrollamount="1" onmouseover="this.stop();" onmouseout="this.start();">
        <span class="font-bold"> E-Tahfidz PPHQ PUTRI 4: Mari pantau bersama rekam jejak perjuangan suci Ananda dalam menjaga kalamullah. Selamat menikmati laporan hasil studi (KHS) tahfidz Ananda.Trimakasih banyak telah mempercayai kami. no hp 085706399238</span>
    </marquee>
</div>

    <!-- APP MAIN CONTENT WORKSPACE -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 pb-20 space-y-6 hidden" id="main-app-container">
        
        <!-- IN-APP TOAST/NOTIF CONTAINER -->
        <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 max-w-sm w-full no-print"></div>

        <!-- ========================================================== -->
        <!-- VIEW 1: INTERFACE ADMINISTRATOR (PPSB) -->
        <!-- ========================================================== -->
        <div id="view-admin" class="hidden space-y-6">
            <!-- REAL-TIME STATISTICS ROW -->
            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4 no-print" id="admin-stats-row">
                <div class="bg-white p-4 rounded-3xl border border-slate-200/60 shadow-sm flex items-center gap-3">
                    <span class="p-3 bg-emerald-50 text-emerald-700 rounded-2xl"><i class="fa-solid fa-users text-base"></i></span>
                    <div>
                        <p class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Total Santriwati</p>
                        <p class="text-lg font-black text-slate-900" id="stat-total-students">0</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-3xl border border-slate-200/60 shadow-sm flex items-center gap-3">
                    <span class="p-3 bg-blue-50 text-blue-700 rounded-2xl"><i class="fa-solid fa-user-check text-base"></i></span>
                    <div>
                        <p class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Halaqah Aktif</p>
                        <p class="text-lg font-black text-slate-900" id="stat-active-students">0</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-3xl border border-slate-200/60 shadow-sm flex items-center gap-3">
                    <span class="p-3 bg-amber-50 text-amber-700 rounded-2xl"><i class="fa-solid fa-user-clock text-base"></i></span>
                    <div>
                        <p class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Menunggu (Pending)</p>
                        <p class="text-lg font-black text-slate-900" id="stat-pending-students">0</p>
                    </div>
                </div>
                <div class="bg-white p-4 rounded-3xl border border-slate-200/60 shadow-sm flex items-center gap-3">
                    <span class="p-3 bg-rose-50 text-rose-700 rounded-2xl"><i class="fa-solid fa-wallet text-base"></i></span>
                    <div>
                        <p class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Lunas SPP Aktif</p>
                        <p class="text-lg font-black text-slate-900" id="stat-paid-students">0</p>
                    </div>
                </div>
            </div>

            <!-- Navigation Tabs Internal for Admin -->
            <div class="border-b border-slate-200 no-print">
                <nav class="-mb-px flex space-x-8" aria-label="Tabs">
                    <button id="admin-tab-register" onclick="switchAdminTab('register')" class="border-emerald-600 text-emerald-800 border-b-2 py-4 px-1 text-sm font-black flex items-center gap-2">
                        <i class="fa-solid fa-user-plus text-xs"></i> Registrasi Santri Baru
                    </button>
                    <button id="admin-tab-directory" onclick="switchAdminTab('directory')" class="border-transparent text-slate-500 hover:text-slate-700 hover:border-slate-300 border-b-2 py-4 px-1 text-sm font-bold flex items-center gap-2">
                        <i class="fa-solid fa-address-book text-xs"></i> Direktori Seluruh Santriwati
                    </button>
                </nav>
            </div>

            <!-- TAB 1 CONTENT: REGISTRATION FORM WITH INTEGRATED LOGISTICS & FINANCIAL SPP -->
            <div id="admin-content-register" class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Left Column: Primary Registration Info Form -->
                <div class="lg:col-span-2 bg-white p-6 rounded-3xl border border-slate-200 shadow-sm space-y-5">
                    <div class="flex items-center gap-2.5 pb-3 border-b border-slate-100">
                        <span class="p-2.5 bg-emerald-50 text-emerald-700 rounded-xl"><i class="fa-solid fa-file-signature text-xs"></i></span>
                        <div>
                            <h3 class="font-extrabold text-sm text-slate-900">Formulir Pendaftaran & Rencana Keuangan</h3>
                            <p class="text-[10px] text-slate-400">Pastikan seluruh data penunjang awal & logistik santri dicentang valid sebelum diterbitkan.</p>
                        </div>
                    </div>

                    <form class="space-y-4" onsubmit="handleAdminAddStudent(event)">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Nama Lengkap Santriwati</label>
                                <input type="text" id="admin-add-name" required placeholder="Contoh: Aisyah Humaira Khansa" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold">
                            </div>
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Tempat, Tanggal Lahir</label>
                                <input type="text" id="admin-add-pobdob" required placeholder="Contoh: Kediri, 12 April 2007" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-700">
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">No. WhatsApp Wali (Aktif)</label>
                                <input type="tel" id="admin-add-phone" required placeholder="Contoh: 0812345678" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold tracking-wider text-slate-800">
                            </div>
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Riwayat Menghafal</label>
                                <select id="admin-add-memorized" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-slate-700 cursor-pointer">
                                    <option value="Belum Pernah">Belum Pernah Menghafal</option>
                                    <option value="Sudah Pernah">Sudah Memiliki Hafalan</option>
                                </select>
                            </div>
                        </div>

                        <!-- Rencana Keuangan Administrasi Masuk -->
                        <div class="bg-emerald-50/50 p-4 rounded-2xl border border-emerald-100 space-y-3">
                            <span class="block text-[10px] font-black text-emerald-800 uppercase tracking-wider"><i class="fa-solid fa-calculator mr-1"></i> Rencana Keuangan Administrasi Masuk</span>
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-3">
                                <label class="bg-white border border-emerald-200 rounded-xl p-3 flex items-center gap-3 cursor-pointer select-none">
                                    <input type="checkbox" id="admin-add-fee-reg" checked class="w-4.5 h-4.5 text-emerald-600 focus:ring-emerald-500 border-slate-300 rounded">
                                    <div>
                                        <span class="block text-[10px] font-extrabold text-slate-700">Infaq Pendaftaran</span>
                                        <span class="text-[9px] font-bold text-emerald-800">Rp 250.000</span>
                                    </div>
                                </label>
                                <label class="bg-white border border-emerald-200 rounded-xl p-3 flex items-center gap-3 cursor-pointer select-none">
                                    <input type="checkbox" id="admin-add-fee-spp1" checked class="w-4.5 h-4.5 text-emerald-600 focus:ring-emerald-500 border-slate-300 rounded">
                                    <div>
                                        <span class="block text-[10px] font-extrabold text-slate-700">Syahriyah SPP Bulan-1</span>
                                        <span class="text-[9px] font-bold text-emerald-800">Rp 900.000</span>
                                    </div>
                                </label>
                                <div class="bg-white border border-emerald-200 rounded-xl p-2.5">
                                    <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Daftar Ulang Manual (Rp)</label>
                                    <input type="number" id="admin-add-fee-rereg" value="0" min="0" class="w-full bg-slate-50 border border-slate-200 rounded-lg text-[11px] p-1.5 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-emerald-950">
                                </div>
                            </div>
                        </div>

                        <!-- INTEGRASI LOGISTIK LANGSUNG DI DALAM FORMULIR -->
                        <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-3">
                            <div class="flex items-center gap-2 pb-1 border-b border-slate-150">
                                <span class="text-emerald-700"><i class="fa-solid fa-boxes-packing text-xs"></i></span>
                                <span class="block text-[10px] font-black text-slate-700 uppercase tracking-wider">Serah Terima Fisik &amp; Logistik Awal</span>
                            </div>
                            <div class="grid grid-cols-2 gap-3 text-xs">
                                <label class="flex items-center gap-2.5 p-2.5 bg-white border border-slate-150 rounded-xl transition cursor-pointer select-none">
                                    <input type="checkbox" id="admin-add-fac-buku" checked class="w-4.5 h-4.5 text-emerald-600 focus:ring-emerald-500 border-slate-300 rounded">
                                    <div>
                                        <span class="font-bold text-slate-800 block text-[10px] leading-tight">Buku Pegangan</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Target mutabaah harian</span>
                                    </div>
                                </label>
                                <label class="flex items-center gap-2.5 p-2.5 bg-white border border-slate-150 rounded-xl transition cursor-pointer select-none">
                                    <input type="checkbox" id="admin-add-fac-meja" checked class="w-4.5 h-4.5 text-emerald-600 focus:ring-emerald-500 border-slate-300 rounded">
                                    <div>
                                        <span class="font-bold text-slate-800 block text-[10px] leading-tight">Meja Belajar Lipat</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Mengaji mandiri di kamar</span>
                                    </div>
                                </label>
                                <label class="flex items-center gap-2.5 p-2.5 bg-white border border-slate-150 rounded-xl transition cursor-pointer select-none">
                                    <input type="checkbox" id="admin-add-fac-kerudung" checked class="w-4.5 h-4.5 text-emerald-600 focus:ring-emerald-500 border-slate-300 rounded">
                                    <div>
                                        <span class="font-bold text-slate-800 block text-[10px] leading-tight">Hijab Almamater</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Seragam resmi HQ Putri 4</span>
                                    </div>
                                </label>
                                <label class="flex items-center gap-2.5 p-2.5 bg-white border border-slate-150 rounded-xl transition cursor-pointer select-none">
                                    <input type="checkbox" id="admin-add-fac-loker" class="w-4.5 h-4.5 text-emerald-600 focus:ring-emerald-500 border-slate-300 rounded">
                                    <div>
                                        <span class="font-bold text-slate-800 block text-[10px] leading-tight">Loker Lemari Pakaian</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Kunci lemari asrama eksklusif</span>
                                    </div>
                                </label>
                            </div>
                        </div>

                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Alamat Domisili Lengkap Wali</label>
                            <textarea id="admin-add-address" required rows="2" placeholder="Tuliskan nama jalan, RT/RW, kelurahan, kecamatan, kabupaten." class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none resize-none font-medium"></textarea>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Kamar Asrama & Halaqah Asuhan</label>
                                <select id="admin-add-room" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-emerald-900 cursor-pointer">
                                    <option value="Ayu">Ustazah Ayu - Ruang Ayu (Halaqah Al-Mulk)</option>
                                    <option value="Ayuniz">Ustazah Ayu - Ruang Ayuniz (Halaqah Ar-Rahman)</option>
                                    <option value="Rima">Ustazah Rima - Ruang Rima (Halaqah Ya-Sin)</option>
                                    <option value="Nafis">Ustazah Nafis - Ruang Nafis (Halaqah Al-Waqi'ah)</option>
                                </select>
                            </div>
                            <div class="grid grid-cols-2 gap-2">
                                <div>
                                    <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Program Kelas</label>
                                    <select id="admin-add-program" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-slate-700 cursor-pointer">
                                        <option value="Tahfidz Reguler">Reguler</option>
                                        <option value="Takhassus 30 Juz">Takhassus</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Target Celengan</label>
                                    <input type="text" id="admin-add-celengan" value="5 Juz" placeholder="cth: 5 Juz" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold">
                                </div>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Tanggal Kedatangan</label>
                                <input type="date" id="admin-add-arrival-date" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold">
                            </div>
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Status Syahriyah SPP Awal (Bulan-1)</label>
                                <select id="admin-add-paystatus" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-slate-700 cursor-pointer">
                                    <option value="Lunas">Selesai Dibayar (Lunas)</option>
                                    <option value="Belum Lunas" selected>Pending Pembayaran (Belum)</option>
                                </select>
                            </div>
                        </div>

                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Motivasi Menghafal</label>
                            <input type="text" id="admin-add-motivation" placeholder="Contoh: Mengabdi pada Al-Qur'an dan membahagiakan orang tua" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-600">
                        </div>

                        <button type="submit" class="w-full bg-emerald-700 hover:bg-emerald-855 text-white font-extrabold text-xs p-3.5 rounded-2xl shadow-xl shadow-emerald-700/20 transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-floppy-disk"></i> Simpan Pendaftaran &amp; Terbitkan Kuitansi
                        </button>
                    </form>
                </div>

                <!-- Right Side: PIN System Configurations & Admin security -->
                <div class="space-y-6">
                    <div class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm space-y-4">
                        <div class="flex items-center gap-2.5 pb-2.5 border-b border-slate-100">
                            <span class="p-2.5 bg-emerald-50 text-emerald-700 rounded-2xl"><i class="fa-solid fa-key text-xs"></i></span>
                            <div>
                                <h3 class="font-black text-xs text-slate-900 uppercase">🛡️ Sandi PIN Otoritas</h3>
                                <p class="text-[9px] text-slate-400 font-semibold">Ubah PIN untuk Admin &amp; Ustazah secara real-time</p>
                            </div>
                        </div>

                        <form id="admin-pin-settings-form" onsubmit="handleUpdatePins(event)" class="space-y-3.5">
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase tracking-wider mb-1">PIN Otoritas Admin</label>
                                <input type="text" id="pin-cfg-admin" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs px-3 py-2.5 outline-none font-mono font-extrabold tracking-widest focus:ring-2 focus:ring-emerald-500">
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase tracking-wider mb-1">PIN Ustazah Ayu (Al-Mulk)</label>
                                <input type="text" id="pin-cfg-ayu" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs px-3 py-2.5 outline-none font-mono font-extrabold tracking-widest focus:ring-2 focus:ring-emerald-500">
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase tracking-wider mb-1">PIN Ustazah Ayuniz (Ar-Rahman)</label>
                                <input type="text" id="pin-cfg-ayuniz" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs px-3 py-2.5 outline-none font-mono font-extrabold tracking-widest focus:ring-2 focus:ring-emerald-500">
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase tracking-wider mb-1">PIN Ustazah Rima (Ya-Sin)</label>
                                <input type="text" id="pin-cfg-rima" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs px-3 py-2.5 outline-none font-mono font-extrabold tracking-widest focus:ring-2 focus:ring-emerald-500">
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase tracking-wider mb-1">PIN Ustazah Nafis (Al-Waqi'ah)</label>
                                <input type="text" id="pin-cfg-nafis" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs px-3 py-2.5 outline-none font-mono font-extrabold tracking-widest focus:ring-2 focus:ring-emerald-500">
                            </div>

                            <button type="submit" class="w-full mt-2 bg-slate-800 hover:bg-slate-950 text-white font-extrabold text-[11px] py-3 rounded-xl transition-all flex items-center justify-center gap-1.5 shadow-sm">
                                <i class="fa-solid fa-lock"></i> Perbarui Semua PIN
                            </button>
                        </form>
                    </div>
                </div>
            </div>

            <!-- TAB 2 CONTENT: INTERACTIVE STUDENT DIRECTORY -->
            <div id="admin-content-directory" class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm space-y-4 hidden">
                <div class="flex flex-col md:flex-row items-center justify-between gap-4">
                    <div>
                        <h3 class="font-black text-sm text-slate-900"><i class="fa-solid fa-folder-open text-emerald-700 mr-1.5"></i> Arsip Induk Santriwati Baru</h3>
                        <p class="text-[10px] text-slate-400">Cari, tinjau status halaqah, cetak kuitansi, impor CSV, atau hapus database secara luring/cloud.</p>
                    </div>
                    
                    <div class="flex flex-col sm:flex-row items-center gap-2.5 w-full md:w-auto">
                        <!-- Impor CSV button verbatim named santri_students_rows.csv -->
                        <div class="relative w-full sm:w-auto">
                            <input type="file" id="csv-file-input" accept=".csv" onchange="handleCSVImport(event)" class="hidden">
                            <button onclick="document.getElementById('csv-file-input').click()" class="w-full sm:w-auto bg-amber-600 hover:bg-amber-700 text-white text-xs font-black px-4 py-2.5 rounded-xl transition flex items-center justify-center gap-1.5 shadow-sm">
                                <i class="fa-solid fa-file-import"></i> Impor CSV (santri_students_rows.csv)
                            </button>
                        </div>

                        <div class="relative w-full sm:w-48">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3 text-slate-400">
                                <i class="fa-solid fa-magnifying-glass text-xs"></i>
                            </span>
                            <input type="text" id="admin-search-student" oninput="renderAdminStudentsDirectory()" placeholder="Ketik nama / ID..." class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs pl-9 pr-4 py-2.5 outline-none focus:ring-2 focus:ring-emerald-500">
                        </div>
                        <select id="admin-filter-ustazah" onchange="renderAdminStudentsDirectory()" class="w-full sm:w-auto bg-slate-50 border border-slate-200 rounded-xl text-xs px-3 py-2.5 outline-none font-bold text-slate-600 cursor-pointer">
                            <option value="all">Semua Halaqah</option>
                            <option value="Ayu">Halaqah Ayu</option>
                            <option value="Ayuniz">Halaqah Ayuniz</option>
                            <option value="Rima">Halaqah Rima</option>
                            <option value="Nafis">Halaqah Nafis</option>
                        </select>
                    </div>
                </div>

                <div class="overflow-x-auto rounded-2xl border border-slate-100">
                    <table class="w-full text-left text-xs border-collapse">
                        <thead>
                            <tr class="bg-slate-50 text-slate-400 border-b border-slate-150 font-black tracking-wider uppercase text-[9px]">
                                <th class="p-3">Santriwati &amp; No. WhatsApp</th>
                                <th class="p-3">Program Studi</th>
                                <th class="p-3 text-center">Ustazah Pengampu</th>
                                <th class="p-3 text-center">Status Halaqah</th>
                                <th class="p-3 text-center">Syahriyah (SPP)</th>
                                <th class="p-3 text-center">Tindakan Otoritas</th>
                            </tr>
                        </thead>
                        <tbody id="admin-students-directory-list" class="divide-y divide-slate-100 font-medium text-slate-600">
                            <!-- Filled dynamically -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- ========================================================== -->
        <!-- VIEW 2: INTERFACE USTAZAH (HALAQAH) -->
        <!-- ========================================================== -->
        <div id="view-ustazah" class="hidden space-y-6">
            <!-- Calon Anggota Baru (PENDING APPROVAL) - ONLY SHOWS IF THERE IS PENDING STUDENT -->
            <div id="ustazah-pending-section" class="hidden bg-amber-50/50 border border-amber-200 p-5 rounded-3xl space-y-4">
                <div class="flex items-center gap-2">
                    <span class="p-2 bg-amber-100 text-amber-800 rounded-xl animate-pulse"><i class="fa-solid fa-user-clock text-xs"></i></span>
                    <div>
                        <h4 class="font-black text-xs text-slate-900 uppercase">Calon Anggota Halaqah Baru (Menunggu Otorisasi)</h4>
                        <p class="text-[10px] text-slate-500">Santriwati baru yang didaftarkan Admin membutuhkan konfirmasi Anda untuk masuk halaqah aktif.</p>
                    </div>
                </div>
                <div class="overflow-x-auto rounded-2xl border border-amber-150 bg-white">
                    <table class="w-full text-left text-xs border-collapse">
                        <thead>
                            <tr class="bg-amber-50 text-amber-900/60 border-b border-amber-150 font-black text-[9px] uppercase">
                                <th class="p-3">Nama Santriwati</th>
                                <th class="p-3">Pondok Asal &amp; POB</th>
                                <th class="p-3">Program &amp; Target</th>
                                <th class="p-3 text-center">Otorisasi Masuk</th>
                            </tr>
                        </thead>
                        <tbody id="ustazah-pending-list" class="divide-y divide-amber-100">
                            <!-- Filled dynamically with "+" button -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Main Active Halaqah Workspace Grid -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Left: Daily Setoran Input Form (Ustazah Form) -->
                <div class="bg-white p-6 rounded-3xl border border-slate-200 shadow-sm space-y-5 h-fit">
                    <div class="flex items-center gap-2.5 pb-3 border-b border-slate-100">
                        <span class="p-2.5 bg-emerald-50 text-emerald-700 rounded-xl"><i class="fa-solid fa-pen-to-square text-xs"></i></span>
                        <div>
                            <h3 id="ustazah-directory-title" class="font-extrabold text-sm text-slate-900">Form Input Data Santri (Ustadzah)</h3>
                            <p class="text-[10px] text-slate-400">Pencatatan setoran harian, target mingguan, &amp; Laporan perkembangan santri.</p>
                        </div>
                    </div>

                    <form class="space-y-4" onsubmit="handleUstazahSetoranSubmit(event)">
                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Nama Santri:</label>
                            <select id="ustazah-student-select" onchange="populateUstazahForm(this.value)" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-slate-800 cursor-pointer">
                                <!-- Filled dynamically -->
                            </select>
                        </div>

                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Setoran Awal:</label>
                                <input type="text" id="ustazah-setoran-awal" placeholder="Contoh: Juz 1 Hal 1" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-700">
                            </div>
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Setoran Akhir:</label>
                                <input type="text" id="ustazah-setoran-akhir" placeholder="Contoh: Juz 1 Hal 5" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-700">
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Target Mingguan:</label>
                                <input type="text" id="ustazah-target-mingguan" placeholder="Contoh: 5 Halaman" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-700">
                            </div>
                            <div>
                                <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Status Capaian:</label>
                                <select id="ustazah-status-capaian" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-slate-700 cursor-pointer">
                                    <option value="Tercapai">Tercapai</option>
                                    <option value="Belum Tercapai">Belum Tercapai</option>
                                </select>
                            </div>
        <div class="space-y-4">
    <div>
        <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Nilai Fasohah:</label>
        <select id="ustazah-fasohah" class="w-full bg-white border border-slate-200 rounded-xl text-xs p-2 outline-none font-bold text-slate-700 cursor-pointer">
            <option value="Istimewa (A+)">Istimewa (A+)</option>
            <option value="Sangat Baik (A)">Sangat Baik (A)</option>
            <option value="Baik (B)">Baik (B)</option>
            <option value="Cukup (C)">Cukup (C)</option>
            <option value="Belum Dinilai" selected>Belum Dinilai</option>
        </select>
    </div>
    <div>
        <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Nilai Kelancaran:</label>
        <select id="ustazah-kelancaran" class="w-full bg-white border border-slate-200 rounded-xl text-xs p-2 outline-none font-bold text-slate-700 cursor-pointer">
            <option value="Lancar Sekali (A+)">Lancar Sekali (A+)</option>
            <option value="Lancar (A)">Lancar (A)</option>
            <option value="Sedang (B)">Sedang (B)</option>
            <option value="Kurang (C)">Kurang (C)</option>
            <option value="Belum Dinilai" selected>Belum Dinilai</option>
        </select>
    </div>
</div>             </div>

                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Total Juz Hafalan Saat Ini (Format Angka, Contoh: 3.5):</label>
                            <input type="number" step="0.1" id="ustazah-total-juz" placeholder="Contoh: 3.5" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-bold text-emerald-900">
                        </div>

                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Perkembangan Positif (+):</label>
                            <textarea id="ustazah-perkembangan-positif" rows="2" placeholder="Kelebihan/kemajuan pekan ini" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none resize-none font-semibold text-slate-600"></textarea>
                        </div>

                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Catatan Negatif (-):</label>
                            <textarea id="ustazah-catatan-negatif" rows="2" placeholder="Evaluasi/kendala pekan ini" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none resize-none font-semibold text-slate-600"></textarea>
                        </div>

                        <!-- Administrasi Sub-Group -->
                        <div class="bg-slate-50 p-4 rounded-2xl border border-slate-150 space-y-3">
                            <span class="block text-[10px] font-black text-emerald-800 uppercase tracking-wider"><i class="fa-solid fa-file-invoice-dollar mr-1"></i> Status Administrasi</span>
                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Syahriyah Bulan Ini:</label>
                                    <select id="ustazah-syahriyah" class="w-full bg-white border border-slate-200 rounded-xl text-xs p-2 outline-none font-bold text-slate-700 cursor-pointer">
                                        <option value="Lunas">Lunas</option>
                                        <option value="Belum Lunas">Belum Lunas</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Daftar Ulang:</label>
                                    <select id="ustazah-daftar-ulang" class="w-full bg-white border border-slate-200 rounded-xl text-xs p-2 outline-none font-bold text-slate-700 cursor-pointer">
                                        <option value="Lunas">Lunas</option>
                                        <option value="Belum Lunas">Belum Lunas</option>
                                        <option value="Cicil">Cicil</option>
                                    </select>
                                </div>
                            </div>
                        </div>

                        <div>
                            <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1.5">Catatan Lain-lain:</label>
                            <textarea id="ustazah-catatan-lain" rows="2" placeholder="Keterangan tambahan (sakit, izin, dll)" class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs p-3 focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none resize-none font-semibold text-slate-600"></textarea>
                        </div>

                        <button type="submit" class="w-full bg-emerald-700 hover:bg-emerald-855 text-white font-extrabold text-xs p-3.5 rounded-2xl shadow-xl shadow-emerald-700/20 transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-floppy-disk"></i> Simpan Data &amp; Update KHS
                        </button>
                    </form>
                </div>

                <!-- Right: Active Halaqah Students List Directory -->
                <div class="lg:col-span-2 bg-white p-6 rounded-3xl border border-slate-200 shadow-sm flex flex-col h-[650px]">
                    <div class="flex items-center justify-between pb-3 border-b border-slate-100 mb-4">
                        <h3 class="font-extrabold text-xs text-slate-900 uppercase flex items-center gap-1.5">
                            <i class="fa-solid fa-people-group text-emerald-700"></i> Daftar Rekapitulasi Santriwati Aktif Mengaji
                        </h3>
                    </div>
                    <div id="ustazah-active-list" class="flex-1 overflow-y-auto space-y-3.5 pr-1.5">
                        <!-- Dynamic Cards with Whatsapp and KHS access buttons -->
                    </div>
                </div>
            </div>
        </div>

        <!-- ==================== VIEW 3: INTERFACE WALI SANTRI (KHS DIGITAL) ==================== -->
        <div id="view-wali" class="hidden space-y-6">
            <!-- Navigation back button specifically for Admin/Ustazah testing -->
            <div id="parent-back-btn-container" class="flex flex-col sm:flex-row justify-between items-center bg-slate-100 p-4 rounded-3xl border border-slate-200/50 gap-3 no-print">
                <div class="flex items-center gap-2">
                    <span class="p-1.5 bg-emerald-50 text-emerald-700 rounded-lg"><i class="fa-solid fa-shield-halved text-xs"></i></span>
                    <span class="text-xs font-bold text-slate-600">Sesi KHS Privat Terkunci Keamanan</span>
                </div>
                <div class="flex items-center gap-2 w-full sm:w-auto">
                    <button onclick="refreshWaliData()" class="flex-1 sm:flex-initial bg-emerald-50 hover:bg-emerald-100 text-emerald-800 text-xs font-black px-4 py-2 rounded-xl transition border border-emerald-200 flex items-center justify-center gap-1.5 shadow-2xs">
                        <i class="fa-solid fa-rotate text-xs"></i> Segarkan Data
                    </button>
                    <button onclick="goBackToDashboard()" class="flex-1 sm:flex-initial bg-white hover:bg-slate-50 text-slate-700 text-xs font-black px-4 py-2 rounded-xl transition border border-slate-200 flex items-center justify-center gap-1.5 shadow-2xs">
                        <i class="fa-solid fa-arrow-left text-emerald-700"></i> Kembali Ke Panel Utama
                    </button>
                </div>
            </div>

            <!-- PREMIUM PORTRAIT KHS RAPORT CARD -->
            <div id="wali-khs-card" class="bg-white rounded-3xl border border-slate-200 p-6 md:p-8 shadow-xl space-y-6 relative max-w-4xl mx-auto" style="-webkit-print-color-adjust: exact !important; print-color-adjust: exact !important;">
                
                <!-- KHS HEADER: Official Identity of Pesantren -->
                <div class="border-b-4 border-double border-emerald-800 pb-4 text-center">
                    <h3 class="font-extrabold text-[10px] tracking-widest text-slate-500 uppercase leading-none">YAYASAN INSAN BUDI MULIA DARUSSOLIKHIN</h3>
                    <h2 class="font-black text-sm text-slate-900 uppercase tracking-tight mt-1.5">PP HAMALATUL QUR'AN PUTRI 4 AL-KARIMA</h2>
                    <p class="text-[9px] font-bold text-emerald-800 uppercase tracking-wider mt-1">Laporan Hasil Perkembangan Tahfidz &amp; Administrasi Santriwati</p>
                    <p class="text-[8px] font-medium text-slate-400 mt-1 font-mono">Jl. Mawar No. 4, Kampung Inggris, Pare, Kediri | WA: 085706399238</p>
                </div>

                <!-- SUB-TITLE -->
                <div class="text-center space-y-1">
                    <div class="text-[10px] font-black uppercase text-emerald-800 tracking-widest">KARTU HASIL STUDI (KHS) DIGITAL</div>
                </div>

                <!-- WALI KHS DATA: Avatar & Large Biodata Card -->
                <div class="flex flex-col sm:flex-row items-center gap-6 p-6 bg-slate-50 rounded-2xl border border-slate-150">
    <div class="w-24 h-32 bg-slate-200 rounded-xl overflow-hidden border-2 border-emerald-600/20 shadow-inner flex items-center justify-center flex-shrink-0">
        <img id="khs-student-photo" src="https://via.placeholder.com/150x200?text=Foto+Santri" alt="Foto Santri" class="w-full h-full object-cover hidden">
        <i id="khs-photo-placeholder" class="fa-solid fa-user-gradient text-3xl text-slate-400"></i>
    </div>

    <div class="flex flex-col md:flex-row gap-6 items-center bg-slate-50/50 p-5 rounded-3xl border border-slate-150">
                    <!-- Circular Monogram Avatar -->
                    <div class="">
                        <span id="wali-khs-initial" class="leading-none text-white font-black"></span>
                        <span class="text-[9px] font-extrabold tracking-widest uppercase text-emerald-200 mt-1"></span>
                    </div>

                    <!-- Responsive Biodata Fields Grid -->
                    <div class="flex-1 space-y-2">
                        <div class="flex flex-wrap items-center gap-2">
                            <h4 id="wali-khs-name" class="text-xl font-black text-slate-900">-</h4>
                            <span id="wali-khs-presence-badge" class="bg-emerald-100 text-emerald-800 text-[9px] px-2 py-0.5 rounded-full font-black flex items-center gap-1">
                                <i class="fa-solid fa-circle-check"></i> Sudah Di Asrama
                            </span>
                        </div>

                        <!-- Biodata Grid -->
        
                            <div class="space-y-1">
                                <p class="text-slate-500 font-medium"><i class="fa-solid fa-cake-candles text-emerald-700 w-2"></i> TTL: <strong id="wali-khs-pobdob" class="text-slate-800 font-bold">-</strong></p>
                                <p class="text-slate-500 font-medium"><i class="fa-solid fa-phone text-emerald-700 w-4"></i> HP Wali: <strong id="wali-khs-parent" class="text-slate-800 font-bold">-</strong></p>
                                <p class="text-slate-500 font-medium"><i class="fa-solid fa-location-dot text-emerald-700 w-4"></i> Alamat: <strong id="wali-khs-address" class="text-slate-800 font-semibold">-</strong></p>
                            </div>
                            <div class="space-y-1">
                                <p class="text-slate-500 font-medium"><i class="fa-solid fa-graduation-cap text-emerald-700 w-4"></i> Program: <strong id="wali-khs-program" class="text-slate-800 font-bold">-</strong></p>
                                <p class="text-slate-500 font-medium"><i class="fa-solid fa-user-tie text-emerald-700 w-4"></i> Ustazah: <strong id="wali-khs-ustazah" class="text-slate-800 font-bold">-</strong></p>
                                <p class="text-slate-500 font-medium"><i class="fa-solid fa-bullseye text-emerald-700 w-4"></i> Celengan Awal: <strong id="wali-khs-celengan" class="text-emerald-800 font-extrabold">-</strong></p>
                            </div>
                        
                    </div>
                </div>
        
                
                </div>

                <!-- PETA JALUR PERJALANAN HAFAKAN 30 JUZ -->
                <div class="space-y-3">
                    <span class="block text-[10px] font-black text-emerald-800 uppercase tracking-wider"><i class="fa-solid fa-map-location-dot mr-1"></i> Peta Jalur Perjalanan Visual Menuju 30 Juz Al-Qur'an</span>
                    <div id="peta-tahfidz-container" class="grid grid-cols-6 sm:grid-cols-10 gap-1.5 p-4 bg-emerald-50/30 rounded-3xl border border-emerald-150">
                        <!-- Filled dynamically: 30 visual progress circles -->
                    </div>
                </div>

                <!-- CARDS PANEL DETAIL: Setoran & Keuangan SPP -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    
                    <!-- COLUMN 1 & 2: REKAP SETORAN PEKAN INI -->
                    <div class="lg:col-span-2 bg-slate-50 p-5 rounded-3xl border border-slate-150 space-y-4">
                        <span class="block text-[10px] font-black text-emerald-855 uppercase tracking-wider"><i class="fa-solid fa-book-open text-emerald-750 mr-1"></i> Perkembangan Hafalan Terkini</span>
                        
                        <div class="grid grid-cols-2 md:grid-cols-4 gap-3 text-xs">
                            <div class="bg-white p-3 rounded-2xl border border-slate-200">
                                <span class="text-[9px] text-slate-400 font-bold block uppercase">Setoran Awal</span>
                                <span id="wali-khs-setoran-awal" class="font-extrabold text-slate-800 mt-1 block">-</span>
                            </div>
                            <div class="bg-white p-3 rounded-2xl border border-slate-200">
                                <span class="text-[9px] text-slate-400 font-bold block uppercase">Setoran Akhir</span>
                                <span id="wali-khs-setoran-akhir" class="font-extrabold text-emerald-800 mt-1 block">-</span>
                            </div>
                            <div class="bg-white p-3 rounded-2xl border border-slate-200">
                                <span class="text-[9px] text-slate-400 font-bold block uppercase">Target Pekanan</span>
                                <span id="wali-khs-target-mingguan" class="font-extrabold text-slate-800 mt-1 block">-</span>
                            </div>
                            <div class="bg-white p-3 rounded-2xl border border-slate-200">
                                <span class="text-[9px] text-slate-400 font-bold block uppercase">Status Capaian</span>
                                <span id="wali-khs-status-capaian" class="font-extrabold mt-1 block">-</span>
                            </div>
                            <div class="bg-white p-3 rounded-2xl border border-slate-200">
    <span class="text-[9px] text-slate-400 font-bold block uppercase">Nilai Fasohah</span>
    <span id="wali-khs-fasohah" class="font-extrabold text-emerald-700 mt-1 block text-sm">-</span>
</div>
<div class="bg-white p-3 rounded-2xl border border-slate-200">
    <span class="text-[9px] text-slate-400 font-bold block uppercase">Nilai Kelancaran</span>
    <span id="wali-khs-kelancaran" class="font-extrabold text-emerald-700 mt-1 block text-sm">-</span>
</div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-3 text-xs pt-1">
                            <div class="bg-emerald-50/50 p-3 rounded-2xl border border-emerald-100">
                                <span class="text-[9px] text-emerald-800 font-black block uppercase"><i class="fa-solid fa-circle-check"></i> Perkembangan Positif (+)</span>
                                <p id="wali-khs-perkembangan-positif" class="text-slate-700 font-medium mt-1 leading-relaxed">-</p>
                            </div>
                            <div class="bg-rose-50/30 p-3 rounded-2xl border border-rose-100">
                                <span class="text-[9px] text-rose-800 font-black block uppercase"><i class="fa-solid fa-circle-exclamation"></i> Catatan Evaluasi (-)</span>
                                <p id="wali-khs-catatan-negatif" class="text-slate-700 font-medium mt-1 leading-relaxed">-</p>
                            </div>
                        </div>
                    </div>

                    <!-- COLUMN 3: INFORMASI ADMINISTRASI AKTIF -->
                    <div class="bg-slate-50 p-5 rounded-3xl border border-slate-150 space-y-4">
                        <span class="block text-[10px] font-black text-slate-900 uppercase tracking-wider"><i class="fa-solid fa-file-invoice-dollar text-emerald-700 mr-1"></i> Keuangan &amp; Administrasi</span>
                        
                        <div class="space-y-3 text-xs">
                            <div class="bg-white p-3 rounded-2xl border border-slate-200 flex justify-between items-center">
                                <div>
                                    <span class="text-[9px] text-slate-400 font-bold block uppercase">Syahriyah SPP</span>
                                    <span id="wali-khs-spp-status-label" class="font-bold text-slate-700">SPP Bulan Berjalan</span>
                                </div>
                                <span id="wali-khs-syahriyah-badge" class="px-2.5 py-1 rounded-full font-black text-[10px]">-</span>
                            </div>

                            <div class="bg-white p-3 rounded-2xl border border-slate-200 flex justify-between items-center">
                                <div>
                                    <span class="text-[9px] text-slate-400 font-bold block uppercase">Daftar Ulang</span>
                                    <span class="font-bold text-slate-700">Fasilitas &amp; Sarana</span>
                                </div>
                                <span id="wali-khs-daftarulang-badge" class="px-2.5 py-1 rounded-full font-black text-[10px]">-</span>
                            </div>

                            <div class="bg-emerald-50/40 p-3 rounded-2xl border border-emerald-100 space-y-1">
                                <span class="text-[9px] text-emerald-800 font-black block uppercase"><i class="fa-solid fa-circle-info"></i> Catatan Lain-lain:</span>
                                <p id="wali-khs-catatan-lain" class="text-slate-600 leading-normal font-semibold text-[10px]">-</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- ADDED MONTH-BY-MONTH SPP CHECKLIST VISUALIZATION FOR PARENTS -->
                <div class="bg-slate-50 p-5 rounded-3xl border border-slate-150 space-y-4">
                    <div class="flex justify-between items-center border-b border-slate-200 pb-2">
                        <span class="block text-[10px] font-black text-emerald-900 uppercase tracking-wider">
                            <i class="fa-solid fa-calendar-days text-emerald-700 mr-1"></i> Histori Pembayaran Syahriyah SPP (12 Bulan)
                        </span>
                        <span class="text-[10px] bg-emerald-150 text-emerald-800 px-2.5 py-0.5 rounded-full font-black font-mono" id="wali-spp-summary">0 dari 12 Bulan Lunas</span>
                    </div>
                    <div class="grid grid-cols-3 sm:grid-cols-4 md:grid-cols-6 gap-2" id="wali-spp-months-grid">
                        <!-- Filled dynamically -->
                    </div>
                </div>

                <!-- TIMELINE: HISTORI PERKEMBANGAN SETORAN HAFIZAH -->
                <div class="space-y-4">
                    <span class="block text-[10px] font-black text-emerald-800 uppercase tracking-wider"><i class="fa-solid fa-timeline mr-1"></i> Linimasa Catatan Sejarah Setoran &amp; Perkembangan Adab</span>
                    <div id="wali-timeline-container" class="space-y-3 max-h-72 overflow-y-auto pr-2">
                        <!-- Filled dynamically -->
                    </div>
                </div>

                <!-- SIGNATURE SECTION FOR FORMAL REPORT -->
                <div class="grid grid-cols-2 gap-4 pt-8 border-t border-slate-100 text-center text-xs mt-6">
                    <div class="space-y-12">
                        <span class="text-slate-400 font-bold block leading-none">Pendaftar / Wali Santriwati,</span>
                        <span id="wali-khs-parent-signature" class="font-extrabold text-slate-800 border-b border-slate-300 pb-1 px-8 inline-block leading-none font-semibold">Wali Santriwati</span>
                    </div>
                    <div class="space-y-12">
                        <span class="text-slate-400 font-bold block leading-none">PPSB HQ Putri 4,</span>
                        <span class="font-extrabold text-slate-800 border-b border-slate-300 pb-1 px-8 inline-block leading-none font-semibold">Ustazah Administrasi</span>
                    </div>
                </div>
            </div>

            <!-- ACTION BUTTONS BELOW KHS CARD -->
            <div class="max-w-4xl mx-auto grid grid-cols-2 gap-3 pt-3 border-t border-slate-100 no-print">
                <button onclick="printKHS()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-black py-3 rounded-2xl transition-all flex items-center justify-center gap-1.5 shadow-2xs">
                    <i class="fa-solid fa-print text-emerald-700"></i> Cetak Raport KHS
                </button>
                <button onclick="saveKHSPDF()" class="bg-emerald-700 hover:bg-emerald-855 text-white text-xs font-black py-3 rounded-2xl transition-all flex items-center justify-center gap-1.5 shadow-md">
                    <i class="fa-solid fa-file-pdf"></i> Simpan Raport PDF (1 Lembar)
                </button>
            </div>
        </div>

    </main>

    <!-- BUKTI PENDAFTARAN (RECEIPT) MODAL -->
    <div id="receipt-modal" class="hidden fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 no-print">
        <div class="bg-white rounded-3xl max-w-3xl w-full p-5 shadow-2xl flex flex-col max-h-[95vh] border border-slate-100">
            
            <div class="flex items-center justify-between pb-3 border-b border-slate-100 shrink-0">
                <div class="flex items-center gap-2">
                    <span class="p-2 bg-emerald-50 text-emerald-700 rounded-xl"><i class="fa-solid fa-file-invoice text-xs"></i></span>
                    <h3 class="font-black text-sm text-slate-900 uppercase">BUKTI REGISTRASI (KUITANSI RESMI)</h3>
                </div>
                <button onclick="closeReceiptModal()" class="text-slate-400 hover:text-slate-600 transition text-lg"><i class="fa-solid fa-circle-xmark"></i></button>
            </div>

            <!-- Scrollable Container Area -->
            <div class="overflow-y-auto flex-1 pr-1.5 space-y-4 my-4 scrollbar-thin">
                <div id="print-receipt-area" class="p-8 bg-white text-slate-900 leading-relaxed relative border-4 border-double border-emerald-900/60 shadow-xs" 
                     style="width: 100%; max-width: 680px; min-height: 870px; margin: 0 auto; box-sizing: border-box; font-family: 'Inter', sans-serif; -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; background-image: radial-gradient(circle at 50% 50%, rgba(16, 185, 129, 0.02) 0%, transparent 80%);">
                    
                    <!-- WATERMARK BACKGROUND -->
                    <div class="absolute inset-0 flex items-center justify-center pointer-events-none select-none opacity-[0.03] overflow-hidden">
                        <span class="text-emerald-900 text-6xl font-black tracking-widest uppercase rotate-[-25deg]">AL KARIMA KEDIRI</span>
                    </div>

                    <!-- Receipt Header -->
                    <div class="border-b-4 border-double border-emerald-850 pb-4 text-center">
                        <h4 class="text-[9px] font-bold text-slate-400 uppercase tracking-widest leading-none">YAYASAN AL KARIMA KEDIRI</h4>
                        <h2 class="text-sm font-black text-slate-900 uppercase tracking-tight mt-1">PESANTREN HAMALATUL QUR'AN PUTRI 4</h2>
                        <p class="text-[9px] text-emerald-800 font-bold uppercase mt-0.5 tracking-wider">Kuitansi Pembayaran &amp; Bukti Pendaftaran Santriwati Baru</p>
                        <p class="text-[8px] text-slate-400 font-semibold font-mono mt-0.5">Pare, Kediri • Telp/WA: 0838-2970-4141 • Email: hqputri4@alkarima.id</p>
                    </div>

                    <div class="flex justify-between items-center text-xs mt-4">
                        <div>
                            <span class="text-slate-400 font-bold uppercase text-[9px] block">No. Registrasi Sistem</span>
                            <strong id="receipt-reg-number" class="text-slate-800 font-black tracking-wide">-</strong>
                        </div>
                        <div class="text-right">
                            <span class="text-slate-400 font-bold uppercase text-[9px] block">Tanggal Penerbitan</span>
                            <strong id="receipt-print-date" class="text-slate-800 font-bold">-</strong>
                        </div>
                    </div>

                    <!-- Biodata & Logistics Summary Table -->
                    <div class="mt-4 bg-slate-50 border border-slate-200/60 p-4 rounded-2xl space-y-3">
                        <span class="text-[9px] font-black text-emerald-855 uppercase tracking-widest block border-b border-slate-200 pb-1.5"><i class="fa-solid fa-address-card mr-1"></i> Data Identitas Santriwati Baru</span>
                        <div class="grid grid-cols-2 gap-3 text-xs leading-tight">
                            <div>
                                <p class="text-slate-400 font-semibold">Nama Lengkap:</p>
                                <p id="rec-name" class="font-extrabold text-slate-900">-</p>
                            </div>
                            <div>
                                <p class="text-slate-400 font-semibold">Tempat, Tgl Lahir:</p>
                                <p id="rec-pobdob" class="font-bold text-slate-700">-</p>
                            </div>
                            <div>
                                <p class="text-slate-400 font-semibold">HP Wali:</p>
                                <p id="rec-phone" class="font-bold text-slate-700">-</p>
                            </div>
                            <div>
                                <p class="text-slate-400 font-semibold">Target Hafalan:</p>
                                <p id="rec-celengan" class="font-extrabold text-emerald-800">-</p>
                            </div>
                            <div>
                                <p class="text-slate-400 font-semibold">Program:</p>
                                <p id="rec-program" class="font-bold text-slate-700">-</p>
                            </div>
                            <div>
                                <p class="text-slate-400 font-semibold">Halaqah / Ustazah:</p>
                                <p id="rec-ustazah" class="font-bold text-slate-700">-</p>
                            </div>
                        </div>
                    </div>

                    <!-- Financial Transactions Breakdown Table -->
                    <div class="mt-4 space-y-2">
                        <span class="text-[9px] font-black text-emerald-855 uppercase tracking-widest block"><i class="fa-solid fa-receipt mr-1"></i> Rincian Transaksi Keuangan Masuk</span>
                        <div class="border border-slate-200 rounded-2xl overflow-hidden text-xs">
                            <table class="w-full text-left">
                                <tbody class="divide-y divide-slate-100 text-slate-600 font-semibold">
                                    <tr>
                                        <td class="p-2.5">Infaq Pendaftaran Santri Baru (PPSB)</td>
                                        <td id="rec-fee-reg" class="p-2.5 text-right text-slate-900">-</td>
                                    </tr>
                                    <tr>
                                        <td class="p-2.5">Syahriyah (SPP) 1 Bulan Pertama berjalan</td>
                                        <td id="rec-fee-spp1" class="p-2.5 text-right text-slate-900">-</td>
                                    </tr>
                                    <tr>
                                        <td class="p-2.5">Biaya Daftar Ulang &amp; Logistik Terintegrasi</td>
                                        <td id="rec-fee-rereg" class="p-2.5 text-right text-slate-900">-</td>
                                    </tr>
                                    <tr class="bg-emerald-50/50 text-slate-900 border-t border-slate-200 font-black">
                                        <td class="p-2.5 uppercase tracking-wide">Total Terbayar Lunas</td>
                                        <td id="rec-fee-total" class="p-2.5 text-right text-emerald-850">-</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <!-- Serah Terima Fasilitas & Logistik checklist block -->
                    <div class="mt-4 bg-slate-50/70 border border-slate-200 rounded-2xl p-4 space-y-2">
                        <span class="text-[9px] font-black text-emerald-855 uppercase tracking-widest block"><i class="fa-solid fa-cubes mr-1"></i> Bukti Serah Terima Fasilitas Fisik &amp; Sarana</span>
                        <div id="rec-logistics" class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-[10px] font-bold text-slate-700">
                            <!-- Filled dynamically -->
                        </div>
                    </div>

                    <!-- Secure Verifications and Codes -->
                    <div class="mt-5 border-t border-dashed border-slate-200 pt-4 flex flex-col sm:flex-row items-center justify-between gap-4 text-[10px] text-slate-400 leading-relaxed">
                        <div class="space-y-1 text-center sm:text-left">
                            <p class="font-extrabold uppercase tracking-widest text-emerald-800 flex items-center gap-1 justify-center sm:justify-start">
                                <i class="fa-solid fa-circle-check"></i> Bukti Registrasi Valid
                            </p>
                            <p class="font-medium max-w-sm">Dokumen ini diterbitkan secara otomatis oleh sistem administrasi E-Tahfidz Al Karima HQ Putri 4 dan sah tanpa tanda tangan basah fisik.</p>
                            <p class="font-mono">Secure Auth Code: <strong class="text-slate-800" id="secure-receipt-code">654321</strong></p>
                        </div>
                        <div class="border-2 border-slate-900/10 p-1.5 rounded-xl bg-white shadow-xs">
                            <div class="w-14 h-14 bg-slate-100 flex flex-col items-center justify-center border border-slate-200 rounded-lg text-slate-500">
                                <i class="fa-solid fa-qrcode text-3xl"></i>
                                <span class="text-[7px] tracking-tighter leading-none mt-0.5 uppercase font-mono">PHQ4 VERIFY</span>
                            </div>
                        </div>
                    </div>

                    <!-- Formal Signatures inside printed card -->
                    <div class="grid grid-cols-2 gap-4 pt-6 border-t border-slate-100 text-center text-xs mt-6">
                        <div class="space-y-10">
                            <span class="text-slate-400 font-bold block leading-none">Wali Santriwati Pendaftar,</span>
                            <span id="rec-parent-sign" class="font-extrabold text-slate-800 border-b border-slate-300 pb-1 px-6 inline-block leading-none font-semibold">Wali Santriwati</span>
                        </div>
                        <div class="space-y-10">
                            <span class="text-slate-400 font-bold block leading-none">Otoritas Sekretariat PPSB,</span>
                            <span class="font-extrabold text-slate-800 border-b border-slate-300 pb-1 px-6 inline-block leading-none font-semibold">Ustazah Administrasi</span>
                        </div>
                    </div>

                    <!-- Status SPP Bulan Pertama Label -->
                    <div class="mt-4 pt-2 text-center border-t border-slate-100">
                        <span class="text-[9px] text-slate-400">Status Syahriyah (SPP) Bulan Pertama berjalan: <strong id="rec-spp" class="text-emerald-800 font-black">-</strong></span>
                    </div>

                </div>
            </div>

            <!-- Receipt Modal Actions -->
            <div class="grid grid-cols-2 gap-3 pt-3 border-t border-slate-150 shrink-0">
                <button type="button" onclick="printReceipt()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-black py-3 rounded-2xl transition-all flex items-center justify-center gap-1">
                    <i class="fa-solid fa-print"></i> Cetak Dokumen
                </button>
                <button type="button" onclick="saveReceiptPDF()" class="bg-emerald-700 hover:bg-emerald-855 text-white text-xs font-black py-3 rounded-2xl transition-all flex items-center justify-center gap-1.5">
                    <i class="fa-solid fa-file-pdf"></i> Unduh PDF Resmi
                </button>
            </div>
        </div>
    </div>

    <!-- EDIT STUDENT MODAL -->
    <div id="edit-student-modal" class="hidden fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 no-print">
        <div class="bg-white rounded-3xl max-w-4xl w-full p-6 shadow-2xl flex flex-col max-h-[95vh] border border-slate-100">
            <div class="flex items-center justify-between pb-3.5 border-b border-slate-150 shrink-0">
                <div class="flex items-center gap-2.5">
                    <span class="p-2.5 bg-blue-50 text-blue-700 rounded-2xl"><i class="fa-solid fa-user-pen text-base"></i></span>
                    <div>
                        <h3 class="font-black text-sm text-slate-900 uppercase">Edit Seluruh Data &amp; Logistik Santri</h3>
                        <p class="text-[10px] text-slate-400 font-semibold">Otoritas perubahan penuh atas biodata, sarana fisik asrama, &amp; riwayat KHS.</p>
                    </div>
                </div>
                <button onclick="closeEditStudentModal()" class="text-slate-400 hover:text-slate-600 transition text-lg"><i class="fa-solid fa-circle-xmark"></i></button>
            </div>

            <!-- Scrollable Edit Form Body -->
            <form id="admin-edit-student-form" onsubmit="handleSaveEditStudent(event)" class="overflow-y-auto flex-1 pr-1.5 space-y-5 my-4 scrollbar-thin">
                <input type="hidden" id="edit-student-id">

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-5 text-xs">
                    
                    <!-- LEFT COLUMN: BIODATA, LOGISTIK, & IDENTITAS UTAMA -->
                    <div class="space-y-4">
                        <span class="block text-[10px] font-black text-blue-900 uppercase tracking-widest pb-1 border-b border-blue-100"><i class="fa-solid fa-address-card mr-1"></i> Biodata Primer &amp; Logistik Fisik</span>
                        
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Nama Lengkap Santriwati</label>
                                <input type="text" id="edit-name" required class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-bold text-slate-900 focus:ring-2 focus:ring-blue-500">
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Tempat, Tanggal Lahir</label>
                                <input type="text" id="edit-pobdob" required class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-semibold text-slate-700 focus:ring-2 focus:ring-blue-500">
                            </div>
                        </div>

                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">No. WhatsApp Wali (Kontak Utama)</label>
                                <input type="tel" id="edit-phone" required class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-bold tracking-wide text-slate-800 focus:ring-2 focus:ring-blue-500">
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Tanggal Kedatangan</label>
                                <input type="date" id="edit-arrival-date" required class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-bold focus:ring-2 focus:ring-blue-500">
                            </div>
                        </div>

                        <div>
                            <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Alamat Domisili Lengkap Wali</label>
                            <textarea id="edit-address" rows="2" required class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none resize-none font-medium text-slate-700 focus:ring-2 focus:ring-blue-500"></textarea>
                        </div>

                        <!-- LOGISTIK INTERAKTIF DI KELAS ADMIN -->
                        <div class="bg-blue-50/50 p-4 rounded-2xl border border-blue-100/80 space-y-3">
                            <span class="block text-[9px] font-black text-blue-900 uppercase tracking-wider"><i class="fa-solid fa-boxes-packing mr-1"></i> Inventaris Logistik Fisik (Serah Terima)</span>
                            <div class="grid grid-cols-2 gap-2 text-[11px] font-bold">
                                <label class="flex items-center gap-2 p-2 bg-white border border-blue-200/50 rounded-xl cursor-pointer select-none">
                                    <input type="checkbox" id="edit-fac-buku" class="w-4 h-4 text-blue-600 focus:ring-blue-500 border-slate-300 rounded">
                                    <div>
                                        <span class="text-[10px] block text-slate-800 leading-none">Buku Pegangan</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Target harian</span>
                                    </div>
                                </label>
                                <label class="flex items-center gap-2 p-2 bg-white border border-blue-200/50 rounded-xl cursor-pointer select-none">
                                    <input type="checkbox" id="edit-fac-meja" class="w-4 h-4 text-blue-600 focus:ring-blue-500 border-slate-300 rounded">
                                    <div>
                                        <span class="text-[10px] block text-slate-800 leading-none">Meja Ngaji</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Belajar di asrama</span>
                                    </div>
                                </label>
                                <label class="flex items-center gap-2 p-2 bg-white border border-blue-200/50 rounded-xl cursor-pointer select-none">
                                    <input type="checkbox" id="edit-fac-kerudung" class="w-4 h-4 text-blue-600 focus:ring-blue-500 border-slate-300 rounded">
                                    <div>
                                        <span class="text-[10px] block text-slate-800 leading-none">Hijab Almamater</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Seragam resmi</span>
                                    </div>
                                </label>
                                <label class="flex items-center gap-2 p-2 bg-white border border-blue-200/50 rounded-xl cursor-pointer select-none">
                                    <input type="checkbox" id="edit-fac-loker" class="w-4 h-4 text-blue-600 focus:ring-blue-500 border-slate-300 rounded">
                                    <div>
                                        <span class="text-[10px] block text-slate-800 leading-none">Loker Lemari</span>
                                        <span class="text-[8px] text-slate-400 font-semibold">Lemari pakaian</span>
                                    </div>
                                </label>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Riwayat Menghafal</label>
                                <select id="edit-memorized" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-bold text-slate-700">
                                    <option value="Belum Pernah">Belum Pernah Menghafal</option>
                                    <option value="Sudah Pernah">Sudah Memiliki Hafalan</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Motivasi Menghafal</label>
                                <input type="text" id="edit-motivation" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-semibold text-slate-600">
                            </div>
                        </div>
                    </div>

                    <!-- RIGHT COLUMN: HALAQAH, TARGET, & DETAIL KEUANGAN / SPP -->
                    <div class="space-y-4">
                        <span class="block text-[10px] font-black text-emerald-900 uppercase tracking-widest pb-1 border-b border-emerald-100"><i class="fa-solid fa-graduation-cap mr-1"></i> Akademik, Penempatan, &amp; Keuangan</span>
                        
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Kamar Asrama &amp; Halaqah</label>
                                <select id="edit-room" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-2.5 outline-none font-bold text-emerald-950">
                                    <option value="Ayu">Ustazah Ayu - Ruang Ayu (Halaqah Al-Mulk)</option>
                                    <option value="Ayuniz">Ustazah Ayu - Ruang Ayuniz (Halaqah Ar-Rahman)</option>
                                    <option value="Rima">Ustazah Rima - Ruang Rima (Halaqah Ya-Sin)</option>
                                    <option value="Nafis">Ustazah Nafis - Ruang Nafis (Halaqah Al-Waqi'ah)</option>
                                </select>
                            </div>
                            <div class="grid grid-cols-3 gap-1.5">
                                <div>
                                    <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Program</label>
                                    <select id="edit-program" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-1.5 outline-none font-bold text-slate-700 text-[11px]">
                                        <option value="Tahfidz Reguler">Reguler</option>
                                        <option value="Takhassus 30 Juz">Takhassus</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Celengan</label>
                                    <input type="text" id="edit-celengan" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-1.5 outline-none font-bold text-center text-[11px]">
                                </div>
                                <div>
                                    <label class="block text-[9px] font-bold text-slate-500 uppercase mb-1">Total Juz</label>
                                    <input type="number" step="0.1" id="edit-total-juz" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-1.5 outline-none font-bold text-center text-[11px] text-emerald-900">
                                </div>
                            </div>
                        </div>

                        <!-- DETAIL INPUT PERKEMBANGAN DARI USTAZAH -->
                        <div class="bg-emerald-50/40 p-4 rounded-2xl border border-emerald-100 space-y-3">
                            <span class="block text-[9px] font-black text-emerald-900 uppercase tracking-wider"><i class="fa-solid fa-book-open mr-1"></i> Data Setoran Hafalan &amp; Catatan Perkembangan</span>
                            
                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="block text-[8px] font-bold text-emerald-800 uppercase mb-0.5">Setoran Awal</label>
                                    <input type="text" id="edit-setoran-awal" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none font-semibold">
                                </div>
                                <div>
                                    <label class="block text-[8px] font-bold text-emerald-800 uppercase mb-0.5">Setoran Akhir</label>
                                    <input type="text" id="edit-setoran-akhir" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none font-semibold">
                                </div>
                            </div>

                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="block text-[8px] font-bold text-emerald-800 uppercase mb-0.5">Target Mingguan</label>
                                    <input type="text" id="edit-target-mingguan" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none font-semibold">
                                </div>
                                <div>
                                    <label class="block text-[8px] font-bold text-emerald-800 uppercase mb-0.5">Status Capaian</label>
                                    <select id="edit-status-capaian" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none font-bold">
                                        <option value="Tercapai">Tercapai</option>
                                        <option value="Belum Tercapai">Belum Tercapai</option>
                                    </select>
                                </div>
                            </div>

                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="block text-[8px] font-bold text-emerald-800 uppercase mb-0.5">Kelebihan Adab/Hafalan (+)</label>
                                    <textarea id="edit-positive" rows="2" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none resize-none font-medium"></textarea>
                                </div>
                                <div>
                                    <label class="block text-[8px] font-bold text-emerald-800 uppercase mb-0.5">Catatan Evaluasi (-)</label>
                                    <textarea id="edit-negative" rows="2" class="w-full bg-white border border-slate-200 rounded-xl p-2 resize-none font-medium outline-none"></textarea>
                                </div>
                            </div>
                        </div>

                        <!-- KELOLA DETAIL STATUS KEUANGAN ADM -->
                        <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-3">
                            <span class="block text-[9px] font-black text-slate-800 uppercase tracking-wider"><i class="fa-solid fa-file-invoice-dollar mr-1"></i> Pengaturan Status Administrasi Keuangan</span>
                            
                            <!-- SPP MONTH BY MONTH DETAILED TRACKER CHECKBOXES -->
                            <div class="bg-white p-3 rounded-2xl border border-slate-150 space-y-2">
                                <span class="block text-[8px] font-black text-emerald-900 uppercase tracking-wider"><i class="fa-solid fa-calendar-days"></i> Ceklis Bulanan Syahriyah SPP (Lunas)</span>
                                <div class="grid grid-cols-4 gap-1.5" id="edit-spp-months-container">
                                    <!-- Populated dynamically with checkboxes -->
                                </div>
                            </div>

                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="block text-[8px] font-bold text-slate-500 uppercase mb-1">Status Daftar Ulang</label>
                                    <select id="edit-daftarulang" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none font-bold text-slate-700">
                                        <option value="Lunas">Selesai (Lunas)</option>
                                        <option value="Belum Lunas">Pending (Belum)</option>
                                        <option value="Cicil">Mencicil (Cicil)</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-[8px] font-bold text-slate-500 uppercase mb-1">Status Keaktifan</label>
                                    <select id="edit-inhalaqah" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none font-bold text-slate-700">
                                        <option value="true">Aktif Mengaji</option>
                                        <option value="false">Pending (Menunggu)</option>
                                    </select>
                                </div>
                            </div>
                            <div>
                                <label class="block text-[8px] font-bold text-slate-500 uppercase mb-1">Keterangan Lain-lain (Sakit/Izin/Buku Keluar)</label>
                                <textarea id="edit-catatan-lain" rows="1" class="w-full bg-white border border-slate-200 rounded-xl p-2 outline-none resize-none font-medium text-slate-600"></textarea>
                            </div>
                        </div>

                    </div>
                </div>

                <!-- Action Button Row -->
                <div class="grid grid-cols-2 gap-3 pt-3.5 border-t border-slate-150 shrink-0">
                    <button type="button" onclick="closeEditStudentModal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold py-3 rounded-xl transition-all">
                        Batalkan Perubahan
                    </button>
                    <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white text-xs font-black py-3 rounded-xl transition-all flex items-center justify-center gap-1.5 shadow-md">
                        <i class="fa-solid fa-cloud-arrow-up"></i> Simpan Seluruh Perubahan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- SUPABASE CONFIG MODAL -->
    <div id="supabase-config-modal" class="hidden fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 no-print">
        <div class="bg-white rounded-3xl max-w-lg w-full p-6 shadow-2xl border border-slate-100 flex flex-col max-h-[90vh]">
            <div class="flex items-center justify-between pb-3 border-b border-slate-100 shrink-0">
                <div class="flex items-center gap-2">
                    <span class="p-2 bg-emerald-50 text-emerald-700 rounded-xl"><i class="fa-solid fa-database text-xs"></i></span>
                    <h3 class="font-black text-sm text-slate-900 uppercase">Hubungkan Supabase Cloud</h3>
                </div>
                <button onclick="closeSupabaseConfigModal()" class="text-slate-400 hover:text-slate-600 transition text-lg"><i class="fa-solid fa-circle-xmark"></i></button>
            </div>
            
            <div class="overflow-y-auto flex-1 pr-1.5 space-y-4 my-3 text-xs leading-relaxed">
                <p class="text-slate-500 font-semibold">
                    Sambungkan sistem asrama Anda ke proyek cloud database Supabase secara instan untuk sinkronisasi multi-perangkat real-time.
                </p>

                <form id="supabase-config-form" onsubmit="handleSaveSupabaseConfig(event)" class="space-y-4">
                    <div>
                        <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1">Supabase URL Proyek</label>
                        <input type="url" id="cfg-supabase-url" placeholder="https://your-project.supabase.co" class="w-full bg-slate-50 border border-slate-200 rounded-xl p-3 focus:ring-2 focus:ring-emerald-500 outline-none font-semibold">
                    </div>
                    <div>
                        <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1">Supabase Anon Public API Key</label>
                        <textarea id="cfg-supabase-key" rows="2" placeholder="eyJhbGciOiJIUzI1NiIs..." class="w-full bg-slate-50 border border-slate-200 rounded-xl p-3 focus:ring-2 focus:ring-emerald-500 outline-none font-mono text-[10px] resize-none"></textarea>
                    </div>

                    <div class="bg-slate-50 p-3 rounded-2xl border border-slate-200 space-y-2">
                        <div class="flex justify-between items-center">
                            <span class="font-black text-[9px] uppercase tracking-wider text-slate-600"><i class="fa-solid fa-code mr-1"></i> Jalankan SQL Schema di Supabase Editor:</span>
                            <button type="button" onclick="copySupabaseSchema()" class="bg-emerald-50 hover:bg-emerald-100 text-emerald-800 text-[9px] px-2 py-1 rounded font-black border border-emerald-200 transition">
                                <i class="fa-solid fa-copy"></i> Salin SQL
                            </button>
                        </div>
                        <pre class="bg-slate-950 text-emerald-400 p-2.5 rounded-lg text-[9px] font-mono overflow-x-auto max-h-32">
-- BERSIHKAN TABEL LAMA JIKA SUDAH ADA
DROP TABLE IF EXISTS "tahfidz_logs";
DROP TABLE IF EXISTS "santri_students";

-- BUAT TABEL DENGAN FORMAT STANDAR SNAKE_CASE
CREATE TABLE "santri_students" (
  "id" text PRIMARY KEY,
  "name" text,
  "pob_dob" text,
  "address" text,
  "parent_phone" text,
  "memorized_before" text,
  "celengan_target" text,
  "motivation" text,
  "arrival_date" text,
  "room" text,
  "program" text,
  "payment_status" text,
  "spp_months" jsonb,
  "fac_buku" boolean,
  "fac_meja" boolean,
  "fac_kerudung" boolean,
  "fac_loker" boolean,
  "in_halaqah" boolean,
  "total_juz" float8,
  "setoran_awal" text,
  "setoran_akhir" text,
  "target_mingguan" text,
  "status_capaian" text,
  "perkembangan_positif" text,
  "catatan_negatif" text,
  "daftar_ulang_status" text,
  "catatan_lain" text
);

CREATE TABLE "tahfidz_logs" (
  "id" text PRIMARY KEY,
  "student_id" text,
  "date" text,
  "setoran_awal" text,
  "setoran_akhir" text,
  "total_juz" float8,
  "pos" text,
  "neg" text
);

-- MATIKAN SEC SECURITY RLS SUPABASE
ALTER TABLE "santri_students" DISABLE ROW LEVEL SECURITY;
ALTER TABLE "tahfidz_logs" DISABLE ROW LEVEL SECURITY;</pre>
                    </div>

                    <div class="grid grid-cols-2 gap-2 pt-2">
                        <button type="button" onclick="closeSupabaseConfigModal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold py-3 rounded-xl transition-all">
                            Batalkan
                        </button>
                        <button type="submit" class="bg-emerald-700 hover:bg-emerald-855 text-white font-black py-3 rounded-xl transition-all shadow-md">
                            Simpan &amp; Hubungkan
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- BEAUTIFUL CONFIRMATION MODAL -->
    <div id="confirm-modal" class="hidden fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4">
        <div class="bg-white rounded-3xl max-w-sm w-full p-6 shadow-2xl space-y-4 text-center border border-slate-100">
            <div class="w-12 h-12 bg-amber-100 text-amber-600 rounded-2xl flex items-center justify-center text-xl mx-auto">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <div class="space-y-1">
                <h3 id="confirm-title" class="text-sm font-bold text-slate-900">Konfirmasi Tindakan</h3>
                <p id="confirm-message" class="text-xs text-slate-500 leading-relaxed">Apakah Anda yakin ingin melanjutkan tindakan ini? Data yang terhapus tidak dapat dikembalikan.</p>
            </div>
            <div class="grid grid-cols-2 gap-2 pt-2">
                <button id="confirm-btn-cancel" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold py-2.5 rounded-xl transition-all">
                    Batal
                </button>
                <button id="confirm-btn-ok" class="bg-emerald-700 hover:bg-emerald-880 text-white text-xs font-bold py-2.5 rounded-xl transition-all">
                    Ya, Lanjutkan
                </button>
            </div>
        </div>
    </div>

    <!-- SEED MODAL -->
    <div id="seed-modal" class="hidden fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4">
        <div class="bg-white rounded-3xl max-w-sm w-full p-6 shadow-2xl space-y-4 text-center border border-slate-100">
            <div class="w-12 h-12 bg-emerald-100 text-emerald-600 rounded-2xl flex items-center justify-center text-xl mx-auto">
                <i class="fa-solid fa-arrows-rotate"></i>
            </div>
            <div class="space-y-1">
                <h3 class="text-sm font-bold text-slate-900">Muat Ulang Database Contoh</h3>
                <p class="text-xs text-slate-500 leading-relaxed">Apakah Anda yakin ingin memuat ulang data default? Tindakan ini akan mengganti data saat ini dengan data contoh bawaan.</p>
            </div>
            <div class="grid grid-cols-2 gap-2 pt-2">
                <button onclick="closeSeedModal()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold py-2.5 rounded-xl transition-all">
                    Batal
                </button>
                <button onclick="confirmResetSeedData()" class="bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-bold py-2.5 rounded-xl transition-all">
                    Ya, Muat Ulang
                </button>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-emerald-950 border-t border-emerald-900 text-slate-500 text-xs py-6 text-center mt-auto no-print">
        <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-3">
            <p>&copy; 2026 E-Tahfidz Al Karima HQ Putri 4. All rights reserved.</p>
            <p class="flex items-center gap-1"><i class="fa-solid fa-shield-halved text-emerald-400"></i> Portal Real-Time Sinkronisasi Cloud Otomatis</p>
        </div>
    </footer>

    <!-- CORE JAVASCRIPT LOGIC -->
    <script>
        // =========================================================================
        // KONFIGURASI DATABASE TERKONEKSI CLOUD (PRE-CONFIGURED FOR INSTANT DEPLOY)
        // =========================================================================
        const DEFAULT_SUPABASE_URL = "https://ucneuumyslkuweyyadlr.supabase.co"; 
        const DEFAULT_SUPABASE_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InVjbmV1dW15c2xrdXdleXlhZGxyIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODE3NDU5ODcsImV4cCI6MjA5NzMyMTk4N30.PXfkMU6im2eV0s1z38vtw0F36f299NQZRjyf30UNnwc"; 
        // =========================================================================

        let supabaseClient = null;
        let studentsList = []; // Sterilized (Empty)
        let tahfidzLogs = [];  // Sterilized (Empty)
        let currentRole = null; 
        let currentWaliStudent = null; 
        let isCloudMode = false;
        let adminActiveTab = 'register';
        let confirmCallback = null;

        const monthsShortList = ["Jan", "Feb", "Mar", "Apr", "Mei", "Jun", "Jul", "Agu", "Sep", "Okt", "Nov", "Des"];

        let systemPins = JSON.parse(localStorage.getItem('karima_system_pins')) || {
            'admin': 'admin4',
            'Ayu': 'ayu4',
            'Ayuniz': 'ayuniz4',
            'Rima': 'rima4',
            'Nafis': 'nafis4'
        };

        const roleLabels = {
            'admin': 'Panel Penerimaan Santriwati Baru (Admin)',
            'ustazah_Ayu': 'Halaqah Al-Mulk (Ustazah Ayu)',
            'ustazah_Ayuniz': 'Halaqah Ar-Rahman (Ustazah Ayuniz)',
            'ustazah_Rima': 'Halaqah Ya-Sin (Ustazah Rima)',
            'ustazah_Nafis': 'Halaqah Al-Waqi\'ah (Ustazah Nafis)',
            'wali': 'KHS Digital Wali Santri'
        };

        function getHalaqahName(roomKey) {
            const mapping = {
                "Ayu": "Halaqah Al-Mulk (Ruang Ayu)",
                "Ayuniz": "Halaqah Ar-Rahman (Ruang Ayuniz)",
                "Rima": "Halaqah Ya-Sin (Ruang Rima)",
                "Nafis": "Halaqah Al-Waqi'ah (Ruang Nafis)"
            };
            return mapping[roomKey] || "Halaqah Umum";
        }

        function getFormattedMonthWeek(dateString) {
            if (!dateString) return "-";
            if (dateString === "Inisialisasi") return "Inisialisasi";
            const d = new Date(dateString);
            if (isNaN(d.getTime())) return dateString;
            const months = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
            const monthName = months[d.getMonth()];
            const day = d.getDate();
            const weekNum = Math.ceil(day / 7);
            return `${monthName} Minggu ke-${weekNum}`;
        }

        function initVisitorCounter() {
            let visitors = localStorage.getItem('karima_visitor_count');
            if (!visitors) {
                visitors = "156"; 
            } else {
                visitors = (parseInt(visitors) + 1).toString();
            }
            localStorage.setItem('karima_visitor_count', visitors);

            const gateCount = document.getElementById('gate-visitor-count');
            const headerCount = document.getElementById('header-visitor-count');
            const gateOnline = document.getElementById('gate-online-count');

            if (gateCount) gateCount.textContent = parseInt(visitors).toLocaleString('id-ID');
            if (headerCount) headerCount.textContent = parseInt(visitors).toLocaleString('id-ID');
            
            const simulatedOnline = Math.floor(Math.random() * 5) + 6; 
            if (gateOnline) gateOnline.textContent = `${simulatedOnline} Online`;
        }

        function loadLocalData() {
            const storedStudents = localStorage.getItem('karima_students');
            const storedLogs = localStorage.getItem('karima_logs');
            
            if (storedStudents) {
                try {
                    studentsList = JSON.parse(storedStudents);
                    studentsList = studentsList.map(s => {
                        if (!s.sppMonths) {
                            s.sppMonths = {
                                "Jan": s.paymentStatus || "Belum Lunas", "Feb": "Belum Lunas", "Mar": "Belum Lunas", "Apr": "Belum Lunas",
                                "Mei": "Belum Lunas", "Jun": "Belum Lunas", "Jul": "Belum Lunas", "Agu": "Belum Lunas",
                                "Sep": "Belum Lunas", "Okt": "Belum Lunas", "Nov": "Belum Lunas", "Des": "Belum Lunas"
                            };
                        }
                        if (s.inHalaqah === undefined) s.inHalaqah = true;
                        if (!s.daftarUlangStatus) s.daftarUlangStatus = "Belum Lunas";
                        return s;
                    });
                } catch (e) {
                    studentsList = [];
                }
            } else {
                studentsList = [];
                localStorage.setItem('karima_students', JSON.stringify(studentsList));
            }

            if (storedLogs) {
                try {
                    tahfidzLogs = JSON.parse(storedLogs);
                } catch (e) {
                    tahfidzLogs = [];
                }
            } else {
                tahfidzLogs = [];
                localStorage.setItem('karima_logs', JSON.stringify(tahfidzLogs));
            }
        }

        function saveLocalData() {
            localStorage.setItem('karima_students', JSON.stringify(studentsList));
            localStorage.setItem('karima_logs', JSON.stringify(tahfidzLogs));
        }

        function initSupabase() {
            const url = localStorage.getItem('karima_supabase_url') || DEFAULT_SUPABASE_URL || "";
            let key = localStorage.getItem('karima_supabase_key') || DEFAULT_SUPABASE_KEY || "";
            
            // Proteksi kuat: Bersihkan sisa vsn query parameter jika pengguna menyimpan token bermasalah
            if (key.includes('&vsn=')) {
                key = key.split('&vsn=')[0];
            }

            const storageTitle = document.getElementById('storage-mode-title');
            const storageDesc = document.getElementById('storage-mode-desc');
            const syncBadge = document.getElementById('header-sync-badge');
            const syncTimeLabel = document.getElementById('sync-time-label');

            loadLocalData();

            if (url && url !== "https://your-project.supabase.co" && key && key !== "your-anon-key-here" && typeof supabase !== 'undefined') {
                try {
                    supabaseClient = supabase.createClient(url, key, {
                        auth: { persistSession: false }
                    });
                    isCloudMode = true;
                    if (storageTitle) storageTitle.innerText = "Sinkronisasi Cloud Aktif";
                    if (storageDesc) storageDesc.innerText = "Koneksi multi-perangkat stabil. Perubahan data langsung terupdate secara real-time.";
                    if (syncBadge) {
                        syncBadge.classList.remove('hidden');
                        if (syncTimeLabel) syncTimeLabel.innerText = "TERHUBUNG";
                    }

                    // Muat data dari cloud dan jalankan langganan background polling
                    fetchCloudData().then(() => {
                        setupRealtimeSubscription();
                    });
                    return;
                } catch (e) {
                    console.error("Gagal inisialisasi Supabase: ", e);
                    isCloudMode = false;
                }
            }
            
            supabaseClient = null;
            isCloudMode = false;
            if (storageTitle) storageTitle.innerText = "Penyimpanan Lokal Aktif";
            if (storageDesc) storageDesc.innerText = "Laporan tahfidz tersimpan aman di memori lokal penjelajah Anda. Hubungkan ke Supabase untuk cadangan permanen.";
            if (syncBadge) syncBadge.classList.add('hidden');
            setupActiveWorkspace();
        }

        // =========================================================================
        // SAFE HTTP-POLLING SYNC (SUPPRESSED WEBSOCKET PREVIEW CRASH FOR CLEAN CONSOLE)
        // =========================================================================
        let pollingInterval = null;
        
        function setupRealtimeSubscription() {
            if (pollingInterval) {
                clearInterval(pollingInterval);
            }
            
            // Atur polling interval 5 detik sebagai cadangan utama yang handal
            pollingInterval = setInterval(() => {
                if (isCloudMode && supabaseClient && document.visibilityState === 'visible') {
                    fetchCloudDataSilent();
                }
            }, 5000); 

            document.removeEventListener('visibilitychange', handleVisibilityChange);
            document.addEventListener('visibilitychange', handleVisibilityChange);

            // DETEKSI SECARA OTOMATIS APAKAH BERJALAN DI DALAM SANDBOX PREVIEW (CANVAS)
            const isSandboxed = window.location.hostname.includes('goog') || window.self !== window.top;

            if (isSandboxed) {
                // Di dalam editor preview, gunakan HTTP Polling secara senyap & abaikan inisialisasi Websocket
                const syncTimeLabel = document.getElementById('sync-time-label');
                if (syncTimeLabel) syncTimeLabel.innerText = "TERHUBUNG (POLLING)";
                return; 
            }

            // JIKA DI LUAR EDITOR / HP ASLI / PRODUKSI, AKTIFKAN WEBSOCKET REAL-TIME SECARA INSTAN
            if (isCloudMode && supabaseClient && typeof window.WebSocket !== 'undefined') {
                try {
                    const subscription = supabaseClient.channel('realtime-updates')
                        .on('postgres_changes', { event: '*', schema: 'public', table: 'santri_students' }, () => {
                            fetchCloudDataSilent();
                        })
                        .on('postgres_changes', { event: '*', schema: 'public', table: 'tahfidz_logs' }, () => {
                            fetchCloudDataSilent();
                        });
                        
                    subscription.subscribe((status) => {
                        const syncTimeLabel = document.getElementById('sync-time-label');
                        if (status === 'SUBSCRIBED') {
                            if (syncTimeLabel) syncTimeLabel.innerText = "REAL-TIME AKTIF";
                        }
                    });
                } catch (err) {
                    console.log("Websocket dinonaktifkan oleh browser, menggunakan sistem Polling HTTP.");
                }
            }
        }

        function handleVisibilityChange() {
            if (document.visibilityState === 'visible') {
                if (isCloudMode && supabaseClient) {
                    fetchCloudDataSilent();
                }
            }
        }

        // =========================================================================
        // TRANSLATION LAYER: CAMELCASE <-> SNAKE_CASE MAPPING
        // =========================================================================
        function mapStudentToDb(s) {
            return {
                id: s.id,
                name: s.name,
                pob_dob: s.pobDob,
                address: s.address,
                parent_phone: s.parentPhone,
                memorized_before: s.memorizedBefore,
                celengan_target: s.celenganTarget,
                motivation: s.motivation,
                arrival_date: s.arrivalDate,
                room: s.room,
                program: s.program,
                payment_status: s.paymentStatus,
                spp_months: s.sppMonths,
                fac_buku: !!s.facBuku,
                fac_meja: !!s.facMeja,
                fac_kerudung: !!s.facKerudung,
                fac_loker: !!s.facLoker,
                in_halaqah: !!s.inHalaqah,
                total_juz: parseFloat(s.totalJuz) || 0,
                setoran_awal: s.setoranAwal,
                setoran_akhir: s.setoranAkhir,
                target_mingguan: s.targetMingguan,
                status_capaian: s.statusCapaian,
                perkembangan_positif: s.perkembanganPositif,
                catatan_negatif: s.catatanNegatif,
                daftar_ulang_status: s.daftarUlangStatus,
                catatan_lain: s.catatanLain

            };
        }

        function mapStudentFromDb(db) {
            return {
                id: db.id,
                name: db.name,
                pobDob: db.pob_dob,
                address: db.address,
                parentPhone: db.parent_phone,
                memorizedBefore: db.memorized_before,
                celenganTarget: db.celengan_target,
                motivation: db.motivation,
                arrivalDate: db.arrival_date,
                room: db.room,
                program: db.program,
                paymentStatus: db.payment_status,
                sppMonths: db.spp_months,
                facBuku: !!db.fac_buku,
                facMeja: !!db.fac_meja,
                facKerudung: !!db.fac_kerudung,
                facLoker: !!db.fac_loker,
                inHalaqah: !!db.in_halaqah,
                totalJuz: parseFloat(db.total_juz) || 0,
                setoranAwal: db.setoran_awal,
                setoranAkhir: db.setoran_akhir,
                targetMingguan: db.target_mingguan,
                statusCapaian: db.status_capaian,
                fasohah: db.fasohah ,
                kelancaran: db.kelancaran,
                perkembanganPositif: db.perkembangan_positif,
                catatanNegatif: db.catatan_negatif,
                daftarUlangStatus: db.daftar_ulang_status,
                catatanLain: db.catatan_lain
            };
        }

        function mapLogToDb(l) {
            return {
                id: l.id,
                student_id: l.student_id,
                date: l.date,
                setoran_awal: l.setoran_awal || l.setoranAwal,
                setoran_akhir: l.setoran_akhir || l.setoranAkhir,
                total_juz: parseFloat(l.total_juz || l.totalJuz) || 0,
                pos: l.pos,
                neg: l.neg
            };
        }

        function mapLogFromDb(db) {
            return {
                id: db.id,
                student_id: db.student_id,
                date: db.date,
                setoran_awal: db.setoran_awal,
                setoran_akhir: db.setoran_akhir,
                total_juz: parseFloat(db.total_juz) || 0,
                pos: db.pos,
                neg: db.neg
            };
        }

        async function fetchCloudData() {
            if (!supabaseClient) return;
            try {
                let { data: st, error: err1 } = await supabaseClient.from('santri_students').select('*');
                let { data: lg, error: err2 } = await supabaseClient.from('tahfidz_logs').select('*');

                if (err1 || err2) {
                    const errMsg = (err1?.message || err2?.message || 'Akses tidak sah/RLS aktif');
                    console.error("Koneksi Supabase bermasalah, mengalihkan ke mode luring/lokal.", err1, err2);
                    isCloudMode = false; // Matikan cloud mode agar tidak merusak data lokal yang sehat
                    const syncBadge = document.getElementById('header-sync-badge');
                    if (syncBadge) syncBadge.classList.add('hidden');
                    showToast(`Terbaca Luring. Cloud Gagal: ${errMsg}`, "error");
                    setupActiveWorkspace();
                    return;
                }

                if (st && st.length === 0 && studentsList.length > 0) {
                    showToast("Mencadangkan data lokal Anda ke cloud Supabase secara permanen...", "info");
                    for (let s of studentsList) {
                        const dbPayload = mapStudentToDb(s);
                        const { error } = await supabaseClient.from('santri_students').insert([dbPayload]);
                        if (error) console.error("Gagal backup student:", error.message);
                    }
                    for (let l of tahfidzLogs) {
                        const dbPayload = mapLogToDb(l);
                        const { error } = await supabaseClient.from('tahfidz_logs').insert([dbPayload]);
                        if (error) console.error("Gagal backup log:", error.message);
                    }
                    showToast("Pencadangan awan pertama berhasil dilakukan!", "success");
                } else {
                    if (st && st.length > 0) {
                        studentsList = st.map(mapStudentFromDb);
                    } else {
                        studentsList = [];
                    }
                    if (lg && lg.length > 0) {
                        tahfidzLogs = lg.map(mapLogFromDb);
                    } else {
                        tahfidzLogs = [];
                    }
                }

                studentsList = studentsList.map(s => {
                    if (!s.sppMonths) {
                        s.sppMonths = {
                            "Jan": s.paymentStatus || "Belum Lunas", "Feb": "Belum Lunas", "Mar": "Belum Lunas", "Apr": "Belum Lunas",
                            "Mei": "Belum Lunas", "Jun": "Belum Lunas", "Jul": "Belum Lunas", "Agu": "Belum Lunas",
                            "Sep": "Belum Lunas", "Okt": "Belum Lunas", "Nov": "Belum Lunas", "Des": "Belum Lunas"
                        };
                    }
                    if (s.inHalaqah === undefined) s.inHalaqah = true;
                    if (!s.daftarUlangStatus) s.daftarUlangStatus = "Belum Lunas";
                    return s;
                });

                studentsList.sort((a, b) => a.name.localeCompare(b.name));
                tahfidzLogs.sort((a, b) => new Date(b.date) - new Date(a.date));

                saveLocalData();
                setupActiveWorkspace();
            } catch (err) {
                console.error("Sinkronisasi cloud gagal fatal: ", err);
                isCloudMode = false;
                const syncBadge = document.getElementById('header-sync-badge');
                if (syncBadge) syncBadge.classList.add('hidden');
                setupActiveWorkspace();
            }
        }

        async function fetchCloudDataSilent() {
            if (!supabaseClient || !isCloudMode) return;
            try {
                let { data: st, error: err1 } = await supabaseClient.from('santri_students').select('*');
                let { data: lg, error: err2 } = await supabaseClient.from('tahfidz_logs').select('*');

                if (err1 || err2) {
                    console.warn("Silent sync terhambat. Menjaga integritas data lokal aktif.", err1, err2);
                    return; 
                }

                if (st && st.length > 0) {
                    studentsList = st.map(mapStudentFromDb).map(s => {
                        if (!s.sppMonths) {
                            s.sppMonths = {
                                "Jan": s.paymentStatus || "Belum Lunas", "Feb": "Belum Lunas", "Mar": "Belum Lunas", "Apr": "Belum Lunas",
                                "Mei": "Belum Lunas", "Jun": "Belum Lunas", "Jul": "Belum Lunas", "Agu": "Belum Lunas",
                                "Sep": "Belum Lunas", "Okt": "Belum Lunas", "Nov": "Belum Lunas", "Des": "Belum Lunas"
                            };
                        }
                        if (s.inHalaqah === undefined) s.inHalaqah = true;
                        if (!s.daftarUlangStatus) s.daftarUlangStatus = "Belum Lunas";
                        return s;
                    });
                    studentsList.sort((a, b) => a.name.localeCompare(b.name));
                }
                
                if (lg && lg.length > 0) {
                    tahfidzLogs = lg.map(mapLogFromDb);
                    tahfidzLogs.sort((a, b) => new Date(b.date) - new Date(a.date));
                }

                saveLocalData();
                
                // Perbarui tampilan interface aktif secara on-the-fly
                if (currentRole) {
                    if (currentRole === 'admin') {
                        recalculateAdminStats();
                        renderAdminStudentsDirectory();
                    } else if (currentRole.startsWith('ustazah_')) {
                        renderUstazahInterface();
                    } else if (currentRole === 'wali' && currentWaliStudent) {
                        const updated = studentsList.find(s => s.id === currentWaliStudent.id);
                        if (updated) {
                            currentWaliStudent = updated;
                            renderWaliKHS(currentWaliStudent.id);
                        }
                    }
                }
            } catch (e) {
                console.error("Gagal menyinkronkan data di latar belakang: ", e);
            }
        }

        async function syncInsertToCloud(table, payload) {
            if (!supabaseClient || !isCloudMode) return;
            try { 
                let dbPayload = payload;
                if (table === 'santri_students') dbPayload = mapStudentToDb(payload);
                if (table === 'tahfidz_logs') dbPayload = mapLogToDb(payload);

                const { error } = await supabaseClient.from(table).insert([dbPayload]); 
                if (error) {
                    console.error("Gagal mengunggah data baru ke Cloud: ", error);
                    showToast(`Gagal kirim Cloud: ${error.message} (Cek RLS di SQL Editor)`, "error");
                }
            } catch (err) { 
                console.error("Exception saat insert cloud: ", err); 
            }
        }

        async function syncUpdateToCloud(table, recordId, payload) {
    if (!supabaseClient || !isCloudMode) return;
    try {
        let dbPayload = payload;
        if (table === 'santri_students') {
            dbPayload = {};
            const mappings = {
                id: 'id',
                name: 'name',
                pobDob: 'pob_dob',
                address: 'address',
                parentPhone: 'parent_phone',
                memorizedBefore: 'memorized_before',
                celenganTarget: 'celengan_target',
                motivation: 'motivation',
                arrivalDate: 'arrival_date',
                room: 'room',
                program: 'program',
                paymentStatus: 'payment_status',
                sppMonths: 'spp_months',
                facBuku: 'fac_buku',
                facMeja: 'fac_meja',
                facKerudung: 'fac_kerudung',
                facLoker: 'fac_loker',
                inHalaqah: 'in_halaqah',
                totalJuz: 'total_juz',
                setoranAwal: 'setoran_awal',
                setoranAkhir: 'setoran_akhir',
                targetMingguan: 'target_mingguan',
                statusCapaian: 'status_capaian',
                fasohah: 'fasohah',
                kelancaran: 'kelancaran',
                perkembanganPositif: 'perkembangan_positif',
                catatanNegatif: 'catatan_negatif',
                daftarUlangStatus: 'daftar_ulang_status',
                catatanLain: 'catatan_lain'
            };
            for (let key in payload) {
                if (mappings[key]) {
                    dbPayload[mappings[key]] = payload[key];
                } else {
                    dbPayload[key] = payload[key];
                }
            }
        }
        if (table === 'tahfidz_logs') {
            dbPayload = mapLogToDb(payload);
        }
        const { error } = await supabaseClient.from(table).update(dbPayload).eq('id', recordId);
        if (error) {
            console.error("Gagal memperbarui data di Cloud: ", error);
            showToast(`Gagal update Cloud: ${error.message} (Cek RLS di SQL Editor)`, "error");
        }
    } catch (err) {
        console.error("Exception saat update cloud: ", err);
    }
}

        async function syncDeleteFromCloud(table, recordId) {
            if (!supabaseClient || !isCloudMode) return;
            try { 
                const { error } = await supabaseClient.from(table).delete().eq('id', recordId); 
                if (error) {
                    console.error("Gagal menghapus data di Cloud: ", error);
                    showToast(`Gagal hapus Cloud: ${error.message}`, "error");
                }
            } catch (err) { 
                console.error("Exception saat hapus cloud: ", err); 
            }
        }

        window.setGateRole = function(role) {
            document.getElementById('selected-gate-role').value = role;
            const btnWali = document.getElementById('role-btn-wali');
            const btnUstazah = document.getElementById('role-btn-ustazah');
            const btnAdmin = document.getElementById('role-btn-admin');
            const wrapWali = document.getElementById('gate-input-wrapper-wali');
            const wrapUstazah = document.getElementById('gate-input-wrapper-ustazah');
            const wrapPin = document.getElementById('gate-input-wrapper-pin');

            [btnWali, btnUstazah, btnAdmin].forEach(btn => {
                btn.className = "py-2.5 rounded-xl text-xs font-bold text-slate-500 transition-all";
            });

            if (role === 'wali') {
                btnWali.className = "py-2.5 rounded-xl text-xs font-black transition-all bg-white text-emerald-900 shadow-xs";
                wrapWali.classList.remove('hidden');
                wrapUstazah.classList.add('hidden');
                wrapPin.classList.add('hidden');
            } else if (role === 'ustazah') {
                btnUstazah.className = "py-2.5 rounded-xl text-xs font-black transition-all bg-white text-emerald-900 shadow-xs";
                wrapWali.classList.add('hidden');
                wrapUstazah.classList.remove('hidden');
                wrapPin.classList.remove('hidden');
            } else {
                btnAdmin.className = "py-2.5 rounded-xl text-xs font-black transition-all bg-white text-emerald-900 shadow-xs";
                wrapWali.classList.add('hidden');
                wrapUstazah.classList.add('hidden');
                wrapPin.classList.remove('hidden');
            }
        };

        window.handleWaliSearch = function() {
            const query = document.getElementById('gate-wali-student-name').value.toLowerCase().trim();
            const box = document.getElementById('gate-wali-matches-box');
            const list = document.getElementById('gate-wali-matches-list');
            
            if (!query) {
                box.classList.add('hidden');
                return;
            }

            const matches = studentsList.filter(s => s.name.toLowerCase().includes(query));
            list.innerHTML = '';

            if (matches.length > 0) {
                box.classList.remove('hidden');
                matches.forEach(s => {
                    const d = document.createElement('div');
                    d.className = "p-2 hover:bg-emerald-50 rounded-xl cursor-pointer font-bold text-xs text-slate-700 transition flex justify-between items-center";
                    d.innerHTML = `<span>${s.name}</span> <span class="text-[9px] bg-slate-200 px-1.5 py-0.5 rounded-md text-slate-500">${s.room}</span>`;
                    d.onclick = () => {
                        document.getElementById('gate-wali-student-name').value = s.name;
                        box.classList.add('hidden');
                    };
                    list.appendChild(d);
                });
            } else {
                box.classList.remove('hidden');
                list.innerHTML = `<p class="text-[10px] text-slate-400 font-bold p-2 text-center">Tidak ditemukan santriwati.</p>`;
            }
        };

        window.handleGateLogin = function(e) {
            e.preventDefault();
            const role = document.getElementById('selected-gate-role').value;
            
            if (role === 'wali') {
                const nameInput = document.getElementById('gate-wali-student-name').value.trim();
                const matched = studentsList.find(s => s.name.toLowerCase() === nameInput.toLowerCase());
                if (matched) {
                    currentRole = 'wali';
                    currentWaliStudent = matched;
                    showToast(`Sesi KHS Privat ${matched.name} berhasil dimuat!`, 'success');
                    triggerConfettiFeedback('success');
                    enterWorkspace();
                } else {
                    showToast("Nama lengkap putri Anda tidak ditemukan dalam arsip pendaftaran.", "error");
                }
            } else if (role === 'ustazah') {
                const selectedUstazah = document.getElementById('gate-ustazah-select').value;
                const pinInput = document.getElementById('gate-pin').value;
                if (systemPins[selectedUstazah] === pinInput) {
                    currentRole = `ustazah_${selectedUstazah}`;
                    showToast(`Selamat datang di Halaqah Ustazah ${selectedUstazah}!`, 'success');
                    triggerConfettiFeedback('success');
                    enterWorkspace();
                } else {
                    showToast("Sandi PIN Otoritas Pembina Halaqah salah.", "error");
                }
            } else if (role === 'admin') {
                const pinInput = document.getElementById('gate-pin').value;
                if (systemPins['admin'] === pinInput) {
                    currentRole = 'admin';
                    showToast("Akses Otoritas Panel Administrasi Induk diizinkan.", "success");
                    triggerConfettiFeedback('success');
                    enterWorkspace();
                } else {
                    showToast("Sandi PIN Otoritas Admin Utama salah.", "error");
                }
            }
            window.addEventListener('DOMContentLoaded', () => {
    window.scrollTo({
        top: 0,
        behavior: 'smooth' // gunakan 'auto' jika ingin instan tanpa animasi scroll
    });
});
        };

        function enterWorkspace() {
            document.getElementById('gate-screen').classList.add('hidden');
            document.getElementById('main-app-header').classList.remove('hidden');
            document.getElementById('main-app-container').classList.remove('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
            
            // Tambahkan kelas transisi premium
            const workspace = document.getElementById('main-app-container');
            workspace.classList.add('fade-in-workspace');
            
            let labelText = roleLabels[currentRole] || "Pengguna";
            document.getElementById('active-user-badge').innerText = labelText;

            setupActiveWorkspace();
        }

        window.handleLogout = function() {
            currentRole = null;
            currentWaliStudent = null;
            document.getElementById('gate-screen').classList.remove('hidden');
            document.getElementById('main-app-header').classList.add('hidden');
            document.getElementById('main-app-container').classList.add('hidden');
            document.getElementById('gate-pin').value = '';
            document.getElementById('gate-wali-student-name').value = '';
            
            const workspace = document.getElementById('main-app-container');
            workspace.classList.remove('fade-in-workspace');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        };

        function setupActiveWorkspace() {
            document.getElementById('view-admin').classList.add('hidden');
            document.getElementById('view-ustazah').classList.add('hidden');
            document.getElementById('view-wali').classList.add('hidden');

            const visitorBadge = document.getElementById('header-visitor-badge');
            if (visitorBadge) {
                if (currentRole === 'admin' || (currentRole && currentRole.startsWith('ustazah_'))) {
                    visitorBadge.classList.remove('hidden');
                } else {
                    visitorBadge.classList.add('hidden');
                }
            }

            if (currentRole === 'admin') {
                document.getElementById('view-admin').classList.remove('hidden');
                recalculateAdminStats();
                switchAdminTab(adminActiveTab);
                
                document.getElementById('pin-cfg-admin').value = systemPins['admin'];
                document.getElementById('pin-cfg-ayu').value = systemPins['Ayu'];
                document.getElementById('pin-cfg-ayuniz').value = systemPins['Ayuniz'];
                document.getElementById('pin-cfg-rima').value = systemPins['Rima'];
                document.getElementById('pin-cfg-nafis').value = systemPins['Nafis'];
            } else if (currentRole && currentRole.startsWith('ustazah_')) {
                document.getElementById('view-ustazah').classList.remove('hidden');
                renderUstazahInterface();
            } else if (currentRole === 'wali' && currentWaliStudent) {
                document.getElementById('view-wali').classList.remove('hidden');
                renderWaliKHS(currentWaliStudent.id);
            }
        }

        window.switchAdminTab = function(tabName) {
            adminActiveTab = tabName;
            const btnReg = document.getElementById('admin-tab-register');
            const btnDir = document.getElementById('admin-tab-directory');
            const contReg = document.getElementById('admin-content-register');
            const contDir = document.getElementById('admin-content-directory');

            btnReg.className = "border-transparent text-slate-500 hover:text-slate-700 hover:border-slate-300 border-b-2 py-4 px-1 text-sm font-bold flex items-center gap-2";
            btnDir.className = "border-transparent text-slate-500 hover:text-slate-700 hover:border-slate-300 border-b-2 py-4 px-1 text-sm font-bold flex items-center gap-2";
            contReg.classList.add('hidden');
            contDir.classList.add('hidden');

            if (tabName === 'register') {
                btnReg.className = "border-emerald-600 text-emerald-800 border-b-2 py-4 px-1 text-sm font-black flex items-center gap-2";
                contReg.classList.remove('hidden');
            } else {
                btnDir.className = "border-emerald-600 text-emerald-800 border-b-2 py-4 px-1 text-sm font-black flex items-center gap-2";
                contDir.classList.remove('hidden');
                renderAdminStudentsDirectory();
            }
            window.scrollTo({ top: 0, behavior: 'smooth' });
        };

        function recalculateAdminStats() {
            document.getElementById('stat-total-students').innerText = studentsList.length;
            document.getElementById('stat-active-students').innerText = studentsList.filter(s => s.inHalaqah).length;
            document.getElementById('stat-pending-students').innerText = studentsList.filter(s => !s.inHalaqah).length;
            document.getElementById('stat-paid-students').innerText = studentsList.filter(s => s.paymentStatus === 'Lunas').length;
        }

        window.handleAdminAddStudent = function(e) {
            e.preventDefault();
            const newId = "s_" + Date.now();
            const name = document.getElementById('admin-add-name').value.trim();
            const room = document.getElementById('admin-add-room').value;
            const initPaymentStatus = document.getElementById('admin-add-paystatus').value;

            const initialSppMonths = {
                "Jan": "Belum Lunas", "Feb": "Belum Lunas", "Mar": "Belum Lunas", "Apr": "Belum Lunas",
                "Mei": "Belum Lunas", "Jun": "Belum Lunas", "Jul": "Belum Lunas", "Agu": "Belum Lunas",
                "Sep": "Belum Lunas", "Okt": "Belum Lunas", "Nov": "Belum Lunas", "Des": "Belum Lunas"
            };
            
            if (initPaymentStatus === 'Lunas') {
                initialSppMonths["Jan"] = "Lunas";
            }

            const newStudent = {
                id: newId,
                name: name,
                pobDob: document.getElementById('admin-add-pobdob').value.trim(),
                address: document.getElementById('admin-add-address').value.trim(),
                parentPhone: document.getElementById('admin-add-phone').value.trim(),
                memorizedBefore: document.getElementById('admin-add-memorized').value,
                celenganTarget: document.getElementById('admin-add-celengan').value.trim(),
                motivation: document.getElementById('admin-add-motivation').value.trim() || "Mengabdi pada Al-Qur'an",
                arrivalDate: document.getElementById('admin-add-arrival-date').value,
                room: room,
                program: document.getElementById('admin-add-program').value,
                paymentStatus: initPaymentStatus,
                sppMonths: initialSppMonths,
                facBuku: document.getElementById('admin-add-fac-buku').checked,
                facMeja: document.getElementById('admin-add-fac-meja').checked,
                facKerudung: document.getElementById('admin-add-fac-kerudung').checked,
                facLoker: document.getElementById('admin-add-fac-loker').checked,
                inHalaqah: false,
                totalJuz: 0.0,
                setoranAwal: 'Belum Setoran',
                setoranAkhir: '-',
                targetMingguan: '4 Halaman',
                statusCapaian: 'Belum Tercapai',
                perkembanganPositif: 'Proses adaptasi awal asrama',
                catatanNegatif: 'Nihil',
                daftarUlangStatus: (parseInt(document.getElementById('admin-add-fee-rereg').value) > 0) ? 'Lunas' : 'Belum Lunas',
                catatanLain: 'Baru mendaftar di kesekretariat.'
            };

            const feeReg = document.getElementById('admin-add-fee-reg').checked ? 250000 : 0;
            const feeSpp = document.getElementById('admin-add-fee-spp1').checked ? 900000 : 0;
            const feeRereg = parseInt(document.getElementById('admin-add-fee-rereg').value) || 0;

            studentsList.push(newStudent);
            saveLocalData();
            syncInsertToCloud('santri_students', newStudent);

            const initialLog = {
                id: "log_" + Date.now(),
                student_id: newId,
                date: "Inisialisasi",
                setoran_awal: "Pendaftaran",
                setoran_akhir: "Santri Baru",
                total_juz: 0.0,
                pos: "Terdaftar Resmi",
                neg: "Nihil"
            };
            tahfidzLogs.push(initialLog);
            saveLocalData();
            syncInsertToCloud('tahfidz_logs', initialLog);

            showToast(`Santriwati ${name} Berhasil Didaftarkan! Data tersimpan aman.`, 'success');
            triggerConfettiFeedback('register');
            recalculateAdminStats();
            
            openReceiptModal(newStudent, feeReg, feeSpp, feeRereg);
            e.target.reset();
        };

        window.handleUpdatePins = function(e) {
            e.preventDefault();
            systemPins['admin'] = document.getElementById('pin-cfg-admin').value;
            systemPins['Ayu'] = document.getElementById('pin-cfg-ayu').value;
            systemPins['Ayuniz'] = document.getElementById('pin-cfg-ayuniz').value;
            systemPins['Rima'] = document.getElementById('pin-cfg-rima').value;
            systemPins['Nafis'] = document.getElementById('pin-cfg-nafis').value;

            localStorage.setItem('karima_system_pins', JSON.stringify(systemPins));
            showToast("Seluruh Kredensial PIN Otoritas Diperbarui!", "success");
            triggerConfettiFeedback('success');
        };

        window.renderAdminStudentsDirectory = function() {
            const listContainer = document.getElementById('admin-students-directory-list');
            const searchQ = document.getElementById('admin-search-student').value.toLowerCase().trim();
            const filterU = document.getElementById('admin-filter-ustazah').value;

            listContainer.innerHTML = '';

            let filtered = studentsList;
            if (filterU !== 'all') {
                filtered = filtered.filter(s => s.room === filterU);
            }
            if (searchQ) {
                filtered = filtered.filter(s => s.name.toLowerCase().includes(searchQ) || s.id.toLowerCase().includes(searchQ));
            }

            if (filtered.length === 0) {
                listContainer.innerHTML = `<tr><td colspan="6" class="p-8 text-center text-slate-400 font-bold">Tidak ada data santriwati yang sesuai filter.</td></tr>`;
                return;
            }

            filtered.forEach(s => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 transition border-b border-slate-100";
                
                const halaqahBadge = s.inHalaqah 
                    ? `<span class="bg-emerald-100 text-emerald-800 px-2.5 py-1 rounded-full text-[10px] font-black"><i class="fa-solid fa-circle-check"></i> Aktif Halaqah</span>`
                    : `<span class="bg-amber-100 text-amber-800 px-2.5 py-1 rounded-full text-[10px] font-black animate-pulse"><i class="fa-solid fa-clock"></i> Pending (Ustazah)</span>`;

                const studentSpp = s.sppMonths || {};
                let paidMonthsCount = 0;
                monthsShortList.forEach(m => {
                    if (studentSpp[m] === "Lunas") paidMonthsCount++;
                });

                const payBadge = paidMonthsCount > 0
                    ? `<span class="bg-emerald-50 text-emerald-700 px-2 py-0.5 rounded border border-emerald-200 font-extrabold text-[10px]">${paidMonthsCount}/12 Bulan Lunas</span>`
                    : `<span class="bg-rose-50 text-rose-700 px-2 py-0.5 rounded border border-rose-200 font-extrabold text-[10px]">Belum Lunas</span>`;

                tr.innerHTML = `
                    <td class="p-3">
                        <p class="font-extrabold text-slate-900 text-xs">${s.name}</p>
                        <p class="text-[10px] text-slate-400 mt-0.5 font-mono">${s.id} | WA: ${s.parentPhone}</p>
                    </td>
                    <td class="p-3 font-bold text-slate-700 text-[11px]">${s.program} <br/><span class="text-[9px] text-slate-400">Target: ${s.celenganTarget}</span></td>
                    <td class="p-3 text-center font-extrabold text-slate-800 text-[11px]">Ustz. ${s.room}</td>
                    <td class="p-3 text-center">${halaqahBadge}</td>
                    <td class="p-3 text-center">${payBadge}</td>
                    <td class="p-3 text-center space-x-1 whitespace-nowrap">
                        <button onclick="openEditStudentModal('${s.id}')" class="bg-blue-50 text-blue-700 border border-blue-200 hover:bg-blue-100 px-2 py-1 rounded-lg text-[10px] font-black transition"><i class="fa-solid fa-user-pen"></i> Edit</button>
                        <button onclick="triggerDirectReceiptPrint('${s.id}')" class="bg-slate-50 text-slate-600 border border-slate-200 hover:bg-slate-100 px-2 py-1 rounded-lg text-[10px] font-black transition"><i class="fa-solid fa-receipt"></i> Kuitansi</button>
                        <button onclick="deleteStudentData('${s.id}')" class="bg-rose-50 text-rose-700 border border-rose-200 hover:bg-rose-100 px-2 py-1 rounded-lg text-[10px] font-black transition"><i class="fa-solid fa-trash-can"></i> Hapus</button>
                    </td>
                `;
                listContainer.appendChild(tr);
            });
        };

        window.deleteStudentData = function(studentId) {
            const student = studentsList.find(s => s.id === studentId);
            if (!student) return;

            openConfirmModal(
                "Hapus Permanen Santriwati",
                `Apakah Anda yakin ingin menghapus seluruh berkas & riwayat KHS untuk ${student.name}? Tindakan ini tidak bisa dibatalkan.`,
                async () => {
                    studentsList = studentsList.filter(s => s.id !== studentId);
                    tahfidzLogs = tahfidzLogs.filter(l => l.student_id !== studentId);
                    saveLocalData();
                    await syncDeleteFromCloud('santri_students', studentId);
                    
                    showToast(`Data ${student.name} berhasil dimusnahkan secara permanen.`, "success");
                    recalculateAdminStats();
                    renderAdminStudentsDirectory();
                }
            );
        };

        window.triggerDirectReceiptPrint = function(studentId) {
            const student = studentsList.find(s => s.id === studentId);
            if (!student) return;
            openReceiptModal(student, 250000, 900000, 0); 
        };

        // =========================================================================
        // AUTOMATIC CSV IMPORT FUNCTION (santri_students_rows.csv VERBATIM REFERENCE)
        // =========================================================================
        window.handleCSVImport = function(e) {
            const file = e.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = async function(evt) {
                const text = evt.target.result;
                const lines = text.split('\n');
                let importCount = 0;

                // Membaca baris demi baris, melewati baris judul (header) pertama
                for (let i = 1; i < lines.length; i++) {
                    const row = lines[i].trim();
                    if (!row) continue;

                    // Parse CSV sederhana menggunakan pemisah koma
                    const columns = row.split(',');
                    if (columns.length < 5) continue; 

                    const name = columns[0].replace(/"/g, '').trim();
                    const phone = columns[1].replace(/"/g, '').trim();
                    const pobDob = columns[2].replace(/"/g, '').trim() || "Pare, 10 Oktober 2008";
                    const address = columns[3].replace(/"/g, '').trim() || "Pondok Asrama HQ Putri 4";
                    const room = columns[4].replace(/"/g, '').trim() || "Ayu";
                    const program = columns[5] ? columns[5].replace(/"/g, '').trim() : "Tahfidz Reguler";
                    const celenganTarget = columns[6] ? columns[6].replace(/"/g, '').trim() : "5 Juz";

                    const newId = "s_" + Date.now() + "_" + i;
                    
                    const initialSppMonths = {
                        "Jan": "Lunas", "Feb": "Belum Lunas", "Mar": "Belum Lunas", "Apr": "Belum Lunas",
                        "Mei": "Belum Lunas", "Jun": "Belum Lunas", "Jul": "Belum Lunas", "Agu": "Belum Lunas",
                        "Sep": "Belum Lunas", "Okt": "Belum Lunas", "Nov": "Belum Lunas", "Des": "Belum Lunas"
                    };

                    const importedStudent = {
                        id: newId,
                        name: name,
                        pobDob: pobDob,
                        address: address,
                        parentPhone: phone,
                        memorizedBefore: "Belum Pernah",
                        celenganTarget: celenganTarget,
                        motivation: "Mengabdi pada Al-Qur'an",
                        arrivalDate: "2026-01-01",
                        room: room,
                        program: program,
                        paymentStatus: "Lunas",
                        sppMonths: initialSppMonths,
                        facBuku: true,
                        facMeja: true,
                        facKerudung: true,
                        facLoker: false,
                        inHalaqah: false, // Membutuhkan otorisasi Ustazah untuk masuk halaqah
                        totalJuz: 0.0,
                        setoranAwal: 'Belum Setoran',
                        setoranAkhir: '-',
                        targetMingguan: '4 Halaman',
                        statusCapaian: 'Belum Tercapai',
                        perkembanganPositif: 'Hasil impor otomatis CSV',
                        catatanNegatif: 'Nihil',
                        daftarUlangStatus: 'Lunas',
                        catatanLain: 'Ditambahkan via Impor CSV santri_students_rows.csv.'
                    };

                    studentsList.push(importedStudent);
                    await syncInsertToCloud('santri_students', importedStudent);

                    const initialLog = {
                        id: "log_import_" + Date.now() + "_" + i,
                        student_id: newId,
                        date: "Inisialisasi",
                        setoran_awal: "Impor CSV",
                        setoran_akhir: "Santri Baru",
                        total_juz: 0.0,
                        pos: "Terdaftar dari berkas CSV",
                        neg: "Nihil"
                    };
                    tahfidzLogs.push(initialLog);
                    await syncInsertToCloud('tahfidz_logs', initialLog);

                    importCount++;
                }

                saveLocalData();
                showToast(`Alhamdulillah! Sukses mengimpor ${importCount} santriwati dari santri_students_rows.csv!`, 'success');
                triggerConfettiFeedback('register');
                recalculateAdminStats();
                renderAdminStudentsDirectory();
            };
            reader.readAsText(file);
        };

        function renderUstazahInterface() {
            const activeUstazah = currentRole.replace('ustazah_', '');
            document.getElementById('ustazah-directory-title').innerText = `Form Input Halaqah - Ustazah ${activeUstazah}`;
            
            const pendingSection = document.getElementById('ustazah-pending-section');
            const pendingList = document.getElementById('ustazah-pending-list');
            const pendingStudents = studentsList.filter(s => s.room === activeUstazah && !s.inHalaqah);

            if (pendingStudents.length > 0) {
                pendingSection.classList.remove('hidden');
                pendingList.innerHTML = '';
                pendingStudents.forEach(s => {
                    const tr = document.createElement('tr');
                    tr.className = "border-b border-amber-100 text-slate-700 font-medium";
                    tr.innerHTML = `
                        <td class="p-3"><strong>${s.name}</strong><br/><span class="text-[9px] text-slate-400">${s.id}</span></td>
                        <td class="p-3 text-[11px]">${s.pobDob}<br/><span class="text-[9px] text-slate-400">${s.address}</span></td>
                        <td class="p-3 font-bold text-[11px] text-emerald-900">${s.program} (${s.celenganTarget})</td>
                        <td class="p-3 text-center">
                            <button onclick="approveStudentIntoHalaqah('${s.id}')" class="bg-emerald-700 text-white hover:bg-emerald-800 font-black text-[10px] px-3 py-1.5 rounded-xl shadow-xs transition flex items-center gap-1 mx-auto">
                                <i class="fa-solid fa-user-plus"></i> Terima Santri
                            </button>
                        </td>
                    `;
                    pendingList.appendChild(tr);
                });
            } else {
                pendingSection.classList.add('hidden');
            }

            const selectBox = document.getElementById('ustazah-student-select');
            
            // FORM STATE LOCK: Catat pilihan dropdown saat ini sebelum dibuat ulang
            const prevSelectedValue = selectBox.value;

            const activeStudents = studentsList.filter(s => s.room === activeUstazah && s.inHalaqah);
            selectBox.innerHTML = '';
            
            if (activeStudents.length === 0) {
                selectBox.innerHTML = `<option value="">Tidak ada santri aktif di halaqah ini</option>`;
            } else {
                activeStudents.forEach(s => {
                    const opt = document.createElement('option');
                    opt.value = s.id;
                    opt.innerText = `${s.name} (${s.totalJuz} Juz)`;
                    selectBox.appendChild(opt);
                });
            }

            // Kembalikan pilihan dropdown jika nama santriwati yang sama masih ada dalam lis
            if (prevSelectedValue && activeStudents.some(s => s.id === prevSelectedValue)) {
                selectBox.value = prevSelectedValue;
            } else if (activeStudents.length > 0) {
                selectBox.value = activeStudents[0].id;
                // Populasikan formulir dengan nama santri pertama di daftar secara default
                populateUstazahForm(activeStudents[0].id);
            }

            const cardsContainer = document.getElementById('ustazah-active-list');
            cardsContainer.innerHTML = '';

            if (activeStudents.length === 0) {
                cardsContainer.innerHTML = `
                    <div class="text-center p-12 bg-slate-50 border border-dashed border-slate-200 rounded-3xl text-slate-400 font-bold">
                        <i class="fa-solid fa-people-slash text-3xl block mb-2 text-slate-300"></i> Belum ada anggota halaqah yang diaktifkan.
                    </div>`;
                return;
            }

            activeStudents.forEach(s => {
                const card = document.createElement('div');
                card.className = "bg-slate-50 hover:bg-emerald-50/40 p-4 rounded-2xl border border-slate-200/70 transition flex flex-col sm:flex-row sm:items-center justify-between gap-4";
                
                const statusColor = s.statusCapaian === 'Tercapai' ? 'text-emerald-700 bg-emerald-100' : 'text-amber-700 bg-amber-100';
                
                card.innerHTML = `
                    <div class="space-y-1.5 flex-1">
                        <div class="flex items-center gap-2 flex-wrap">
                            <span class="text-xs font-black text-slate-900">${s.name}</span>
                            <span class="text-[9px] px-2 py-0.5 rounded-full font-black ${statusColor}">${s.statusCapaian}</span>
                        </div>
                        <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-[11px] font-bold text-slate-500">
                            <p>Hafalan: <strong class="text-emerald-800 font-extrabold">${s.totalJuz} Juz</strong></p>
                            <p class="truncate">Setoran: <strong class="text-slate-700">${s.setoranAkhir}</strong></p>
                            <p>SPP: <strong class="${s.paymentStatus === 'Lunas' ? 'text-emerald-700':'text-rose-600'}">${s.paymentStatus}</strong></p>
                            <p>Daftar Ulang: <strong class="text-slate-700">${s.daftarUlangStatus || 'Lunas'}</strong></p>
                        </div>
                    </div>
                    <div class="flex items-center gap-1.5 shrink-0">
                        <a href="https://wa.me/${s.parentPhone}" target="_blank" class="bg-white hover:bg-emerald-50 text-emerald-700 border border-emerald-200 p-2.5 rounded-xl text-xs font-bold transition flex items-center gap-1 shadow-2xs">
                            <i class="fa-brands fa-whatsapp text-sm"></i> <span class="hidden md:inline">Wali</span>
                        </a>
                        <button onclick="triggerUstazahViewKHS('${s.id}')" class="bg-emerald-700 hover:bg-emerald-855 text-white p-2.5 rounded-xl text-xs font-black transition flex items-center gap-1 shadow-xs">
                            <i class="fa-solid fa-chart-line"></i> Tinjau KHS
                        </button>
                    </div>
                `;
                cardsContainer.appendChild(card);
            });
        }

        // =========================================================================
        // AUTO-POPULATE FORM FIELDS UPON SELECTING A STUDENT
        // =========================================================================
        window.populateUstazahForm = function(studentId) {
    const student = studentsList.find(s => s.id === studentId);
    if (!student) return;

    document.getElementById('ustazah-student-id').value = student.id;
    document.getElementById('ustazah-setoran-awal').value = student.setoranAwal || "";
    document.getElementById('ustazah-setoran-akhir').value = student.setoranAkhir || "";
    document.getElementById('ustazah-target-mingguan').value = student.targetMingguan || "4 Halaman";
    document.getElementById('ustazah-status-capaian').value = student.statusCapaian || "Belum Tercapai";
    document.getElementById('ustazah-total-juz').value = student.totalJuz || 0.0;
    
    // PEMUATAN VALUE BARU KE FORM
    document.getElementById('ustazah-fasohah').value = student.fasohah || "Belum Dinilai";
    document.getElementById('ustazah-kelancaran').value = student.kelancaran || "Belum Dinilai";

    document.getElementById('ustazah-perkembangan-positif').value = student.perkembanganPositif || "Proses adaptasi awal asrama";
    document.getElementById('ustazah-catatan-negatif').value = student.catatanNegatif || "Nihil";
    document.getElementById('ustazah-syahriyah').value = student.paymentStatus || "Belum Lunas";
    document.getElementById('ustazah-daftar-ulang').value = student.daftarUlangStatus || "Belum Lunas";
    document.getElementById('ustazah-catatan-lain').value = student.catatanLain || "Baru mendaftar di kesekretariat.";
};
    

        window.approveStudentIntoHalaqah = async function(studentId) {
            const student = studentsList.find(s => s.id === studentId);
            if (!student) return;

            student.inHalaqah = true;
            saveLocalData();
            await syncUpdateToCloud('santri_students', studentId, { inHalaqah: true });

            showToast(`Otorisasi Berhasil! ${student.name} masuk halaqah aktif Anda.`, 'success');
            triggerConfettiFeedback('success');
            renderUstazahInterface();
        };

        window.triggerUstazahViewKHS = function(studentId) {
            const targetStudent = studentsList.find(s => s.id === studentId);
            if (!targetStudent) return;
            
            document.getElementById('view-ustazah').classList.add('hidden');
            document.getElementById('view-wali').classList.remove('hidden');
            document.getElementById('parent-back-btn-container').classList.remove('hidden'); 
            renderWaliKHS(studentId);
        };

        window.goBackToDashboard = function() {
            document.getElementById('view-wali').classList.add('hidden');
            setupActiveWorkspace();
        };

        window.handleUstazahSetoranSubmit = async function(e) {
            e.preventDefault();
            const studentId = document.getElementById('ustazah-student-select').value;
            if (!studentId) {
                showToast("Silahkan pilih santriwati terlebih dahulu.", "error");
                return;
            }

            const student = studentsList.find(s => s.id === studentId);
            if (!student) return;

            const setAwal = document.getElementById('ustazah-setoran-awal').value.trim();
            const setAkhir = document.getElementById('ustazah-setoran-akhir').value.trim();
            const targetMinggu = document.getElementById('ustazah-target-mingguan').value.trim();
            const statusCapai = document.getElementById('ustazah-status-capaian').value;
            const totalJuzInput = parseFloat(document.getElementById('ustazah-total-juz').value) || 0.0;
            const nilaiFasohah = document.getElementById('ustazah-fasohah').value;
            const nilaiKelancaran = document.getElementById('ustazah-kelancaran').value;
            const pos = document.getElementById('ustazah-perkembangan-positif').value.trim() || "Menunjukkan kemajuan hafalan.";
            const neg = document.getElementById('ustazah-catatan-negatif').value.trim() || "Nihil";
            const syahriyah = document.getElementById('ustazah-syahriyah').value;
            const daftarUlang = document.getElementById('ustazah-daftar-ulang').value;
            const catatanLain = document.getElementById('ustazah-catatan-lain').value.trim() || "Sehat wal afiat.";

            student.setoranAwal = setAwal;
            student.setoranAkhir = setAkhir;
            student.targetMingguan = targetMinggu;
            student.statusCapaian = statusCapai;
            student.totalJuz = totalJuzInput;
            student.fasohah = nilaiFasohah;
            student.kelancaran = nilaiKelancaran;
            student.perkembanganPositif = pos;
            student.catatanNegatif = neg;
            student.paymentStatus = syahriyah;
            student.daftarUlangStatus = daftarUlang;
            student.catatanLain = catatanLain;

            const currentMonthShort = monthsShortList[new Date().getMonth()];
            if (!student.sppMonths) student.sppMonths = {};
            student.sppMonths[currentMonthShort] = syahriyah;

            saveLocalData();
            await syncUpdateToCloud('santri_students', studentId, {
               setoranAwal: setAwal,
                setoranAkhir: setAkhir,
                targetMingguan: targetMinggu,
                statusCapaian: statusCapai,
                totalJuz: totalJuzInput,
                fasohah: nilaiFasohah, 
                kelancaran: nilaiKelancaran,
                perkembanganPositif: pos,
                catatanNegatif: neg,
                paymentStatus: syahriyah,
                sppMonths: student.sppMonths,
                daftarUlangStatus: daftarUlang,
                catatanLain: catatanLain
            });

            const newLog = {
                id: "log_" + Date.now(),
                student_id: studentId,
                date: new Date().toISOString().split('T')[0],
                setoran_awal: setAwal,
                setoran_akhir: setAkhir,
                total_juz: totalJuzInput,
                fasohah: nilaiFasohah,      
                kelancaran: nilaiKelancaran,
                pos: pos,
                neg: neg
            };
            tahfidzLogs.unshift(newLog);
            saveLocalData();
            await syncInsertToCloud('tahfidz_logs', newLog);

            showToast(`Laporan Pekan Berjalan untuk ${student.name} Berhasil Disimpan & Dicadangkan!`, 'success');
            triggerConfettiFeedback('success');
            renderUstazahInterface();
            
            // Populasikan ulang agar form memuat data terupdate tanpa reset kosong
            populateUstazahForm(studentId);
        };

        window.renderWaliKHS = function(studentId) {
            const s = studentsList.find(st => st.id === studentId);
            if (!s) return;

            document.getElementById('wali-khs-initial').innerText = s.name.charAt(0).toUpperCase();
            document.getElementById('wali-khs-name').innerText = s.name;
            document.getElementById('wali-khs-pobdob').innerText = s.pobDob;
            document.getElementById('wali-khs-parent').innerText = s.parentPhone;
            document.getElementById('wali-khs-address').innerText = s.address;
            document.getElementById('wali-khs-program').innerText = s.program;
            document.getElementById('wali-khs-ustazah').innerText = `Ustazah ${s.room}`;
            document.getElementById('wali-khs-celengan').innerText = s.celenganTarget || "5 Juz";
            document.getElementById('wali-khs-parent-signature').innerText = `Wali, ${s.name}`;
            document.getElementById('wali-khs-setoran-awal').innerText = s.setoranAwal;
            document.getElementById('wali-khs-setoran-akhir').innerText = s.setoranAkhir;
            document.getElementById('wali-khs-target-mingguan').innerText = s.targetMingguan;
            
            const fillCapaian = document.getElementById('wali-khs-status-capaian');
            fillCapaian.innerText = s.statusCapaian;
            fillCapaian.className = s.statusCapaian === 'Tercapai' ? "font-extrabold text-emerald-700 mt-1 block" : "font-extrabold text-amber-600 mt-1 block";
                // Tambahkan ini di dalam fungsi render / pemuatan data wali santri
            document.getElementById('wali-khs-fasohah').innerText = s.fasohah || 'Belum Dinilai';
                document.getElementById('wali-khs-kelancaran').innerText = s.kelancaran || 'Belum Dinilai';
            document.getElementById('wali-khs-perkembangan-positif').innerText = s.perkembanganPositif;
            document.getElementById('wali-khs-catatan-negatif').innerText = s.catatanNegatif;
            document.getElementById('wali-khs-catatan-lain').innerText = s.catatanLain || "Nihil";

            const sppBadge = document.getElementById('wali-khs-syahriyah-badge');
            sppBadge.innerText = s.paymentStatus === 'Lunas' ? 'LUNAS SELESAI' : 'MENUNGGU (PENDING)';
            sppBadge.className = s.paymentStatus === 'Lunas' 
                ? "px-2.5 py-1 rounded-full font-black text-[9px] bg-emerald-100 text-emerald-800" 
                : "px-2.5 py-1 rounded-full font-black text-[9px] bg-rose-100 text-rose-800";

            const duBadge = document.getElementById('wali-khs-daftarulang-badge');
            const duStatus = s.daftarUlangStatus || 'Belum Lunas';
            duBadge.innerText = duStatus === 'Lunas' ? 'LUNAS FISIK' : (duStatus === 'Cicil' ? 'MENCICIL' : 'PENDING');
            duBadge.className = duStatus === 'Lunas' 
                ? "px-2.5 py-1 rounded-full font-black text-[9px] bg-emerald-100 text-emerald-800" 
                : (duStatus === 'Cicil' ? "px-2.5 py-1 rounded-full font-black text-[9px] bg-amber-100 text-amber-800" : "px-2.5 py-1 rounded-full font-black text-[9px] bg-rose-100 text-rose-800");

            const currentFullMonth = new Date().toLocaleString('id-ID', { month: 'long', year: 'numeric' });
            document.getElementById('wali-khs-spp-status-label').innerText = `Syahriyah ${currentFullMonth}`;

            const sppGrid = document.getElementById('wali-spp-months-grid');
            sppGrid.innerHTML = '';
            const studentSpp = s.sppMonths || {};
            let lunasMonthsCount = 0;

            monthsShortList.forEach(m => {
                const isPaid = studentSpp[m] === "Lunas";
                if (isPaid) lunasMonthsCount++;

                const monthPill = document.createElement('div');
                monthPill.className = `p-2 rounded-xl text-center border text-[10px] font-black transition-all ${isPaid ? 'bg-gradient-to-br from-emerald-600 to-emerald-800 text-white border-emerald-500 shadow-2xs' : 'bg-slate-100 text-slate-400 border-slate-200'}`;
                monthPill.innerHTML = `
                    <div class="uppercase text-[9px] opacity-75">${m}</div>
                    <div class="mt-0.5 text-[8px] font-medium">${isPaid ? 'Lunas' : 'Belum'}</div>
                `;
                sppGrid.appendChild(monthPill);
            });
            document.getElementById('wali-spp-summary').innerText = `${lunasMonthsCount} dari 12 Bulan Lunas`;

            const visualMapContainer = document.getElementById('peta-tahfidz-container');
            visualMapContainer.innerHTML = '';
            
            const roundedActiveJuz = Math.floor(s.totalJuz || 0);

            for (let i = 1; i <= 30; i++) {
                const circle = document.createElement('div');
                circle.className = "flex flex-col items-center justify-center p-1 rounded-xl text-[9px] font-black border transition-all duration-300";
                
                if (i <= roundedActiveJuz) {
                    circle.className += " bg-gradient-to-br from-emerald-700 to-emerald-900 text-white border-emerald-600 shadow-xs ring-2 ring-emerald-100";
                    circle.innerHTML = `<span>${i}</span><i class="fa-solid fa-square-check text-[7px] text-emerald-300 mt-0.5"></i>`;
                } else if (i === roundedActiveJuz + 1 && (s.totalJuz % 1) > 0) {
                    circle.className += " bg-emerald-50 text-emerald-800 border-emerald-400 border-dashed animate-pulse";
                    circle.innerHTML = `<span>${i}</span><span class="text-[6px] tracking-tighter text-emerald-600 font-medium">Proses</span>`;
                } else {
                    circle.className += " bg-white text-slate-300 border-slate-150";
                    circle.innerHTML = `<span>${i}</span><i class="fa-solid fa-circle text-[5px] text-slate-200 mt-1"></i>`;
                }
                visualMapContainer.appendChild(circle);
            }

            const timelineContainer = document.getElementById('wali-timeline-container');
            timelineContainer.innerHTML = '';
            
            const studentLogs = tahfidzLogs.filter(l => l.student_id === studentId);
            
            if (studentLogs.length === 0) {
                timelineContainer.innerHTML = `<p class="text-[11px] font-bold text-slate-400 text-center py-4">Belum memiliki riwayat setoran minggu.</p>`;
            } else {
                studentLogs.forEach(l => {
                    const block = document.createElement('div');
                    block.className = "bg-slate-50 border border-slate-200/60 p-3 rounded-2xl text-[11px] leading-relaxed relative overflow-hidden";
                    
                    const logFormattedDate = getFormattedMonthWeek(l.date);
                    
                    block.innerHTML = `
                        <div class="flex justify-between items-center border-b border-slate-150 pb-1 mb-1.5">
                            <span class="font-extrabold text-emerald-800 uppercase text-[9px]"><i class="fa-solid fa-calendar-check"></i> ${logFormattedDate}</span>
                            <span class="bg-white px-2 py-0.5 rounded-md border text-slate-700 font-mono text-[9px] font-black">Akumulasi: ${l.total_juz} Juz</span>
                        </div>
                        <p class="font-semibold text-slate-700">Setoran: <strong class="text-slate-900">${l.setoran_awal} s/d ${l.setoran_akhir}</strong></p>
                        <p class="text-slate-500 font-medium mt-0.5"><span class="text-emerald-700 font-bold">(+)</span> ${l.pos} | <span class="text-rose-600 font-bold">(-)</span> ${l.neg}</p>
                    `;
                    timelineContainer.appendChild(block);
                });
            }
        };

        window.refreshWaliData = async function() {
            if (isCloudMode && supabaseClient) {
                showToast("Menyegarkan data dari server cloud...", "info");
                await fetchCloudData();
                if (currentWaliStudent) {
                    const updated = studentsList.find(s => s.id === currentWaliStudent.id);
                    if (updated) {
                        currentWaliStudent = updated;
                        renderWaliKHS(currentWaliStudent.id);
                    }
                }
                showToast("Data raport paling mutakhir berhasil dimuat.", "success");
            } else {
                showToast("Modus luring aktif. Mengambil data instan dari browser.", "info");
            }
        };

        window.openReceiptModal = function(studentObj, feeReg, feeSpp, feeRereg) {
            document.getElementById('receipt-modal').classList.remove('hidden');
            
            document.getElementById('receipt-reg-number').innerText = "REG-" + studentObj.id.replace('s_', '').toUpperCase();
            document.getElementById('receipt-print-date').innerText = new Date().toLocaleDateString('id-ID', { day: 'numeric', month: 'long', year: 'numeric' });
            
            document.getElementById('rec-name').innerText = studentObj.name;
            document.getElementById('rec-pobdob').innerText = studentObj.pobDob;
            document.getElementById('rec-phone').innerText = studentObj.parentPhone;
            document.getElementById('rec-celengan').innerText = studentObj.celenganTarget || "5 Juz";
            document.getElementById('rec-program').innerText = studentObj.program;
            document.getElementById('rec-ustazah').innerText = getHalaqahName(studentObj.room);
            document.getElementById('rec-parent-sign').innerText = `Wali, ${studentObj.name}`;
            document.getElementById('rec-spp').innerText = studentObj.paymentStatus === 'Lunas' ? 'LUNAS (SELESAI)' : 'PENDING (BELUM LUNAS)';

            document.getElementById('rec-fee-reg').innerText = "Rp " + feeReg.toLocaleString('id-ID');
            document.getElementById('rec-fee-spp1').innerText = "Rp " + feeSpp.toLocaleString('id-ID');
            document.getElementById('rec-fee-rereg').innerText = "Rp " + feeRereg.toLocaleString('id-ID');
            
            const total = feeReg + feeSpp + feeRereg;
            document.getElementById('rec-fee-total').innerText = "Rp " + total.toLocaleString('id-ID');

            document.getElementById('secure-receipt-code').innerText = "AUTH-" + Math.floor(100000 + Math.random() * 900000);

            const logBox = document.getElementById('rec-logistics');
            logBox.innerHTML = '';
            
            const items = [
                { val: studentObj.facBuku, label: "Buku Pegangan" },
                { val: studentObj.facMeja, label: "Meja Ngaji Lipat" },
                { val: studentObj.facKerudung, label: "Hijab Almamater" },
                { val: studentObj.facLoker, label: "Kunci Loker Lemari" }
            ];

            items.forEach(it => {
                const div = document.createElement('div');
                div.className = "flex items-center gap-1.5 p-1.5 bg-white border border-slate-200 rounded-xl";
                div.innerHTML = it.val 
                    ? `<i class="fa-solid fa-square-check text-emerald-600 text-xs"></i> <span class="line-through text-slate-400 truncate">${it.label}</span>`
                    : `<i class="fa-regular fa-square text-slate-300 text-xs"></i> <span class="text-slate-600 truncate">${it.label}</span>`;
                logBox.appendChild(div);
            });
        };

        window.closeReceiptModal = function() {
            document.getElementById('receipt-modal').classList.add('hidden');
        };

        window.openEditStudentModal = function(studentId) {
            const s = studentsList.find(st => st.id === studentId);
            if (!s) return;

            document.getElementById('edit-student-modal').classList.remove('hidden');
            
            document.getElementById('edit-student-id').value = s.id;
            document.getElementById('edit-name').value = s.name;
            document.getElementById('edit-pobdob').value = s.pobDob;
            document.getElementById('edit-phone').value = s.parentPhone;
            document.getElementById('edit-arrival-date').value = s.arrivalDate || "";
            document.getElementById('edit-address').value = s.address;
            document.getElementById('edit-motivation').value = s.motivation || "";
            document.getElementById('edit-celengan').value = s.celenganTarget || "5 Juz";
            document.getElementById('edit-total-juz').value = s.totalJuz || 0.0;
            document.getElementById('edit-setoran-awal').value = s.setoranAwal || "";
            document.getElementById('edit-setoran-akhir').value = s.setoranAkhir || "";
            document.getElementById('edit-target-mingguan').value = s.targetMingguan || "";
            document.getElementById('edit-positive').value = s.perkembanganPositif || "";
            document.getElementById('edit-negative').value = s.catatanNegatif || "";
            document.getElementById('edit-catatan-lain').value = s.catatanLain || "";

            document.getElementById('edit-memorized').value = s.memorizedBefore || "Belum Pernah";
            document.getElementById('edit-room').value = s.room || "Ayu";
            document.getElementById('edit-program').value = s.program || "Tahfidz Reguler";
            document.getElementById('edit-daftarulang').value = s.daftarUlangStatus || "Belum Lunas";
            document.getElementById('edit-inhalaqah').value = s.inHalaqah ? "true" : "false";

            document.getElementById('edit-fac-buku').checked = !!s.facBuku;
            document.getElementById('edit-fac-meja').checked = !!s.facMeja;
            document.getElementById('edit-fac-kerudung').checked = !!s.facKerudung;
            document.getElementById('edit-fac-loker').checked = !!s.facLoker;

            const container = document.getElementById('edit-spp-months-container');
            container.innerHTML = '';
            
            const studentSpp = s.sppMonths || {};

            monthsShortList.forEach(m => {
                const isPaid = studentSpp[m] === "Lunas";
                const chkId = `edit-spp-month-${m}`;
                const label = document.createElement('label');
                label.className = `flex items-center gap-1.5 p-1.5 rounded-lg border text-[10px] font-bold cursor-pointer transition-all ${isPaid ? 'bg-emerald-50 border-emerald-300 text-emerald-900' : 'bg-slate-50 border-slate-200 text-slate-500'}`;
                label.innerHTML = `
                    <input type="checkbox" id="${chkId}" ${isPaid ? 'checked':''} onchange="toggleEditSppClass('${m}')" class="w-3.5 h-3.5 rounded text-emerald-600 focus:ring-emerald-500 border-slate-300">
                    <span>${m}</span>
                `;
                container.appendChild(label);
            });
        };

        window.toggleEditSppClass = function(m) {
            const chk = document.getElementById(`edit-spp-month-${m}`);
            const lbl = chk.closest('label');
            if (chk.checked) {
                lbl.className = 'flex items-center gap-1.5 p-1.5 rounded-lg border text-[10px] font-bold cursor-pointer transition-all bg-emerald-50 border-emerald-300 text-emerald-900';
            } else {
                lbl.className = 'flex items-center gap-1.5 p-1.5 rounded-lg border text-[10px] font-bold cursor-pointer transition-all bg-slate-50 border-slate-200 text-slate-500';
            }
        };

        window.closeEditStudentModal = function() {
            document.getElementById('edit-student-modal').classList.add('hidden');
        };

        window.handleSaveEditStudent = async function(e) {
            e.preventDefault();
            const id = document.getElementById('edit-student-id').value;
            const s = studentsList.find(st => st.id === id);
            if (!s) return;

            s.name = document.getElementById('edit-name').value.trim();
            s.pobDob = document.getElementById('edit-pobdob').value.trim();
            s.parentPhone = document.getElementById('edit-phone').value.trim();
            s.arrivalDate = document.getElementById('edit-arrival-date').value;
            s.address = document.getElementById('edit-address').value.trim();
            s.motivation = document.getElementById('edit-motivation').value.trim();
            s.celenganTarget = document.getElementById('edit-celengan').value.trim();
            s.totalJuz = parseFloat(document.getElementById('edit-total-juz').value) || 0.0;
            s.setoranAwal = document.getElementById('edit-setoran-awal').value.trim();
            s.setoranAkhir = document.getElementById('edit-setoran-akhir').value.trim();
            s.targetMingguan = document.getElementById('edit-target-mingguan').value.trim();
            s.perkembanganPositif = document.getElementById('edit-positive').value.trim();
            s.catatanNegatif = document.getElementById('edit-negative').value.trim();
            s.catatanLain = document.getElementById('edit-catatan-lain').value.trim();

            s.memorizedBefore = document.getElementById('edit-memorized').value;
            s.room = document.getElementById('edit-room').value;
            s.program = document.getElementById('edit-program').value;
            s.daftarUlangStatus = document.getElementById('edit-daftarulang').value;
            s.inHalaqah = document.getElementById('edit-inhalaqah').value === "true";

            s.facBuku = document.getElementById('edit-fac-buku').checked;
            s.facMeja = document.getElementById('edit-fac-meja').checked;
            s.facKerudung = document.getElementById('edit-fac-kerudung').checked;
            s.facLoker = document.getElementById('edit-fac-loker').checked;

            const updatedSppMonths = {};
            monthsShortList.forEach(m => {
                const isChecked = document.getElementById(`edit-spp-month-${m}`).checked;
                updatedSppMonths[m] = isChecked ? "Lunas" : "Belum Lunas";
            });
            s.sppMonths = updatedSppMonths;

            const currentMonthShort = monthsShortList[new Date().getMonth()];
            s.paymentStatus = updatedSppMonths[currentMonthShort] || "Belum Lunas";

            saveLocalData();
            await syncUpdateToCloud('santri_students', id, s);

            showToast(`Berkas Induk Eksekutif ${s.name} Berhasil Disinkronkan Permanen!`, 'success');
            triggerConfettiFeedback('success');
            closeEditStudentModal();
            recalculateAdminStats();
            renderAdminStudentsDirectory();
        };

        window.printReceipt = function() { window.print(); };
        window.printKHS = function() { window.print(); };

        window.saveReceiptPDF = function() {
            const element = document.getElementById('print-receipt-area');
            const studentName = document.getElementById('rec-name').innerText;
            const opt = {
                margin: 0.2,
                filename: `Kuitansi_${studentName.replace(/\s+/g, '_')}.pdf`,
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { scale: 2, useCORS: true },
                jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
            };
            html2pdf().set(opt).from(element).save();
        };

        window.saveKHSPDF = function() {
            const element = document.getElementById('wali-khs-card');
            const studentName = document.getElementById('wali-khs-name').innerText;
            const opt = {
                margin: 0.3,
                filename: `Raport_KHS_${studentName.replace(/\s+/g, '_')}.pdf`,
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { scale: 2, useCORS: true },
                jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
            };
            html2pdf().set(opt).from(element).save();
        };

        window.exportDashboardToPDF = function() {
            window.print();
        };

        window.openSupabaseConfigModal = function() {
            document.getElementById('supabase-config-modal').classList.remove('hidden');
            document.getElementById('cfg-supabase-url').value = localStorage.getItem('karima_supabase_url') || (DEFAULT_SUPABASE_URL !== "https://your-project.supabase.co" ? DEFAULT_SUPABASE_URL : '') || '';
            document.getElementById('cfg-supabase-key').value = localStorage.getItem('karima_supabase_key') || (DEFAULT_SUPABASE_KEY !== "your-anon-key-here" ? DEFAULT_SUPABASE_KEY : '') || '';
        };
        window.closeSupabaseConfigModal = function() { document.getElementById('supabase-config-modal').classList.add('hidden'); };
        
        window.copySupabaseSchema = function() {
            const sql = `-- BERSIHKAN TABEL LAMA JIKA SUDAH ADA
DROP TABLE IF EXISTS "tahfidz_logs";
DROP TABLE IF EXISTS "santri_students";

-- BUAT TABEL DENGAN FORMAT STANDAR SNAKE_CASE
CREATE TABLE "santri_students" (
  "id" text PRIMARY KEY,
  "name" text,
  "pob_dob" text,
  "address" text,
  "parent_phone" text,
  "memorized_before" text,
  "celengan_target" text,
  "motivation" text,
  "arrival_date" text,
  "room" text,
  "program" text,
  "payment_status" text,
  "spp_months" jsonb,
  "fac_buku" boolean,
  "fac_meja" boolean,
  "fac_kerudung" boolean,
  "fac_loker" boolean,
  "in_halaqah" boolean,
  "total_juz" float8,
  "setoran_awal" text,
  "setoran_akhir" text,
  "target_mingguan" text,
  "status_capaian" text,
  "perkembangan_positif" text,
  "catatan_negatif" text,
  "daftar_ulang_status" text,
  "catatan_lain" text
);

CREATE TABLE "tahfidz_logs" (
  "id" text PRIMARY KEY,
  "student_id" text,
  "date" text,
  "setoran_awal" text,
  "setoran_akhir" text,
  "total_juz" float8,
  "pos" text,
  "neg" text
);

-- MATIKAN SEC SECURITY RLS SUPABASE
ALTER TABLE "santri_students" DISABLE ROW LEVEL SECURITY;
ALTER TABLE "tahfidz_logs" DISABLE ROW LEVEL SECURITY;`;
            const dummy = document.createElement("textarea");
            document.body.appendChild(dummy);
            dummy.value = sql;
            dummy.select();
            document.execCommand("copy");
            document.body.removeChild(dummy);
            showToast("SQL Schema disalin! Silakan hapus & buat ulang tabel di SQL Editor Supabase Anda.", "success");
        };

        window.handleSaveSupabaseConfig = function(e) {
            e.preventDefault();
            const u = document.getElementById('cfg-supabase-url').value.trim();
            const k = document.getElementById('cfg-supabase-key').value.trim();
            
            localStorage.setItem('karima_supabase_url', u);
            localStorage.setItem('karima_supabase_key', k);
            
            showToast("Konfigurasi API Supabase Disimpan! Memuat Ulang...", "success");
            triggerConfettiFeedback('success');
            closeSupabaseConfigModal();
            setTimeout(() => { location.reload(); }, 1000);
        };

        window.openConfirmModal = function(title, msg, callback) {
            document.getElementById('confirm-modal').classList.remove('hidden');
            document.getElementById('confirm-title').innerText = title;
            document.getElementById('confirm-message').innerText = msg;
            confirmCallback = callback;
        };

        document.getElementById('confirm-btn-cancel').onclick = function() {
            document.getElementById('confirm-modal').classList.add('hidden');
            confirmCallback = null;
        };

        document.getElementById('confirm-btn-ok').onclick = function() {
            document.getElementById('confirm-modal').classList.add('hidden');
            if (confirmCallback) confirmCallback();
            confirmCallback = null;
        };

        window.openSeedModal = function() { document.getElementById('seed-modal').classList.remove('hidden'); };
        window.closeSeedModal = function() { document.getElementById('seed-modal').classList.add('hidden'); };
        
        window.confirmResetSeedData = function() {
            localStorage.removeItem('karima_students');
            localStorage.removeItem('karima_logs');
            closeSeedModal();
            showToast("Database Contoh Dimuat Ulang!", "success");
            setTimeout(() => { location.reload(); }, 800);
        };

        // =========================================================================
        // PREMIUM CONFETTI FEEDBACK SYSTEM ON SUCCESS ACTIONS
        // =========================================================================
        function triggerConfettiFeedback(actionType = 'success') {
            if (typeof confetti === 'undefined') return;

            if (actionType === 'register') {
                // Skema kembang api ganda berturut-turut untuk Registrasi Sukses
                const duration = 2.5 * 1000;
                const animationEnd = Date.now() + duration;
                const defaults = { startVelocity: 28, spread: 360, ticks: 60, zIndex: 100, colors: ['#047857', '#eab308', '#1e293b'] };

                function randomInRange(min, max) {
                    return Math.random() * (max - min) + min;
                }

                const interval = setInterval(function() {
                    const timeLeft = animationEnd - Date.now();

                    if (timeLeft <= 0) {
                        return clearInterval(interval);
                    }

                    const particleCount = 50 * (timeLeft / duration);
                    confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
                    confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
                }, 250);
            } else {
                // Letupan melingkar instan di tengah layar untuk Kesuksesan Umum (Login/Simpan)
                confetti({
                    particleCount: 100,
                    spread: 70,
                    origin: { y: 0.6 },
                    colors: ['#047857', '#eab308', '#ffffff']
                });
            }
        }

        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            if (!container) return;

            const toast = document.createElement('div');
            let bg = 'bg-slate-900';
            let icon = '<i class="fa-solid fa-circle-info text-blue-400"></i>';
            
            if (type === 'success') {
                bg = 'bg-emerald-950 border border-emerald-500/30';
                icon = '<i class="fa-solid fa-circle-check text-emerald-400"></i>';
            } else if (type === 'error') {
                bg = 'bg-rose-950 border border-rose-500/30';
                icon = '<i class="fa-solid fa-circle-exclamation text-rose-400"></i>';
            }

            toast.className = `${bg} text-white text-xs font-bold p-4 rounded-2xl shadow-xl flex items-center gap-3 transition-all duration-300 transform translate-y-2 opacity-0`;
            toast.innerHTML = `${icon} <span class="flex-1">${message}</span>`;
            
            container.appendChild(toast);
            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 10);

            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-x-4');
                setTimeout(() => { toast.remove(); }, 300);
            }, 4000);
        }

        document.addEventListener('DOMContentLoaded', () => {
            initVisitorCounter();
            initSupabase();
        });
    </script>
</body>
</html>
