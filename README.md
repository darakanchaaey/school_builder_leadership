<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>เกมสร้างภาวะผู้นำ (Leadership Game) - All in One</title>
    
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
                <p id="question-text">ผู้นำที่ดีควรใช้หลักการใดในการจัดลำดับความสำคัญของงานที่ต้องทำ?</p>
                <div id="options-area">
                    <button class="answer-btn" data-id="1" data-choice="A">A. งานที่ชอบที่สุด</button>
                    <button class="answer-btn" data-id="1" data-choice="B">B. งานที่เร่งด่วนและสำคัญ</button>
                    <button class="answer-btn" data-id="1" data-choice="C">C. งานที่ง่ายและเสร็จเร็ว</button>
                    <button class="answer-btn" data-id="1" data-choice="D">D. งานที่มีคนสั่งมา</button>
                </div>
            </div>
            
            <div id="reward-area" class="hidden">
                <h3 id="reward-message">🎉 คำตอบถูกต้อง! ได้รับสิทธิ์เปิดแผ่นป้ายเงินทุน <span id="board-count">0</span> แผ่น</h3>
                <div id="money-boards">
                </div>
                <button id="next-stage-btn" class="hidden">ไปยังภารกิจถัดไป &gt;</button>
            </div>

            <div id="school-creation" class="hidden">
                <h2>สำเร็จ! คุณสร้างโรงเรียนได้สำเร็จ!</h2>
                <div id="school-blueprint">
                    
                    <h3>เงินทุนรวมที่สะสม: <span id="total-money">0</span> บาท</h3>
                    <p>จากการสำรวจภาวะผู้นำของคุณ คุณได้สร้างห้องเรียน/อาคารรวม <span id="room-count">0</span> ห้องเรียน</p>
                    <input type="text" id="school-name-input" placeholder="ตั้งชื่อโรงเรียนของคุณอย่างเป็นทางการ">
                    <button id="finish-game-btn">ดูผลวิเคราะห์ภาวะผู้นำ</button>
                </div>
            </div>
        </section>
    </main>

    <script>
        // --- 1. ข้อมูลเกมและคำถามทั้งหมด ---
        const GAME_DATA = [
            {
                section: 1,
                title: "วิสัยทัศน์และการตัดสินใจ",
                questions: [
                    {
                        id: 1,
                        text: "ผู้นำที่ดีควรใช้หลักการใดในการจัดลำดับความสำคัญของงานที่ต้องทำ?",
                        options: {
                            A: "งานที่ชอบที่สุด",
                            B: "งานที่เร่งด่วนและสำคัญ", // คำตอบถูก
                            C: "งานที่ง่ายและเสร็จเร็ว",
                            D: "งานที่มีคนสั่งมา"
                        },
                        answer: "B",
                        points: 100
                    },
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
        }

        // --- 4. ฟังก์ชันจัดการเมื่อตอบคำถาม ---
        function handleAnswer(questionId, selectedChoice) {
            if (gameState.isQuestionAnswered) return;
            
            const currentSectionData = GAME_DATA.find(s => s.section === gameState.currentSection);
            const question = currentSectionData.questions.find(q => q.id === questionId);

            if (!question) return;

            gameState.isQuestionAnswered = true;
            
            // ไฮไลต์ปุ่มที่เลือกและปิดการใช้งานปุ่มอื่น
            document.querySelectorAll('.answer-btn').forEach(btn => {
                btn.disabled = true;
                if (btn.dataset.choice === selectedChoice) {
                    btn.style.backgroundColor = (selectedChoice === question.answer) ? '#28a745' : '#dc3545';
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
            
            // สร้างแผ่นป้าย
            createMoneyBoards(boardsToOpen);
        }

        // --- 5. ฟังก์ชันสร้างแผ่นป้ายเงินรางวัล ---
        function createMoneyBoards(count) {
            const boardArea = document.getElementById('money-boards');
            boardArea.innerHTML = '';
            
            for (let i = 0; i < 3; i++) {
                const reward = (i + 1) * 5000 + Math.floor(Math.random() * 10) * 100;
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
            if (gameState.moneyBoardsOpened >= gameState.boardsAllowed || boardElement.classList.contains('revealed')) {
                // ให้แสดงข้อความเตือนเล็กน้อยถ้าคลิกเกินสิทธิ์
                if (gameState.moneyBoardsOpened >= gameState.boardsAllowed) {
                    alert('คุณเปิดแผ่นป้ายครบตามสิทธิ์แล้ว!');
                }
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
            boardElement.removeEventListener('click', openBoard);
            
            // ตรวจสอบว่าเปิดครบตามสิทธิ์แล้วหรือยัง
            if (gameState.moneyBoardsOpened >= gameState.boardsAllowed) {
                document.getElementById('next-stage-btn').classList.remove('hidden');
            }
        }

        // --- 7. ฟังก์ชันเปลี่ยนไปยังภารกิจ/ด่านถัดไป ---
        function nextStage() {
            // รีเซ็ตสถานะและ UI
            document.getElementById('reward-area').classList.add('hidden');
            document.getElementById('next-stage-btn').classList.add('hidden');
            document.getElementById('question-area').classList.remove('hidden');
            gameState.isQuestionAnswered = false;
            
            gameState.currentMission++;
            
            if (gameState.currentMission > 5) {
                gameState.currentSection++;
                gameState.currentMission = 1;
                
                if (gameState.currentSection > 4) {
                    showSchoolCreation();
                    return;
                }
            }
            
            loadMission(gameState.currentMission);
            updateStatusUI();
        }

        // --- 8. ฟังก์ชันโหลดภารกิจ/คำถาม ---
        function loadMission(missionNumber) {
            const currentSectionData = GAME_DATA.find(s => s.section === gameState.currentSection);
            // เนื่องจากมีคำถามเดียว จึงใช้ Index 0 ซ้ำเพื่อสาธิต
            const question = currentSectionData.questions[0]; 

            document.getElementById('stage-title').textContent = `${currentSectionData.title} (ภารกิจที่ ${missionNumber})`;
            document.getElementById('question-text').textContent = question.text;
            
            const optionsArea = document.getElementById('options-area');
            optionsArea.innerHTML = '';
            
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
            
            const rooms = Math.floor(gameState.totalMoney / 50000);
            document.getElementById('total-money').textContent = gameState.totalMoney.toLocaleString('th-TH');
            document.getElementById('room-count').textContent = rooms;
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
