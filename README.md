<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>เกมสร้างภาวะผู้นำ (Leadership Game)</title>
    
    <style>
        body {
            font-family: 'Tahoma', sans-serif;
            background-color: #e8f5e9;
            color: #2e7d32;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        header {
            background-color: #4caf50;
            color: white;
            width: 100%;
            text-align: center;
            padding: 20px 0;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        #game-container {
            background: #ffffff;
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0,0,0,0.2);
            padding: 30px;
            width: 90%;
            max-width: 800px;
            margin: 20px auto;
        }

        #status-bar {
            display: flex;
            justify-content: space-around;
            padding: 15px;
            margin-bottom: 25px;
            border-bottom: 3px solid #c8e6c9;
            font-weight: bold;
            font-size: 1.1em;
        }

        #question-area {
            margin-bottom: 30px;
            padding: 20px;
            border: 1px dashed #a5d6a7;
            border-radius: 10px;
        }

        #question-text {
            font-size: 1.2em;
            font-weight: 500;
            margin-bottom: 20px;
        }

        #options-area {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        .answer-btn {
            padding: 18px;
            border: none;
            background-color: #66bb6a;
            color: white;
            font-size: 1em;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.1s;
        }

        .answer-btn:hover:not(:disabled) {
            background-color: #43a047;
            transform: translateY(-2px);
        }

        .answer-btn:disabled {
            opacity: 0.5;
            cursor: default;
        }

        #reward-area {
            text-align: center;
            padding: 20px;
            background-color: #fff9c4;
            border: 2px solid #ffeb3b;
            border-radius: 10px;
        }

        #money-boards {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px 0;
        }

        .board-card {
            width: 110px;
            height: 110px;
            background-color: #ffc107;
            color: #333;
            font-size: 36px;
            font-weight: bold;
            border-radius: 10px;
            border: 4px solid #ff9800;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.5s;
            line-height: 100px;
        }

        .board-card:hover:not(.revealed) {
            transform: scale(1.05);
        }

        .board-card.revealed {
            background-color: #e91e63;
            color: white;
            cursor: default;
        }

        #next-stage-btn, #finish-game-btn {
            padding: 15px 30px;
            font-size: 1.1em;
            background-color: #1976d2;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 15px;
        }

        .hidden {
            display: none !important;
        }

        #school-creation {
            text-align: center;
            padding: 40px 20px;
            border: 3px solid #4caf50;
            border-radius: 15px;
        }
        
        #school-creation h2 {
            color: #4caf50;
        }

        #school-name-input {
            padding: 10px;
            width: 70%;
            margin: 15px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
    </style>
</head>
<body>

    <header>
        <h1>เกมสร้างภาวะผู้นำในตัวเอง: สร้างโรงเรียนแห่งความสำเร็จ</h1>
    </header>

    <main id="game-container">
        
        <section id="status-bar">
            <p>💰 เงินทุน: <span id="current-money">0</span> บาท</p>
            <p>⭐ Section: <span id="current-section">1</span> / 4</p>
            <p>🎯 ภารกิจ: <span id="current-mission">1</span> / 5</p>
        </section>

        <section id="game-stage">
            <h2 id="stage-title">Section 1: วิสัยทัศน์และการตัดสินใจ (ภารกิจที่ 1)</h2>
            
            <div id="question-area">
                <p id="question-text">Loading...</p>
                <div id="options-area">
                </div>
            </div>
            
            <div id="reward-area" class="hidden">
                <h3 id="reward-message">🎉 คำตอบถูกต้อง! ได้รับสิทธิ์เปิดแผ่นป้ายเงินทุน <span id="board-count">0</span> แผ่น</h3>
                <div id="money-boards">
                </div>
                <button id="next-stage-btn" class="hidden">ไปยังภารกิจถัดไป &gt;</button>
            </div>

            <div id="school-creation" class="hidden">
                <h2>สำเร็จ! คุณคือผู้นำที่สร้างโรงเรียนแห่งความสำเร็จ!</h2>
                <div id="school-blueprint">
                    <p style="font-size: 2em;">🏫</p>
                    <h3>เงินทุนรวมที่สะสม: <span id="total-money">0</span> บาท</h3>
                    <p>จากการสำรวจภาวะผู้นำของคุณ คุณได้สร้างห้องเรียน/อาคารรวม <span id="room-count">0</span> ห้องเรียน</p>
                    <input type="text" id="school-name-input" placeholder="ตั้งชื่อโรงเรียนของคุณอย่างเป็นทางการ">
                    <button id="finish-game-btn">ดูผลวิเคราะห์ภาวะผู้นำ</button>
                </div>
            </div>
        </section>
    </main>

    <script>
        // --- 1. ข้อมูลเกมและคำถามทั้งหมด (ขยายให้ครบ 4 Section x 5 ภารกิจ) ---
        const GAME_DATA = [
            // Section 1: 5 Questions
            {
                section: 1,
                title: "วิสัยทัศน์และการตัดสินใจ",
                questions: [
                    { id: 101, text: "ภารกิจ 1: ผู้นำที่ดีควรใช้หลักการใดในการจัดลำดับความสำคัญของงาน?", options: { A: "งานที่ชอบที่สุด", B: "งานที่เร่งด่วนและสำคัญ", C: "งานที่ง่ายและเสร็จเร็ว", D: "งานที่มีคนสั่งมา" }, answer: "B" },
                    { id: 102, text: "ภารกิจ 2: คุณจะสื่อสารวิสัยทัศน์กับทีมอย่างไร?", options: { A: "ส่งอีเมลสั้นๆ", B: "จัดประชุมใหญ่ที่น่าเบื่อ", C: "พูดคุยรายคนอย่างเป็นกันเอง", D: "ใช้ทุกช่องทางเพื่อสร้างความเข้าใจร่วมกัน" }, answer: "D" },
                    { id: 103, text: "ภารกิจ 3: เมื่อเกิดความผิดพลาด ผู้นำควรทำอย่างไร?", options: { A: "ตำหนิทีมทันที", B: "หาผู้รับผิดชอบอย่างรวดเร็ว", C: "วิเคราะห์และเรียนรู้จากความผิดพลาด", D: "ทำเป็นไม่รู้ไม่เห็น" }, answer: "C" },
                    { id: 104, text: "ภารกิจ 4: การตัดสินใจที่ยากที่สุดสำหรับคุณคือ?", options: { A: "เลือกอาหารกลางวัน", B: "เลือกกลยุทธ์ทางธุรกิจในภาวะวิกฤต", C: "เลือกเสื้อผ้าที่ใส่", D: "เลือกเพื่อนร่วมงาน" }, answer: "B" },
                    { id: 105, text: "ภารกิจ 5: อะไรคือการวัดผลความสำเร็จที่สำคัญที่สุด?", options: { A: "จำนวนเงินเดือนที่ได้รับ", B: "ความสุขและสุขภาพจิตของทีม", C: "ผลกำไรในระยะสั้น", D: "การเติบโตอย่างยั่งยืนขององค์กรและบุคลากร" }, answer: "D" },
                ]
            },
            // Section 2: 5 Questions (จำลอง)
            {
                section: 2,
                title: "การสร้างแรงจูงใจและการมอบหมายงาน",
                questions: [
                    { id: 201, text: "ภารกิจ 1: การสร้างแรงจูงใจแบบใดมีประสิทธิภาพที่สุด?", options: { A: "ขู่ว่าจะลงโทษ", B: "ให้เงินรางวัลเยอะๆ", C: "ให้อิสระและความรับผิดชอบในงาน", D: "ชมเชยทุกครั้งที่ทำสำเร็จ" }, answer: "C" },
                    { id: 202, text: "ภารกิจ 2: เมื่อมอบหมายงาน ผู้นำควรทำอย่างไร?", options: { A: "ปล่อยให้ทำเองโดยไม่ยุ่งเกี่ยว", B: "ควบคุมทุกขั้นตอนอย่างละเอียด", C: "กำหนดเป้าหมายที่ชัดเจนและสนับสนุนเครื่องมือ", D: "แค่บอกว่าทำอะไรก็พอ" }, answer: "C" },
                    { id: 203, text: "ภารกิจ 3: จะรับมือกับทีมที่ขาดความเชื่อมั่นได้อย่างไร?", options: { A: "ไม่สนใจและรอให้ดีขึ้นเอง", B: "ให้กำลังใจด้วยคำพูดอย่างเดียว", C: "สร้างความสำเร็จเล็กๆ ให้พวกเขาเห็นคุณค่าตัวเอง", D: "เปลี่ยนทีมใหม่ทันที" }, answer: "C" },
                    { id: 204, text: "ภารกิจ 4: การสื่อสารแบบสองทางคืออะไร?", options: { A: "พูดอย่างเดียว", B: "ฟังอย่างเดียว", C: "พูดและฟังอย่างมีประสิทธิภาพ", D: "ไม่พูดเลย" }, answer: "C" },
                    { id: 205, text: "ภารกิจ 5: การให้คำติชมที่สร้างสรรค์ควรเป็นอย่างไร?", options: { A: "ต่อหน้าทุกคน", B: "มุ่งเน้นที่ตัวบุคคล", C: "มุ่งเน้นที่พฤติกรรมที่ต้องปรับปรุง", D: "รอจนจบโครงการจึงค่อยบอก" }, answer: "C" },
                ]
            },
            // Section 3: 5 Questions (จำลอง)
            {
                section: 3,
                title: "ความสามารถในการปรับตัวและการเรียนรู้",
                questions: [
                    { id: 301, text: "ภารกิจ 1: ผู้นำควรทำอย่างไรในสถานการณ์ที่เปลี่ยนแปลงเร็ว?", options: { A: "ยึดติดกับแผนเดิม", B: "เปิดรับข้อมูลใหม่และปรับแผนอย่างยืดหยุ่น", C: "ปิดกั้นข้อมูลภายนอก", D: "หนีปัญหา" }, answer: "B" },
                    { id: 302, text: "ภารกิจ 2: 'Growth Mindset' คืออะไร?", options: { A: "คิดว่าเก่งแล้วไม่ต้องเรียนรู้", B: "เชื่อว่าความสามารถพัฒนาได้ด้วยความพยายาม", C: "ไม่ชอบความท้าทาย", D: "คิดเล็ก" }, answer: "B" },
                    { id: 303, text: "ภารกิจ 3: จะสร้างวัฒนธรรมการเรียนรู้ในทีมอย่างไร?", options: { A: "ลงโทษเมื่อผิดพลาด", B: "ส่งไปอบรมอย่างเดียว", C: "ให้เวลาและพื้นที่สำหรับการทดลองและล้มเหลว", D: "จ้างคนเก่งมาทำแทน" }, answer: "C" },
                    { id: 304, text: "ภารกิจ 4: การยอมรับความผิดพลาดของตนเองบ่งบอกถึงอะไร?", options: { A: "ความอ่อนแอ", B: "ความเข้มแข็งและซื่อสัตย์", C: "ความไม่แน่นอน", D: "ความโง่เขลา" }, answer: "B" },
                    { id: 305, text: "ภารกิจ 5: เทคโนโลยีมีผลต่อภาวะผู้นำอย่างไร?", options: { A: "ไม่มีเลย", B: "ทำให้ทำงานง่ายขึ้น", C: "บังคับให้ต้องปรับตัวและเรียนรู้ตลอดเวลา", D: "เพิ่มงาน" }, answer: "C" },
                ]
            },
            // Section 4: 5 Questions (จำลอง)
            {
                section: 4,
                title: "การสร้างความร่วมมือและมรดกผู้นำ",
                questions: [
                    { id: 401, text: "ภารกิจ 1: การสร้างความร่วมมือข้ามสายงานต้องเริ่มจากอะไร?", options: { A: "กฎเกณฑ์ที่เข้มงวด", B: "การสร้างความเชื่อใจและเป้าหมายร่วมกัน", C: "เงินเดือนที่เท่าเทียม", D: "การแข่งขัน" }, answer: "B" },
                    { id: 402, text: "ภารกิจ 2: คุณจะเตรียมผู้นำรุ่นต่อไปอย่างไร?", options: { A: "เก็บความรู้ไว้คนเดียว", B: "ให้โอกาสฝึกฝนและรับผิดชอบงานสำคัญ", C: "เน้นงานปัจจุบันเท่านั้น", D: "จ้างคนจากภายนอก" }, answer: "B" },
                    { id: 403, text: "ภารกิจ 3: บทบาทของผู้นำในการแก้ไขความขัดแย้งคือ?", options: { A: "เลือกข้างที่ชนะ", B: "เป็นคนกลางไกล่เกลี่ยและหาทางออกร่วมกัน", C: "หลีกเลี่ยงความขัดแย้ง", D: "ตัดสินด้วยอำนาจ" }, answer: "B" },
                    { id: 404, text: "ภารกิจ 4: การสร้างมรดกผู้นำหมายถึงอะไร?", options: { A: "ชื่อเสียงส่วนตัว", B: "ความร่ำรวยขององค์กร", C: "การสร้างระบบที่ดีและบุคลากรที่มีคุณภาพ", D: "อาคารใหญ่โต" }, answer: "C" },
                    { id: 405, text: "ภารกิจ 5: เป้าหมายสุดท้ายของการเป็นผู้นำคือ?", options: { A: "ควบคุมทุกคน", B: "ทำให้องค์กรอยู่ได้ด้วยตนเองโดยไม่ต้องมีคุณ", C: "รับคำชม", D: "มีอำนาจสูงสุด" }, answer: "B" },
                ]
            }
        ];

        // --- 2. ตัวแปรสถานะของเกม (Game State) ---
        let gameState = {
            currentSection: 1,
            currentMission: 1, // 1-5
            totalMoney: 0,
            moneyBoardsOpened: 0,
            boardsAllowed: 0,
            isQuestionAnswered: false,
        };

        // --- 3. ฟังก์ชันอัปเดต UI สถานะเกม ---
        function updateStatusUI() {
            document.getElementById('current-money').textContent = gameState.totalMoney.toLocaleString('th-TH');
            document.getElementById('current-section').textContent = gameState.currentSection;
            document.getElementById('current-mission').textContent = gameState.currentMission;
            
            // อัปเดตข้อมูลในหน้าสร้างโรงเรียนด้วย
            document.getElementById('total-money').textContent = gameState.totalMoney.toLocaleString('th-TH');
            const rooms = Math.floor(gameState.totalMoney / 50000); // 1 ห้องใช้ 50,000 บาท
            document.getElementById('room-count').textContent = rooms;
        }

        // --- 4. ฟังก์ชันจัดการเมื่อตอบคำถาม ---
        function handleAnswer(questionId, selectedChoice) {
            if (gameState.isQuestionAnswered) return;
            
            const sectionIndex = gameState.currentSection - 1;
            const missionIndex = gameState.currentMission - 1;
            const question = GAME_DATA[sectionIndex].questions[missionIndex];

            gameState.isQuestionAnswered = true;
            
            // ไฮไลต์ปุ่มที่เลือกและแสดงคำตอบที่ถูกต้อง
            document.querySelectorAll('.answer-btn').forEach(btn => {
                btn.disabled = true;
                if (btn.dataset.choice === selectedChoice) {
                    btn.style.backgroundColor = (selectedChoice === question.answer) ? '#28a745' : '#dc3545';
                } else if (btn.dataset.choice === question.answer) {
                    btn.style.backgroundColor = '#28a745'; 
                }
            });

            // ตรวจสอบคะแนน
            let score = (selectedChoice === question.answer) ? 100 : 50;
            
            // กำหนดจำนวนแผ่นป้ายที่เปิดได้
            let boardsToOpen = 0;
            if (score === 100) {
                boardsToOpen = 3;
            } else if (score >= 50) {
                boardsToOpen = 2;
            } else {
                boardsToOpen = 1;
            }
            gameState.boardsAllowed = boardsToOpen;
            gameState.moneyBoardsOpened = 0;

            // แสดงส่วนเปิดแผ่นป้าย
            document.getElementById('question-area').classList.add('hidden');
            document.getElementById('reward-message').innerHTML = `🎉 คำตอบถูกต้อง! ได้รับสิทธิ์เปิดแผ่นป้ายเงินทุน <span id="board-count">${boardsToOpen}</span> แผ่น`;
            document.getElementById('reward-area').classList.remove('hidden');
            
            createMoneyBoards();
        }

        // --- 5. ฟังก์ชันสร้างแผ่นป้ายเงินรางวัล ---
        function createMoneyBoards() {
            const boardArea = document.getElementById('money-boards');
            boardArea.innerHTML = '';
            
            for (let i = 0; i < 3; i++) {
                // สุ่มเงิน 5000 - 15900 บาท
                const reward = (i + 1) * 5000 + Math.floor(Math.random() * 10) * 100 + Math.floor(Math.random() * 90) + 10;
                const button = document.createElement('button');
                button.className = 'board-card';
                button.dataset.reward = reward;
                button.textContent = '?';
                button.addEventListener('click', openBoard);
                boardArea.appendChild(button);
            }
        }

        // --- 6. ฟังก์ชันจัดการการเปิดแผ่นป้าย ---
        function openBoard(event) {
            const boardElement = event.target;
            if (boardElement.classList.contains('revealed')) return;

            if (gameState.moneyBoardsOpened >= gameState.boardsAllowed) {
                alert('คุณเปิดแผ่นป้ายครบตามสิทธิ์แล้ว!');
                return;
            }
            
            const reward = parseInt(boardElement.dataset.reward);
            
            // อัปเดตสถานะ
            gameState.totalMoney += reward;
            gameState.moneyBoardsOpened++;
            updateStatusUI();
            
            // อัปเดต UI แผ่นป้าย
            boardElement.textContent = `${reward.toLocaleString('th-TH')}฿`;
            boardElement.classList.add('revealed');
            
            // ตรวจสอบว่าเปิดครบตามสิทธิ์แล้วหรือยัง
            if (gameState.moneyBoardsOpened >= gameState.boardsAllowed) {
                document.getElementById('next-stage-btn').classList.remove('hidden');
            }
        }

        // --- 7. ฟังก์ชันเปลี่ยนไปยังภารกิจ/ด่านถัดไป (แก้ไขให้เปลี่ยน Section ได้ถูกต้อง) ---
        function nextStage() {
            // 7.1 รีเซ็ต UI
            document.getElementById('reward-area').classList.add('hidden');
            document.getElementById('next-stage-btn').classList.add('hidden');
            document.getElementById('question-area').classList.remove('hidden');
            gameState.isQuestionAnswered = false;
            
            gameState.currentMission++;
            
            if (gameState.currentMission > 5) {
                // 7.2 จบ Section ปัจจุบัน
                gameState.currentSection++;
                gameState.currentMission = 1; // เริ่มภารกิจ 1 ของ Section ใหม่
                
                if (gameState.currentSection > 4) {
                    // 7.3 จบเกม: เล่นครบ 4 Section
                    showSchoolCreation();
                    return;
                }
            }
            
            // 7.4 โหลดภารกิจ/Section ใหม่
            loadMission(gameState.currentMission);
            updateStatusUI();
        }

        // --- 8. ฟังก์ชันโหลดภารกิจ/คำถาม (แก้ไขให้ดึงข้อมูลตาม index ได้ถูกต้อง) ---
        function loadMission(missionNumber) {
            const sectionIndex = gameState.currentSection - 1;
            const questionIndex = missionNumber - 1;

            if (sectionIndex >= GAME_DATA.length || questionIndex >= GAME_DATA[sectionIndex].questions.length) {
                 // ถ้าโหลดเกิน ให้จบเกม
                 showSchoolCreation(); 
                 return;
            }

            const currentSectionData = GAME_DATA[sectionIndex];
            const question = currentSectionData.questions[questionIndex];

            document.getElementById('stage-title').textContent = `${currentSectionData.title} (ภารกิจที่ ${missionNumber})`;
            document.getElementById('question-text').textContent = question.text;
            
            const optionsArea = document.getElementById('options-area');
            optionsArea.innerHTML = '';
            
            // สร้างปุ่มคำตอบใหม่
            for (const [key, value] of Object.entries(question.options)) {
                const button = document.createElement('button');
                button.className = 'answer-btn';
                button.dataset.id = question.id;
                button.dataset.choice = key;
                button.textContent = `${key}. ${value}`;
                button.addEventListener('click', (e) => handleAnswer(parseInt(e.target.dataset.id), e.target.dataset.choice));
                optionsArea.appendChild(button);
            }
        }

        // --- 9. ฟังก์ชันแสดงหน้าสร้างโรงเรียน (หลังจบเกม) ---
        function showSchoolCreation() {
            document.getElementById('game-stage').classList.add('hidden');
            document.getElementById('school-creation').classList.remove('hidden');
            
            // แสดงผลวิเคราะห์คร่าวๆ 
            document.getElementById('finish-game-btn').addEventListener('click', () => {
                const schoolName = document.getElementById('school-name-input').value || "โรงเรียนแห่งผู้นำ";
                alert(`ขอแสดงความยินดี! คุณคือผู้นำที่สร้าง ${schoolName} ด้วยเงินทุน ${gameState.totalMoney.toLocaleString('th-TH')} บาท\n\nการวิเคราะห์ภาวะผู้นำ (สำหรับเวอร์ชั่นเต็ม): โครงสร้างคำตอบของคุณเน้นไปที่การทำงานเป็นทีมและการตัดสินใจอย่างมีวิสัยทัศน์!`);
            });
        }

        // --- 10. การเริ่มต้นเกม ---
        document.addEventListener('DOMContentLoaded', () => {
            updateStatusUI();
            loadMission(gameState.currentMission);
            
            document.getElementById('next-stage-btn').addEventListener('click', nextStage);
        });
    </script>
</body>
</html>
