import { useState, useEffect } from 'react';
import { Moon, Sun, Delete, RotateCcw, Equal, Percent, Divide, X, Minus, Plus } from 'lucide-react';
import { motion, AnimatePresence } from 'framer-motion';

const Calculator = () => {
  const [display, setDisplay] = useState('0');
  const [formula, setFormula] = useState('');
  const [history, setHistory] = useState<{ formula: string; result: string }[]>([]);
  const [isDarkMode, setIsDarkMode] = useState(true);

  const toggleTheme = () => setIsDarkMode(!isDarkMode);

  useEffect(() => {
    const handleKeyDown = (e: KeyboardEvent) => {
      if (/[0-9]/.test(e.key)) handleNumber(e.key);
      if (['+', '-', '*', '/'].includes(e.key)) handleOperator(e.key);
      if (e.key === 'Enter' || e.key === '=') calculate();
      if (e.key === 'Backspace') deleteLast();
      if (e.key === 'Escape') clear();
      if (e.key === '.') handleNumber('.');
      if (e.key === '%') handleOperator('%');
    };
    window.addEventListener('keydown', handleKeyDown);
    return () => window.removeEventListener('keydown', handleKeyDown);
  }, [display, formula]);

  const handleNumber = (num: string) => {
    if (num === '.' && display.includes('.')) return;
    if (display === '0' && num !== '.') {
      setDisplay(num);
    } else {
      setDisplay(display + num);
    }
  };

  const handleOperator = (op: string) => {
    if (formula && display === '0') {
      setFormula(formula.slice(0, -2) + op + ' ');
    } else {
      setFormula(display + ' ' + op + ' ');
      setDisplay('0');
    }
  };

  const calculate = () => {
    try {
      const fullExpression = formula + display;
      // Using Function constructor as a safer alternative to eval for basic math
      // In a real production app, use a math library like mathjs
      const result = Function(`"use strict"; return (${fullExpression.replace('×', '*').replace('÷', '/')})`)();
      
      const resultStr = Number.isInteger(result) ? result.toString() : result.toFixed(4).replace(/\.?0+$/, "");
      
      setHistory([{ formula: fullExpression, result: resultStr }, ...history].slice(0, 5));
      setDisplay(resultStr);
      setFormula('');
    } catch (error) {
      setDisplay('Error');
    }
  };

  const clear = () => {
    setDisplay('0');
    setFormula('');
  };

  const deleteLast = () => {
    if (display.length > 1) {
      setDisplay(display.slice(0, -1));
    } else {
      setDisplay('0');
    }
  };

  const Button = ({ children, onClick, className = "", variant = "default" }: any) => {
    const variants = {
      default: isDarkMode ? "bg-slate-800 hover:bg-slate-700 text-white" : "bg-white hover:bg-gray-100 text-slate-800",
      operator: "bg-indigo-600 hover:bg-indigo-500 text-white font-bold",
      action: isDarkMode ? "bg-slate-700 hover:bg-slate-600 text-indigo-400" : "bg-indigo-50 hover:bg-indigo-100 text-indigo-600",
      equals: "bg-gradient-to-br from-indigo-500 to-purple-600 hover:from-indigo-600 hover:to-purple-700 text-white"
    };

    return (
      <motion.button
        whileHover={{ scale: 1.05 }}
        whileTap={{ scale: 0.95 }}
        onClick={onClick}
        className={`h-16 rounded-2xl flex items-center justify-center text-xl transition-colors shadow-lg ${variants[variant as keyof typeof variants]} ${className}`}
      >
        {children}
      </motion.button>
    );
  };

  return (
    <div className={`min-h-screen flex items-center justify-center p-4 transition-colors duration-500 ${isDarkMode ? 'bg-slate-950' : 'bg-slate-100'}`}>
      <div className={`w-full max-w-md rounded-[2.5rem] overflow-hidden shadow-2xl transition-all duration-500 ${isDarkMode ? 'bg-slate-900 ring-1 ring-white/10' : 'bg-white ring-1 ring-black/5'}`}>
        
        {/* Header/Controls */}
        <div className="p-6 flex justify-between items-center">
          <button 
            onClick={toggleTheme}
            className={`p-2 rounded-xl ${isDarkMode ? 'bg-slate-800 text-yellow-400' : 'bg-slate-100 text-indigo-600 shadow-inner'}`}
          >
            {isDarkMode ? <Sun size={20} /> : <Moon size={20} />}
          </button>
          <div className={`px-3 py-1 rounded-full text-xs font-medium ${isDarkMode ? 'bg-slate-800 text-slate-400' : 'bg-slate-100 text-slate-500'}`}>
            PRO CALCULATOR
          </div>
          <div className="w-8 h-8 rounded-full bg-gradient-to-tr from-indigo-500 to-purple-500 blur-[2px] opacity-50" />
        </div>

        {/* Display */}
        <div className="px-6 py-8 flex flex-col items-end justify-end gap-2 overflow-hidden">
          <AnimatePresence mode="wait">
            <motion.div 
              key={formula}
              initial={{ opacity: 0, y: 10 }}
              animate={{ opacity: 1, y: 0 }}
              className={`text-sm font-medium h-6 truncate ${isDarkMode ? 'text-slate-500' : 'text-slate-400'}`}
            >
              {formula}
            </motion.div>
          </AnimatePresence>
          <motion.div 
            key={display}
            initial={{ scale: 0.9, opacity: 0 }}
            animate={{ scale: 1, opacity: 1 }}
            className={`text-6xl font-bold tracking-tight truncate w-full text-right ${isDarkMode ? 'text-white' : 'text-slate-900'}`}
          >
            {display}
          </motion.div>
        </div>

        {/* Buttons Grid */}
        <div className={`p-6 grid grid-cols-4 gap-4 ${isDarkMode ? 'bg-slate-900/50' : 'bg-slate-50'}`}>
          <Button onClick={clear} variant="action">C</Button>
          <Button onClick={deleteLast} variant="action"><Delete size={24} /></Button>
          <Button onClick={() => handleOperator('%')} variant="action"><Percent size={20} /></Button>
          <Button onClick={() => handleOperator('/')} variant="operator"><Divide size={24} /></Button>

          <Button onClick={() => handleNumber('7')}>7</Button>
          <Button onClick={() => handleNumber('8')}>8</Button>
          <Button onClick={() => handleNumber('9')}>9</Button>
          <Button onClick={() => handleOperator('*')} variant="operator"><X size={20} /></Button>

          <Button onClick={() => handleNumber('4')}>4</Button>
          <Button onClick={() => handleNumber('5')}>5</Button>
          <Button onClick={() => handleNumber('6')}>6</Button>
          <Button onClick={() => handleOperator('-')} variant="operator"><Minus size={24} /></Button>

          <Button onClick={() => handleNumber('1')}>1</Button>
          <Button onClick={() => handleNumber('2')}>2</Button>
          <Button onClick={() => handleNumber('3')}>3</Button>
          <Button onClick={() => handleOperator('+')} variant="operator"><Plus size={24} /></Button>

          <Button onClick={() => handleNumber('0')} className="col-span-1">0</Button>
          <Button onClick={() => handleNumber('.')}>.</Button>
          <Button onClick={calculate} className="col-span-2" variant="equals">
            <Equal size={28} />
          </Button>
        </div>

        {/* Recent History Preview */}
        {history.length > 0 && (
          <div className={`px-6 py-4 border-t ${isDarkMode ? 'border-slate-800' : 'border-slate-100'}`}>
            <div className="flex items-center gap-2 mb-2 text-[10px] font-bold uppercase tracking-wider text-slate-500">
              <RotateCcw size={10} /> Recent
            </div>
            <div className="flex gap-4 overflow-x-auto pb-2 scrollbar-hide">
              {history.map((item, i) => (
                <div key={i} className={`flex-shrink-0 px-3 py-1.5 rounded-lg text-xs ${isDarkMode ? 'bg-slate-800/50 text-slate-400' : 'bg-slate-100 text-slate-500'}`}>
                  {item.result}
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default Calculator;
