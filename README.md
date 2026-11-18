# memory-pegs-
```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bản Thử Nghiệm (Beta) - Móc Treo Trí Nhớ Fususu 1–100</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
        }
        .fade-in {
            animation: fadeIn 0.25s ease-out forwards;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(6px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes bouncePop {
            0% { transform: scale(0.92); }
            60% { transform: scale(1.04); }
            100% { transform: scale(1); }
        }
        .pop-anim {
            animation: bouncePop 0.25s ease-out;
        }
        /* Tùy chỉnh thanh cuộn */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
    </style>
</head>
<body class="text-slate-800 min-h-screen flex flex-col">

    <!-- ===================================================================== -->
    <!-- HEADER & THANH ĐIỀU HƯỚNG 4 TAB                                       -->
    <!-- ===================================================================== -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-2xs">
        <div class="max-w-6xl mx-auto px-4 py-3.5 flex items-center justify-between gap-3">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 sm:w-11 sm:h-11 rounded-2xl bg-gradient-to-br from-indigo-600 via-violet-600 to-amber-500 flex items-center justify-center text-white shadow-md shadow-indigo-200 shrink-0">
                    <i data-lucide="anchor" class="w-6 h-6"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <h1 class="font-black text-lg sm:text-xl bg-gradient-to-r from-indigo-700 to-violet-700 bg-clip-text text-transparent">
                            Bản Thử Nghiệm
                        </h1>
                        <span class="px-2.5 py-0.5 rounded-full text-[11px] font-extrabold uppercase tracking-wider bg-amber-100 text-amber-800 border border-amber-300">
                            Beta
                        </span>
                    </div>
                    <p class="text-xs text-slate-500 font-medium">Móc Treo Trí Nhớ Fususu (1–100) & Trợ Lý Học Tập AI</p>
                </div>
            </div>

            <button onclick="copyShareUrl()" class="flex items-center gap-1.5 px-3.5 py-2 rounded-xl text-xs sm:text-sm font-bold bg-indigo-50 text-indigo-700 hover:bg-indigo-100 border border-indigo-200/80 transition shrink-0">
                <i data-lucide="share-2" class="w-4 h-4"></i>
                <span class="hidden sm:inline">Gửi cho bạn bè</span>
                <span class="sm:hidden">Chia sẻ</span>
            </button>
        </div>

        <!-- 4 Tab điều hướng -->
        <div class="bg-slate-50/90 border-t border-slate-100">
            <div class="max-w-6xl mx-auto px-4 py-2.5">
                <div class="grid grid-cols-4 gap-1.5 sm:gap-2">
                    <button onclick="switchTab(1)" id="nav-tab-1" class="flex items-center justify-center gap-1.5 py-2.5 px-2 sm:px-3 rounded-xl text-xs sm:text-sm font-bold bg-indigo-600 text-white shadow-sm transition">
                        <i data-lucide="grid" class="w-4 h-4 shrink-0"></i>
                        <span class="truncate">Bảng Mã 1–100</span>
                    </button>
                    <button onclick="switchTab(2)" id="nav-tab-2" class="flex items-center justify-center gap-1.5 py-2.5 px-2 sm:px-3 rounded-xl text-xs sm:text-sm font-bold bg-white text-slate-600 hover:bg-slate-100 border border-slate-200/80 transition">
                        <i data-lucide="wand-2" class="w-4 h-4 shrink-0"></i>
                        <span class="truncate">Tạo Truyện AI</span>
                    </button>
                    <button onclick="switchTab(3)" id="nav-tab-3" class="flex items-center justify-center gap-1.5 py-2.5 px-2 sm:px-3 rounded-xl text-xs sm:text-sm font-bold bg-white text-slate-600 hover:bg-slate-100 border border-slate-200/80 transition">
                        <i data-lucide="gamepad-2" class="w-4 h-4 shrink-0"></i>
                        <span class="truncate">Luyện Phản Xạ</span>
                    </button>
                    <button onclick="switchTab(4)" id="nav-tab-4" class="flex items-center justify-center gap-1.5 py-2.5 px-2 sm:px-3 rounded-xl text-xs sm:text-sm font-bold bg-white text-slate-600 hover:bg-slate-100 border border-slate-200/80 transition">
                        <i data-lucide="help-circle" class="w-4 h-4 shrink-0"></i>
                        <span class="truncate">Hướng Dẫn & Q&A</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Thông báo Toast -->
    <div id="toast" class="fixed bottom-5 left-1/2 -translate-x-1/2 z-50 hidden">
        <div class="bg-slate-900 text-white px-4 py-3 rounded-2xl shadow-xl flex items-center gap-2.5 text-xs sm:text-sm font-semibold max-w-[92vw]">
            <i data-lucide="sparkles" class="w-4 h-4 text-amber-400 shrink-0"></i>
            <span id="toast-message">Thông báo</span>
        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- NỘI DUNG CHÍNH 4 TABS                                                 -->
    <!-- ===================================================================== -->
    <main class="flex-1 max-w-6xl w-full mx-auto px-4 py-6 sm:py-8">

        <!-- ================================================================= -->
        <!-- TAB 1: BẢNG MÃ 1–100 (CHUẨN FUSUSU)                               -->
        <!-- ================================================================= -->
        <section id="tab-1" class="fade-in space-y-5">
            <div class="bg-white rounded-3xl p-5 sm:p-7 shadow-sm border border-slate-200/80">
                <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4 mb-6">
                    <div>
                        <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-bold bg-indigo-50 text-indigo-700 mb-2">
                            <i data-lucide="check-circle-2" class="w-3.5 h-3.5"></i> DỮ LIỆU CHUẨN 100 SỐ (1–100)
                        </span>
                        <h2 class="text-xl sm:text-2xl font-extrabold text-slate-900">Bảng Mã 100 Móc Treo Trí Nhớ Fususu</h2>
                        <p class="text-xs sm:text-sm text-slate-500 mt-1">Sắp xếp chuẩn theo từng hàng ngang 1–10, 11–20... đến 91–100. Bấm vào từng ô để xem mẹo hình dung con số ẩn trong hình.</p>
                    </div>

                    <!-- Tìm kiếm & Chuyển chế độ hiển thị -->
                    <div class="flex flex-col sm:flex-row items-stretch sm:items-center gap-2.5">
                        <div class="relative flex-1 sm:w-64">
                            <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute left-3.5 top-1/2 -translate-y-1/2"></i>
                            <input type="text" id="pegSearchInput" oninput="renderPegsTable()" placeholder="Tìm số (vd: 19, 88) hoặc tên..." class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-slate-200 focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/10 outline-none text-sm bg-slate-50 focus:bg-white transition">
                        </div>

                        <div class="inline-flex rounded-xl bg-slate-100 p-1 border border-slate-200/70 shrink-0">
                            <button id="view-cards-btn" onclick="setCatalogView('cards')" class="px-3 py-1.5 rounded-lg text-xs font-bold bg-white text-indigo-700 shadow-2xs transition">
                                Thẻ chi tiết
                            </button>
                            <button id="view-matrix-btn" onclick="setCatalogView('matrix')" class="px-3 py-1.5 rounded-lg text-xs font-bold text-slate-600 hover:text-slate-900 transition">
                                Lưới 10x10 ảnh gốc
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Bộ lọc 10 hàng ngang (1-10 đến 91-100) -->
                <div class="flex flex-wrap gap-1.5 mb-6" id="rowFilterBar">
                    <button onclick="setRowFilter('all')" data-row="all" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-900 text-white transition">Tất cả (1–100)</button>
                    <button onclick="setRowFilter('1-10')" data-row="1-10" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 1 (1–10)</button>
                    <button onclick="setRowFilter('11-20')" data-row="11-20" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 2 (11–20)</button>
                    <button onclick="setRowFilter('21-30')" data-row="21-30" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 3 (21–30)</button>
                    <button onclick="setRowFilter('31-40')" data-row="31-40" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 4 (31–40)</button>
                    <button onclick="setRowFilter('41-50')" data-row="41-50" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 5 (41–50)</button>
                    <button onclick="setRowFilter('51-60')" data-row="51-60" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 6 (51–60)</button>
                    <button onclick="setRowFilter('61-70')" data-row="61-70" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 7 (61–70)</button>
                    <button onclick="setRowFilter('71-80')" data-row="71-80" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 8 (71–80)</button>
                    <button onclick="setRowFilter('81-90')" data-row="81-90" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 9 (81–90)</button>
                    <button onclick="setRowFilter('91-100')" data-row="91-100" class="row-filter-btn px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 text-slate-600 hover:bg-slate-200 transition">Hàng 10 (91–100)</button>
                </div>

                <!-- Vùng hiển thị lưới móc treo -->
                <div id="pegsCatalogWrapper" class="overflow-x-auto pb-2">
                    <div id="pegsCatalogGrid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-3">
                        <!-- Render bằng JS -->
                    </div>
                </div>
            </div>
        </section>

        <!-- ================================================================= -->
        <!-- TAB 2: TẠO CÂU CHUYỆN MEMORY PEGS (AI)                            -->
        <!-- ================================================================= -->
        <section id="tab-2" class="hidden fade-in space-y-6">
            <div class="bg-white rounded-3xl p-5 sm:p-8 shadow-sm border border-slate-200/80">
                <div class="mb-6">
                    <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-bold bg-emerald-50 text-emerald-700 mb-2">
                        <i data-lucide="sparkles" class="w-3.5 h-3.5"></i> PHÉP THUẬT LIÊN TƯỞNG AI
                    </span>
                    <h2 class="text-xl sm:text-2xl font-extrabold text-slate-900">Gắn Kiến Thức Vào Móc Treo Fususu (1–100)</h2>
                    <p class="text-sm text-slate-500 mt-1">Nhập danh sách kiến thức hoặc các mốc năm lịch sử. Hệ thống sẽ tự động tra bảng 1–100 và dệt thành câu chuyện hài hước cực kỳ dễ nhớ.</p>
                </div>

                <!-- 3 Ví dụ mẫu chuẩn xác 100% -->
                <div class="mb-6">
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-2.5">
                        Thử ngay 1 trong 3 ví dụ mẫu chuẩn bộ số 1–100:
                    </label>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                        <button type="button" onclick="applyStoryPreset(0)" class="text-left p-3.5 rounded-2xl border border-slate-200 hover:border-indigo-400 hover:bg-indigo-50/50 transition">
                            <div class="font-bold text-xs text-indigo-700 mb-1">🧪 1. 5 Nguyên tố Hóa học đầu</div>
                            <p class="text-xs text-slate-600 line-clamp-2">Dùng móc 1–5: 1 Cây kiếm (Hydro), 2 Con vịt (Heli), 3 Lá bài (Liti), 4 Cái ghế (Beri), 5 Bà bầu (Bo).</p>
                        </button>
                        <button type="button" onclick="applyStoryPreset(1)" class="text-left p-3.5 rounded-2xl border border-slate-200 hover:border-amber-400 hover:bg-amber-50/50 transition">
                            <div class="font-bold text-xs text-amber-700 mb-1">📜 2. Các mốc Lịch sử Việt Nam</div>
                            <p class="text-xs text-slate-600 line-clamp-2">Tách cặp số: 1945 (19 Con chó + 45 Nam châm), 1858 (18 Đĩa bánh + 58 Chú hề), 1975 (Con chó + Lính xe tăng).</p>
                        </button>
                        <button type="button" onclick="applyStoryPreset(2)" class="text-left p-3.5 rounded-2xl border border-slate-200 hover:border-emerald-400 hover:bg-emerald-50/50 transition">
                            <div class="font-bold text-xs text-emerald-700 mb-1">📐 3. Công thức & Việc cần làm</div>
                            <p class="text-xs text-slate-600 line-clamp-2">Gắn 5 công thức / việc quan trọng lần lượt từ móc số 11 (Cây nến) đến 15 (Đôi vớ).</p>
                        </button>
                    </div>
                </div>

                <!-- Tùy chọn chế độ & Ô nhập -->
                <div class="space-y-5">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="md:col-span-2">
                            <label class="block text-sm font-bold text-slate-700 mb-2">1. Chọn cách gắn Móc Treo:</label>
                            <div class="grid grid-cols-2 gap-2.5">
                                <button type="button" id="story-mode-seq" onclick="setStoryMode('sequence')" class="p-3 rounded-2xl border-2 border-indigo-600 bg-indigo-50/60 text-left transition">
                                    <div class="font-bold text-xs sm:text-sm text-indigo-700">🔢 Thứ tự liên tiếp (1, 2, 3...)</div>
                                    <div class="text-[11px] text-slate-500 mt-0.5">1 Cây kiếm, 2 Con vịt, 3 Lá bài...</div>
                                </button>
                                <button type="button" id="story-mode-num" onclick="setStoryMode('numbers')" class="p-3 rounded-2xl border border-slate-200 bg-white hover:bg-slate-50 text-left transition">
                                    <div class="font-bold text-xs sm:text-sm text-slate-700">📅 Tách số năm / mã số</div>
                                    <div class="text-[11px] text-slate-500 mt-0.5">VD: 1945 ➔ 19 Con chó + 45 Nam châm</div>
                                </button>
                            </div>
                        </div>

                        <div id="storyStartWrapper">
                            <label for="storyStartNumber" class="block text-sm font-bold text-slate-700 mb-2">Bắt đầu từ số (1–100):</label>
                            <div class="flex items-center gap-2">
                                <input type="number" id="storyStartNumber" min="1" max="100" value="1" oninput="updateStartBadge()" class="w-20 p-3 rounded-2xl border border-slate-200 focus:border-indigo-500 outline-none text-base font-extrabold text-center bg-slate-50">
                                <div id="storyStartBadge" class="flex-1 p-2.5 rounded-2xl bg-indigo-50 border border-indigo-200/80 text-xs font-bold text-indigo-900 truncate">
                                    🗡️ 1: Cây kiếm
                                </div>
                            </div>
                        </div>
                    </div>

                    <div>
                        <label for="storyItemsInput" class="block text-sm font-bold text-slate-700 mb-2">
                            2. Nhập danh sách kiến thức hoặc mốc năm cần ghi nhớ (mỗi ý 1 dòng):
                        </label>
                        <textarea id="storyItemsInput" rows="5" placeholder="Ví dụ:&#10;Hydro (H) - Nguyên tố nhẹ nhất vũ trụ&#10;Heli (He) - Khí bơm bóng bay&#10;Liti (Li) - Kim loại làm pin điện thoại..." class="w-full p-4 rounded-2xl border border-slate-200 focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/10 outline-none text-sm sm:text-base transition resize-none bg-slate-50/60 focus:bg-white"></textarea>
                    </div>

                    <button id="btnGenerateStory" onclick="generatePegStory()" class="w-full py-4 px-6 rounded-2xl bg-gradient-to-r from-indigo-600 via-violet-600 to-emerald-600 hover:from-indigo-700 hover:to-emerald-700 text-white font-extrabold text-base shadow-lg shadow-indigo-200 flex items-center justify-center gap-2.5 transition transform active:scale-[0.99]">
                        <i data-lucide="sparkles" class="w-5 h-5"></i>
                        <span>Biến Thành Câu Chuyện Móc Treo Ngay!</span>
                    </button>
                </div>
            </div>

            <!-- Kết quả câu chuyện -->
            <div id="storyResultContainer" class="hidden fade-in bg-white rounded-3xl p-5 sm:p-8 shadow-sm border border-indigo-200 space-y-6">
                <div class="flex flex-wrap items-center justify-between gap-3 pb-4 border-b border-slate-100">
                    <div>
                        <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-bold bg-emerald-50 text-emerald-700 mb-1.5">
                            <i data-lucide="check-circle-2" class="w-3.5 h-3.5"></i> ĐÃ GẮN MÓC TREO THÀNH CÔNG
                        </span>
                        <h3 id="storyResultTitle" class="text-xl font-extrabold text-slate-900"></h3>
                    </div>
                    <button onclick="copyGeneratedStory()" class="px-3.5 py-2 rounded-xl border border-slate-200 hover:bg-slate-50 text-xs font-bold text-slate-700 flex items-center gap-1.5 transition">
                        <i data-lucide="copy" class="w-3.5 h-3.5"></i> Sao chép kết quả
                    </button>
                </div>

                <!-- Bảng ánh xạ từng bước -->
                <div>
                    <h4 class="text-sm font-bold text-slate-700 mb-3 flex items-center gap-2">
                        <i data-lucide="pin" class="w-4 h-4 text-ind.html