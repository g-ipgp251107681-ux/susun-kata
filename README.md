# susun-kata
<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Susun Kata: Azan & Iqamat</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Plus Jakarta Sans & Amiri -->
    <link href="https://fonts.googleapis.com/css2?family=Amiri:wght@700&family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <!-- Font Awesome untuk Ikon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --emerald-dark: #064e3b;
            --emerald-primary: #047857;
            --emerald-light: #d1fae5;
            --gold-primary: #d97706;
            --gold-light: #fef3c7;
            --cream-bg: #fdfbf7;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--cream-bg);
            color: #1f2937;
            overflow-x: hidden;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        .font-arabic {
            font-family: 'Amiri', serif;
        }

        /* Corak Geometri Islamik Halus pada Latar Belakang */
        .islamic-pattern {
            background-color: #fdfbf7;
            background-image: radial-gradient(#047857 0.75px, transparent 0.75px), radial-gradient(#d97706 0.75px, #fdfbf7 0.75px);
            background-size: 32px 32px;
            background-position: 0 0, 16px 16px;
        }

        /* Gaya Kepingan Perkataan (Word Tiles) dengan Kesan 3D */
        .word-tile {
            transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
            box-shadow: 0 4px 0 #065f46, 0 6px 10px rgba(0, 0, 0, 0.1);
            cursor: pointer;
        }

        .word-tile:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #065f46, 0 8px 14px rgba(0, 0, 0, 0.15);
        }

        .word-tile:active:not(:disabled) {
            transform: translateY(3px);
            box-shadow: 0 1px 0 #065f46, 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .word-tile-answer {
            background: linear-gradient(135deg, #ffffff 0%, #fef3c7 100%);
            border: 2px solid #f59e0b;
            color: #78350f;
            box-shadow: 0 4px 0 #b45309, 0 5px 8px rgba(0, 0, 0, 0.08);
        }

        .word-tile-answer:hover {
            box-shadow: 0 6px 0 #b45309, 0 8px 12px rgba(0, 0, 0, 0.12);
        }

        .word-tile-answer:active {
            box-shadow: 0 1px 0 #b45309;
        }

        .word-tile-hint {
            background: linear-gradient(135deg, #fef08a 0%, #fde047 100%);
            border: 2px solid #eab308;
            color: #713f12;
            box-shadow: 0 4px 0 #ca8a04;
            cursor: default;
        }

        /* Gaya Butang Permainan */
        .game-btn {
            transition: all 0.15s ease;
            position: relative;
        }

        .game-btn:active:not(:disabled) {
            transform: translateY(3px);
        }

        .btn-emerald {
            background: linear-gradient(180deg, #10b981 0%, #059669 100%);
            box-shadow: 0 4px 0 #065f46, 0 6px 12px rgba(5, 150, 105, 0.3);
        }
        .btn-emerald:active:not(:disabled) {
            box-shadow: 0 1px 0 #065f46;
        }

        .btn-gold {
            background: linear-gradient(180deg, #f59e0b 0%, #d97706 100%);
            box-shadow: 0 4px 0 #92400e, 0 6px 12px rgba(217, 119, 6, 0.3);
        }
        .btn-gold:active:not(:disabled) {
            box-shadow: 0 1px 0 #92400e;
        }

        .btn-slate {
            background: linear-gradient(180deg, #f3f4f6 0%, #e5e7eb 100%);
            box-shadow: 0 4px 0 #9ca3af, 0 4px 8px rgba(0, 0, 0, 0.08);
            color: #374151;
        }
        .btn-slate:active:not(:disabled) {
            box-shadow: 0 1px 0 #9ca3af;
        }

        /* Animasi Masuk & Gegar */
        @keyframes popIn {
            0% { transform: scale(0.7); opacity: 0; }
            80% { transform: scale(1.05); opacity: 1; }
            100% { transform: scale(1); opacity: 1; }
        }

        .animate-pop {
            animation: popIn 0.25s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-8px); }
            40%, 80% { transform: translateX(8px); }
        }

        .animate-shake {
            animation: shake 0.4s ease-in-out;
        }

        /* Bingkai Kubah Islamik */
        .arch-header {
            border-radius: 0 0 2.5rem 2.5rem;
        }
    </style>
</head>
<body class="islamic-pattern min-h-screen flex flex-col justify-between">

    <!-- HEADER / BAR STATUS ATAS -->
    <header class="bg-gradient-to-r from-emerald-900 via-emerald-800 to-emerald-900 text-white shadow-lg arch-header px-4 py-3 sm:py-4 border-b-4 border-amber-500">
        <div class="max-w-4xl mx-auto flex flex-wrap items-center justify-between gap-2">
            <!-- Tajuk & Ikon -->
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 sm:w-12 sm:h-12 bg-amber-500 rounded-2xl flex items-center justify-center shadow-inner border-2 border-amber-200 text-emerald-950 text-xl sm:text-2xl">
                    <i class="fa-solid fa-mosque"></i>
                </div>
                <div>
                    <h1 class="font-extrabold text-base sm:text-xl tracking-tight text-amber-100 leading-tight">
                        Susun Kata: Azan & Iqamat
                    </h1>
                    <p class="text-xs text-emerald-200 hidden sm:block">Pendidikan Islam • Ibadah Solat</p>
                </div>
            </div>

            <!-- Statistik Permainan (Nyawa, Skor, Audio) -->
            <div id="hud-stats" class="hidden flex items-center gap-3 sm:gap-5">
                <!-- Nyawa (3 Hati) -->
                <div class="bg-emerald-950/60 px-3 py-1.5 rounded-xl border border-emerald-700/60 flex items-center gap-1.5" title="Nyawa Anda">
                    <div id="hearts-container" class="flex gap-1 text-rose-500 text-sm sm:text-base">
                        <i class="fa-solid fa-heart"></i>
                        <i class="fa-solid fa-heart"></i>
                        <i class="fa-solid fa-heart"></i>
                    </div>
                </div>

                <!-- Skor -->
                <div class="bg-emerald-950/60 px-3 py-1.5 rounded-xl border border-amber-500/40 flex items-center gap-2">
                    <i class="fa-solid fa-star text-amber-400 text-sm sm:text-base"></i>
                    <span id="score-display" class="font-extrabold text-amber-300 text-sm sm:text-base">0</span>
                </div>

                <!-- Butang Bunyi -->
                <button id="sound-toggle" onclick="toggleSound()" class="w-9 h-9 rounded-xl bg-emerald-700/70 hover:bg-emerald-600 flex items-center justify-center text-emerald-100 border border-emerald-500/40 transition" title="Tutup/Buka Bunyi">
                    <i id="sound-icon" class="fa-solid fa-volume-high"></i>
                </button>
            </div>
        </div>

        <!-- Bar Kemajuan (Progress Bar) -->
        <div id="progress-wrapper" class="hidden max-w-4xl mx-auto mt-3 pt-1">
            <div class="flex justify-between text-xs font-semibold text-emerald-200 mb-1">
                <span id="level-indicator">Tahap 1 daripada 10</span>
                <span id="category-badge" class="bg-amber-500/20 text-amber-300 px-2 py-0.5 rounded-full border border-amber-400/30">Maksud Azan</span>
            </div>
            <div class="w-full bg-emerald-950/80 h-2.5 rounded-full overflow-hidden p-0.5 border border-emerald-700">
                <div id="progress-bar" class="bg-gradient-to-r from-amber-400 to-yellow-300 h-full rounded-full transition-all duration-500" style="width: 10%;"></div>
            </div>
        </div>
    </header>

    <!-- KAWASAN UTAMA PERMAINAN -->
    <main class="flex-grow flex items-center justify-center p-4 sm:p-6">
        <div class="w-full max-w-3xl">

            <!-- 1. SKRIN MULA (START SCREEN) -->
            <section id="start-screen" class="bg-white/95 backdrop-blur-sm rounded-3xl shadow-xl border-2 border-emerald-800/15 p-6 sm:p-10 text-center animate-pop">
                <div class="inline-flex items-center justify-center w-20 h-20 sm:w-24 sm:h-24 rounded-full bg-gradient-to-br from-emerald-100 to-amber-100 border-4 border-amber-400 mb-4 shadow-md">
                    <span class="font-arabic text-3xl sm:text-4xl text-emerald-900 font-bold">الله أكبر</span>
                </div>
                
                <h2 class="text-2xl sm:text-4xl font-extrabold text-emerald-950 mb-2">
                    Misi Susun Kata: <span class="text-amber-600">Azan & Iqamat</span>
                </h2>
                <p class="text-gray-600 text-sm sm:text-base max-w-xl mx-auto mb-6 leading-relaxed">
                    Uji kefahaman anda tentang <strong>maksud Azan</strong>, <strong>maksud Iqamat</strong>, serta <strong>perbezaan asas</strong> antara kedua-duanya melalui 10 cabaran menyusun ayat!
                </p>

                <!-- Kad Ringkasan Panduan -->
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-8 text-left">
                    <div class="bg-emerald-50/80 p-4 rounded-2xl border border-emerald-200">
                        <div class="w-8 h-8 rounded-lg bg-emerald-600 text-white flex items-center justify-center mb-2 font-bold">
                            <i class="fa-solid fa-hand-pointer"></i>
                        </div>
                        <h3 class="font-bold text-emerald-900 text-sm mb-1">1. Susun Perkataan</h3>
                        <p class="text-xs text-emerald-800/80">Klik kepingan perkataan di bawah untuk membentuk ayat jawapan yang lengkap.</p>
                    </div>
                    <div class="bg-amber-50/80 p-4 rounded-2xl border border-amber-200">
                        <div class="w-8 h-8 rounded-lg bg-amber-500 text-white flex items-center justify-center mb-2 font-bold">
                            <i class="fa-solid fa-lightbulb"></i>
                        </div>
                        <h3 class="font-bold text-amber-900 text-sm mb-1">2. Guna Petunjuk</h3>
                        <p class="text-xs text-amber-800/80">Tersangkut? Tekan butang Petunjuk untuk meletakkan perkataan pertama (tolak 20 mata).</p>
                    </div>
                    <div class="bg-teal-50/80 p-4 rounded-2xl border border-teal-200">
                        <div class="w-8 h-8 rounded-lg bg-teal-600 text-white flex items-center justify-center mb-2 font-bold">
                            <i class="fa-solid fa-book-open"></i>
                        </div>
                        <h3 class="font-bold text-teal-900 text-sm mb-1">3. Nota Ulang Kaji</h3>
                        <p class="text-xs text-teal-800/80">Tamatkan semua 10 tahap untuk membuka rumusan nota lengkap Azan & Iqamat.</p>
                    </div>
                </div>

                <button onclick="startGame()" class="game-btn btn-emerald text-white font-extrabold text-lg sm:text-xl px-8 py-4 rounded-2xl w-full sm:w-auto inline-flex items-center justify-center gap-3">
                    <i class="fa-solid fa-play"></i>
                    <span>Mula Permainan</span>
                </button>
            </section>

            <!-- 2. SKRIN PERMAINAN UTAMA (GAMEPLAY SCREEN) -->
            <section id="game-screen" class="hidden space-y-5">
                <!-- Kad Soalan & Petunjuk -->
                <div class="bg-white rounded-3xl shadow-md border-2 border-emerald-700/15 p-5 sm:p-7 relative overflow-hidden">
                    <div class="absolute top-0 right-0 w-24 h-24 bg-amber-400/10 rounded-bl-full pointer-events-none"></div>
                    
                    <div class="flex items-start gap-3 sm:gap-4">
                        <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-2xl bg-emerald-100 text-emerald-800 flex items-center justify-center flex-shrink-0 text-lg sm:text-xl font-bold border border-emerald-300">
                            <i class="fa-solid fa-circle-question"></i>
                        </div>
                        <div class="flex-grow">
                            <span class="text-xs font-bold uppercase tracking-wider text-amber-600 block mb-1">Soalan / Tugasan</span>
                            <h2 id="question-text" class="text-lg sm:text-xl font-bold text-gray-800 leading-snug">
                                Memuatkan soalan...
                            </h2>
                            <p id="clue-text" class="text-xs sm:text-sm text-emerald-700 bg-emerald-50 inline-block px-3 py-1 rounded-lg mt-2 border border-emerald-200/70">
                                <i class="fa-solid fa-compass mr-1"></i> Petunjuk: ...
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Kotak Jawapan (Zon Susunan Ayat) -->
                <div class="bg-white/90 rounded-3xl shadow-inner border-2 border-dashed border-amber-400 p-4 sm:p-6">
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-xs font-bold text-amber-800 uppercase tracking-wider flex items-center gap-1.5">
                            <i class="fa-solid fa-pen-to-square"></i> Susun Ayat Jawapan Di Sini:
                        </span>
                        <span id="word-count-helper" class="text-xs font-semibold text-gray-500">0 / 0 perkataan</span>
                    </div>

                    <div id="answer-box" class="min-h-[110px] sm:min-h-[120px] bg-amber-50/50 rounded-2xl p-3 sm:p-4 flex flex-wrap items-center content-start gap-2.5 sm:gap-3 transition-all">
                        <!-- Placeholder apabila kosong -->
                        <div id="answer-placeholder" class="w-full h-20 flex items-center justify-center text-amber-700/50 text-sm italic pointer-events-none">
                            Klik perkataan di bawah untuk mula menyusun...
                        </div>
                    </div>
                </div>

                <!-- Kotak Bank Perkataan (Scrambled Word Tiles) -->
                <div class="bg-emerald-900/5 rounded-3xl p-4 sm:p-6 border border-emerald-800/10">
                    <span class="text-xs font-bold text-emerald-900 uppercase tracking-wider block mb-3">
                        <i class="fa-solid fa-puzzle-piece mr-1"></i> Pilihan Perkataan (Klik untuk pilih):
                    </span>
                    <div id="word-bank" class="min-h-[90px] flex flex-wrap items-center justify-center gap-2.5 sm:gap-3">
                        <!-- Kepingan perkataan akan dijana di sini -->
                    </div>
                </div>

                <!-- Bar Butang Kawalan (Di Luar Zon Kanvas/Susunan) -->
                <div class="flex flex-wrap items-center justify-center gap-3 pt-1">
                    <button onclick="clearAnswer()" id="btn-clear" class="game-btn btn-slate font-bold text-sm sm:text-base px-4 py-3 rounded-2xl flex items-center gap-2">
                        <i class="fa-solid fa-rotate-left"></i>
                        <span>Kosongkan</span>
                    </button>

                    <button onclick="useHint()" id="btn-hint" class="game-btn btn-gold text-white font-bold text-sm sm:text-base px-4 py-3 rounded-2xl flex items-center gap-2">
                        <i class="fa-solid fa-lightbulb"></i>
                        <span>Petunjuk (-20)</span>
                    </button>

                    <button onclick="checkAnswer()" id="btn-check" class="game-btn btn-emerald text-white font-extrabold text-sm sm:text-base px-6 py-3 rounded-2xl flex-grow sm:flex-grow-0 flex items-center justify-center gap-2">
                        <i class="fa-solid fa-check-circle"></i>
                        <span>Semak Jawapan</span>
                    </button>
                </div>
            </section>

            <!-- 3. SKRIN TAMAT & NOTA ULANG KAJI (SUMMARY / END SCREEN) -->
            <section id="end-screen" class="hidden bg-white rounded-3xl shadow-xl border-2 border-emerald-800/15 p-6 sm:p-8 animate-pop">
                <div class="text-center mb-6">
                    <div id="end-badge-icon" class="w-20 h-20 mx-auto rounded-full bg-amber-100 border-4 border-amber-400 flex items-center justify-center text-4xl text-amber-600 mb-3 shadow-md">
                        <i class="fa-solid fa-trophy"></i>
                    </div>
                    <h2 id="end-title" class="text-2xl sm:text-3xl font-extrabold text-emerald-950">Tahniah! Misi Selesai</h2>
                    <p id="end-subtitle" class="text-gray-600 text-sm sm:text-base mt-1">Anda telah menguasai asas Azan dan Iqamat dengan cemerlang.</p>
                    
                    <!-- Paparan Markah Akhir -->
                    <div class="inline-flex items-center gap-4 bg-gradient-to-r from-emerald-900 to-emerald-800 text-white px-6 py-3 rounded-2xl mt-4 shadow-md border border-amber-400/50">
                        <div class="text-left">
                            <span class="text-xs text-emerald-200 block">Jumlah Skor Akhir</span>
                            <span id="final-score" class="text-2xl sm:text-3xl font-extrabold text-amber-300">0</span>
                        </div>
                        <div class="h-8 w-px bg-emerald-700"></div>
                        <div class="text-left">
                            <span class="text-xs text-emerald-200 block">Tahap Selesai</span>
                            <span id="final-levels" class="text-lg sm:text-xl font-bold text-white">10 / 10</span>
                        </div>
                    </div>
                </div>

                <!-- Nota Ringkasan Ulang Kaji -->
                <div class="bg-cream-bg rounded-2xl border-2 border-emerald-700/20 p-4 sm:p-6 mb-6">
                    <h3 class="font-extrabold text-emerald-900 text-base sm:text-lg mb-3 flex items-center gap-2 border-b border-emerald-200 pb-2">
                        <i class="fa-solid fa-book-quran text-amber-600"></i>
                        <span>Nota Ulang Kaji Pantas: Azan & Iqamat</span>
                    </h3>

                    <div class="space-y-4 text-xs sm:text-sm text-gray-700">
                        <!-- Pengertian -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
                            <div class="bg-emerald-50 p-3.5 rounded-xl border border-emerald-200">
                                <span class="font-bold text-emerald-900 block mb-1"><i class="fa-solid fa-bullhorn mr-1 text-emerald-600"></i> Maksud Azan</span>
                                <p>Pemberitahuan atau seruan kepada orang ramai tentang telah masuknya waktu solat fardu dengan lafaz-lafaz tertentu.</p>
                            </div>
                            <div class="bg-amber-50 p-3.5 rounded-xl border border-amber-200">
                                <span class="font-bold text-amber-900 block mb-1"><i class="fa-solid fa-people-group mr-1 text-amber-600"></i> Maksud Iqamat</span>
                                <p>Seruan atau pemberitahuan kepada jemaah yang hadir bahawa solat berjemaah akan segera didirikan.</p>
                            </div>
                        </div>

                        <!-- Jadual Perbezaan Asas -->
                        <div class="overflow-x-auto rounded-xl border border-gray-200">
                            <table class="w-full text-left border-collapse bg-white">
                                <thead>
                                    <tr class="bg-emerald-800 text-white text-xs">
                                        <th class="p-2.5">Aspek</th>
                                        <th class="p-2.5">Azan</th>
                                        <th class="p-2.5">Iqamat</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-gray-200 text-xs">
                                    <tr>
                                        <td class="p-2.5 font-bold text-gray-800">Tujuan</td>
                                        <td class="p-2.5">Menyeru orang ramai solat (masuk waktu).</td>
                                        <td class="p-2.5">Menyeru jemaah bangun memulakan solat.</td>
                                    </tr>
                                    <tr class="bg-gray-50">
                                        <td class="p-2.5 font-bold text-gray-800">Nada & Tempo</td>
                                        <td class="p-2.5">Dilaungkan secara nyaring dan perlahan (tartil).</td>
                                        <td class="p-2.5">Dilaungkan secara cepat (hadar) dan sederhana.</td>
                                    </tr>
                                    <tr>
                                        <td class="p-2.5 font-bold text-gray-800">Bilangan Lafaz</td>
                                        <td class="p-2.5">Kebanyakan lafaz diulang 2 kali (15 kalimah).</td>
                                        <td class="p-2.5">Kebanyakan lafaz disebut 1 kali sahaja (11 kalimah).</td>
                                    </tr>
                                    <tr class="bg-gray-50">
                                        <td class="p-2.5 font-bold text-gray-800">Lafaz Tambahan</td>
                                        <td class="p-2.5"><em>"As-solatu khairum minan naum"</em> (Subuh).</td>
                                        <td class="p-2.5"><em>"Qad qamatis solah"</em> (2 kali).</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <div class="text-center">
                    <button onclick="startGame()" class="game-btn btn-emerald text-white font-extrabold text-base sm:text-lg px-8 py-3.5 rounded-2xl inline-flex items-center gap-2">
                        <i class="fa-solid fa-rotate-right"></i>
                        <span>Main Semula</span>
                    </button>
                </div>
            </section>

        </div>
    </main>

    <!-- KOTAK MESEJ MODAL (MENGGANTIKAN ALERT()) -->
    <div id="feedback-modal" class="fixed inset-0 bg-black/50 backdrop-blur-xs hidden items-center justify-center p-4 z-50">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 text-center shadow-2xl border-2 border-emerald-800/20 animate-pop">
            <div id="modal-icon" class="w-16 h-16 mx-auto rounded-full flex items-center justify-center text-3xl mb-3">
                <!-- Ikon dinamik -->
            </div>
            <h3 id="modal-title" class="text-xl font-extrabold text-gray-900 mb-1">Tajuk</h3>
            <p id="modal-message" class="text-sm text-gray-600 mb-4 leading-relaxed">Mesej maklum balas</p>
            
            <!-- Kotak Fakta Tambahan selepas jawapan betul -->
            <div id="modal-fact-box" class="hidden bg-emerald-50 border border-emerald-200 rounded-xl p-3 mb-5 text-left text-xs text-emerald-900">
                <strong class="block text-emerald-700 mb-0.5"><i class="fa-solid fa-lightbulb mr-1"></i> Tahukah Anda?</strong>
                <span id="modal-fact-text"></span>
            </div>

            <button id="modal-action-btn" onclick="closeModal()" class="game-btn btn-emerald text-white font-bold w-full py-3 rounded-xl text-base">
                Teruskan
            </button>
        </div>
    </div>

    <!-- FOOTER RINGKAS -->
    <footer class="text-center py-3 text-xs text-emerald-900/60 font-medium">
        Permainan Pendidikan Islam Interaktif • Susun Kata: Azan & Iqamat
    </footer>

    <!-- SKRIP LOGIK PERMAINAN & WEB AUDIO API -->
    <script>
        // ==========================================
        // 1. PANGKALAN DATA 10 TAHAP PEMBELAJARAN
        // ==========================================
        const levelsData = [
            {
                level: 1,
                category: "Maksud Azan",
                question: "Apakah maksud Azan dari segi istilah syarak?",
                clue: "Berkaitan pemberitahuan waktu solat kepada umat Islam.",
                words: ["Pemberitahuan", "masuk", "waktu", "solat", "fardu", "kepada", "orang", "ramai"],
                fact: "Dari segi bahasa, Azan bermaksud 'pemberitahuan'. Muazzin melaungkannya supaya masyarakat tahu waktu solat fardu telah tiba."
            },
            {
                level: 2,
                category: "Maksud Iqamat",
                question: "Lengkapkan pengertian Iqamat yang tepat:",
                clue: "Seruan khusus sebelum imam mengangkat takbiratul ihram.",
                words: ["Seruan", "bahawa", "solat", "berjemaah", "akan", "segera", "didirikan"],
                fact: "Iqamat dilaungkan apabila jemaah sudah bersedia untuk memulakan solat fardu secara berjemaah."
            },
            {
                level: 3,
                category: "Hukum Azan & Iqamat",
                question: "Apakah hukum melaungkan Azan dan Iqamat bagi solat fardu?",
                clue: "Hukumnya sangat dituntut dalam Islam.",
                words: ["Sunat", "muakkad", "bagi", "solat", "fardu", "lima", "waktu"],
                fact: "Hukum melaungkan azan dan iqamat adalah sunat muakkad (sunat yang sangat dituntut), terutamanya bagi lelaki yang solat berjemaah."
            },
            {
                level: 4,
                category: "Perbezaan: Tempo Bacaan",
                question: "Bagaimanakah perbezaan nada dan tempo bacaan antara Azan dengan Iqamat?",
                clue: "Azan dilaungkan perlahan dan nyaring, manakala Iqamat...",
                words: ["Azan", "dibaca", "secara", "perlahan", "manakala", "Iqamat", "dibaca", "cepat"],
                fact: "Azan dilaungkan secara tartil (perlahan dan lantang) agar didengari dari jauh, manakala Iqamat dilaungkan secara hadar (cepat) kerana jemaah sudah berada di dalam masjid."
            },
            {
                level: 5,
                category: "Perbezaan: Lafaz Iqamat",
                question: "Apakah lafaz tambahan khusus yang hanya terdapat di dalam Iqamat?",
                clue: "Bermaksud 'Sesungguhnya solat telah didirikan'.",
                words: ["Terdapat", "tambahan", "lafaz", "Qad", "qamatis", "solah", "dalam", "Iqamat"],
                fact: "Lafaz 'Qad qamatis solah' disebut sebanyak dua kali selepas 'Hayya alal falah' di dalam Iqamat."
            },
            {
                level: 6,
                category: "Perbezaan: Azan Subuh",
                question: "Apakah lafaz istimewa yang ditambah ketika Azan Subuh?",
                clue: "Bermaksud 'Solat itu lebih baik daripada tidur'.",
                words: ["Lafaz", "As-solatu", "khairum", "minan", "naum", "dalam", "Azan", "Subuh"],
                fact: "Tambahan ini dipanggil 'Tathwib', khusus untuk mengejutkan umat Islam daripada tidur bagi menunaikan solat Subuh."
            },
            {
                level: 7,
                category: "Perbezaan: Bilangan Kalimah",
                question: "Apakah perbezaan bilangan sebutan lafaz antara Azan dan Iqamat?",
                clue: "Bandingkan kekerapan ulangan kalimah kedua-duanya.",
                words: ["Lafaz", "Azan", "diulang", "dua", "kali", "Iqamat", "sekali", "sahaja"],
                fact: "Dalam Azan, kebanyakan lafaz diulang 2 kali (jumlah 15 kalimah), manakala dalam Iqamat disebut 1 kali sahaja (jumlah 11 kalimah)."
            },
            {
                level: 8,
                category: "Perbezaan: Sasaran Seruan",
                question: "Siapakah sasaran utama seruan Azan berbanding Iqamat?",
                clue: "Azan untuk yang di luar masjid, Iqamat untuk...",
                words: ["Azan", "menyeru", "orang", "ramai", "Iqamat", "untuk", "jemaah", "hadir"],
                fact: "Azan memanggil umat Islam datang ke masjid, manakala Iqamat memberitahu jemaah yang sudah hadir supaya meluruskan saf."
            },
            {
                level: 9,
                category: "Sunat Ketika Azan",
                question: "Apakah perbuatan sunat bagi muazzin ketika melaungkan 'Hayya alas solah'?",
                clue: "Pergerakan kepala ke kanan dan ke kiri.",
                words: ["Memalingkan", "muka", "ke", "kanan", "dan", "ke", "kiri"],
                fact: "Sunat bagi muazzin memalingkan muka ke kanan ketika 'Hayya alas solah' dan ke kiri ketika 'Hayya alal falah' agar suara tersebar luas."
            },
            {
                level: 10,
                category: "Adab Mendengar Azan",
                question: "Apakah tindakan kita apabila mendengar seruan Azan berkumandang?",
                clue: "Menjawab lafaz muazzin secara perlahan.",
                words: ["Menjawab", "seruan", "Azan", "dan", "berdoa", "selepas", "selesai"],
                fact: "Sunat menjawab lafaz azan seperti yang diucapkan muazzin (kecuali pada Hayya alas solah/falah dijawab dengan La haula wala quwwata illa billah) diikuti doa selepas azan."
            }
        ];

        // ==========================================
        // 2. PEMBOLEHUBAH STATUS PERMAINAN
        // ==========================================
        let currentLevelIndex = 0;
        let score = 0;
        let lives = 3;
        let soundEnabled = true;
        let currentAnswerTiles = []; // Array objek { id, text, isHinted }
        let bankTiles = [];          // Array objek { id, text, used }
        let modalCallback = null;

        // ==========================================
        // 3. SISTEM BUNYI SINTETIK (WEB AUDIO API)
        // ==========================================
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        let audioCtx = null;

        function initAudio() {
            if (!audioCtx) {
                audioCtx = new AudioContext();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        }

        function playSound(type) {
            if (!soundEnabled) return;
            try {
                initAudio();
                const now = audioCtx.currentTime;

                if (type === 'click') {
                    // Bunyi ketikan kepingan kayu/kad yang lembut
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(520, now);
                    osc.frequency.exponentialRampToValueAtTime(180, now + 0.06);
                    gain.gain.setValueAtTime(0.2, now);
                    gain.gain.exponentialRampToValueAtTime(0.01, now + 0.06);
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start(now);
                    osc.stop(now + 0.06);
                } 
                else if (type === 'remove') {
                    // Bunyi memulangkan kepingan
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(320, now);
                    osc.frequency.exponentialRampToValueAtTime(220, now + 0.06);
                    gain.gain.setValueAtTime(0.15, now);
                    gain.gain.exponentialRampToValueAtTime(0.01, now + 0.06);
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start(now);
                    osc.stop(now + 0.06);
                }
                else if (type === 'correct') {
                    // Melodi arpeggio ceria (C5 - E5 - G5 - C6)
                    const notes = [523.25, 659.25, 783.99, 1046.50];
                    notes.forEach((freq, idx) => {
                        const osc = audioCtx.createOscillator();
                        const gain = audioCtx.createGain();
                        osc.type = 'sine';
                        osc.frequency.setValueAtTime(freq, now + idx * 0.08);
                        gain.gain.setValueAtTime(0.18, now + idx * 0.08);
                        gain.gain.exponentialRampToValueAtTime(0.001, now + idx * 0.08 + 0.35);
                        osc.connect(gain);
                        gain.connect(audioCtx.destination);
                        osc.start(now + idx * 0.08);
                        osc.stop(now + idx * 0.08 + 0.35);
                    });
                }
                else if (type === 'wrong') {
                    // Bunyi nada rendah (salah)
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'sawtooth';
                    osc.frequency.setValueAtTime(190, now);
                    osc.frequency.linearRampToValueAtTime(135, now + 0.28);
                    gain.gain.setValueAtTime(0.15, now);
                    gain.gain.exponentialRampToValueAtTime(0.01, now + 0.28);
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start(now);
                    osc.stop(now + 0.28);
                }
                else if (type === 'hint') {
                    // Bunyi loceng petunjuk
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(880, now);
                    osc.frequency.setValueAtTime(1174.66, now + 0.1);
                    gain.gain.setValueAtTime(0.15, now);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start(now);
                    osc.stop(now + 0.3);
                }
                else if (type === 'win') {
                    // Fanfare kemenangan
                    const melody = [523.25, 659.25, 783.99, 1046.50, 783.99, 1046.50];
                    const times = [0, 0.12, 0.24, 0.36, 0.52, 0.66];
                    melody.forEach((freq, i) => {
                        const osc = audioCtx.createOscillator();
                        const gain = audioCtx.createGain();
                        osc.type = 'triangle';
                        osc.frequency.setValueAtTime(freq, now + times[i]);
                        gain.gain.setValueAtTime(0.22, now + times[i]);
                        gain.gain.exponentialRampToValueAtTime(0.001, now + times[i] + 0.4);
                        osc.connect(gain);
                        gain.connect(audioCtx.destination);
                        osc.start(now + times[i]);
                        osc.stop(now + times[i] + 0.4);
                    });
                }
            } catch (e) {
                console.warn("Audio tidak disokong:", e);
            }
        }

        function toggleSound() {
            soundEnabled = !soundEnabled;
            const icon = document.getElementById('sound-icon');
            if (soundEnabled) {
                icon.className = 'fa-solid fa-volume-high';
                playSound('click');
            } else {
                icon.className = 'fa-solid fa-volume-xmark text-rose-300';
            }
        }

        // ==========================================
        // 4. LOGIK PERMAINAN & SUSUNAN KATA
        // ==========================================
        function shuffleArray(array) {
            const arr = [...array];
            for (let i = arr.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [arr[i], arr[j]] = [arr[j], arr[i]];
            }
            // Pastikan susunan acak tidak sama persis dengan jawapan asal
            if (arr.join(' ') === array.join(' ') && arr.length > 1) {
                return shuffleArray(array);
            }
            return arr;
        }

        function startGame() {
            playSound('click');
            currentLevelIndex = 0;
            score = 0;
            lives = 3;

            document.getElementById('start-screen').classList.add('hidden');
            document.getElementById('end-screen').classList.add('hidden');
            document.getElementById('game-screen').classList.remove('hidden');
            document.getElementById('hud-stats').classList.remove('hidden');
            document.getElementById('progress-wrapper').classList.remove('hidden');

            updateHUD();
            loadLevel(currentLevelIndex);
        }

        function updateHUD() {
            document.getElementById('score-display').textContent = score;
            
            // Kemas kini ikon hati
            const heartsContainer = document.getElementById('hearts-container');
            heartsContainer.innerHTML = '';
            for (let i = 0; i < 3; i++) {
                const heart = document.createElement('i');
                if (i < lives) {
                    heart.className = 'fa-solid fa-heart text-rose-500 transition-transform';
                } else {
                    heart.className = 'fa-regular fa-heart text-emerald-700/60';
                }
                heartsContainer.appendChild(heart);
            }

            // Kemas kini bar kemajuan
            const total = levelsData.length;
            const currentNum = currentLevelIndex + 1;
            document.getElementById('level-indicator').textContent = `Tahap ${currentNum} daripada ${total}`;
            document.getElementById('progress-bar').style.width = `${(currentNum / total) * 100}%`;
        }

        function loadLevel(index) {
            const levelObj = levelsData[index];
            document.getElementById('category-badge').textContent = levelObj.category;
            document.getElementById('question-text').textContent = levelObj.question;
            document.getElementById('clue-text').innerHTML = `<i class="fa-solid fa-compass mr-1"></i> Petunjuk: ${levelObj.clue}`;

            // Reset susunan perkataan
            currentAnswerTiles = [];
            const scrambled = shuffleArray(levelObj.words);
            bankTiles = scrambled.map((word, idx) => ({
                id: `tile-${index}-${idx}`,
                text: word,
                used: false
            }));

            renderTiles();
        }

        function renderTiles() {
            const answerBox = document.getElementById('answer-box');
            const wordBank = document.getElementById('word-bank');
            const levelObj = levelsData[currentLevelIndex];

            // Kemas kini pembilang perkataan
            document.getElementById('word-count-helper').textContent = `${currentAnswerTiles.length} / ${levelObj.words.length} perkataan`;

            // Render Kotak Jawapan
            answerBox.innerHTML = '';
            if (currentAnswerTiles.length === 0) {
                answerBox.innerHTML = `
                    <div id="answer-placeholder" class="w-full h-20 flex items-center justify-center text-amber-700/50 text-sm italic pointer-events-none">
                        Klik perkataan di bawah untuk mula menyusun...
                    </div>`;
            } else {
                currentAnswerTiles.forEach((tile) => {
                    const btn = document.createElement('button');
                    btn.type = 'button';
                    btn.textContent = tile.text;
                    
                    if (tile.isHinted) {
                        btn.className = 'word-tile word-tile-hint font-bold text-sm sm:text-base px-3.5 py-2 sm:px-4 sm:py-2.5 rounded-xl animate-pop flex items-center gap-1.5';
                        btn.innerHTML = `<i class="fa-solid fa-lock text-xs opacity-70"></i> <span>${tile.text}</span>`;
                        btn.title = "Perkataan petunjuk dikunci di posisi yang betul";
                    } else {
                        btn.className = 'word-tile word-tile-answer font-bold text-sm sm:text-base px-3.5 py-2 sm:px-4 sm:py-2.5 rounded-xl animate-pop';
                        btn.onclick = () => removeWordFromAnswer(tile.id);
                    }
                    answerBox.appendChild(btn);
                });
            }

            // Render Bank Perkataan
            wordBank.innerHTML = '';
            bankTiles.forEach((tile) => {
                const btn = document.createElement('button');
                btn.type = 'button';
                btn.textContent = tile.text;

                if (tile.used) {
                    // Slot kosong yang menunjukkan perkataan sudah dipilih
                    btn.className = 'bg-emerald-950/10 border-2 border-dashed border-emerald-800/20 text-transparent font-bold text-sm sm:text-base px-3.5 py-2 sm:px-4 sm:py-2.5 rounded-xl pointer-events-none';
                    btn.disabled = true;
                } else {
                    btn.className = 'word-tile bg-gradient-to-b from-emerald-600 to-emerald-700 text-white border border-emerald-500 font-bold text-sm sm:text-base px-3.5 py-2 sm:px-4 sm:py-2.5 rounded-xl';
                    btn.onclick = () => selectWordFromBank(tile.id);
                }
                wordBank.appendChild(btn);
            });
        }

        function selectWordFromBank(tileId) {
            const tile = bankTiles.find(t => t.id === tileId);
            if (!tile || tile.used) return;

            playSound('click');
            tile.used = true;
            currentAnswerTiles.push({
                id: tile.id,
                text: tile.text,
                isHinted: false
            });
            renderTiles();
        }

        function removeWordFromAnswer(tileId) {
            const index = currentAnswerTiles.findIndex(t => t.id === tileId);
            if (index === -1 || currentAnswerTiles[index].isHinted) return;

            playSound('remove');
            currentAnswerTiles.splice(index, 1);
            
            const bankTile = bankTiles.find(t => t.id === tileId);
            if (bankTile) bankTile.used = false;

            renderTiles();
        }

        function clearAnswer() {
            // Hanya buang perkataan yang bukan daripada petunjuk
            const hasRemovable = currentAnswerTiles.some(t => !t.isHinted);
            if (!hasRemovable) return;

            playSound('remove');
            currentAnswerTiles = currentAnswerTiles.filter(t => {
                if (t.isHinted) return true;
                const bankTile = bankTiles.find(b => b.id === t.id);
                if (bankTile) bankTile.used = false;
                return false;
            });

            renderTiles();
        }

        function useHint() {
            const levelObj = levelsData[currentLevelIndex];
            const targetWords = levelObj.words;

            // Cari indeks perkataan pertama yang belum dikunci/betul di kedudukan awal
            let hintIndex = 0;
            while (
                hintIndex < currentAnswerTiles.length && 
                currentAnswerTiles[hintIndex].isHinted
            ) {
                hintIndex++;
            }

            if (hintIndex >= targetWords.length) return;

            const neededWord = targetWords[hintIndex];

            // Kosongkan perkataan selepas hintIndex supaya susunan tidak bercelaru
            for (let i = currentAnswerTiles.length - 1; i >= hintIndex; i--) {
                const removed = currentAnswerTiles.pop();
                const bTile = bankTiles.find(b => b.id === removed.id);
                if (bTile) bTile.used = false;
            }

            // Cari kepingan perkataan yang diperlukan dari bank
            const matchingBankTile = bankTiles.find(b => !b.used && b.text === neededWord);
            if (matchingBankTile) {
                playSound('hint');
                matchingBankTile.used = true;
                currentAnswerTiles.push({
                    id: matchingBankTile.id,
                    text: matchingBankTile.text,
                    isHinted: true
                });

                // Potong 20 mata (minimum 0)
                score = Math.max(0, score - 20);
                updateHUD();
                renderTiles();
            }
        }

        function checkAnswer() {
            const levelObj = levelsData[currentLevelIndex];
            const answerBox = document.getElementById('answer-box');

            // Semak jika belum semua perkataan disusun
            if (currentAnswerTiles.length < levelObj.words.length) {
                playSound('wrong');
                answerBox.classList.add('animate-shake');
                setTimeout(() => answerBox.classList.remove('animate-shake'), 400);
                
                showModal(
                    'warning',
                    'Ayat Belum Lengkap!',
                    `Sila susun kesemua ${levelObj.words.length} perkataan sebelum menyemak jawapan.`,
                    null,
                    'Baiklah'
                );
                return;
            }

            const userSentence = currentAnswerTiles.map(t => t.text).join(' ');
            const correctSentence = levelObj.words.join(' ');

            if (userSentence === correctSentence) {
                // JAWAPAN BETUL
                playSound('correct');
                score += 100;
                updateHUD();

                const isLastLevel = currentLevelIndex === levelsData.length - 1;
                showModal(
                    'success',
                    'Syabas! Jawapan Tepat',
                    `"${correctSentence}."`,
                    levelObj.fact,
                    isLastLevel ? 'Lihat Keputusan & Nota' : 'Tahap Seterusnya',
                    () => {
                        if (isLastLevel) {
                            finishGame(true);
                        } else {
                            currentLevelIndex++;
                            updateHUD();
                            loadLevel(currentLevelIndex);
                        }
                    }
                );
            } else {
                // JAWAPAN SALAH
                playSound('wrong');
                lives--;
                updateHUD();

                answerBox.classList.add('animate-shake', 'border-rose-500');
                setTimeout(() => answerBox.classList.remove('animate-shake', 'border-rose-500'), 500);

                if (lives <= 0) {
                    showModal(
                        'gameover',
                        'Nyawa Sudah Habis!',
                        `Jawapan yang tepat ialah: "${correctSentence}." Jangan putus asa, cuba lagi!`,
                        levelObj.fact,
                        'Lihat Rumusan',
                        () => finishGame(false)
                    );
                } else {
                    showModal(
                        'error',
                        'Kurang Tepat!',
                        `Susunan ayat masih belum tepat. Anda mempunyai ${lives} nyawa lagi. Cuba susun semula!`,
                        null,
                        'Cuba Lagi'
                    );
                }
            }
        }

        // ==========================================
        // 5. KAWALAN MODAL & SKRIN TAMAT
        // ==========================================
        function showModal(type, title, message, fact, btnText, callback = null) {
            const modal = document.getElementById('feedback-modal');
            const iconBox = document.getElementById('modal-icon');
            const titleEl = document.getElementById('modal-title');
            const msgEl = document.getElementById('modal-message');
            const factBox = document.getElementById('modal-fact-box');
            const factText = document.getElementById('modal-fact-text');
            const actionBtn = document.getElementById('modal-action-btn');

            modalCallback = callback;
            titleEl.textContent = title;
            msgEl.textContent = message;
            actionBtn.textContent = btnText;

            // Gaya ikon & butang mengikut jenis mesej
            if (type === 'success') {
                iconBox.className = 'w-16 h-16 mx-auto rounded-full bg-emerald-100 text-emerald-600 flex items-center justify-center text-3xl mb-3 border-2 border-emerald-300';
                iconBox.innerHTML = '<i class="fa-solid fa-circle-check"></i>';
                actionBtn.className = 'game-btn btn-emerald text-white font-bold w-full py-3 rounded-xl text-base';
            } else if (type === 'warning') {
                iconBox.className = 'w-16 h-16 mx-auto rounded-full bg-amber-100 text-amber-600 flex items-center justify-center text-3xl mb-3 border-2 border-amber-300';
                iconBox.innerHTML = '<i class="fa-solid fa-circle-exclamation"></i>';
                actionBtn.className = 'game-btn btn-gold text-white font-bold w-full py-3 rounded-xl text-base';
            } else {
                iconBox.className = 'w-16 h-16 mx-auto rounded-full bg-rose-100 text-rose-600 flex items-center justify-center text-3xl mb-3 border-2 border-rose-300';
                iconBox.innerHTML = '<i class="fa-solid fa-circle-xmark"></i>';
                actionBtn.className = 'game-btn btn-gold text-white font-bold w-full py-3 rounded-xl text-base';
            }

            if (fact) {
                factBox.classList.remove('hidden');
                factText.textContent = fact;
            } else {
                factBox.classList.add('hidden');
            }

            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeModal() {
            const modal = document.getElementById('feedback-modal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');

            if (modalCallback) {
                const cb = modalCallback;
                modalCallback = null;
                cb();
            }
        }

        function finishGame(isVictory) {
            document.getElementById('game-screen').classList.add('hidden');
            document.getElementById('hud-stats').classList.add('hidden');
            document.getElementById('progress-wrapper').classList.add('hidden');
            document.getElementById('end-screen').classList.remove('hidden');

            const completedCount = isVictory ? levelsData.length : currentLevelIndex;
            document.getElementById('final-score').textContent = score;
            document.getElementById('final-levels').textContent = `${completedCount} / ${levelsData.length}`;

            const badgeIcon = document.getElementById('end-badge-icon');
            const endTitle = document.getElementById('end-title');
            const endSubtitle = document.getElementById('end-subtitle');

            if (isVictory) {
                playSound('win');
                badgeIcon.className = 'w-20 h-20 mx-auto rounded-full bg-amber-100 border-4 border-amber-400 flex items-center justify-center text-4xl text-amber-600 mb-3 shadow-md';
                badgeIcon.innerHTML = '<i class="fa-solid fa-trophy"></i>';
                endTitle.textContent = 'Tahniah! Semua Tahap Selesai';
                endSubtitle.textContent = 'Anda telah menguasai maksud dan perbezaan asas Azan serta Iqamat!';
            } else {
                badgeIcon.className = 'w-20 h-20 mx-auto rounded-full bg-emerald-100 border-4 border-emerald-400 flex items-center justify-center text-4xl text-emerald-700 mb-3 shadow-md';
                badgeIcon.innerHTML = '<i class="fa-solid fa-book-open-reader"></i>';
                endTitle.textContent = 'Tamat Pusingan';
                endSubtitle.textContent = 'Sila baca nota ulang kaji di bawah sebelum mencuba sekali lagi!';
            }
        }
    </script>
</body>
</html>
