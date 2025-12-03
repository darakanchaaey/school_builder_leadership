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
            display: flex; 
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        .board-card:hover:not(.revealed) {
            transform: scale(1.05);
        }

        .board-card.revealed {
            background-color: #e91e63;
            color: white;
            cursor: default;
            font-size: 18px; 
            line-height: normal; 
            padding: 5px; 
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
            border: 3
