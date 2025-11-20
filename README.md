# myweb
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>카테고리 선택 페이지 (모방)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;700;900&display=swap" rel="stylesheet">

    <style>
        body { font-family: 'Noto Sans KR', sans-serif; word-break: keep-all; }
        .prompt-item.hidden { display: none; }
        .tab-panel.hidden { display: none; }
        .option-btn.active {
            background-color: #eef2ff; border-color: #a5b4fc; color: #4338ca; font-weight: 600;
        }
        /* 스크롤바 커스텀 */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #c1c1c1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #a8a8a8; }
    </style>
</head>
<body class="bg-gray-50 p-6 sm:p-10 relative text-gray-800">

<!-- 전체 컨테이너 -->
<div class="max-w-4xl mx-auto">

    <!-- 상단 광고 배너 [수정: 링크 적용] -->
    <div class="mb-10 flex justify-center">
        <a href="https://www.adobe.com/kr/creativecloud/buy/students.html" target="_blank" rel="noopener noreferrer" title="Adobe 학생 할인 바로가기" class="block w-full overflow-hidden rounded-2xl shadow-lg border border-gray-200 hover:opacity-95 transition-opacity">
            <img src="https://i.postimg.cc/13Gy1SVH/seukeulinsyas-2025-11-17-005813.png" alt="상단 광고" class="w-full h-auto object-cover">
        </a>
    </div>

    <!-- 헤더 -->
    <div class="mb-10 text-center sm:text-left">
        <h1 class="text-4xl sm:text-5xl font-black text-gray-900 mb-3">프롬프트 허브</h1>
        <p class="text-lg sm:text-xl text-gray-500 font-medium">나에게 딱 맞는 AI 프롬프트를 찾거나 만들어보세요.</p>
    </div>

    <!-- 탭 네비게이션 -->
    <div class="mb-8">
        <nav class="flex space-x-6 border-b-2 border-gray-200">
            <button id="tab-gen-btn" class="pb-3 px-2 text-xl font-bold text-gray-400 border-b-4 border-transparent hover:text-gray-600 transition-all">생성</button>
            <button id="tab-exp-btn" class="pb-3 px-2 text-xl font-bold text-gray-900 border-b-4 border-gray-900 transition-all">탐색</button>
        </nav>
    </div>

    <!-- 탭 콘텐츠 -->
    <div class="min-h-[600px]">

        <!-- [생성 탭] -->
        <div id="tab-gen-content" class="tab-panel hidden bg-white rounded-3xl shadow-xl p-8 sm:p-10 border border-gray-100">
            <h2 class="text-2xl font-bold text-gray-900 mb-8">✨ 프롬프트 옵션 선택기</h2>
            <div class="mb-10">
                <label class="block text-lg font-bold text-gray-800 mb-3">1. 어떤 질문을 하고 싶으신가요?</label>
                <textarea id="ai-query-input" rows="4" class="block w-full rounded-2xl bg-gray-50 border-0 py-4 px-5 text-lg shadow-inner ring-1 ring-inset ring-gray-200 focus:ring-2 focus:ring-indigo-600 resize-none" placeholder="예: 주말에 보기 좋은 넷플릭스 영화 추천해줘"></textarea>
            </div>
            <div class="space-y-10" id="prompt-option-container">
                <h3 class="text-lg font-bold text-gray-800 mb-4">2. 원하는 스타일을 선택해주세요</h3>
                <!-- 옵션 그룹들 -->
                <div>
                    <label class="block text-xl font-bold text-gray-800 mb-4">말투</label>
                    <div class="flex flex-wrap gap-3" data-category="말투">
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="친근한">친근한</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="정중한">정중한</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="존댓말">존댓말</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="유머러스한">유머러스한</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="무례한">무례한</button>
                    </div>
                </div>
                <div>
                    <label class="block text-xl font-bold text-gray-800 mb-4">스타일</label>
                    <div class="flex flex-wrap gap-3" data-category="스타일">
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="정확하게">정확하게</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="간결하게">간결하게</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="자세하게">자세하게</button>
                    </div>
                </div>
                <div>
                    <label class="block text-xl font-bold text-gray-800 mb-4">독자수준</label>
                    <div class="flex flex-wrap gap-3" data-category="독자수준">
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="초등학생">초등학생</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="대학생">대학생</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="전문가">전문가</button>
                    </div>
                </div>
                <div>
                    <label class="block text-xl font-bold text-gray-800 mb-4">관점</label>
                    <div class="flex flex-wrap gap-3" data-category="관점">
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="개발자">개발자</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="디자이너">디자이너</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="마케터">마케터</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="기획자">기획자</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="교수">교수</button>
                    </div>
                </div>
                <div>
                    <label class="block text-xl font-bold text-gray-800 mb-4">포맷</label>
                    <div class="flex flex-wrap gap-3" data-category="포맷">
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="마크다운 형태">마크다운 형태</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="표 형태">표 형태</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="리스트">리스트</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="예시와 함께">예시와 함께</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="다이어그램으로 출력하기">다이어그램으로 출력하기</button>
                        <button class="option-btn rounded-full bg-white border border-gray-200 py-3 px-6 font-medium hover:bg-gray-50" data-value="대화문으로 출력하기">대화문으로 출력하기</button>
                    </div>
                </div>
            </div>
            <div class="flex flex-col-reverse sm:flex-row justify-end items-center gap-4 pt-10 border-t border-gray-100 mt-10">
                <button id="clear-options-btn" class="w-full sm:w-auto rounded-2xl bg-gray-100 py-4 px-8 text-lg font-bold text-gray-600 hover:bg-gray-200">초기화</button>
                <button id="generate-prompt-btn" class="w-full sm:w-auto rounded-2xl bg-indigo-600 py-4 px-10 text-lg font-bold text-white shadow-lg hover:bg-indigo-700 hover:-translate-y-0.5 transition-all">프롬프트 생성하기 ✨</button>
            </div>
            <div id="generated-prompt-container" class="hidden pt-10">
                <h3 class="text-2xl font-bold text-gray-900 mb-4">생성된 프롬프트</h3>
                <div class="relative mt-4">
                    <textarea id="generated-prompt-output" rows="12" class="block w-full rounded-2xl bg-gray-800 text-white border-0 py-6 px-8 text-lg shadow-inner leading-relaxed whitespace-pre-wrap resize-none focus:ring-0" readonly></textarea>
                    <button id="copy-generated-btn" class="absolute top-4 right-4 inline-flex justify-center items-center rounded-xl bg-white/10 backdrop-blur-sm border border-white/20 py-2 px-4 text-sm font-bold text-white hover:bg-white/20">복사</button>
                </div>
            </div>
        </div>

        <!-- [탐색 탭] -->
        <div id="tab-exp-content" class="tab-panel">
            <div class="bg-white rounded-3xl shadow-sm border border-gray-100 p-6 sm:p-10 mb-8">
                <!-- 검색창 -->
                <div class="mb-10 relative group">
                    <div class="absolute inset-y-0 left-0 pl-5 flex items-center pointer-events-none">
                        <svg class="h-6 w-6 text-gray-400 group-focus-within:text-indigo-500" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" /></svg>
                    </div>
                    <input type="text" id="prompt-search" class="block w-full rounded-full bg-gray-50 border-0 py-4 pl-14 pr-5 text-gray-900 text-lg ring-1 ring-inset ring-gray-200 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus:bg-white transition-all" placeholder="어떤 프롬프트를 찾으시나요? (예: 블로그, 마케팅)">
                </div>

                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-900 mb-4 sm:mb-0">카테고리</h2>
                    <button id="reset-filters" class="text-base font-semibold text-gray-500 hover:text-indigo-600 flex items-center">
                        <svg class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" /></svg> 초기화
                    </button>
                </div>

                <!-- 필터 -->
                <div class="border-t border-gray-100 pt-6">
                    <ul class="flex flex-wrap gap-3" id="category-filters">
                        <li><input type="checkbox" id="check-writing" value="writing" class="hidden peer"><label for="check-writing" class="inline-flex items-center justify-center px-5 py-2.5 border border-gray-200 rounded-full text-base font-bold text-gray-500 bg-white cursor-pointer hover:bg-gray-50 peer-checked:bg-black peer-checked:text-white peer-checked:border-black">✍️ 글쓰기</label></li>
                        <li><input type="checkbox" id="check-calc" value="calc" class="hidden peer"><label for="check-calc" class="inline-flex items-center justify-center px-5 py-2.5 border border-gray-200 rounded-full text-base font-bold text-gray-500 bg-white cursor-pointer hover:bg-gray-50 peer-checked:bg-black peer-checked:text-white peer-checked:border-black">🧮 계산</label></li>
                        <li><input type="checkbox" id="check-search" value="search" class="hidden peer"><label for="check-search" class="inline-flex items-center justify-center px-5 py-2.5 border border-gray-200 rounded-full text-base font-bold text-gray-500 bg-white cursor-pointer hover:bg-gray-50 peer-checked:bg-black peer-checked:text-white peer-checked:border-black">🔍 검색</label></li>
                        <li><input type="checkbox" id="check-life" value="life" class="hidden peer"><label for="check-life" class="inline-flex items-center justify-center px-5 py-2.5 border border-gray-200 rounded-full text-base font-bold text-gray-500 bg-white cursor-pointer hover:bg-gray-50 peer-checked:bg-black peer-checked:text-white peer-checked:border-black">🌿 생활</label></li>
                        <li><input type="checkbox" id="check-travel" value="travel" class="hidden peer"><label for="check-travel" class="inline-flex items-center justify-center px-5 py-2.5 border border-gray-200 rounded-full text-base font-bold text-gray-500 bg-white cursor-pointer hover:bg-gray-50 peer-checked:bg-black peer-checked:text-white peer-checked:border-black">✈️ 여행</label></li>
                    </ul>
                </div>
            </div>

            <!-- 목록 -->
            <div class="cont mt-10">
                <div class="flex justify-between items-center mb-6 px-2">
                    <h3 class="text-2xl font-bold text-gray-900">프롬프트 목록 <span id="prompt-count" class="text-indigo-600 ml-1">107</span><span class="text-gray-400 text-lg font-medium ml-1">건</span></h3>
                </div>
                <ul id="prompt-list" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- 107개 항목 시작 -->
                    <!-- [글쓰기] 22개 -->
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">블로그 포스팅 1000자 분량으로 작성해줘. 주제: [주제 입력]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">이 이메일 초안을 좀 더 정중하고 전문적인 톤으로 수정해줘: [초안 내용]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">유튜브 영상 대본을 만들어줘. 5분 분량, 주제: [주제 입력]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">매력적인 인스타그램 광고 카피 3가지를 제안해줘. 제품: [제품명]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">이 보고서의 서론을 더 학술적인 문체로 다듬어줘: [보고서 서론 내용]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">졸업 논문 연구 계획서의 목차를 잡아줘. 주제: [주제]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">팀 프로젝트 발표용 스크립트를 10분 분량으로 작성해 줘. 역할: [본인 역할], 주제: [주제]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">교수님께 성적 정정 요청 메일을 정중하게 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">자기소개서 지원동기 항목 초안 좀 잡아줘. 지원 회사: [회사명], 직무: [직무명]</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[상품/서비스] 이름과 핵심 기능을 바탕으로, 설득력 있는 한 문장짜리 광고 헤드라인 5가지를 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[책/영화 제목]의 줄거리를 포함하지 않고, 독자/관객의 호기심을 자극하는 리뷰 도입부 3가지를 제안해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[주제]에 대한 [긍정/부정] 입장을 가진 논설문의 3단 논법(서론-본론-결론) 개요를 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[회사명] [직무]에 지원하는 경력직 자기소개서의 '주요 성과' 항목 초안을 작성해줘. 나의 주요 성과는 [성과 1], [성과 2]야.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[회의 주제]에 대한 회의를 소집하는 공식적인 이메일을 작성해줘. 참석자: [이름 목록], 일시: [날짜와 시간].</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[복잡한 전문 용어]의 의미를, [비유할 대상]에 빗대어 비전문가도 이해하기 쉽게 설명하는 글을 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[개인적인 경험]을 주제로, 감성적인 톤의 에세이 한 단락(약 300자)을 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[제품]의 사용 후기를 [장점], [단점]을 포함하여 솔직하고 유용한 스타일로 작성해줘. (블로그 포스팅용)</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[사과할 내용]에 대해 비즈니스 파트너에게 보내는 정중한 사과 이메일 초안을 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[키워드 1, 2, 3]을 모두 포함하는 SEO 최적화 블로그 포스트 제목 10가지를 제안해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">동료들의 공감을 얻을 수 있는 LinkedIn 포스트 초안을 [150자] 이내로 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[제품명]의 [핵심 기능 3가지]를 강조하는, 고객의 구매를 유도하는 상세 페이지 설명을 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="writing"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-blue-50 text-blue-600">글쓰기</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-indigo-700 transition-colors">[토론 주제]에 대해 [찬성/반대] 입장에서 사용할 수 있는 강력한 근거 3가지와 예상 반론을 작성해줘.</p></div></li>

                    <!-- [계산] 20개 -->
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">월 예산 계획 좀 세워줘. 월 수입 [금액], 고정 지출: [항목과 금액들]</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">서울에서 부산까지 자동차 예상 유류비를 계산해줘. (차종: [차종], 현재 유가: [가격])</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">복리 이자 계산: 원금 [금액], 연이율 [X]%, 기간 [Y]년</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">이번 학기 학점 평균(GPA)을 계산해 줘. (과목 1: [학점, 성적], 과목 2: ...)</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[A 제품 가격], [B 제품 가격]을 각각 [A 할인율]%, [B 할인율]% 할인했을 때, 어떤 제품이 얼마나 더 저렴한지 계산해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[주식 종목명]을 [매수 가격]에 [보유 주식 수]주 만큼 매수했고, 현재 [현재 가격]이야. 나의 총 수익률과 수익금은 얼마야? (수수료/세금 제외)</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[X]평방미터(m²)를 평(坪) 단위로 환산해줘. (1평 = 3.305785m² 기준)</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[대출 원금]을 [연 이율]%로 [상환 기간]년 동안 [원리금/원금] 균등 상환 시, 월 상환액과 총이자는 얼마야?</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[여러 국가의 화폐와 금액 리스트, 예: 100 USD, 5000 JPY]를 현재 환율 기준으로 모두 한국 원(KRW)으로 환산하고 총합을 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[레시피의 기준 인분]인분 기준의 레시피([재료 1: 양], [재료 2: 양])를 [필요한 인분]인분 기준으로 재료 양을 다시 계산해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[시작 날짜]부터 [종료 날짜]까지 총 몇 주, 며칠이 지났는지 계산해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[현재 시각]을 기준으로 [X]시간 [Y]분 뒤의 시각은 몇 시 몇 분이야?</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[총 금액]을 [참석 인원 수]명으로 나누어 더치페이할 금액을 계산하고, [송금받을 계좌번호]와 함께 안내 메시지를 작성해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[총 급여액]에서 4대 보험(국민연금 [X]%, 건강보험 [Y]%)과 소득세를 제외한 실수령액을 추정해줘. (비과세액: [금액])</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">나의 키 [X]cm, 몸무게 [Y]kg이야. 내 BMI 지수를 계산하고, [WHO/아시아] 기준 비만도를 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[A 은행 금리] vs [B 은행 금리] 주택 담보 대출 이자 차이 계산해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[구매 금액]에 [부가세]%를 더한 최종 결제 금액을 계산해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">오늘 먹은 음식([음식 리스트])의 총 섭취 칼로리를 계산해줘.</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[프로젝트 시작일]부터 [영업일 수]일 후의 예상 완료 날짜는? (주말 제외)</p></div></li>
                    <li class="prompt-item group" data-category="calc"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-green-50 text-green-600">계산</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-green-700 transition-colors">[도시 A]의 [시각]은 [도시 B]의 현지 시각으로 언제야?</p></div></li>

                    <!-- [검색] 20개 -->
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">2025년 최신 마케팅 트렌드 5가지를 요약해서 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">파이썬에서 'KeyError'를 해결하는 일반적인 방법들을 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[논문 주제]에 대한 최신 연구 동향 5가지를 요약해 줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[키워드]와 관련된 주요 학술 저널과 논문 3편을 추천해 줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[교수님 성함] 교수님의 주요 연구 분야와 최근 발표 논문을 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[특정 질병]의 초기 증상, 원인, 예방 수칙을 신뢰할 수 있는 출처로 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[경쟁사 A]와 [경쟁사 B]의 최근 1년간 주요 활동을 비교 분석해줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[법률 조항]의 정확한 내용과 관련 판례 1~2개를 요약해줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[IT 기술 용어]의 개념과 실제 기업 사용 사례를 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[역사적 사건]에 대한 [A 관점]과 [B 관점]의 주장을 비교해줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[제품 A]와 [제품 B]의 스펙을 표로 비교 정리해줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[도시]에서 [월]에 열리는 주요 축제나 행사를 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[산업 분야]의 글로벌 시장 점유율 Top 5 기업과 이유를 요약해줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[A 물질]과 [B 물질] 상호작용 및 부작용에 대해 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[영화 제목]에 대한 평론가들의 긍정/부정 평가를 요약해줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[작업, 예: 텐트 치기] 초보자를 위한 단계별 가이드와 영상 링크를 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[언어]에서 [API]를 사용하는 예제 코드와 문서를 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[내 위치] 근처 [24시간 약국] 위치와 연락처를 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[분야]의 업계 모범 사례(Best Practice) 5가지를 찾아줘.</p></div></li>
                    <li class="prompt-item group" data-category="search"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-yellow-100 text-yellow-800">검색</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-yellow-700 transition-colors">[기업]의 [전략] 성공 사례 분석 자료를 찾아 요약해줘.</p></div></li>

                    <!-- [생활] 20개 -->
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">현재 기온 [X]도인데, 오늘 날씨에 맞는 옷차림 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">오늘 저녁 메뉴 추천해줘. 재료: [가지고 있는 재료]</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">세탁하려는 옷의 재질은 [재질]. 손상 없이 세탁하는 방법 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">오늘 할 일: [목록]. 활동 시간: [시간]. 효율적인 일정표 만들어줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[얼룩 종류] 얼룩이 [옷 재질]에 묻었을 때 응급 처치 방법 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[반려 식물] 물 주기, 햇빛, 분갈이 등 관리법 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[운동 목적]을 위한 주 3회 [수준] 헬스 루틴 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[이사 갈 동네]의 장단점(교통, 학군)을 [가구 형태] 관점에서 요약해줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[D-day] 3일 전부터 컨디션 관리를 위한 루틴 제안해줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[대상]에게 [예산] 내외로 선물하기 좋은 아이템 5가지 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[증상] 완화에 좋은 차(tea) 3가지와 효능 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[카드 A], [카드 B] 혜택 비교하고 내 주 소비처([소비처])에 유리한 카드 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[고민]에 대해 [MBTI] 친구처럼 공감하고 해결책 2가지 줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[물건] 버리는 방법과 [지역] 대형 폐기물 처리 비용 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">여름철 에어컨 전기세 아끼면서 시원하게 지내는 팁 5가지 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">집에 있는 재료([재료])로 천연 모기 기피제 만드는 법 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">흰 운동화 집에서 하얗게 세탁하는 방법 단계별로 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[쓰레기 종류] 분리수거 방법 정확하게 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">[OTT]에서 이번 주말 정주행하기 좋은 [장르] 드라마 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="life"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-purple-100 text-purple-800">생활</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-purple-700 transition-colors">편의점 다이어트 간식(저칼로리, 고단백) 3가지 추천해줘.</p></div></li>

                    <!-- [여행] 25개 -->
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">인천공항에서 [지역]까지 비행시간 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지], [일 수], [테마] 일정표 만들어줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지], [일 수], [계절] 준비물 리스트 만들어줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 필수 현지 음식 5가지 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지]의 [월] 날씨 어때?</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지], [인원], [유형], [조건]에 맞는 숙소 3곳 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] [테마] 1일 도보 코스 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[국가] 기본 인사말과 문화 팁 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[공항]에서 [숙소] 가는 [방법]과 비용 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] [활동] 예약 가능한 투어 사이트 3곳 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] [기념품] 구매 팁 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[예산]으로 [여행지] [기간] 여행 시 항공/숙박/식비 배분해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] [현 위치] 근처 현지인 맛집 3곳 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[국가] [통신사 A], [통신사 B] 유심 가격 비교해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 위급 상황 발생 시 대처 매뉴얼과 연락처 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">장거리 비행 기내 꿀팁과 준비물 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 대중교통 이용법과 패스 추천해줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 치안 상황과 주의할 점 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 텍스 리펀 받는 방법과 위치 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">남은 [외화] 동전 처리 방법 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[국가] 입국 신고서 작성 예시 보여줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 브이로그 영상 콘티 짜줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 현지인 친구 사귀기 좋은 대화 주제 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">[여행지] 전통 의상 체험 정보와 사진 명소 알려줘.</p></div></li>
                    <li class="prompt-item group" data-category="travel"><div class="bg-white border border-gray-100 rounded-2xl p-6 h-full shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 cursor-pointer"><div class="flex items-start justify-between mb-3"><span class="inline-block px-3 py-1 rounded-lg text-sm font-bold bg-teal-100 text-teal-800">여행</span></div><p class="text-lg font-bold text-gray-800 group-hover:text-teal-700 transition-colors">한 달 살기 준비 체크리스트(숙소, 비자, 비용 등) 만들어줘.</p></div></li>
                </ul>
            </div>
        </div>
    </div>
</div>

<!-- 사이드 광고 배너 [링크 적용] -->
<div id="side-ad-banner" class="hidden 2xl:block absolute top-40 right-8 w-[240px] space-y-4">
    <a href="https://www.adobe.com/kr/creativecloud/buy/students.html" target="_blank" rel="noopener noreferrer" title="Adobe 학생 할인 바로가기" class="block hover:opacity-90 transition-opacity">
        <img src="https://i.postimg.cc/v8Cy1TrF/20251117-010005.png" alt="사이드 광고 1" class="w-full h-auto rounded-2xl shadow-lg border border-gray-200">
    </a>
    <a href="https://www.adobe.com/kr/creativecloud/buy/students.html" target="_blank" rel="noopener noreferrer" title="Adobe 학생 할인 바로가기" class="block hover:opacity-90 transition-opacity">
        <img src="https://i.postimg.cc/6QSbjkH0/20251117-234339.png" alt="사이드 광고 2" class="w-full h-auto rounded-2xl shadow-lg border border-gray-200">
    </a>
</div>

<!-- 토스트 알림 -->
<div id="copy-toast" class="fixed bottom-10 right-10 bg-gray-900/90 backdrop-blur-sm text-white px-8 py-4 rounded-2xl shadow-2xl transition-all duration-500 opacity-0 invisible transform translate-y-10 z-50 flex items-center gap-3 font-bold text-lg border border-white/10">
    <svg class="h-6 w-6 text-green-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>
    <span>복사 완료!</span>
</div>

<!-- 스크립트 -->
<script>
    document.addEventListener('DOMContentLoaded', () => {
        const toast = document.getElementById('copy-toast');
        let toastTimer;

        const tabs = {
            genBtn: document.getElementById('tab-gen-btn'),
            expBtn: document.getElementById('tab-exp-btn'),
            genContent: document.getElementById('tab-gen-content'),
            expContent: document.getElementById('tab-exp-content')
        };

        const expElements = {
            filters: document.querySelectorAll('#category-filters input[type="checkbox"]'),
            prompts: document.querySelectorAll('#prompt-list .prompt-item'),
            promptCount: document.getElementById('prompt-count'),
            resetBtn: document.getElementById('reset-filters'),
            searchInput: document.getElementById('prompt-search')
        };

        const genElements = {
            aiQueryInput: document.getElementById('ai-query-input'),
            optionButtons: document.querySelectorAll('.option-btn'),
            clearBtn: document.getElementById('clear-options-btn'),
            generateBtn: document.getElementById('generate-prompt-btn'),
            container: document.getElementById('generated-prompt-container'),
            output: document.getElementById('generated-prompt-output'),
            copyBtn: document.getElementById('copy-generated-btn')
        };

        function copyToClipboard(text) {
            const textarea = document.createElement('textarea');
            textarea.value = text;
            textarea.style.position = 'fixed';
            textarea.style.left = '-9999px';
            document.body.appendChild(textarea);
            textarea.select();
            try { document.execCommand('copy'); showToast(); }
            catch (err) { console.error(err); }
            document.body.removeChild(textarea);
        }

        function showToast() {
            clearTimeout(toastTimer);
            toast.classList.remove('opacity-0', 'invisible', 'translate-y-10');
            toast.classList.add('opacity-100', 'visible', 'translate-y-0');
            toastTimer = setTimeout(() => {
                toast.classList.remove('opacity-100', 'visible', 'translate-y-0');
                toast.classList.add('opacity-0', 'invisible', 'translate-y-10');
            }, 2000);
        }

        function showTab(tabName) {
            const activeClass = ['text-gray-900', 'border-gray-900'];
            const inactiveClass = ['text-gray-400', 'border-transparent'];
            if (tabName === 'gen') {
                tabs.genContent.classList.remove('hidden');
                tabs.expContent.classList.add('hidden');
                tabs.genBtn.classList.add(...activeClass);
                tabs.genBtn.classList.remove(...inactiveClass);
                tabs.expBtn.classList.add(...inactiveClass);
                tabs.expBtn.classList.remove(...activeClass);
            } else {
                tabs.genContent.classList.add('hidden');
                tabs.expContent.classList.remove('hidden');
                tabs.genBtn.classList.add(...inactiveClass);
                tabs.genBtn.classList.remove(...activeClass);
                tabs.expBtn.classList.add(...activeClass);
                tabs.expBtn.classList.remove(...inactiveClass);
            }
        }
        tabs.genBtn.addEventListener('click', () => showTab('gen'));
        tabs.expBtn.addEventListener('click', () => showTab('exp'));

        genElements.optionButtons.forEach(button => {
            button.addEventListener('click', () => {
                const siblings = button.parentElement.querySelectorAll('.option-btn');
                const wasActive = button.classList.contains('active');
                siblings.forEach(sibling => sibling.classList.remove('active'));
                if (!wasActive) button.classList.add('active');
            });
        });

        genElements.clearBtn.addEventListener('click', () => {
            genElements.aiQueryInput.value = '';
            genElements.optionButtons.forEach(button => button.classList.remove('active'));
            genElements.container.classList.add('hidden');
            genElements.output.value = '';
        });

        genElements.generateBtn.addEventListener('click', () => {
            let finalPrompt = "";
            const baseQuery = genElements.aiQueryInput.value.trim();
            if (baseQuery) finalPrompt += `## 요청사항\n- ${baseQuery}\n\n`;

            const selectedMap = new Map();
            genElements.optionButtons.forEach(btn => {
                if (btn.classList.contains('active')) {
                    const cat = btn.parentElement.dataset.category;
                    if (!selectedMap.has(cat)) selectedMap.set(cat, []);
                    selectedMap.get(cat).push(btn.dataset.value);
                }
            });

            selectedMap.forEach((vals, cat) => {
                finalPrompt += `## ${cat}\n`;
                vals.forEach(v => finalPrompt += `- ${v}\n`);
                finalPrompt += `\n`;
            });

            if (finalPrompt.trim() === "") {
                genElements.output.value = "요청사항을 입력하거나 옵션을 선택해주세요.";
                genElements.container.classList.remove('hidden');
            } else {
                genElements.output.value = finalPrompt.trim();
                genElements.container.classList.remove('hidden');
                genElements.container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
            }
        });

        genElements.copyBtn.addEventListener('click', () => {
            if (genElements.output.value) copyToClipboard(genElements.output.value);
        });

        function filterPrompts() {
            const checked = Array.from(expElements.filters).filter(i => i.checked).map(i => i.value);
            const search = expElements.searchInput.value.toLowerCase().trim();
            let visibleCount = 0;

            expElements.prompts.forEach(p => {
                const cat = p.dataset.category;
                const txt = p.querySelector('p').textContent.toLowerCase();
                const catMatch = checked.length === 0 || checked.includes(cat);
                const searchMatch = search === "" || txt.includes(search);

                if (catMatch && searchMatch) {
                    p.classList.remove('hidden');
                    visibleCount++;
                } else {
                    p.classList.add('hidden');
                }
            });
            expElements.promptCount.textContent = visibleCount;
        }

        expElements.filters.forEach(i => i.addEventListener('change', filterPrompts));
        expElements.searchInput.addEventListener('input', filterPrompts);

        expElements.resetBtn.addEventListener('click', () => {
            expElements.filters.forEach(i => i.checked = false);
            expElements.searchInput.value = '';
            filterPrompts();
        });

        document.getElementById('prompt-list').addEventListener('click', (e) => {
            const item = e.target.closest('.prompt-item');
            if (item) {
                copyToClipboard(item.querySelector('p').textContent.trim());
            }
        });

        filterPrompts();
    });
</script>
</body>
</html>
