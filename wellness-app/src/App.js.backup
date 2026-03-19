import React, { useState, useEffect, useRef } from 'react';
import {
  MessageCircleHeart, BookHeart, Home, Settings, Droplet,
  Sun, Moon, Send, Loader2, Sparkles, Heart, Activity,
  BarChart3, GlassWater, Download,
  Thermometer, Apple, Dumbbell, LifeBuoy, Users, CalendarDays, X, Trash2
} from 'lucide-react';

// --- Configuration & Initialization ---
const apiKey = ""; // API key is injected by the execution environment

// --- Utility Functions ---
const addDays = (date, days) => {
  const result = new Date(date);
  result.setDate(result.getDate() + days);
  return result;
};

const formatDate = (date) => {
  return date.toLocaleDateString('en-US', { month: 'short', day: 'numeric' });
};

// --- Main Application Component ---
export default function App() {
  const [darkMode, setDarkMode] = useState(false);
  const [showSOS, setShowSOS] = useState(false);

  const [activeTab, setActiveTab] = useState('dashboard');
  const [onboardingComplete, setOnboardingComplete] = useState(false);
  const [loadingData, setLoadingData] = useState(true);

  const [cycleData, setCycleData] = useState({
    averageCycleLength: 28,
    averagePeriodLength: 5,
    lastPeriod: new Date().toISOString(),
  });
  const [logs, setLogs] = useState({});

  // --- Data Fetching (Local Storage) ---
  useEffect(() => {
    try {
      const savedCycleData = localStorage.getItem('aura_cycleData');
      if (savedCycleData) {
        setCycleData(JSON.parse(savedCycleData));
        setOnboardingComplete(true);
      } else {
        setOnboardingComplete(false);
      }

      const savedLogs = localStorage.getItem('aura_logs');
      if (savedLogs) {
        setLogs(JSON.parse(savedLogs));
      }
    } catch (error) {
      console.error("Local Storage Error:", error);
    }
    setLoadingData(false);
  }, []);

  // --- Derived Cycle Calculations ---
  const today = new Date();
  const calculateCycleInfo = () => {
    const lastPeriodDate = new Date(cycleData.lastPeriod);
    const nextPeriod = addDays(lastPeriodDate, cycleData.averageCycleLength);
    const daysUntilNext = Math.ceil((nextPeriod - today) / (1000 * 60 * 60 * 24));
    const cycleDay = Math.max(1, Math.ceil((today - lastPeriodDate) / (1000 * 60 * 60 * 24)) + 1);

    let phase = "Menstruation";
    let phaseDescription = "Your body is shedding its uterine lining.";
    let affirmation = "I listen to my body and give it the rest it deserves.";
    let nutrition = "Focus on iron-rich foods (spinach, red meat, lentils) and vitamin C to aid absorption. Drink warm teas.";
    let exercise = "Rest is best. Light walking, restorative yoga, or gentle stretching if you feel up to it.";

    if (cycleDay > cycleData.averagePeriodLength && cycleDay <= 13) {
      phase = "Follicular";
      phaseDescription = "Estrogen is rising. Energy and creativity are boosting!";
      affirmation = "I embrace my rising energy and creative potential today.";
      nutrition = "Incorporate fermented foods (kimchi, yogurt) and lean proteins to support rising estrogen levels.";
      exercise = "Great time to push yourself! Try running, dancing, or moderate-intensity cardio.";
    } else if (cycleDay >= 14 && cycleDay <= 16) {
      phase = "Ovulation";
      phaseDescription = "Peak fertility window. You might feel most social and energetic.";
      affirmation = "I am vibrant, confident, and deeply connected to my power.";
      nutrition = "Antioxidant-rich foods like berries, nuts, and leafy greens support egg health and liver function.";
      exercise = "Peak energy levels. High-intensity interval training (HIIT) or heavy weightlifting are ideal now.";
    } else if (cycleDay > 16) {
      phase = "Luteal";
      phaseDescription = "Progesterone rises. Time to wind down, you may experience PMS.";
      affirmation = "I give myself grace and permission to slow down.";
      nutrition = "Magnesium-rich foods (dark chocolate, pumpkin seeds) and complex carbs (sweet potatoes) help curb cravings and stabilize mood.";
      exercise = "Scale back intensity. Pilates, strength training with lighter weights, or long walks.";
    }

    const ovulationDay = addDays(lastPeriodDate, cycleData.averageCycleLength - 14);
    const fertileStart = addDays(ovulationDay, -5);
    const fertileEnd = addDays(ovulationDay, 1);

    return { cycleDay, nextPeriod, daysUntilNext, phase, phaseDescription, affirmation, nutrition, exercise, ovulationDay, fertileStart, fertileEnd };
  };

  if (loadingData) {
    return (
      <div className="flex justify-center items-center h-screen bg-rose-50 text-rose-400">
        <Loader2 className="w-10 h-10 animate-spin" />
      </div>
    );
  }

  const cycleInfo = onboardingComplete ? calculateCycleInfo() : null;

  return (
    <div className={`${darkMode ? 'dark' : ''}`}>
      <div className="flex justify-center bg-rose-50 dark:bg-gray-950 min-h-screen font-sans text-gray-800 dark:text-gray-100 transition-colors duration-300">
        <div className="w-full max-w-md bg-white dark:bg-gray-900 shadow-xl min-h-screen relative flex flex-col overflow-hidden sm:border-x sm:border-rose-100 dark:sm:border-gray-800 transition-colors duration-300">

          {/* Header */}
          <header className="bg-white/80 dark:bg-gray-900/80 backdrop-blur-md sticky top-0 z-10 px-6 pt-10 pb-4 border-b border-rose-50 dark:border-gray-800">
            <div className="flex justify-between items-center">
              <div className="flex items-center gap-2">
                <Sparkles className="w-6 h-6 text-rose-400 dark:text-purple-400" />
                <h1 className="text-2xl font-semibold bg-gradient-to-r from-rose-400 to-purple-500 bg-clip-text text-transparent">
                  Aura
                </h1>
              </div>
              <div className="flex gap-2">
                <button
                  onClick={() => setShowSOS(true)}
                  className="w-10 h-10 rounded-full bg-red-100 dark:bg-red-900/50 flex items-center justify-center text-red-500 dark:text-red-400 font-medium shadow-sm border border-red-200 dark:border-red-800 hover:scale-105 transition-transform animate-pulse"
                >
                  <LifeBuoy className="w-5 h-5"/>
                </button>
                <button
                  onClick={() => setDarkMode(!darkMode)}
                  className="w-10 h-10 rounded-full bg-rose-100 dark:bg-gray-800 flex items-center justify-center text-rose-500 dark:text-purple-400 font-medium shadow-sm border border-rose-200 dark:border-gray-700 hover:scale-105 transition-transform"
                >
                  {darkMode ? <Sun className="w-5 h-5"/> : <Moon className="w-5 h-5"/>}
                </button>
              </div>
            </div>
          </header>

          {/* Main Content Area */}
          <main className="flex-1 overflow-y-auto pb-28 scroll-smooth">
            {!onboardingComplete ? (
              <OnboardingTab setCycleData={setCycleData} setOnboardingComplete={setOnboardingComplete} />
            ) : (
              <>
                {activeTab === 'dashboard' && <DashboardTab cycleInfo={cycleInfo} today={today} logs={logs} />}
                {activeTab === 'journal' && <JournalTab today={today} logs={logs} setLogs={setLogs} />}
                {activeTab === 'insights' && <InsightsTab logs={logs} today={today} />}
                {activeTab === 'calendar' && <CalendarTab cycleInfo={cycleInfo} today={today} />}
                {activeTab === 'chat' && <ChatTab cycleInfo={cycleInfo} />}
                {activeTab === 'settings' && <SettingsTab cycleData={cycleData} cycleInfo={cycleInfo} setOnboardingComplete={setOnboardingComplete} setLogs={setLogs} />}
              </>
            )}
          </main>

          {/* Bottom Navigation */}
          {onboardingComplete && (
            <nav className="bg-white dark:bg-gray-900 border-t border-rose-100 dark:border-gray-800 absolute bottom-0 w-full px-4 py-4 flex justify-between items-center z-20 shadow-[0_-4px_20px_-15px_rgba(0,0,0,0.1)] transition-colors duration-300">
              <NavItem icon={<Home />} label="Home" active={activeTab === 'dashboard'} onClick={() => setActiveTab('dashboard')} />
              <NavItem icon={<BookHeart />} label="Journal" active={activeTab === 'journal'} onClick={() => setActiveTab('journal')} />
              <div className="relative -top-6 mx-2">
                <button
                  onClick={() => setActiveTab('chat')}
                  className={`p-4 rounded-full shadow-lg transform transition hover:scale-105 active:scale-95 ${activeTab === 'chat' ? 'bg-purple-500 dark:bg-purple-600 text-white' : 'bg-gradient-to-tr from-rose-400 to-rose-500 dark:from-purple-500 dark:to-indigo-500 text-white'}`}
                >
                  <MessageCircleHeart className="w-7 h-7" />
                </button>
              </div>
              <NavItem icon={<BarChart3 />} label="Insights" active={activeTab === 'insights'} onClick={() => setActiveTab('insights')} />
              <NavItem icon={<Settings />} label="Settings" active={activeTab === 'settings'} onClick={() => setActiveTab('settings')} />
            </nav>
          )}

          {/* SOS Modal Overlay */}
          {showSOS && <SOSModal onClose={() => setShowSOS(false)} />}
        </div>
      </div>
    </div>
  );
}

// --- SOS Modal Component ---
function SOSModal({ onClose }) {
  return (
    <div className="absolute inset-0 z-50 bg-gray-900/95 backdrop-blur-md flex flex-col items-center justify-center p-6 animate-in fade-in duration-300">
      <button onClick={onClose} className="absolute top-10 right-6 text-gray-400 hover:text-white transition-colors">
        <X className="w-8 h-8" />
      </button>

      <h2 className="text-2xl font-semibold text-rose-300 mb-8 text-center">Breathe with me...</h2>

      {/* Breathing Animation */}
      <div className="relative w-48 h-48 flex items-center justify-center mb-12">
        <div className="absolute inset-0 bg-rose-500/20 rounded-full animate-[ping_4s_ease-in-out_infinite]"></div>
        <div className="absolute w-32 h-32 bg-gradient-to-tr from-rose-400 to-purple-500 rounded-full shadow-lg flex items-center justify-center">
          <Heart className="w-12 h-12 text-white" />
        </div>
      </div>

      <div className="w-full max-w-sm space-y-4">
        <h3 className="text-white font-medium mb-2 flex items-center gap-2"><LifeBuoy className="w-5 h-5 text-rose-400"/> Instant Relief Tips</h3>
        <div className="bg-gray-800/80 p-4 rounded-2xl border border-gray-700 text-sm text-gray-300">
          <span className="font-bold text-rose-300">1. Heat:</span> Apply a heating pad or hot water bottle to your lower abdomen or back.
        </div>
        <div className="bg-gray-800/80 p-4 rounded-2xl border border-gray-700 text-sm text-gray-300">
          <span className="font-bold text-rose-300">2. Hydrate:</span> Drink warm chamomile or peppermint tea to relax uterine muscles.
        </div>
        <div className="bg-gray-800/80 p-4 rounded-2xl border border-gray-700 text-sm text-gray-300">
          <span className="font-bold text-rose-300">3. Position:</span> Try the "Child's Pose" or lie on your side with knees tucked to your chest.
        </div>
      </div>
    </div>
  );
}

// --- Navigation Item Component ---
function NavItem({ icon, label, active, onClick }) {
  return (
    <button onClick={onClick} className={`flex flex-col items-center gap-1 transition-colors w-12 ${active ? 'text-rose-500 dark:text-purple-400' : 'text-gray-400 dark:text-gray-500 hover:text-rose-300 dark:hover:text-purple-300'}`}>
      <div className={`${active ? 'scale-110' : 'scale-100'} transition-transform`}>{React.cloneElement(icon, { className: 'w-6 h-6' })}</div>
      <span className="text-[10px] font-medium tracking-wide">{label}</span>
    </button>
  );
}

// --- Onboarding Tab ---
function OnboardingTab({ setCycleData, setOnboardingComplete }) {
  const [lastPeriod, setLastPeriod] = useState(new Date().toISOString().split('T')[0]);
  const [cycleLen, setCycleLen] = useState(28);
  const [periodLen, setPeriodLen] = useState(5);
  const [saving, setSaving] = useState(false);

  const handleSave = () => {
    setSaving(true);
    const newCycleData = {
      lastPeriod: new Date(lastPeriod).toISOString(),
      averageCycleLength: Number(cycleLen),
      averagePeriodLength: Number(periodLen)
    };
    localStorage.setItem('aura_cycleData', JSON.stringify(newCycleData));
    setCycleData(newCycleData);
    setOnboardingComplete(true);
    setSaving(false);
  };

  return (
    <div className="p-8 flex flex-col items-center text-center space-y-8 animate-in fade-in zoom-in-95 duration-500 mt-10">
      <div className="w-20 h-20 bg-rose-100 dark:bg-purple-900/50 rounded-full flex items-center justify-center shadow-inner mb-2">
        <Sparkles className="w-10 h-10 text-rose-500 dark:text-purple-400" />
      </div>
      <div>
        <h2 className="text-3xl font-light text-gray-800 dark:text-white">Welcome to Aura</h2>
        <p className="text-gray-500 dark:text-gray-400 mt-2 text-sm">Let's personalize your experience.</p>
      </div>
      <div className="w-full space-y-5 text-left bg-white dark:bg-gray-800 p-6 rounded-3xl shadow-sm border border-gray-100 dark:border-gray-700">
        <div>
          <label className="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Last period start date</label>
          <input type="date" value={lastPeriod} onChange={(e) => setLastPeriod(e.target.value)} className="w-full bg-gray-50 dark:bg-gray-900 border border-gray-200 dark:border-gray-700 rounded-xl p-3 text-gray-800 dark:text-gray-200 outline-none" />
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Average cycle length (days)</label>
          <input type="number" value={cycleLen} onChange={(e) => setCycleLen(e.target.value)} className="w-full bg-gray-50 dark:bg-gray-900 border border-gray-200 dark:border-gray-700 rounded-xl p-3 text-gray-800 dark:text-gray-200 outline-none" />
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Average period length (days)</label>
          <input type="number" value={periodLen} onChange={(e) => setPeriodLen(e.target.value)} className="w-full bg-gray-50 dark:bg-gray-900 border border-gray-200 dark:border-gray-700 rounded-xl p-3 text-gray-800 dark:text-gray-200 outline-none" />
        </div>
      </div>
      <button onClick={handleSave} disabled={saving} className="w-full bg-gray-900 dark:bg-white dark:text-gray-900 text-white py-4 rounded-full font-medium shadow-md hover:bg-gray-800 active:scale-95 transition-all flex justify-center items-center">
        {saving ? <Loader2 className="w-5 h-5 animate-spin" /> : "Start My Journey"}
      </button>
    </div>
  );
}

// --- Dashboard Tab ---
function DashboardTab({ cycleInfo, today, logs }) {
  return (
    <div className="p-6 space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
      <div>
        <h2 className="text-3xl font-light text-gray-800 dark:text-white tracking-tight">
          Hello, <span className="font-medium text-rose-500 dark:text-purple-400">Beautiful</span>.
        </h2>
      </div>

      {/* Daily Affirmation */}
      <div className="bg-gradient-to-r from-rose-100 to-purple-100 dark:from-gray-800 dark:to-gray-800 p-4 rounded-2xl border border-rose-200 dark:border-gray-700 flex gap-3 shadow-sm">
        <Heart className="w-5 h-5 text-rose-400 dark:text-rose-500 shrink-0 mt-0.5" />
        <p className="text-sm text-gray-700 dark:text-gray-300 italic font-medium">"{cycleInfo.affirmation}"</p>
      </div>

      {/* Cycle Ring */}
      <div className="bg-gradient-to-br from-rose-50 to-purple-50 dark:from-gray-800 dark:to-gray-900 rounded-3xl p-6 shadow-sm border border-white/50 dark:border-gray-700 relative overflow-hidden">
        <div className="absolute top-0 right-0 -mr-8 -mt-8 w-32 h-32 rounded-full bg-gradient-to-br from-rose-200 to-rose-100 dark:from-purple-900/40 opacity-40 blur-2xl"></div>
        <div className="relative z-10 flex flex-col items-center text-center">
          <div className="w-48 h-48 rounded-full border-[12px] border-white dark:border-gray-800 shadow-inner flex flex-col items-center justify-center bg-gradient-to-b from-rose-100/50 dark:from-gray-700/50 to-transparent relative">
            <svg className="absolute inset-0 w-full h-full -rotate-90 transform" viewBox="0 0 100 100">
               <circle cx="50" cy="50" r="44" fill="none" stroke="currentColor" className="text-rose-100 dark:text-gray-700" strokeWidth="12" />
               <circle cx="50" cy="50" r="44" fill="none" stroke="currentColor" className="text-rose-500 dark:text-purple-500" strokeWidth="12" strokeDasharray="276" strokeDashoffset={276 - (276 * (cycleInfo.cycleDay / 28))} strokeLinecap="round" style={{ transition: 'stroke-dashoffset 1s ease-out' }} />
            </svg>
            <span className="text-sm font-semibold text-rose-400 dark:text-purple-400 uppercase tracking-widest mt-2">{cycleInfo.phase}</span>
            <span className="text-5xl font-bold text-gray-800 dark:text-white my-1">Day {cycleInfo.cycleDay}</span>
            <span className="text-xs text-gray-500 dark:text-gray-400 font-medium">of cycle</span>
          </div>

          <div className="mt-6 flex items-center justify-between w-full px-4 text-sm bg-white/60 dark:bg-gray-800/80 backdrop-blur-sm rounded-2xl py-3 shadow-sm border border-white dark:border-gray-700">
             <div className="flex flex-col text-left">
               <span className="text-gray-500 dark:text-gray-400 text-xs">Next Period</span>
               <span className="font-semibold text-gray-800 dark:text-gray-200">{formatDate(cycleInfo.nextPeriod)}</span>
             </div>
             <div className="h-8 w-[1px] bg-rose-200 dark:bg-gray-600"></div>
             <div className="flex flex-col text-right">
               <span className="text-gray-500 dark:text-gray-400 text-xs">Fertile Window</span>
               <span className="font-semibold text-purple-600 dark:text-purple-400">{formatDate(cycleInfo.fertileStart)}</span>
             </div>
          </div>
        </div>
      </div>

      {/* Body & Fuel Guide */}
      <div className="space-y-3">
        <h3 className="text-lg font-semibold text-gray-800 dark:text-white px-1">Phase Fuel & Body</h3>
        <div className="grid grid-cols-1 gap-3">
          <div className="bg-white dark:bg-gray-800 rounded-2xl p-4 shadow-sm border border-gray-100 dark:border-gray-700 flex gap-4">
            <div className="bg-orange-100 dark:bg-orange-900/30 p-2.5 rounded-xl shrink-0 h-fit"><Apple className="w-5 h-5 text-orange-500"/></div>
            <div>
              <h4 className="font-semibold text-gray-800 dark:text-white text-sm mb-1">Nutrition Focus</h4>
              <p className="text-xs text-gray-600 dark:text-gray-300 leading-relaxed">{cycleInfo.nutrition}</p>
            </div>
          </div>
          <div className="bg-white dark:bg-gray-800 rounded-2xl p-4 shadow-sm border border-gray-100 dark:border-gray-700 flex gap-4">
            <div className="bg-blue-100 dark:bg-blue-900/30 p-2.5 rounded-xl shrink-0 h-fit"><Dumbbell className="w-5 h-5 text-blue-500"/></div>
            <div>
              <h4 className="font-semibold text-gray-800 dark:text-white text-sm mb-1">Movement</h4>
              <p className="text-xs text-gray-600 dark:text-gray-300 leading-relaxed">{cycleInfo.exercise}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

// --- Journal Tab (Advanced Data) ---
function JournalTab({ today, logs, setLogs }) {
  const todayKey = today.toISOString().split('T')[0];
  const currentLog = logs[todayKey] || { symptoms: [], notes: '', water: 0, bbt: '', fluid: '' };

  const updateLog = (key, value) => {
    const newLog = { ...currentLog, [key]: value, date: todayKey };
    const updatedLogs = { ...logs, [todayKey]: newLog };
    setLogs(updatedLogs);
    localStorage.setItem('aura_logs', JSON.stringify(updatedLogs));
  };

  const toggleSymptom = (symptom) => {
    const symptoms = currentLog.symptoms || [];
    if (symptoms.includes(symptom)) updateLog('symptoms', symptoms.filter(s => s !== symptom));
    else updateLog('symptoms', [...symptoms, symptom]);
  };

  const fluids = ['Dry', 'Sticky', 'Creamy', 'Egg White'];
  const symptomList = ['Cramps', 'Bloating', 'Headache', 'Tender Breasts', 'Acne', 'Fatigue', 'Cravings', 'Backache'];

  return (
    <div className="p-6 space-y-8 animate-in fade-in slide-in-from-bottom-4 duration-500">
      <div>
        <h2 className="text-3xl font-light text-gray-800 dark:text-white">Journal</h2>
        <p className="text-gray-500 dark:text-gray-400 font-medium mt-1">{formatDate(today)}</p>
      </div>

      {/* Advanced Fertility: BBT & Cervical Fluid */}
      <section className="bg-purple-50 dark:bg-purple-900/10 p-5 rounded-3xl border border-purple-100 dark:border-purple-900/50 space-y-5">
        <div>
          <h3 className="text-sm font-semibold text-purple-900 dark:text-purple-300 uppercase tracking-wider mb-3 flex items-center gap-2">
            <Thermometer className="w-4 h-4" /> Basal Body Temp (BBT)
          </h3>
          <div className="flex items-center gap-3">
             <input
               type="number" step="0.01" placeholder="97.50" value={currentLog.bbt || ''}
               onChange={(e) => updateLog('bbt', e.target.value)}
               className="w-24 bg-white dark:bg-gray-800 border border-purple-200 dark:border-purple-800 rounded-xl p-2 text-center text-gray-800 dark:text-gray-200 outline-none focus:ring-2 focus:ring-purple-400"
             />
             <span className="text-gray-500 dark:text-gray-400 text-sm">°F (First thing in morning)</span>
          </div>
        </div>

        <div>
          <h3 className="text-sm font-semibold text-purple-900 dark:text-purple-300 uppercase tracking-wider mb-3 flex items-center gap-2">
            <Droplet className="w-4 h-4" /> Cervical Fluid
          </h3>
          <div className="flex flex-wrap gap-2">
            {fluids.map(fluid => (
              <button
                key={fluid} onClick={() => updateLog('fluid', fluid)}
                className={`px-3 py-1.5 rounded-full text-xs transition-all duration-200 ${
                  currentLog.fluid === fluid ? 'bg-purple-500 text-white shadow-md font-medium' : 'bg-white dark:bg-gray-800 border border-purple-200 dark:border-purple-800 text-purple-700 dark:text-purple-300'
                }`}
              >{fluid}</button>
            ))}
          </div>
        </div>
      </section>

      {/* Flow & Symptoms */}
      <section>
        <h3 className="text-sm font-semibold text-gray-400 dark:text-gray-500 uppercase tracking-wider mb-3 flex items-center gap-2">
          <Activity className="w-4 h-4" /> Symptoms
        </h3>
        <div className="flex flex-wrap gap-2">
          {symptomList.map(sym => (
            <button key={sym} onClick={() => toggleSymptom(sym)} className={`px-4 py-2 rounded-full text-sm transition-all duration-200 ${
                (currentLog.symptoms || []).includes(sym) ? 'bg-rose-500 text-white shadow-md font-medium' : 'bg-white dark:bg-gray-800 border border-gray-200 dark:border-gray-700 text-gray-600 dark:text-gray-300'
              }`}>{sym}</button>
          ))}
        </div>
      </section>

      {/* Hydration */}
      <section className="bg-blue-50 dark:bg-blue-900/10 p-4 rounded-3xl border border-blue-100 dark:border-blue-900/50">
        <h3 className="text-sm font-semibold text-blue-900 dark:text-blue-300 uppercase tracking-wider mb-3 flex justify-between">
          <span className="flex items-center gap-2"><GlassWater className="w-4 h-4" /> Water Intake</span>
          <span>{currentLog.water || 0}/8</span>
        </h3>
        <div className="flex justify-between">
          {[...Array(8)].map((_, i) => (
            <button key={i} onClick={() => updateLog('water', i + 1 === currentLog.water ? i : i + 1)} className={`w-8 h-10 rounded-lg transition-all ${
                i < (currentLog.water || 0) ? 'bg-blue-400 dark:bg-blue-500 shadow-sm scale-105' : 'bg-white dark:bg-gray-800 border border-blue-100 dark:border-gray-700'
              }`} />
          ))}
        </div>
      </section>
      <div className="pb-4 text-center text-xs text-gray-400">Saved Locally 💾</div>
    </div>
  );
}

// --- Insights Tab (Includes BBT Chart) ---
function InsightsTab({ logs, today }) {
  // Aggregate symptom data
  const symptomCounts = {};
  let totalLogs = 0;

  // Extract BBT Data for last 7 days
  const bbtData = [];
  for(let i=6; i>=0; i--) {
    const d = new Date(today);
    d.setDate(today.getDate() - i);
    const dateStr = d.toISOString().split('T')[0];
    bbtData.push({ day: d.getDate(), temp: logs[dateStr]?.bbt ? parseFloat(logs[dateStr].bbt) : null });
  }

  Object.values(logs).forEach(log => {
    totalLogs++;
    if (log.symptoms) log.symptoms.forEach(sym => symptomCounts[sym] = (symptomCounts[sym] || 0) + 1);
  });
  const topSymptoms = Object.entries(symptomCounts).sort((a, b) => b[1] - a[1]).slice(0, 3);

  // Simple calculation for SVG graph height based on min/max temp
  const validTemps = bbtData.map(d => d.temp).filter(t => t !== null);
  const minTemp = validTemps.length ? Math.min(...validTemps) - 0.2 : 97.0;
  const maxTemp = validTemps.length ? Math.max(...validTemps) + 0.2 : 99.0;
  const range = maxTemp - minTemp || 1;

  return (
    <div className="p-6 space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
      <h2 className="text-3xl font-light text-gray-800 dark:text-white">Insights</h2>

      {/* BBT Chart */}
      <div className="bg-white dark:bg-gray-800 p-6 rounded-3xl border border-gray-100 dark:border-gray-700 shadow-sm">
        <h3 className="text-sm font-semibold text-gray-800 dark:text-white mb-4 flex justify-between items-center">
          <span>BBT Curve (Last 7 Days)</span>
          <Thermometer className="w-4 h-4 text-purple-400"/>
        </h3>

        {validTemps.length === 0 ? (
          <div className="h-32 flex items-center justify-center text-xs text-gray-400 bg-gray-50 dark:bg-gray-900 rounded-xl">No BBT data logged yet.</div>
        ) : (
          <div className="relative h-40 w-full flex items-end justify-between pb-6 pt-2">
            {/* Y-Axis rough guides */}
            <div className="absolute left-0 top-0 bottom-6 flex flex-col justify-between text-[10px] text-gray-400 pr-2 border-r border-gray-100 dark:border-gray-700 w-8">
              <span>{maxTemp.toFixed(1)}</span>
              <span>{minTemp.toFixed(1)}</span>
            </div>
            {/* Plot Points */}
            <div className="w-full h-full relative ml-8 flex justify-between items-end">
              {bbtData.map((data, i) => {
                const heightPercent = data.temp ? ((data.temp - minTemp) / range) * 100 : 0;
                return (
                  <div key={i} className="flex flex-col items-center w-8 group">
                    {data.temp && (
                      <div
                        className="w-3 bg-purple-400 dark:bg-purple-500 rounded-full transition-all duration-500 relative"
                        style={{ height: `${Math.max(10, heightPercent)}%` }}
                      >
                         {/* Tooltip on hover */}
                         <div className="opacity-0 group-hover:opacity-100 absolute -top-8 left-1/2 transform -translate-x-1/2 bg-gray-900 text-white text-[10px] px-2 py-1 rounded shadow-lg transition-opacity pointer-events-none z-10">
                           {data.temp}°
                         </div>
                      </div>
                    )}
                    {!data.temp && <div className="w-1 h-1 bg-gray-200 dark:bg-gray-700 rounded-full mb-1"></div>}
                    <span className="text-[10px] text-gray-400 absolute -bottom-6">{data.day}</span>
                  </div>
                );
              })}
            </div>
          </div>
        )}
      </div>

      {/* Symptoms */}
      {topSymptoms.length > 0 && (
        <div className="bg-white dark:bg-gray-800 p-6 rounded-3xl border border-gray-100 dark:border-gray-700 shadow-sm mt-4">
            <h3 className="text-sm font-semibold text-gray-800 dark:text-white mb-4">Top Symptoms</h3>
            <div className="space-y-4">
              {topSymptoms.map(([sym, count]) => (
                <div key={sym}>
                  <div className="flex justify-between text-sm mb-1">
                    <span className="text-gray-700 dark:text-gray-300">{sym}</span>
                    <span className="text-gray-400 text-xs">{count} logs</span>
                  </div>
                  <div className="w-full bg-gray-100 dark:bg-gray-700 rounded-full h-2">
                    <div className="bg-rose-400 h-2 rounded-full" style={{ width: `${(count / totalLogs) * 100}%` }}></div>
                  </div>
                </div>
              ))}
            </div>
        </div>
      )}
    </div>
  );
}

// --- Calendar Tab ---
function CalendarTab({ cycleInfo, today }) {
  const currentMonth = today.getMonth();
  const currentYear = today.getFullYear();
  const daysInMonth = new Date(currentYear, currentMonth + 1, 0).getDate();
  const firstDayOfMonth = new Date(currentYear, currentMonth, 1).getDay();
  const days = Array(firstDayOfMonth).fill(null).concat(Array.from({length: daysInMonth}, (_, i) => new Date(currentYear, currentMonth, i + 1)));

  const getDayStyle = (date) => {
    if (!date) return '';
    const dateStr = date.toDateString();
    const isNextPeriod = date >= cycleInfo.nextPeriod && date < addDays(cycleInfo.nextPeriod, 5);
    const isFertile = date >= cycleInfo.fertileStart && date <= cycleInfo.fertileEnd;
    let style = "bg-white dark:bg-gray-800 text-gray-700 dark:text-gray-300 border border-transparent";
    if (dateStr === today.toDateString()) style += " ring-2 ring-gray-900 dark:ring-white font-bold";
    if (isNextPeriod) style = "bg-rose-100 dark:bg-rose-900/50 text-rose-800 dark:text-rose-200 font-medium";
    else if (dateStr === cycleInfo.ovulationDay.toDateString()) style = "bg-purple-500 text-white font-bold shadow-md z-10 scale-105";
    else if (isFertile) style = "bg-purple-100 dark:bg-purple-900/30 text-purple-800 font-medium";
    return style;
  };

  return (
    <div className="p-6 space-y-6">
      <h2 className="text-3xl font-light text-gray-800 dark:text-white">Cycle Map</h2>
      <div className="bg-white dark:bg-gray-800 rounded-3xl p-5 shadow-sm border border-gray-100 dark:border-gray-700">
        <h3 className="text-center font-medium mb-4 dark:text-white">{today.toLocaleString('default', { month: 'long', year: 'numeric' })}</h3>
        <div className="grid grid-cols-7 gap-1 mb-2 text-center text-[10px] font-bold text-gray-400 uppercase tracking-widest">
          {['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa'].map(d => <div key={d}>{d}</div>)}
        </div>
        <div className="grid grid-cols-7 gap-1 sm:gap-2">
          {days.map((date, i) => <div key={i} className={`aspect-square flex items-center justify-center rounded-xl text-sm ${getDayStyle(date)}`}>{date?.getDate()}</div>)}
        </div>
      </div>
    </div>
  );
}

// --- Chat Tab ---
function ChatTab({ cycleInfo }) {
  const [messages, setMessages] = useState([{ role: 'model', text: `Hi there! I'm Aura. I see you're on Day ${cycleInfo.cycleDay} (${cycleInfo.phase}). How can I support you today?` }]);
  const [input, setInput] = useState('');
  const [isTyping, setIsTyping] = useState(false);
  const messagesEndRef = useRef(null);

  useEffect(() => messagesEndRef.current?.scrollIntoView({ behavior: "smooth" }), [messages, isTyping]);

  const handleSend = async () => {
    if (!input.trim()) return;
    const userMessage = { role: 'user', text: input };
    setMessages(prev => [...prev, userMessage]);
    setInput(''); setIsTyping(true);

    try {
      const systemPrompt = `You are Aura, an empathetic AI menstrual wellness companion. Context: User is on Day ${cycleInfo.cycleDay} (${cycleInfo.phase} phase). Keep responses concise, warm, and helpful. Format with short paragraphs.`;
      let retries = 3, data = null;
      const payload = {
        contents: [...messages, userMessage].map(m => ({ role: m.role, parts: [{ text: m.text }] })),
        systemInstruction: { parts: [{ text: systemPrompt }] }
      };

      while (retries > 0) {
        try {
          const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
            method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload)
          });
          if (!res.ok) throw new Error();
          data = await res.json();
          break;
        } catch (e) { retries--; await new Promise(r => setTimeout(r, 1000)); }
      }
      if (data?.candidates?.[0]) setMessages(prev => [...prev, { role: 'model', text: data.candidates[0].content.parts[0].text }]);
    } catch (error) {
      setMessages(prev => [...prev, { role: 'model', text: "I'm having trouble connecting right now, but please rest and take care! 🌸" }]);
    } finally { setIsTyping(false); }
  };

  return (
    <div className="flex flex-col h-full bg-gray-50/50 dark:bg-gray-900/50 absolute inset-0 pt-20 pb-20">
      <div className="px-6 py-2 bg-purple-50/90 dark:bg-gray-800/90 backdrop-blur border-b border-purple-100 dark:border-gray-700 flex items-center gap-3 z-10">
        <div className="w-10 h-10 rounded-full bg-gradient-to-tr from-purple-400 to-rose-400 flex items-center justify-center shadow-md"><Sparkles className="w-5 h-5 text-white" /></div>
        <div><h3 className="font-semibold text-gray-800 dark:text-white text-sm">Aura AI</h3><p className="text-[10px] text-purple-600 dark:text-purple-400 font-medium tracking-wide uppercase">Wellness Guide</p></div>
      </div>
      <div className="flex-1 overflow-y-auto p-4 space-y-6">
        {messages.map((msg, i) => (
          <div key={i} className={`flex ${msg.role === 'user' ? 'justify-end' : 'justify-start'}`}>
            <div className={`max-w-[80%] p-4 text-sm leading-relaxed shadow-sm ${msg.role === 'user' ? 'bg-gray-900 dark:bg-gray-100 text-white dark:text-gray-900 rounded-3xl rounded-br-sm' : 'bg-white dark:bg-gray-800 text-gray-700 dark:text-gray-200 border border-purple-100 dark:border-gray-700 rounded-3xl rounded-bl-sm'}`}>
              {msg.text.split('\n').map((line, idx) => <p key={idx} className={idx !== 0 ? 'mt-2' : ''}>{line.replace(/\*\*(.*?)\*\*/g, '$1')}</p>)}
            </div>
          </div>
        ))}
        {isTyping && (
           <div className="bg-white dark:bg-gray-800 p-4 w-fit rounded-3xl rounded-bl-sm flex items-center gap-2"><Loader2 className="w-4 h-4 animate-spin text-purple-400" /><span className="text-xs text-purple-400">Typing...</span></div>
        )}
        <div ref={messagesEndRef} />
      </div>
      <div className="p-4 bg-white dark:bg-gray-900 border-t border-purple-100 dark:border-gray-800">
        <div className="flex items-center gap-2 bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700 rounded-full p-1 pl-4">
          <input type="text" value={input} onChange={(e) => setInput(e.target.value)} onKeyDown={(e) => e.key === 'Enter' && handleSend()} placeholder="Ask Aura anything..." className="flex-1 bg-transparent border-none focus:outline-none text-sm text-gray-700 dark:text-gray-200 py-2" />
          <button onClick={handleSend} disabled={!input.trim() || isTyping} className="w-10 h-10 rounded-full bg-purple-500 text-white flex items-center justify-center disabled:opacity-50"><Send className="w-4 h-4 ml-0.5" /></button>
        </div>
      </div>
    </div>
  );
}

// --- Settings Tab (New Features Added) ---
function SettingsTab({ cycleData, cycleInfo, setOnboardingComplete, setLogs }) {
  const [linkCopied, setLinkCopied] = useState(false);

  // Generates a mock .ics file to download
  const handleCalendarExport = () => {
    const formatIcsDate = (date) => date.toISOString().split('T')[0].replace(/-/g, '');
    const startDate = formatIcsDate(cycleInfo.nextPeriod);
    const endDate = formatIcsDate(addDays(cycleInfo.nextPeriod, cycleData.averagePeriodLength));

    const icsContent = `BEGIN:VCALENDAR\nVERSION:2.0\nBEGIN:VEVENT\nDTSTART;VALUE=DATE:${startDate}\nDTEND;VALUE=DATE:${endDate}\nSUMMARY:Aura - Predicted Period\nDESCRIPTION:Take care of yourself!\nEND:VEVENT\nEND:VCALENDAR`;

    const blob = new Blob([icsContent], { type: 'text/calendar;charset=utf-8' });
    const link = document.createElement('a');
    link.href = window.URL.createObjectURL(blob);
    link.setAttribute('download', 'aura-cycle.ics');
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  const handlePartnerSync = () => {
    const randomId = Math.random().toString(36).substring(2, 10);
    navigator.clipboard.writeText(`https://aura.app/partner/${randomId}`);
    setLinkCopied(true);
    setTimeout(() => setLinkCopied(false), 3000);
  };

  return (
    <div className="p-6 space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
      <h2 className="text-3xl font-light text-gray-800 dark:text-white">Settings</h2>

      {/* Integrations */}
      <div className="bg-white dark:bg-gray-800 rounded-3xl p-5 border border-gray-100 dark:border-gray-700 shadow-sm space-y-3">
        <h3 className="font-semibold text-gray-800 dark:text-white mb-2 border-b border-gray-100 dark:border-gray-700 pb-2">Integrations</h3>

        <button onClick={handleCalendarExport} className="w-full flex items-center justify-between p-3 text-sm text-gray-700 dark:text-gray-200 bg-gray-50 dark:bg-gray-700/50 rounded-xl hover:bg-gray-100 dark:hover:bg-gray-700 transition border border-gray-200 dark:border-gray-600">
          <span className="flex items-center gap-2"><CalendarDays className="w-4 h-4 text-blue-500" /> Export to Calendar</span>
          <Download className="w-4 h-4 text-gray-400" />
        </button>

        <button onClick={handlePartnerSync} className="w-full flex items-center justify-between p-3 text-sm text-gray-700 dark:text-gray-200 bg-rose-50 dark:bg-rose-900/20 rounded-xl hover:bg-rose-100 dark:hover:bg-rose-900/40 transition border border-rose-200 dark:border-rose-900/50">
          <span className="flex items-center gap-2"><Users className="w-4 h-4 text-rose-500" /> Partner Sync Link</span>
          <span className="text-xs font-medium text-rose-500">{linkCopied ? "Copied!" : "Copy Link"}</span>
        </button>
        <p className="text-[10px] text-gray-400 dark:text-gray-500 px-1 leading-tight">Partner link creates a secure, read-only dashboard showing your current cycle phase and gentle tips.</p>
      </div>

      {/* Data Management */}
      <div className="bg-white dark:bg-gray-800 rounded-3xl p-5 border border-gray-100 dark:border-gray-700 shadow-sm space-y-4 mt-4">
        <h3 className="font-semibold text-gray-800 dark:text-white mb-2 border-b border-gray-100 dark:border-gray-700 pb-2">Data Management</h3>
        <button
          onClick={() => {
            if(window.confirm('Are you sure you want to clear all your data? This cannot be undone.')) {
              localStorage.removeItem('aura_cycleData');
              localStorage.removeItem('aura_logs');
              setOnboardingComplete(false);
              setLogs({});
            }
          }}
          className="w-full flex items-center justify-center gap-2 py-3 text-sm text-red-500 font-medium bg-red-50 dark:bg-red-900/20 rounded-xl hover:bg-red-100 dark:hover:bg-red-900/40 transition border border-red-100 dark:border-red-900/50">
          <Trash2 className="w-4 h-4" /> Clear Local Data
        </button>
      </div>
    </div>
  );
}
