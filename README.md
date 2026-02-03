<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>French Hoops Hub | AI Edition</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Inter:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        h1, h2 { font-family: 'Oswald', sans-serif; text-transform: uppercase; }
        .fr-gradient { background: linear-gradient(90deg, #002395 0%, #ffffff 50%, #ED2939 100%); height: 8px; }
        .glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border: 1px solid #e2e8f0; }
        .chat-box { height: 400px; overflow-y: auto; }
    </style>
</head>
<body class="bg-slate-50 text-slate-900">

    <div class="fr-gradient"></div>

    <header class="py-16 px-6 text-center bg-white border-b">
        <h1 class="text-6xl mb-4 text-blue-900">French Hoops Hub</h1>
        <p class="text-xl text-slate-600 max-w-2xl mx-auto">Złota era francuskiej koszykówki. Od legend NBA po nową krew. Poznaj historię "Les Bleus".</p>
    </header>

    <main class="max-w-6xl mx-auto p-6">
        <section class="grid md:grid-cols-3 gap-8 my-12">
            <div class="glass p-6 rounded-2xl shadow-sm hover:shadow-md transition">
                <h3 class="font-bold text-blue-800 text-xl mb-2">Victor Wembanyama</h3>
                <p class="text-sm text-slate-600">Nowa twarz NBA. "Alien", który zmienia zasady gry swoim wzrostem i techniką.</p>
            </div>
            <div class="glass p-6 rounded-2xl shadow-sm hover:shadow-md transition">
                <h3 class="font-bold text-blue-800 text-xl mb-2">Tony Parker</h3>
                <p class="text-sm text-slate-600">4-krotny mistrz NBA. Członek Hall of Fame i ikona San Antonio Spurs.</p>
            </div>
            <div class="glass p-6 rounded-2xl shadow-sm hover:shadow-md transition">
                <h3 class="font-bold text-blue-800 text-xl mb-2">Rudy Gobert</h3>
                <p class="text-sm text-slate-600">4-krotny Obrońca Roku (DPOY). Mur nie do przejścia pod samym koszem.</p>
            </div>
        </section>

        <section class="bg-white rounded-3xl shadow-xl overflow-hidden border border-slate-200">
            <div class="bg-blue-900 p-6 text-white">
                <h2 class="text-2xl">Asystent AI Francuskiego Basketu</h2>
                <p class="text-blue-200 text-sm">Zapytaj o zawodnika lub historię...</p>
            </div>
            
            <div id="chat-box" class="chat-box p-6 space-y-4 bg-slate-50">
                <div class="bg-white p-4 rounded-2xl rounded-bl-none shadow-sm max-w-[80%] border border-slate-100">
                    Bonjour! O kim chciałbyś porozmawiać? Wpisz nazwisko: <b>Wemby</b>, <b>Parker</b> lub <b>Gobert</b>.
                </div>
            </div>

            <div class="p-4 border-t bg-white flex gap-2">
                <input id="user-input" type="text" placeholder="Wpisz pytanie..." class="flex-1 p-3 border rounded-xl outline-none focus:ring-2 focus:ring-blue-500">
                <button onclick="askAI()" class="bg-blue-900 text-white px-8 py-3 rounded-xl font-bold hover:bg-blue-800 transition">Wyślij</button>
            </div>
        </section>

        <section class="my-16 p-8 bg-blue-900 rounded-3xl text-white relative overflow-hidden">
            <div class="relative z-10">
                <h2 class="text-3xl mb-4">Ciekawostka od Autora</h2>
                <p class="text-blue-100 text-lg">Czy wiesz, że Francja to jedyny kraj, który w XXI wieku regularnie stawia czoła potędze USA na Igrzyskach? System szkolenia INSEP pod Paryżem jest uznawany za najlepszą fabrykę talentów na świecie.</p>
            </div>
            <div class="absolute -right-10 -bottom-10 text-9xl opacity-10">🏀</div>
        </section>
    </main>

    <footer class="py-12 text-center text-slate-400 text-sm">
        <p>© 2026 French Hoops Hub. Projekt stworzony dla fanów basketu.</p>
    </footer>

    <script>
        const knowledge = {
            'wemby': 'Victor Wembanyama to 224-centymetrowy fenomen, który w 2024 roku został Rookie of the Year. Gra w San Antonio Spurs.',
            'parker': 'Tony Parker to legenda. Zdobył 4 tytuły NBA i był pierwszym Europejczykiem, który został MVP Finałów NBA.',
            'gobert': 'Rudy Gobert to Stifle Tower. Jest jednym z najlepszych obrońców w historii NBA, z 4 nagrodami DPOY na koncie.',
            'francja': 'Reprezentacja Francji to obecnie wicemistrzowie olimpijscy z Paryża 2024. Ich siłą jest niesamowita obrona.',
            'default': 'Ciekawe pytanie! Francuska koszykówka jest teraz w najlepszym momencie historii. Zapytaj o Wembyego lub Parkera!'
        };

        function askAI() {
            const input = document.getElementById('user-input');
            const chat = document.getElementById('chat-box');
            const text = input.value.toLowerCase();
            
            if(!text) return;

            // Wiadomość użytkownika
            chat.innerHTML += `<div class="flex justify-end"><div class="bg-blue-600 text-white p-4 rounded-2xl rounded-br-none max-w-[80%]">${input.value}</div></div>`;
            
            input.value = '';

            // Odpowiedź AI
            setTimeout(() => {
                let response = knowledge.default;
                if(text.includes('wemby')) response = knowledge.wemby;
                if(text.includes('parker')) response = knowledge.parker;
                if(text.includes('gobert')) response = knowledge.gobert;
                if(text.includes('francja')) response = knowledge.francja;

                chat.innerHTML += `<div class="flex justify-start"><div class="bg-white p-4 rounded-2xl rounded-bl-none shadow-sm max-w-[80%] border border-slate-100">${response}</div></div>`;
                chat.scrollTop = chat.scrollHeight;
            }, 600);
        }

        // Obsługa Entera
        document.getElementById('user-input').addEventListener('keypress', function (e) {
            if (e.key === 'Enter') askAI();
        });
    </script>
</body>
</html>
