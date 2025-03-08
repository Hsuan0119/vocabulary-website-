<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Learning</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
    <h1 class="text-2xl font-bold mb-4">Interactive Vocabulary Learning</h1>
    
    <div class="word-card bg-white p-4 rounded-lg shadow-lg text-center">
        <h2 class="word-text text-xl font-semibold">Apple</h2>
        <img src="apple.jpg" alt="Apple" class="w-32 mx-auto my-2">
        <button onclick="speakWord('Apple')" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">🔊 發音</button>
        <p class="mt-2">例句：I like eating an apple every day.</p>
    </div>
    
    <p class="mt-4 text-lg">What is the meaning of "Apple"?</p>
    <button onclick="checkAnswer('fruit')" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded m-2">A. A fruit</button>
    <button onclick="checkAnswer('animal')" class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded m-2">B. An animal</button>
    
    <p id="userSpeech" class="mt-4 font-semibold"></p>
    <button onclick="startSpeechTest()" class="bg-purple-500 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded mt-4">🎤 試試看發音</button>
    
    <script>
        function speakWord(word) {
            let utterance = new SpeechSynthesisUtterance(word);
            utterance.lang = 'en-US';
            speechSynthesis.speak(utterance);
        }

        function checkAnswer(answer) {
            if (answer === 'fruit') {
                alert('Correct!');
            } else {
                alert('Try again!');
            }
        }

        let recognition = new webkitSpeechRecognition();
        recognition.lang = "en-US";
        recognition.onresult = function(event) {
            let spokenWord = event.results[0][0].transcript;
            document.getElementById("userSpeech").innerText = "You said: " + spokenWord;
        };
        
        function startSpeechTest() {
            recognition.start();
        }
        
        let learnedWords = JSON.parse(localStorage.getItem("learnedWords")) || [];
        function markAsLearned(word) {
            if (!learnedWords.includes(word)) {
                learnedWords.push(word);
                localStorage.setItem("learnedWords", JSON.stringify(learnedWords));
                alert(word + " 已學會！");
            }
        }
    </script>
</body>
</html>
