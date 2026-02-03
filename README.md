<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>French Hoops Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://unpkg.com/recharts/umd/Recharts.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&family=Oswald:wght@700&display=swap" rel="stylesheet">
    
    <style>
        /* Twoje oryginalne style */
        body { font-family: 'Inter', sans-serif; }
        .font-oswald { font-family: 'Oswald', sans-serif; }
        .bg-bleu-de-france { background-color: #002395; }
        .text-bleu-de-france { color: #002395; }
        .bg-rouge-france { background-color: #ED2939; }
        .chat-scroll::-webkit-scrollbar { width: 6px; }
        .chat-scroll::-webkit-scrollbar-thumb { background: #002395; border-radius: 10px; }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect, useRef } = React;
        const { AreaChart, Area, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } = Recharts;

        // SEKCJA DANYCH (Wszystko tak jak w oryginale)
        const PLAYERS = [
            { id: 1, name: "Victor Wembanyama", team: "San Antonio Spurs", pos: "C/PF", desc: "Największy talent dekady, numer 1 draftu 2023.", img: "https://images.unsplash.com/photo-1546519638-68e109498ffc?q=80&w=800" },
            { id: 2, name: "Tony Parker", team: "Legend", pos: "PG", desc: "4-krotny mistrz NBA, legenda San Antonio Spurs.", img: "https://images.unsplash.com/photo-1504450758481-7338eba7524a?q=80&w=800" },
            { id: 3, name: "Rudy Gobert", team: "Minnesota Timberwolves", pos: "C", desc: "4-krotny najlepszy obrońca ligi NBA.", img: "https://images.unsplash.com/photo-1519861531473-9200362f46b3?q=80&w=800" }
        ];

        const STATS_DATA = [
            { year: '2000', count: 2 }, { year: '2010', count: 8 }, { year: '2020', count: 12 }, { year: '2024', count: 14 }
        ];

        // KOMPONENTY (Pełna struktura Twojej strony)
        const App = () => {
            const [messages, setMessages] = useState([{ role: 'bot', text: 'Bonjour! O czym chcesz porozmawiać?' }]);
            const [input, setInput] = useState('');

            const handleSend = () => {
                if(!input) return;
                setMessages([...messages, { role: 'user', text: input }, { role: 'bot', text: 'Analizuję Twoje pytanie o francuski basket...' }]);
                setInput('');
            };

            return (
                <div className="min-h-screen bg-gray-50">
                    {/* Menu */}
                    <nav className="bg-white border-b-4 border-bleu-de-france p-6 shadow-md">
                        <div className="max-w-7xl mx-auto flex justify-between items-center">
                            <h1 className="text-3xl font-oswald font-bold tracking-tighter">FRENCH<span className="text-rouge-france">HOOPS</span></h1>
                            <div className="space-x-6 font-bold text-sm uppercase">
                                <a href="#">Start</a>
                                <a href="#players">Gwiazdy</a>
                                <a href="#ai">AI Assistant</a>
                            </div>
                        </div>
                    </nav>

                    {/* Hero */}
                    <header className="relative h-[500px] bg-black text-white flex items-center justify-center overflow-hidden">
                        <img src="https://images.unsplash.com/photo-1544919982-b61976f0ba43?q=80&w=1200" className="absolute inset-0 w-full h-full object-cover opacity-50" />
                        <div className="relative z-10 text-center px-4">
                            <h2 className="text-6xl font-oswald mb-4">ZŁOTA ERA BASKETU</h2>
                            <p className="text-xl max-w-2xl mx-auto">Odkryj potęgę francuskiej koszykówki - od ulic Paryża po parkiety NBA.</p>
                        </div>
                    </header>

                    {/* Gwiazdy */}
                    <section id="players" className="max-w-7xl mx-auto py-20 px-4">
                        <h3 className="text-4xl font-oswald text-center mb-12">LEGENDY I GWIAZDY</h3>
                        <div className="grid md:grid-cols-3 gap-8">
                            {PLAYERS.map(p => (
                                <div key={p.id} className="bg-white rounded-xl shadow-lg overflow-hidden border border-gray-100">
                                    <img src={p.img} className="w-full h-64 object-cover" />
                                    <div className="p-6">
                                        <p className="text-bleu-de-france font-bold text-xs">{p.team}</p>
                                        <h4 className="text-2xl font-oswald my-2">{p.name}</h4>
                                        <p className="text-gray-600 text-sm">{p.desc}</p>
                                    </div>
                                </div>
                            ))}
                        </div>
                    </section>

                    {/* Statystyki */}
                    <section className="bg-gray-900 py-20 text-white">
                        <div className="max-w-7xl mx-auto px-4 grid md:grid-cols-2 gap-12 items-center">
                            <div>
                                <h3 className="text-4xl font-oswald mb-6">EKSPANSJA NBA</h3>
                                <p className="text-gray-400">Francja dostarcza rekordową liczbę zawodników do najlepszej ligi świata.</p>
                            </div>
                            <div className="h-64 bg-gray-800 p-4 rounded-xl">
                                <ResponsiveContainer width="100%" height="100%">
                                    <AreaChart data={STATS_DATA}>
                                        <CartesianGrid strokeDasharray="3 3" stroke="#444" />
                                        <XAxis dataKey="year" stroke="#888" />
                                        <YAxis stroke="#888" />
                                        <Tooltip />
                                        <Area type="monotone" dataKey="count" stroke="#002395" fill="#002395" fillOpacity={0.3} />
                                    </AreaChart>
                                </ResponsiveContainer>
                            </div>
                        </div>
                    </section>

                    {/* AI Chat */}
                    <section id="ai" className="max-w-4xl mx-auto py-20 px-4">
                        <div className="bg-white rounded-3xl shadow-2xl overflow-hidden border">
                            <div className="bg-bleu-de-france p-6 text-white font-bold uppercase tracking-widest">AI Expert Assistant</div>
                            <div className="h-96 p-6 overflow-y-auto chat-scroll bg-gray-50 space-y-4">
                                {messages.map((m, i) => (
                                    <div key={i} className={`flex ${m.role === 'user' ? 'justify-end' : 'justify-start'}`}>
                                        <div className={`p-4 rounded-2xl max-w-[80%] ${m.role === 'user' ? 'bg-bleu-de-france text-white' : 'bg-white shadow-sm text-gray-800'}`}>
                                            {m.text}
                                        </div>
                                    </div>
                                ))}
                            </div>
                            <div className="p-4 border-t flex gap-2 bg-white">
                                <input value={input} onChange={e => setInput(e.target.value)} onKeyPress={e => e.key === 'Enter' && handleSend()} className="flex-1 border p-3 rounded-xl outline-none" placeholder="Zapytaj o zawodnika..." />
                                <button onClick={handleSend} className="bg-bleu-de-france text-white px-8 rounded-xl font-bold">Wyślij</button>
                            </div>
                        </div>
                    </section>

                    <footer className="bg-white border-t-8 border-bleu-de-france py-12 text-center">
                        <p className="font-oswald text-2xl mb-2">FRENCH HOOPS HUB</p>
                        <p className="text-gray-500 text-sm">© 2026 Portal Fanów Francuskiej Koszykówki</p>
                    </footer>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
