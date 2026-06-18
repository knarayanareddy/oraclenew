🔮 ORACLE × ALPACA — Complete Lovable Prompt Suite
Every prompt. Full detail. Copy. Paste. In order.
📋 MASTER BUILD ORDER
text

PROMPT    NAME                        OBJECTIVE COVERAGE
──────────────────────────────────────────────────────────────────
  0       Foundation                  Design system + router + data
  1       Alpaca API Layer            Obj 1 (broker connection)
  2       War Room                    Obj 2 (market view) + Obj 5
  3       Order Ticket                Obj 3 (buy/sell orders)
  4       Swarm Simulation            Obj 4 + Obj 7 (creativity)
  5       Strategy Builder            Obj 4 + Obj 5
  6       Memory & Learning           Obj 5 + Obj 4
  7       Autopilot + Agentic         Obj 6 (agentic AI)
  8       Polish + Explainability     Obj 8 + global UX finish
──────────────────────────────────────────────────────────────────
🟣 PROMPT 0 — FOUNDATION
The Design System, Router, and All Mock Data
text

Create a full-stack web application called ORACLE — 
The Swarm Intelligence Broker. This is an AI-native 
brokerage intelligence platform with a dark, 
institutional, futuristic aesthetic.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TECH STACK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
- React 18 with TypeScript
- Vite as build tool
- Tailwind CSS for styling
- Framer Motion for animations
- Recharts for all financial charts
- React Router v6 for navigation
- lucide-react for icons
- shadcn/ui components as base

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DESIGN TOKENS — Apply globally via Tailwind config
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Colors (extend Tailwind config):
  oracle-bg:        #050810
  oracle-surface:   #0A1628
  oracle-surface2:  #0F1F3D
  oracle-card:      #111827
  oracle-border:    #1E3A5F
  oracle-blue:      #3B82F6
  oracle-gold:      #F59E0B
  oracle-green:     #10B981
  oracle-red:       #EF4444
  oracle-amber:     #F59E0B
  oracle-text:      #F1F5F9
  oracle-muted:     #94A3B8
  oracle-dim:       #475569

Typography:
  - Inter: all UI text
  - JetBrains Mono: all numbers, prices, percentages, 
    code, IDs — import from Google Fonts

Global CSS (index.css):
  body { background: #050810; color: #F1F5F9; }
  
  * Custom scrollbar:
  ::-webkit-scrollbar { width: 4px; height: 4px; }
  ::-webkit-scrollbar-track { background: #1E3A5F; }
  ::-webkit-scrollbar-thumb { background: #3B82F6; 
    border-radius: 2px; }

  * Standard card class:
  .oracle-card {
    background: #111827;
    border: 1px solid #1E3A5F;
    border-radius: 12px;
    box-shadow: 0 0 30px rgba(59,130,246,0.05);
  }

  * Input class:
  .oracle-input {
    background: #050810;
    border: 1px solid #1E3A5F;
    border-radius: 8px;
    color: #F1F5F9;
    font-family: 'Inter', sans-serif;
  }
  .oracle-input:focus {
    border-color: #3B82F6;
    box-shadow: 0 0 0 3px rgba(59,130,246,0.15);
    outline: none;
  }

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
APP SHELL LAYOUT — src/components/layout/AppShell.tsx
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
The app shell wraps all pages. It has 4 zones:

ZONE 1 — DEMO BANNER (top, 36px, full width):
  Background: linear-gradient(90deg, #92400E, #F59E0B)
  Text (center, 13px, font-weight 600):
  "⚡ ORACLE DEMO — Paper trading active via Alpaca 
  API · All simulations run on live mock data · 
  Built at Amsterdam AI Broker Hackathon 2026"
  Right side: "×" dismiss button (stores 
  dismissed=true in localStorage, hides banner)
  When dismissed: all other zones expand to fill space

ZONE 2 — TOP BAR (56px tall, fixed, full width, 
  top = 36px when banner visible, top = 0 when dismissed):
  Background: #0A1628
  Border bottom: 1px solid #1E3A5F
  Layout: flex, space-between, px-4, items-center
  
  LEFT SECTION:
  - "🔮" emoji (24px, gold color, mr-2)
  - "ORACLE" text: 
    font-size: 20px, font-weight: 800
    background: linear-gradient(90deg, #3B82F6, #F59E0B)
    -webkit-background-clip: text
    -webkit-text-fill-color: transparent
  - Alpaca connection status badge (ml-3):
    Connected state: green dot + "PAPER LIVE" 
      (green pill, 11px)
    Disconnected state: red dot + "DISCONNECTED" 
      (red pill, 11px)
    Clicking badge opens AlpacaStatusDropdown 
      (implement later in Prompt 1)
  
  CENTER SECTION:
  - Current page breadcrumb (text-sm, text-oracle-muted)
    Changes based on active route
  
  RIGHT SECTION (flex, gap-3, items-center):
  - AUTOPILOT toggle:
    Label: "AUTOPILOT" (text-xs, mr-2, text-oracle-muted)
    Toggle switch component
    OFF state: gray (#475569 background)
    ON state: pulsing green (#10B981) with 
      animated "LIVE" badge (red pill, pulse animation)
    State stored in React context: AutopilotContext
  - Notification bell icon (lucide BellIcon, 20px)
    Red dot badge showing unread count
    onClick: opens NotificationPanel dropdown
  - User avatar circle (32px, bg-oracle-blue):
    Shows initials "TM" in white, 12px
    
ZONE 3 — SIDEBAR (64px wide, fixed left, full height 
  below top bar, background #0A1628, 
  border-right: 1px solid #1E3A5F):
  
  Flex column, items-center, py-4, gap-2
  
  Icons (top to bottom):
  1. Home/Grid icon → route "/" 
     Tooltip: "War Room"
  2. Waves icon → route "/swarm"
     Tooltip: "Swarm Simulation"
  3. Candlestick/BarChart2 icon → route "/strategy"
     Tooltip: "Strategy Builder"
  4. Brain icon → route "/memory"
     Tooltip: "Memory & Learning"
  5. ShoppingCart icon → opens OrderTicketDrawer
     Tooltip: "Order Ticket"
     (at bottom, above settings)
  6. Settings icon → route "/settings" (at very bottom)
     Tooltip: "Settings"
  
  Each icon button:
  - Size: 40×40px, border-radius: 10px
  - Default: text-oracle-dim, hover: 
    text-oracle-text + bg-oracle-surface2
  - Active route: text-oracle-blue + 
    bg-oracle-surface2 + 
    box-shadow: 0 0 12px rgba(59,130,246,0.3)
  - Transition: all 150ms ease
  - Show tooltip on hover (right side, 
    dark pill with arrow)

ZONE 4 — MAIN CONTENT (fills remaining space):
  margin-left: 64px
  margin-top: 92px (36px banner + 56px topbar)
  When banner dismissed: margin-top: 56px
  overflow-y: auto
  padding: 24px

ZONE 5 — RIGHT PANEL (320px, fixed right, 
  collapsible, top below topbar, 
  background #0A1628, 
  border-left: 1px solid #1E3A5F):
  
  Default state: collapsed (hidden)
  Only expands when Autopilot is ON
  
  When expanded, MAIN CONTENT gets 
  margin-right: 320px
  
  Panel contents (implement fully in Prompt 7):
  Header: "TRANSPARENCY FEED" (12px, 
    font-weight: 700, letter-spacing: 0.1em)
  Green pulsing "LIVE" dot next to header
  Scrollable feed area (implement in Prompt 7)

ZONE 6 — VOICE BAR (fixed bottom, full width, 
  height: 64px, background: #0A1628, 
  border-top: 1px solid #1E3A5F):
  (Implement contents in Prompt 7, 
  for now just render the empty bar)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROUTING — src/main.tsx + src/App.tsx
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Set up React Router v6 with these routes, all 
wrapped in AppShell:
  / → WarRoom page
  /swarm → SwarmSimulation page
  /strategy → StrategyBuilder page
  /memory → MemoryLearning page
  /settings → Settings page (basic, build in Prompt 1)

Wrap <Routes> in <AnimatePresence mode="wait"> 
from framer-motion for page transitions.

Each page component should be wrapped in:
<motion.div
  initial={{ opacity: 0, y: 8 }}
  animate={{ opacity: 1, y: 0 }}
  exit={{ opacity: 0, y: -8 }}
  transition={{ duration: 0.2, ease: "easeInOut" }}
>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
GLOBAL STATE — src/context/
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create these React contexts:

1. AlpacaContext (src/context/AlpacaContext.tsx):
   State:
   - isConnected: boolean
   - apiKey: string
   - secretKey: string
   - accountData: AlpacaAccount | null
   - positions: AlpacaPosition[]
   - orders: AlpacaOrder[]
   Actions:
   - connect(apiKey, secretKey): Promise<boolean>
   - disconnect(): void
   - refreshAccount(): Promise<void>
   - refreshPositions(): Promise<void>
   On mount: read keys from localStorage, 
   if present auto-connect

2. AutopilotContext (src/context/AutopilotContext.tsx):
   State:
   - isActive: boolean
   - paperTradingMode: boolean (default true)
   - requireConfirmation: boolean (default true)
   - maxDailyTrades: number (default 5)
   - tradesToday: number
   Actions:
   - toggle(): void
   - configure(settings): void

3. NotificationContext (src/context/NotificationContext.tsx):
   State:
   - notifications: Notification[]
   - unreadCount: number
   Actions:
   - addNotification(type, title, message): void
   - markAllRead(): void
   
   Types: 'action' | 'success' | 'warning' | 
          'learning' | 'swarm' | 'trade'
   
   Auto-dismissing toast renderer (top-right, 
   z-index: 9999, stacked):
   Each toast: slides in from right (framer-motion),
   auto-dismisses after 4 seconds
   Colors by type:
   action → blue border
   success → green border  
   warning → amber border
   learning → purple border
   swarm → teal border
   trade → gold border

4. OrderTicketContext (src/context/OrderTicketContext.tsx):
   State:
   - isOpen: boolean
   - prefilledSymbol: string | null
   - prefilledSide: 'buy' | 'sell' | null
   Actions:
   - openOrderTicket(symbol?, side?): void
   - closeOrderTicket(): void

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MOCK DATA — src/data/
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create these TypeScript data files:

FILE: src/data/mockPositions.ts
Export mockPositions array with 5 objects:
Each object: {
  symbol: string,           // NVDA, AAPL, SPY, BTC, TLT
  companyName: string,
  qty: number,              // 15, 20, 10, 0.5, 30
  entryPrice: number,
  currentPrice: number,     // slightly above/below entry
  marketValue: number,
  unrealizedPL: number,
  unrealizedPLPercent: number,
  oracleSignal: 'BUY' | 'HOLD' | 'REDUCE' | 'WATCH',
  swarmSentiment: number,   // 0-100
  layer: string
}

FILE: src/data/mockEquityCurve.ts
Export 252 data points (1 year of trading days):
Each: { date: string, oracle: number, spy: number }
oracle starts at 100000, ends around 128700
spy starts at 100000, ends around 114200
Add realistic volatility curves

FILE: src/data/mockTransparencyFeed.ts
Export 15 feed entry objects:
Each: {
  id: string,
  timestamp: string,        // "14:32:18"
  layer: string,            // "L1" through "L10"
  type: 'data' | 'simulation' | 'action' | 'risk',
  icon: string,             // emoji
  message: string
}
Entries should tell a coherent story:
"📡 L1: Market data synced — 847 assets indexed"
"📰 L3: Breaking — Fed signals hold on rates"
"🌊 L6: Launching swarm (500 agents)..."
"🌊 L6: Swarm complete — 63% bearish consensus"
"🤖 L7: Bull agent: momentum still intact"
"🤖 L7: Bear agent: yield curve signal flagged"
"⚖️ L8: Risk score elevated on tech sector"
"✅ Action: Reducing NVDA by 8%"
"📚 L9: Lesson #47 stored to memory graph"
... 6 more entries

FILE: src/data/mockSimulations.ts
Export 8 past simulation objects:
Each: {
  id: string,
  date: string,
  seed: string,
  bullish: number,
  neutral: number,
  bearish: number,
  verdict: 'BULLISH' | 'BEARISH' | 'NEUTRAL',
  confidence: number,
  accuracy: 'CORRECT' | 'WRONG' | 'PENDING',
  agents: number,
  rounds: number
}

FILE: src/data/mockLessons.ts
Export 12 lesson objects:
Each: {
  id: number,
  timestamp: string,
  confidence: number,       // 1-5
  text: string,
  tags: string[]
}
Cover topics: rate hikes, retail panic, 
earnings surprises, sector rotation, 
Polymarket accuracy, behavioral corrections

FILE: src/data/mockStrategies.ts
Export 6 saved strategy objects:
Each: {
  id: string,
  name: string,
  description: string,
  totalReturn: number,
  sharpe: number,
  maxDrawdown: number,
  winRate: number,
  status: 'LIVE' | 'SAVED' | 'BACKTESTED',
  trades: number
}

FILE: src/data/mockMarketData.ts
Export watchlist array for 8 symbols:
NVDA, AAPL, MSFT, SPY, QQQ, BTC/USD, TLT, GLD
Each: {
  symbol: string,
  name: string,
  price: number,
  change: number,
  changePercent: number,
  volume: string,
  sparkline: number[]   // 24 data points for mini chart
}

FILE: src/data/mockNarratives.ts
Export array of 6 swarm narrative strings 
that cycle during simulation

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TYPES — src/types/index.ts
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Export these TypeScript interfaces:

AlpacaAccount {
  id: string
  account_number: string
  status: string
  cash: string
  portfolio_value: string
  buying_power: string
  equity: string
  last_equity: string
  long_market_value: string
  short_market_value: string
  daytrade_count: number
  pattern_day_trader: boolean
}

AlpacaPosition {
  asset_id: string
  symbol: string
  qty: string
  avg_entry_price: string
  current_price: string
  market_value: string
  unrealized_pl: string
  unrealized_plpc: string
  side: string
}

AlpacaOrder {
  id: string
  symbol: string
  qty: string
  side: 'buy' | 'sell'
  type: 'market' | 'limit' | 'stop' | 'stop_limit'
  time_in_force: string
  status: string
  filled_avg_price: string | null
  created_at: string
  filled_at: string | null
}

AlpacaOrderRequest {
  symbol: string
  qty?: string
  notional?: string
  side: 'buy' | 'sell'
  type: 'market' | 'limit' | 'stop' | 'stop_limit'
  time_in_force: 'day' | 'gtc' | 'ioc' | 'fok'
  limit_price?: string
  stop_price?: string
}

SwarmResult {
  bullish: number
  neutral: number
  bearish: number
  confidence: number
  verdict: string
  narrative: string
  rounds: number
  totalRounds: number
  agents: number
}

Notification {
  id: string
  type: 'action'|'success'|'warning'|
        'learning'|'swarm'|'trade'
  title: string
  message: string
  timestamp: string
  read: boolean
}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SHARED COMPONENTS — src/components/ui/
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create these reusable components now:

StatCard.tsx — props: label, value, subtitle, 
  trend (up/down/neutral), sparkline data (optional)
  Hover: scale(1.02), border becomes oracle-blue
  Value animates counting up on mount (0 to final, 
  800ms, easeOut)
  JetBrains Mono for value

LayerBadge.tsx — props: layer (L1-L10), size (sm/md)
  Shows "L3" etc as a small pill
  Color by layer:
  L1-L2: gray, L3: blue, L4: purple, 
  L5: gold, L6-L7: teal, L8: red, 
  L9-L10: indigo

SignalPill.tsx — props: signal (BUY/HOLD/REDUCE/WATCH)
  BUY: green bg, HOLD: gray bg, 
  REDUCE: red bg, WATCH: amber bg
  Small rounded pill

PulsingDot.tsx — props: color (green/blue/gold/red)
  Animated pulsing circle dot
  CSS keyframe: scale 1→1.4→1, opacity 1→0.7→1

SkeletonCard.tsx — animated shimmer placeholder
  Dark gray (#1E3A5F) with shimmer animation
  Props: height, width

OracleLoadingScreen.tsx — full screen branded loader:
  Dark background, centered:
  "🔮" emoji (48px) with rotating gold ring around it
  Below: "ORACLE" wordmark in gradient
  Below: cycling text (fades in/out every 1.5s):
    "Extracting entities from seed..."
    "Constructing knowledge graph..."
    "Spawning 500 agents..."
    "Running simulation rounds..."
    "Synthesizing consensus..."
    "Generating Oracle Report..."
  Below: progress bar (fills from 0-100% 
  over specified duration prop)
  Props: isVisible, duration, onComplete

All components use the design tokens above.
No placeholder pages needed — just the shell, 
contexts, data, types, and components described.
Ensure the app compiles and renders the AppShell 
with empty page content at all routes.
🟣 PROMPT 1 — ALPACA API LAYER + CONNECTION
Objective 1: Connected Broker Account (/5)
text

Add the Alpaca Paper Trading API integration layer 
to ORACLE. This covers the full connection flow, 
API service, and Settings page.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART A — API SERVICE LAYER
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/services/alpacaApi.ts

Constants:
const PAPER_BASE = "https://paper-api.alpaca.markets"
const DATA_BASE = "https://data.alpaca.markets"

Helper function: alpacaFetch
- Signature: alpacaFetch(base, endpoint, options?)
- Reads apiKey + secretKey from localStorage keys 
  "oracle_alpaca_key" and "oracle_alpaca_secret"
- Constructs headers:
  { 
    "APCA-API-KEY-ID": apiKey,
    "APCA-API-SECRET-KEY": secretKey,
    "Content-Type": "application/json"
  }
- If no keys stored: throws Error("NO_KEYS")
- On 401/403: throws Error("INVALID_KEYS")
- On network error: throws Error("NETWORK_ERROR")
- Returns: response.json()

Export these async functions 
(all use alpacaFetch internally):

// ── ACCOUNT ──────────────────────────────────
export async function getAccount(): 
  Promise<AlpacaAccount>
  GET PAPER_BASE/v2/account

export async function getPortfolioHistory(
  period?: string, 
  timeframe?: string
): Promise<{ equity: number[], timestamp: number[], 
             profit_loss_pct: number[] }>
  GET PAPER_BASE/v2/account/portfolio/history
  params: period (default "1M"), 
          timeframe (default "1D")

// ── POSITIONS ─────────────────────────────────
export async function getPositions(): 
  Promise<AlpacaPosition[]>
  GET PAPER_BASE/v2/positions

export async function closePosition(symbol: string): 
  Promise<AlpacaOrder>
  DELETE PAPER_BASE/v2/positions/{symbol}

// ── ORDERS ────────────────────────────────────
export async function getOrders(
  status?: 'open'|'closed'|'all'
): Promise<AlpacaOrder[]>
  GET PAPER_BASE/v2/orders
  params: status (default "all"), limit: 20

export async function placeOrder(
  req: AlpacaOrderRequest
): Promise<AlpacaOrder>
  POST PAPER_BASE/v2/orders
  body: JSON.stringify(req)

export async function cancelOrder(
  orderId: string
): Promise<void>
  DELETE PAPER_BASE/v2/orders/{orderId}

// ── MARKET DATA ───────────────────────────────
export async function getLatestBar(
  symbol: string
): Promise<{ 
  bar: { c: number, h: number, l: number, 
         o: number, v: number, t: string } 
}>
  GET DATA_BASE/v2/stocks/{symbol}/bars/latest

export async function getLatestQuote(
  symbol: string
): Promise<{
  quote: { ap: number, bp: number, 
           as: number, bs: number, t: string }
}>
  GET DATA_BASE/v2/stocks/
  {symbol}/quotes/latest

export async function getBars(
  symbol: string,
  timeframe: string,
  start: string,
  end: string
): Promise<{ bars: Array<{
  t: string, o: number, h: number, 
  l: number, c: number, v: number
}> }>
  GET DATA_BASE/v2/stocks/{symbol}/bars
  params: timeframe, start, end, limit: 100

export async function getMultipleLatestBars(
  symbols: string[]
): Promise<Record<string, { 
  c: number, h: number, l: number, 
  o: number, v: number, t: string 
}>>
  GET DATA_BASE/v2/stocks/bars/latest
  params: symbols (comma-separated)
  Returns: { bars: { NVDA: {...}, AAPL: {...} } }
  
// ── VALIDATION ────────────────────────────────
export async function validateConnection(
  apiKey: string, 
  secretKey: string
): Promise<AlpacaAccount>
  Temporarily sets headers with provided keys 
  (not from localStorage)
  Makes GET PAPER_BASE/v2/account call
  If success: returns account data
  If fails: throws descriptive error

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART B — UPDATE AlpacaContext
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Update src/context/AlpacaContext.tsx to use the 
API service:

connect(apiKey, secretKey):
  1. Call validateConnection(apiKey, secretKey)
  2. If success: 
     - Store keys in localStorage
     - Set isConnected = true
     - Set accountData = response
     - Start refresh interval (every 30 seconds)
     - Return true
  3. If fails: return false, set error message

disconnect():
  - Clear localStorage keys
  - Set isConnected = false
  - Set accountData = null
  - Clear positions and orders
  - Stop refresh interval

refreshAccount():
  - Call getAccount() and getPositions() 
    and getOrders() in parallel
  - Update context state

On mount (useEffect):
  - Check localStorage for stored keys
  - If present: call connect() automatically
  - Set loading state while connecting

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART C — CONNECTION MODAL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/components/AlpacaConnectModal.tsx

This modal appears when isConnected = false 
and user navigates to any page except /settings.
It can also be opened from the Settings page.

MODAL DESIGN:
Full-screen overlay: rgba(5,8,16,0.95) background
Central card: 480px wide, oracle-card style, 
  border: 1px solid #1E3A5F
  padding: 40px
  border-radius: 16px
  
CONTENT:
- Top: "🔮" (40px) centered
- Title: "CONNECT ALPACA PAPER ACCOUNT" 
  (20px, bold, gradient text blue→gold)
- Subtitle: "Enter your Alpaca Paper Trading API 
  credentials to activate live data and trading."
  (14px, oracle-muted, center, mt-2, max-w: 360px)

- Info box (mt-6, bg-oracle-surface, 
  border: oracle-border, rounded-10, p-3):
  Icon: 🏦 
  Text: "Paper trading only — no real money involved.
  Get free credentials at alpaca.markets"
  Link: "Get API keys →" in oracle-blue

- INPUTS (mt-6):
  
  Label: "API KEY ID"
  Input: type="text", placeholder="PK...", 
    monospace font, full width
    On paste: auto-trim whitespace
  
  Label: "SECRET KEY" (mt-4)
  Input: type="password", placeholder="••••••••"
    Right side: eye toggle icon 
    (toggles text/password type)
  
  Label: "BASE URL" (mt-4)
  Read-only input showing:
    "https://paper-api.alpaca.markets"
    Gold text, gold left border
    Small "PAPER" pill badge on right

- Error message area (mt-3, text-red-400, text-sm):
  Hidden unless error exists
  Shows: "Invalid credentials — check your 
  Alpaca paper trading API keys"

- BUTTON (mt-6):
  Full width, 48px height
  Text: "CONNECT ACCOUNT →"
  Background: linear-gradient(135deg, #2563EB, #3B82F6)
  Border: 1px solid rgba(59,130,246,0.5)
  
  Loading state: spinner + "Verifying connection..."
  Success state: green checkmark + 
    "CONNECTED — Paper Account Active"
    Then auto-closes after 1.5 seconds with 
    scale-up fade-out animation

- Below button (mt-4, text-center):
  "Skip for now → use demo mode"
  (text-xs, oracle-dim, cursor-pointer)
  Clicking: closes modal, sets a 
  demoMode=true flag in context

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART D — ALPACA STATUS DROPDOWN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/components/AlpacaStatusDropdown.tsx

This dropdown opens from the connection badge 
in the top bar when clicked.

CONNECTED STATE dropdown (240px wide card 
below the badge):
- Header: "ALPACA PAPER ACCOUNT" (12px, bold, 
  letter-spacing: 0.1em)
- Divider
- Row: Account # — "PA•••••••1234" (masked)
- Row: Status — "ACTIVE" (green pill)
- Row: Buying Power — real value from accountData 
  in JetBrains Mono, green
- Row: Portfolio Value — real value, JetBrains Mono
- Row: Cash — real value, JetBrains Mono
- Row: Day Trades — count number
- Divider
- "Refresh Data" button (text-sm, oracle-blue)
  onClick: calls refreshAccount()
- "Disconnect" link (text-sm, text-red-400)
  onClick: calls disconnect()

DISCONNECTED STATE dropdown:
- "Not connected" message
- "Connect Alpaca →" button

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART E — SETTINGS PAGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/pages/Settings.tsx

Page title: "⚙️ SETTINGS"
Subtitle: "Configure your ORACLE and Alpaca 
paper trading connection"

SECTION 1 — "ALPACA CONNECTION" card:
Shows AlpacaConnectModal inline (not as overlay):
  If connected: show account summary + 
    green CONNECTED badge + Disconnect button
  If disconnected: show the input form inline

SECTION 2 — "ORACLE PREFERENCES" card:
  Toggle: "Show Transparency Feed automatically" 
    (default: on when Autopilot is on)
  Toggle: "Auto-run simulation on Swarm page load" 
    (default: on)
  Toggle: "Sound effects on trade execution" 
    (default: off)
  Dropdown: "Default chart timeframe" 
    (1D / 1W / 1M / 3M / 1Y)

SECTION 3 — "EXPLAINABILITY" card (important!):
  Title: "ORACLE FEATURE EXPLAINABILITY"
  Subtitle: "Full documentation of every feature 
  and why it was built"
  Renders a markdown-like document inline:
  
  Use code blocks / styled sections to show:
  
  FEATURE 1: Connected Broker Account
  - How: Alpaca Paper Trading REST API v2
  - Endpoint: GET /v2/account
  - Why: Real portfolio data without financial risk.
    Paper trading is identical to live trading 
    infrastructure.
  
  FEATURE 2: Market View
  - How: Alpaca Market Data API v2
  - Endpoint: GET /v2/stocks/{symbol}/bars/latest
  - Refresh: every 10 seconds
  - Why: Real prices enable accurate signal 
    validation and P&L calculation.
  
  FEATURE 3: Order Ticket (Buy/Sell)
  - How: POST /v2/orders with JSON body
  - Supports: market, limit, stop, stop-limit
  - Time in force: day, gtc, ioc, fok
  - Why: Closes the loop from AI signal to 
    real (paper) execution.
  
  FEATURE 4: AI Trade Ideas — MiroFish Swarm
  - How: 1,000 simulated agents (institutional 35%, 
    retail 50%, media 15%) run debate rounds, 
    form coalitions, reach consensus
  - Why: Models the human psychology that moves 
    markets, not just historical price patterns.
    Based on opinion dynamics research 
    (DeGroot learning model).
  
  FEATURE 5: Portfolio Intelligence
  - How: Combines real Alpaca position data with 
    10-layer signal attribution
  - Metrics: Sharpe ratio, max drawdown, win rate, 
    signal contribution analysis
  - Why: Institutional-grade analytics surfaced in 
    a consumer-friendly UI.
  
  FEATURE 6: Agentic AI — Autopilot
  - How: Monitors 10 intelligence layers, generates 
    swarm signal, evaluates confidence threshold 
    (>70%), submits order via POST /v2/orders
  - Why: Removes emotional bias from execution. 
    Every autonomous decision is logged and 
    explainable in the Transparency Feed.
  
  FEATURE 7: Creativity — Swarm Simulation
  - How: Force-directed agent network visualization, 
    real-time sentiment gauges, narrative emergence 
    feed, Oracle Verdict report
  - Tagline: "We don't predict markets. We simulate 
    the humans that move them."
  - Why: Unique approach to market intelligence 
    that addresses root causes rather than symptoms.
  
  FEATURE 8: Explainability
  - How: This document + in-app Transparency Feed 
    (logs every decision with layer attribution) + 
    Signal Contribution charts in Strategy Builder
  - Why: Regulatory-grade auditability. 
    Every trade has a paper trail. 
    Every signal has a source.
  
  Below document: "Download as PDF" button 
  (outlined, oracle-border)
  (For demo: just trigger window.print())
🟣 PROMPT 2 — WAR ROOM
Objectives 2 (Market View) + 5 (Portfolio Intelligence)
text

Build the WAR ROOM page at route "/". 
This is the main command center of ORACLE.
It uses real Alpaca API data where connected, 
falling back to mock data when in demo mode.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE LAYOUT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Full page layout (inside AppShell content area):
- No extra padding beyond AppShell's 24px

Row 1: TOP STATS BAR — full width, 4 stat cards
Row 2: THREE COLUMN GRID
  Column A (35%): Portfolio Intelligence
  Column B (40%): Active Simulation + Signal Matrix
  Column C (25%): Quick Actions + Layer Status + 
                  Latest Lesson
Row 3: MARKET VIEW — full width watchlist

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 1 — TOP STATS BAR
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
4 StatCards in a responsive grid (4 cols desktop, 
2 cols tablet):

Card 1 — PORTFOLIO VALUE:
  If Alpaca connected: show real 
    accountData.portfolio_value
  If demo mode: show "$124,350.00"
  Subtitle: change from yesterday 
    (real: compare to accountData.last_equity)
    (demo: "+$2,847 today (+2.34%)" in green)
  sparkline: small 7-point line from 
    mockEquityCurve last 7 days

Card 2 — BUYING POWER:
  If connected: accountData.buying_power
  If demo: "$87,230.00"
  Subtitle: "Available to trade" in oracle-muted
  Icon: Wallet icon in blue

Card 3 — ORACLE ACCURACY:
  Value: "71%" in gold color
  Subtitle: "Last 47 simulations"
  Small circular progress arc in gold 
  (SVG, 40px diameter, 71% filled)

Card 4 — OPEN POSITIONS:
  If connected: count of real positions array
  If demo: "5"
  Subtitle: "Active holdings"
  Below: small row of symbol pills 
    (NVDA, AAPL, SPY in blue pills)

Each StatCard:
- mount animation: count up from 0 to value 
  over 800ms using requestAnimationFrame
- hover: scale(1.02), border-color → oracle-blue
- transition: all 200ms ease

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 2 — THREE COLUMN GRID
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COLUMN A — PORTFOLIO INTELLIGENCE (35%)

Card: PORTFOLIO PERFORMANCE
  Header row:
  - Title "PORTFOLIO PERFORMANCE" (12px, bold, 
    letter-spacing: 0.1em)
  - Timeframe pills: 1D | 1W | 1M | 3M | 1Y
    Active pill: bg-oracle-blue text-white
    Inactive: bg-oracle-surface2 text-oracle-muted
    On click: filter the chart data accordingly

  AreaChart (Recharts, height: 220px):
    Data: mockEquityCurve filtered by timeframe
    
    If Alpaca connected + has portfolio history:
    Use real portfolioHistory data for ORACLE line
    
    Two data series:
    1. "ORACLE" — solid line, #3B82F6, 
       area fill: linearGradient top=#3B82F6 20% 
       opacity → bottom=transparent
    2. "SPY" — dashed line, #F59E0B, 
       area: no fill or very faint
    
    XAxis: date strings, 
      tickFormatter: show abbreviated dates
      tickLine: false, axisLine: false
      tick: { fill: '#475569', fontSize: 11 }
    
    YAxis: dollar values
      tickFormatter: (v) => "$" + 
        (v/1000).toFixed(0) + "k"
      tickLine: false, axisLine: false
      tick: { fill: '#475569', fontSize: 11 }
    
    CartesianGrid: 
      strokeDasharray: "3 3"
      stroke: #1E3A5F
      vertical: false
    
    Custom Tooltip:
      Dark card (#0F1F3D, border #1E3A5F, 
        border-radius: 8px, padding: 12px):
      Date line (bold, white)
      "ORACLE: $XXX,XXX" (blue)
      "SPY: $XXX,XXX" (gold)
      "Difference: +$X,XXX (+X.X%)" 
        (green if positive, red if negative)
    
    Legend: below chart, horizontal
      custom renderLegend: 
        "— ORACLE Portfolio" (blue)
        "- - SPY Benchmark" (gold)
    
    Animation: animationBegin=0, 
      animationDuration=1200

  Metrics row (3 items, mt-3):
    "Sharpe: 2.14" — green text
    "Max DD: -8.3%" — red text
    "Win Rate: 67%" — green text
    Each: label in oracle-muted, 
      value in JetBrains Mono

Card: POSITIONS (mt-4)
  Header: "POSITIONS" title + count badge 
    (bg-oracle-blue text-white rounded-full 
    px-2 py-0.5 text-xs)
  
  Data source:
    If Alpaca connected: use real positions array
    Merge with mock for oracleSignal + swarmSentiment
    If demo: use mockPositions
  
  Table:
    No outer border, rows separated by 
    border-bottom: 1px solid #1E3A5F opacity 50%
    
    Columns:
    ASSET | SIZE | ENTRY | CURRENT | P&L | SIGNAL
    
    Column headers: 
      10px, oracle-dim, uppercase, letter-spacing
    
    Each row:
    - Left border: 3px solid [signal color]
      BUY=green, HOLD=gray, REDUCE=red, WATCH=amber
    - ASSET: bold symbol + muted company name below
    - SIZE: qty + "$" value below (oracle-muted)
      JetBrains Mono
    - ENTRY: avg_entry_price, JetBrains Mono
    - CURRENT: current_price, JetBrains Mono
      Updates every 10s from Alpaca API
    - P&L: unrealized_pl + unrealized_plpc below
      Green if positive, red if negative
      JetBrains Mono, font-weight: 600
    - SIGNAL: SignalPill component
    
    Row hover:
      bg-oracle-surface2 transition
      Right edge: "Run Swarm →" button appears
        (text-xs, oracle-blue, cursor-pointer)
        onClick: opens /swarm with symbol 
        pre-filled as seed


COLUMN B — SIMULATION + SIGNALS (40%)

Card: ACTIVE SWARM
  Header: "ACTIVE SWARM" + blue pulsing dot + 
    "RUNNING" badge (blue pill)
  
  Simulation title: 
    "Fed Rate Decision — June 2026" 
    (14px, oracle-gold, font-weight: 600)
  
  Progress bar:
    "Round 23 / 40" text (JetBrains Mono, 
      text-oracle-muted, text-sm)
    Bar: full width, height: 6px, 
      border-radius: 999px
      Background: #1E3A5F
      Fill: linear-gradient(90deg, #3B82F6, #F59E0B)
      Width: 57.5% (animated via framer-motion)
      transition: width 500ms ease
  
  Three gauge displays (flex row, mt-4, gap-4):
    Each gauge: centered flex-col, flex: 1
    
    SVG circular gauge (80px × 80px):
      Background circle: stroke #1E3A5F, 
        strokeWidth: 8, fill: none
      Foreground arc: 
        BULLISH: stroke #10B981
        NEUTRAL: stroke #475569
        BEARISH: stroke #EF4444
      Arc fills clockwise from top
      Percentage animates from 0 on mount
      Center text: percentage in JetBrains Mono, 
        14px, bold, same color as arc
    
    Label below: "BULLISH" / "NEUTRAL" / "BEARISH"
      text-xs, oracle-muted, uppercase
  
  Agent Activity (mt-4):
    "1,000 AGENTS ACTIVE" 
      (12px, oracle-blue, letter-spacing: 0.1em)
    
    3 rows with icon + label + mini progress bar:
    🏦 Institutional — 350 — blue bar
    🐦 Retail — 500 — green bar
    📰 Media/Analyst — 150 — gold bar
    
    Each bar: height 4px, border-radius 999px
    Background #1E3A5F
    Fill animated width (350/1000 = 35% etc)
    Subtle pulse animation on fill color:
      @keyframes pulse-bar: opacity 0.7→1→0.7 
        2s infinite
  
  Emerging Narrative box (mt-4):
    bg-oracle-bg border border-oracle-border 
    rounded-10 p-3
    Label: "EMERGING NARRATIVE" 
      (10px, oracle-dim, uppercase, mb-2)
    Text: italic, oracle-muted, 14px, line-height: 1.5
    Content cycles through mockNarratives 
    every 5 seconds with framer-motion 
    AnimatePresence (fade transition, 300ms)
  
  Buttons row (mt-4, flex gap-2):
    "VIEW FULL SIMULATION →" 
      outlined blue button, flex:1
      onClick: navigate to /swarm
    "APPLY SIGNAL" 
      filled blue button, flex:1
      onClick: openOrderTicket()

Card: SIGNAL MATRIX (mt-4)
  Header: "SIGNAL MATRIX"
  
  5 signal rows:
  Each row (flex, items-center, gap-3, py-2, 
    border-bottom: 1px solid oracle-border/50):
  
  LEFT: icon (16px emoji) + signal name 
    (13px, font-weight: 500)
  
  MIDDLE-LEFT: LayerBadge component
  
  MIDDLE: Signal strength bars 
    (5 bars like WiFi icon, 4px wide each, 
    gap 2px, heights: 6,9,12,15,18px)
    Filled bars: oracle-blue
    Empty bars: oracle-border
    
  MIDDLE-RIGHT: Direction arrow + confidence
    ↑ green text or ↓ red text
    Confidence: "84%" JetBrains Mono oracle-muted
  
  Data:
  Row 1: 📰 "Fed Hawkish Tone" | L3 | ↓4/5 | 84%
  Row 2: 📊 "NVDA RSI Oversold" | L4 | ↑3/5 | 71%
  Row 3: 🎲 "Rate Hike >70%" | L5 | ↓5/5 | 91%
  Row 4: 🌊 "Retail Panic Selling" | L6 | ↑2/5 | 63%
  Row 5: 📈 "Yield Curve Flatten" | L2 | ↓4/5 | 78%


COLUMN C — QUICK ACTIONS + LAYERS (25%)

Card: ORACLE ACTIONS
  Title: "ORACLE ACTIONS"
  
  4 large action buttons stacked (gap-3):
  
  Button 1: "🌊 RUN NEW SWARM"
    bg-oracle-blue text-white, full width, h-14
    Subtitle: "Simulate market psychology" 
      (11px, opacity: 0.7)
    onClick: navigate('/swarm')
    border-radius: 10px
  
  Button 2: "🧬 BUILD STRATEGY"
    Outlined oracle-blue, full width, h-14
    Subtitle: "Plain English → Live backtest"
    onClick: navigate('/strategy')
  
  Button 3: "🎙️ VOICE COMMAND"
    Outlined oracle-gold text-oracle-gold, 
    full width, h-14
    Subtitle: "Speak to your portfolio"
    Right side: 3 small vertical bars 
      (4px wide, heights 8/12/8px)
      animating up/down at different speeds
      (CSS animation, gold color)
    onClick: activates voice mode (Prompt 7)
  
  Button 4: "🤖 AUTOPILOT"
    Outlined oracle-green text-oracle-green, 
    full width, h-14
    Subtitle text changes:
      OFF: "Autonomous trading mode"
      ON: "Running — 10 layers active"
    Right side: toggle switch (uses AutopilotContext)
    Toggle ON: shows pulsing green dot

Card: INTELLIGENCE LAYERS (mt-4)
  Header row: 
    "INTELLIGENCE LAYERS" title
    "ALL SYSTEMS ✓" (text-oracle-green, text-xs) 
      on right
  
  10 layer rows (stacked, gap-0):
  Each row (flex items-center gap-2, py-2, 
    hover: bg-oracle-surface2 rounded-8 px-2,
    cursor: default, 
    has Tooltip with description on hover):
  
  LEFT: layer badge (L1-L10, custom color)
  MIDDLE: layer name (13px)
  RIGHT: pulsing dot + status text (text-xs, 
    oracle-muted, text-right, flex-shrink-0)
  
  Layers:
  L1 | Market Data | green | "Live — 2s ago"
  L2 | Macro Signals | green | "CPI, Fed, GDP"
  L3 | News NLP | green | "847 articles"
  L4 | Technical | green | "RSI, MACD, BB"
  L5 | Polymarket | gold/syncing | "71% rate hike"
  L6 | Swarm Engine | blue/pulse | "1,000 agents"
  L7 | Agent Debate | blue/pulse | "Consensus..."
  L8 | Risk Scoring | green | "MODERATE"
  L9 | Memory Graph | green | "847 nodes"
  L10 | Explanation AI | green | "Ready"
  
  L6+L7 rows have subtle pulse bg animation
  Tooltip (on hover, right-side pop): 
    1-line description per layer

Card: LATEST LESSON (mt-4)
  Left gold border (4px, border-radius 2px)
  bg-oracle-surface, p-3, rounded-10
  
  "📚 Lesson #47" (12px bold oracle-muted)
  Lesson text (13px italic oracle-muted mt-1):
    "When Polymarket shows >65% rate hike 
    probability + bearish swarm consensus, 
    tech positions historically underperform 
    by 3.2% over the following week."
  
  Footer row (mt-2):
    "Confidence: HIGH ●●●●○" (oracle-gold text-xs)
    "2 hours ago" (oracle-dim text-xs ml-auto)
  
  "View all 47 lessons →" 
    (text-xs oracle-blue mt-2, 
    onClick: navigate('/memory'))

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 3 — MARKET VIEW (full width, mt-4)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
This section satisfies Objective 2 (Market View).

Card header row:
  Left: "📊 MARKET VIEW" title
  Right: 
    Market status pill:
      Check if current time is between 
      15:30–22:00 Amsterdam (UTC+2):
      OPEN: green pulsing dot + "MARKET OPEN"
      CLOSED: red dot + "MARKET CLOSED"
    "Updated Xs ago" (text-xs oracle-muted)
      auto-increments every second
    "↺ Refresh" button 
      onClick: triggers re-fetch of market data

Grid of 8 symbol cards 
(8 columns desktop, 4 tablet, 2 mobile):

For each symbol in 
[NVDA, AAPL, MSFT, SPY, QQQ, TLT, GLD, BTCUSD]:

  Card (bg-oracle-surface2 border-oracle-border 
    rounded-10 p-3):
  
  DATA SOURCE:
    On mount and every 10 seconds:
    If Alpaca connected: 
      call getLatestBar(symbol) for each symbol
      Use bar.c as current price
      Calculate change from bar.o
    If demo mode:
      Use mockMarketData
  
  CARD CONTENT:
    Symbol (12px bold white)
    Company name (10px oracle-muted)
    
    Price (18px JetBrains Mono, font-bold, mt-1):
      "$X,XXX.XX" or "$X.XX" depending on asset
    
    Change row (mt-1):
      "▲ +$X.XX (X.X%)" in oracle-green
      "▼ -$X.XX (-X.X%)" in oracle-red
      (12px JetBrains Mono)
    
    Mini sparkline (mt-2, height: 32px):
      Recharts LineChart, minimal
      No axes, no tooltip
      Line color: green if positive change, 
        red if negative
      Data: mockMarketData[symbol].sparkline 
        (24 points)
      Responsive: width=100%
    
    HOVER STATE: 
      border-color → oracle-blue
      scale(1.01)
      "Trade →" button slides up from bottom of card
        (absolute positioned, bottom: 0)
        onClick: openOrderTicket(symbol, 'buy')

Data loading state:
  While fetching: show SkeletonCard in each slot
  Shimmer animation (dark gray bg, shimmer overlay)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ENTRANCE ANIMATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
All cards animate on page load:
  initial: { opacity: 0, y: 16 }
  animate: { opacity: 1, y: 0 }
  transition: { duration: 0.3, delay: index * 0.08 }
  
Stat cards: delays 0, 0.08, 0.16, 0.24
Column A cards: delays 0.2, 0.3
Column B cards: delays 0.25, 0.35
Column C cards: delays 0.3, 0.38, 0.44
Market view: delay 0.4

All animations use framer-motion variants 
with staggerChildren.
🟣 PROMPT 3 — ORDER TICKET
Objective 3: Buy/Sell Orders via Alpaca (/5)
text

Build the ORDER TICKET drawer component for ORACLE. 
This is how users place real paper trades via 
the Alpaca API. It is accessible from multiple 
locations across the app.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMPONENT: src/components/OrderTicketDrawer.tsx
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
This drawer is always mounted in AppShell.
It slides in from the right when 
OrderTicketContext.isOpen = true.

DRAWER DIMENSIONS:
  Width: 420px
  Full height (below topbar)
  Fixed position, right: 0
  z-index: 500
  Background: #0A1628
  Border-left: 1px solid #1E3A5F
  Box-shadow: -20px 0 60px rgba(0,0,0,0.5)
  
Framer Motion animation:
  initial: { x: 420 }
  animate: { x: 0 }
  exit: { x: 420 }
  transition: { type: "spring", damping: 25, 
    stiffness: 200 }

DRAWER HEADER (sticky top, bg: #0A1628, 
  border-bottom: oracle-border, p-4):
  Left: "📋 ORDER TICKET" (14px bold)
  Center: Alpaca badge "PAPER" (gold pill, 10px)
  Right: X close button (20px, oracle-muted, 
    onClick: closeOrderTicket())

DRAWER BODY (scrollable, p-4, flex-col, gap-4):

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 1 — ASSET SELECTOR
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Label: "ASSET"
Input: text input, uppercase, oracle-input style
  placeholder: "Enter ticker (e.g. NVDA)"
  Pre-fills with prefilledSymbol from context
  onChange: triggers price fetch after 500ms debounce
  
When valid symbol entered and price fetched:
  Show asset info row below input:
  - Symbol (bold, white)
  - Asset name (oracle-muted)
  - Live bid/ask prices from getLatestQuote():
    "Bid: $XXX.XX" | "Ask: $XXX.XX"
    (JetBrains Mono, oracle-muted, text-sm)
  - Last price in large format:
    "$XXX.XX" (20px, JetBrains Mono, bold)
    Change: "+$X.XX (X.X%)" color coded
  - Small indicator: "● LIVE" (green, 10px) 
    if market open, "● CLOSED" (gray) if not

Loading state (while fetching price):
  SkeletonCard in asset info area

Error state (invalid symbol):
  "Symbol not found" in oracle-red

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 2 — ORDER CONFIGURATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BUY / SELL TOGGLE:
  Two large pill buttons side by side:
  BUY: active=bg-oracle-green text-white, 
       inactive=outlined oracle-border text-oracle-muted
  SELL: active=bg-oracle-red text-white,
        inactive=outlined oracle-border text-oracle-muted
  Pre-fills from prefilledSide context
  Transition: 150ms ease

ORDER TYPE:
  4 pill buttons in a row:
  Market | Limit | Stop | Stop Limit
  Active: bg-oracle-surface2 border-oracle-blue text-white
  Inactive: text-oracle-dim

QUANTITY METHOD TOGGLE (mt-3):
  Two small pill toggles: 
    "Shares" (default) | "Dollars (notional)"
  
  If Shares mode:
    Label: "NUMBER OF SHARES"
    Number input (type="number", min=1, step=1)
    Below: "≈ $X,XXX.XX" estimated value
      (calculated from current price × qty)
  
  If Dollars mode:
    Label: "DOLLAR AMOUNT"
    Number input with "$" prefix
    Below: "≈ X.XX shares"

LIMIT PRICE (only shown if Limit or Stop Limit):
  Label: "LIMIT PRICE"
  Number input, pre-fills with current price

STOP PRICE (only shown if Stop or Stop Limit):
  Label: "STOP PRICE"
  Number input

TIME IN FORCE:
  Label: "TIME IN FORCE"
  4 small pills: DAY | GTC | IOC | FOK
  Default: DAY
  Tooltip on hover for each explaining what it means

ORDER SUMMARY BOX (mt-3, 
  bg-oracle-bg border-oracle-border rounded-10 p-3):
  "ORDER SUMMARY" label (10px uppercase oracle-dim)
  
  Summary rows:
  Side: "BUY" (green) or "SELL" (red)
  Asset: "NVDA"
  Qty: "10 shares" or "$1,000 notional"
  Type: "Market Order"
  Est. Total: "$4,253.00" (JetBrains Mono)
  Buying Power After: "$83,000.00" 
    (oracle-muted, smaller)
  
  All values update in real-time as user types.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 3 — ORACLE SIGNAL CONTEXT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
(Shows ORACLE's current view on the asset — 
always visible if we have a valid symbol)

Card: bg-oracle-surface2 rounded-10 p-3

Row 1: "🌊 ORACLE SIGNAL" label (10px oracle-dim)
Signal bar: 
  "63% BEARISH" on the symbol 
  (color matches direction, JetBrains Mono)
  Source: "L6 Swarm · L5 Polymarket" (oracle-dim)

Row 2: Risk indicator
  "⚖️ RISK: ELEVATED" (oracle-amber) 
    or "MODERATE" (oracle-green)

Conflict warning (shows if order direction 
contradicts ORACLE signal):
  If BUY and signal is BEARISH:
  Amber warning box:
    "⚠️ This order goes against ORACLE's current 
    bearish signal (63%). Consider reviewing 
    the swarm results before proceeding."
  
  If SELL and signal is BULLISH: similar message

If order aligns with ORACLE signal:
  Green info box:
    "✓ This order aligns with ORACLE's 
    current signal."

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 4 — SUBMIT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Two-step process:

STEP 1: "PREVIEW ORDER" button
  Full width, outlined oracle-blue, h-12
  onClick: validates inputs, shows confirmation step
  Validation:
    - Symbol must be entered and valid
    - Qty/notional must be > 0
    - If Alpaca not connected: shows 
      "Connect Alpaca to place orders" 
      with "Connect Now →" link

STEP 2: Confirmation view replaces form
  Shows final order summary card with all details
  Text: "Ready to submit this paper trade?"
  
  Two buttons:
  "← Back" (ghost button, left)
  "SUBMIT ORDER ▶" (gold gradient, right, prominent)
  
  SUBMIT onClick: 
    Set loading state: spinner + "Submitting..."
    Call placeOrder({
      symbol: symbolInput.toUpperCase(),
      qty: qty.toString() (if shares mode)
      notional: notional.toString() (if dollar mode)
      side: selectedSide,
      type: selectedType,
      time_in_force: selectedTIF
    })
    
    SUCCESS:
      Animate: 
        Green checkmark scales in (framer-motion 
        scale: 0 → 1.2 → 1, duration: 0.4s)
      Show:
        "✅ ORDER SUBMITTED"
        Order ID: "PA-847291XX" (JetBrains Mono)
        "View in Order History →" link
      
      Add to NotificationContext:
        type: 'trade'
        title: "Order Placed"
        message: "BUY 10 NVDA submitted 
          via Alpaca Paper Trading"
      
      Add to Transparency Feed:
        "✅ Order: BUY 10 NVDA @ Market
        Paper Trade · Alpaca PA-XXXXXX"
      
      Refresh positions in AlpacaContext
      Auto-close drawer after 3 seconds
    
    ERROR:
      Red error box shows Alpaca error message
      "Retry" button appears
      Stay on confirmation screen

If Alpaca not connected at any point:
  Show inline banner: 
  "⚠️ Connect your Alpaca account to place 
  real paper trades"
  "Connect Now →" button (opens connection modal)
  (User can still preview orders in demo mode 
  but cannot submit)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 5 — ORDER HISTORY TAB
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Tabs at top of drawer body: 
[New Order] [Order History]

ORDER HISTORY tab content:
  Data: getOrders('all') from AlpacaContext
  
  If no orders: 
    Empty state with order icon + 
    "No orders yet. Place your first paper trade."
  
  If orders exist:
  Scrollable list of order cards:
  Each card (bg-oracle-surface2 rounded-10 p-3 mb-2):
    Row 1: 
      Side pill (BUY=green, SELL=red) + 
      Symbol (bold) + 
      Qty
    Row 2: 
      Type (small oracle-muted) + 
      Filled price (JetBrains Mono) + 
      Status pill
      Status colors:
        FILLED: green
        PENDING_NEW: blue pulsing
        CANCELLED: gray
        REJECTED: red
    Row 3: 
      Created at timestamp (oracle-dim, text-xs)
      If PENDING: "Cancel" link on right 
        (text-xs text-red-400)
        onClick: cancelOrder(order.id) with confirm
  
  "Refresh Orders" button at bottom
    (text-sm oracle-blue, 
    onClick: refreshAccount())
🟣 PROMPT 4 — SWARM SIMULATION SCREEN
Objectives 4 (AI Features) + 7 (Creativity)
text

Build the SWARM SIMULATION page at route "/swarm". 
This is ORACLE's hero screen — the MiroFish 
swarm simulation chamber.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE LAYOUT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Page header (full width)
Then two-zone layout:
  Left zone (42%, overflow-y: auto): 
    Configuration + Results
  Right zone (58%, sticky top, 
    height: calc(100vh - 160px)): 
    Live Visualization

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE HEADER
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Title: "🌊 ORACLE SWARM" (28px, font-bold, white)
Subtitle: "Simulate 1,000 human agents 
  before every trade" (oracle-muted)
Right side pills:
  "SWARMS TODAY: 47" (bg-oracle-surface2, 
    oracle-blue border, text-oracle-muted)
  "ACCURACY: 71%" (gold bg/8, gold border, 
    text-oracle-gold)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LEFT ZONE — CONFIGURATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card 1: SIMULATION SEED
  Title: "SIMULATION SEED"
  
  Textarea (7 rows, oracle-input style, 
    full width, font-size: 14px, line-height: 1.6):
    placeholder: "Paste any financial trigger here — 
    earnings report, Fed statement, news article, 
    macro data, or your own thesis..."
    On focus: blue glow border + 
      box-shadow: 0 0 0 3px rgba(59,130,246,0.15)
  
  Quick seed buttons (2×2 grid, mt-3, gap-2):
  Each button: outlined, oracle-border, 
    hover: bg-oracle-surface2, text-sm, 
    border-radius: 8px, h-10
  
  "📰 Today's Fed Statement" (gold outlined)
  onClick: fills textarea with:
    "The Federal Reserve has indicated a 
    cautious approach to rate adjustments, 
    citing persistent inflation above the 2% 
    target at 3.1%, while acknowledging signs 
    of labor market cooling. Chair Powell 
    emphasized data dependence for June 2026 
    decisions. Markets currently pricing 
    71% probability of a hold."
  
  "📊 NVDA Earnings Report" (blue outlined)
  onClick: fills with NVDA mock earnings text
  
  "📈 CPI Data Release" (blue outlined)
  onClick: fills with CPI mock data text
  
  "🌍 Geopolitical Risk" (gold outlined)
  onClick: fills with geopolitical risk text

Card 2: CONFIGURE SWARM (mt-4)
  Title: "CONFIGURE SWARM"
  
  AGENT COUNT:
  Label row: "AGENT COUNT" (label) + 
    large display "500 AGENTS" (JetBrains Mono, 
    text-oracle-blue, text-2xl)
  
  HTML range input (custom styled):
    min: 100, max: 1000, step: 50
    value: agentCount (state)
    Track: #1E3A5F background
    Fill: #3B82F6 (use CSS background trick)
    Thumb: #3B82F6, 18px circle
  
  Preset pills below slider (gap-2):
    "Quick (100)" | "Standard (500)" | "Deep (1000)"
    onclick: sets slider value
    Active (matches current): 
      bg-oracle-blue text-white
  
  SIMULATION ROUNDS (mt-4):
  Same pattern: slider 10-40, display "25 ROUNDS"
  Presets: "Fast (10)" | "Standard (25)" | "Deep (40)"
  
  AGENT MIX (mt-4):
  Label: "AGENT MIX" 
  Subtitle: "(sliders are linked, total = 100%)"
    (text-xs oracle-dim)
  
  3 sliders with linked state:
  🏦 Institutional: [slider] 35%
  🐦 Retail: [slider] 50%  
  📰 Media/Analyst: [slider] 15%
  
  Each slider shows its percentage on the right
  Linked logic: adjusting one redistributes 
    remaining % proportionally between the other two
  Total always = 100%
  
  ENVIRONMENT TOGGLES (mt-4):
  Label: "MARKET ENVIRONMENT"
  Toggleable pills (multi-select):
    "🐦 Twitter-like" (default ON) 
    "💬 Reddit-like" (default ON)
    "📺 News-heavy" (default OFF)
  Active: bg-oracle-surface2 border-oracle-blue
  
  LLM MODEL (mt-4):
  Label: "SIMULATION QUALITY"
  3 selection cards:
  
  Each card: bg-oracle-surface2 border rounded-10 
    p-3 cursor-pointer
  Active: border-oracle-blue 
    box-shadow: 0 0 12px rgba(59,130,246,0.2)
  
  Card 1: "GPT-4o"
    Subtitle: "Highest quality"
    Cost: "~$0.12/run" (oracle-dim)
  
  Card 2: "GPT-4o-mini"  
    Subtitle: "Balanced"
    Cost: "~$0.02/run"
  
  Card 3: "Qwen-plus" 
    "⚡ RECOMMENDED" pill (gold, tiny)
    Subtitle: "Best value"
    Cost: "~$0.004/run"
    Default selected
  
  POLYMARKET INTEGRATION (mt-4):
  Flex row: 
    Left: 
      "Polymarket Integration" (13px bold)
      "Inject prediction market data as seed" 
      (text-xs oracle-muted)
    Right: Toggle switch (uses local state, default ON)
  When ON: info box below:
    bg-oracle-surface p-2 rounded-8
    "📊 Injecting: 71% rate hike probability 
    (L5-Polymarket)"

Card 3: LAUNCH BUTTON (mt-4)
  Full width button, height: 56px, 
  border-radius: 12px
  Background: linear-gradient(135deg, 
    #1D4ED8, #3B82F6)
  Border: 1px solid rgba(59,130,246,0.6)
  Box-shadow: 0 0 20px rgba(59,130,246,0.2)
  Text: "🌊 LAUNCH SWARM SIMULATION" 
    (15px, bold, white, letter-spacing: 0.02em)
  
  Hover: 
    Background: linear-gradient(135deg, 
      #2563EB, #60A5FA)
    Box-shadow: 0 0 30px rgba(59,130,246,0.4)
    scale(1.01)
  Active: scale(0.99)
  
  LOADING STATE (when simulation is running):
    Button becomes: bg-oracle-surface2 disabled
    Shows spinner left + 
    "Simulation Running..." text
    Countdown: "~45s remaining"
  
  onClick:
    1. Validate seed is not empty
    2. Set simulationState = 'running'
    3. Start simulation setInterval (every 1800ms):
       - Increment current round
       - Randomly adjust bullish/bearish percentages 
         (small increments, staying realistic)
       - Add new narrative to feed
       - Update agent interaction count
       - When round reaches totalRounds: 
         set simulationState = 'complete'
         trigger final verdict calculation

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LEFT ZONE — RESULTS PANEL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
(Shows after simulation starts. 
Animates in from bottom with framer-motion)

Card 4: LIVE PROGRESS (mt-4)
  AnimatePresence: 
    Shows when simulationState = 'running'
    initial: { opacity: 0, y: 20 }
    animate: { opacity: 1, y: 0 }
  
  Header: 
    "SIMULATION IN PROGRESS" + 
    blue pulsing dot + "RUNNING" pill
  
  Round counter: 
    "ROUND {currentRound} / {totalRounds}"
    Large text, JetBrains Mono
  
  Progress bar:
    height: 8px, border-radius: 999px
    Background: #1E3A5F
    Fill: gradient blue→gold
    Animated width transition: 400ms ease
  
  Stats row (3 items, mt-3):
  Wrapped in framer-motion with stagger
    "Agents Interacted: {count}"
    "Opinions Shifted: {count}"
    "Coalitions Formed: {count}"
    All in JetBrains Mono, oracle-muted, text-sm
  
  Elapsed timer: "01:23 elapsed" (updates live)

Card 5: LIVE CONSENSUS (mt-3)
  Three percentage displays in a row:
  
  Each: flex-col items-center, flex: 1
  
  Large percentage (32px JetBrains Mono, bold):
    BULLISH: oracle-green (animates on change)
    NEUTRAL: oracle-muted
    BEARISH: oracle-red
  
  Values update via the simulation interval
  When value changes: animate with framer-motion
    scale: 1 → 1.1 → 1 (100ms bounce)
  
  Label below: text-xs oracle-dim uppercase
  
  Full-width stacked bar (mt-3, height: 8px):
    3 segments proportional to percentages
    Colors: green | gray | red
    Animated width transitions
  
  Confidence badge (mt-2):
    "Confidence: HIGH" (oracle-gold pill)
    or MEDIUM (oracle-muted) 
    based on dominant % strength

Card 6: NARRATIVE FEED (mt-3)
  Title: "EMERGING NARRATIVES" (12px bold)
  
  ScrollArea (max-height: 200px, 
    overflow-y: auto):
  
  Narrative items added by simulation interval:
  Each item animates in from bottom:
    initial: { opacity: 0, x: -10 }
    animate: { opacity: 1, x: 0 }
  
  Item format:
    Left border (3px): 
      blue=institutional, green=retail, 
      gold=media
    Agent icon (12px) + timestamp + text (13px)
    "14:32 🏦 Institutional agents rotating 
      to defensive positions"

Card 7: ORACLE VERDICT (mt-3)
  AnimatePresence: 
    Only shows when simulationState = 'complete'
    initial: { opacity: 0, scale: 0.95 }
    animate: { opacity: 1, scale: 1 }
    transition: spring, damping: 20
  
  Border: 2px solid oracle-gold
  Background: rgba(245,158,11,0.05)
  border-radius: 12px
  p-4
  
  "⚡ ORACLE VERDICT" (12px, oracle-gold, 
    uppercase, letter-spacing: 0.1em)
  
  Large verdict: 
    "BEARISH" (36px, JetBrains Mono, bold, 
    oracle-red if bearish, oracle-green if bullish)
  
  Prediction text (13px oracle-muted mt-2):
    "Tech sector expected to underperform 
    -3.2% over 5-day horizon"
  
  Stats grid (mt-3, 2×2):
    "Confidence" / "71%" (gold)
    "Key Signal" / "Rate fear" (oracle-muted)
    "Dominant Agent" / "Institutional" (blue)
    "Polymarket Align" / "✓ 71% hike" (green)
  
  3 action buttons (mt-4, flex gap-2):
  "PLACE TRADE" — blue filled
    onClick: openOrderTicket(primarySymbol, 
      verdict === 'BEARISH' ? 'sell' : 'buy')
  "BUILD STRATEGY" — outlined blue
    onClick: navigate('/strategy')
  "SAVE REPORT" — outlined oracle-muted
    onClick: addNotification('success', 
      'Report Saved', 'Swarm report saved to memory')

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RIGHT ZONE — LIVE VISUALIZATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/components/SwarmVizualizer.tsx

This is a React component that renders an 
animated agent network visualization using 
CSS and SVG (no D3 required — pure React).

CONTAINER: 
  Full right zone height, bg: #050810
  border-radius: 12px
  border: 1px solid #1E3A5F
  overflow: hidden
  position: relative

NODES SYSTEM:
  Generate 80 node objects on mount:
  Each node: {
    id, 
    x: random 5-95% of container width,
    y: random 5-95% of container height,
    vx: random velocity (-0.3 to 0.3),
    vy: random velocity (-0.3 to 0.3),
    type: 'institutional'|'retail'|'media',
    size: random 4-12px,
    opinion: 'bull'|'bear'|'neutral',
    influence: random 0.1-1.0
  }
  
  Distribution matches agent mix sliders:
    ~35% institutional (blue)
    ~50% retail (green)
    ~15% media (gold)

ANIMATION LOOP (useEffect + requestAnimationFrame):
  Each frame:
  1. Update node positions: 
     x += vx, y += vy
     Bounce off walls (reverse velocity)
     Add very small random drift each frame
  
  2. Clustering behavior:
     When bullish% is high: 
       institutional nodes drift 
       toward center-right
       retail follows
     When bearish% high:
       nodes spread apart (chaos)
     As rounds progress:
       same-opinion nodes 
       slowly gravitate toward each other
  
  3. Interaction flashes:
     Every 15-30 frames: pick 2 random 
     nearby nodes, briefly flash an 
     edge between them (opacity 0.8 → 0, 
     200ms, colored by agreement/conflict)

RENDERING (SVG full container size):
  Edges layer (rendered first, behind nodes):
    Active interaction edges: 
      thin lines (1px), 
      agreement=blue opacity 0.4, 
      conflict=red opacity 0.4
      Fade in/out over 300ms
    Permanent edges between close nodes:
      very thin (0.5px), opacity 0.1,
      oracle-border color
  
  Nodes layer:
    Each node: SVG circle
    Fill colors:
      institutional: #3B82F6
      retail: #10B981
      media: #F59E0B
    Radius: node.size / 2
    Opacity: 0.7-1.0 based on influence
    Filter: url(#glow) — subtle glow filter
    Pulse animation: 
      transform-origin: center
      @keyframes node-pulse: 
        scale 1→1.15→1, 2-4s, infinite
        Each node has different duration 
        (randomized 2-4s) for organic feel
  
  SVG defs: 
    linearGradient for background
    feGaussianBlur glow filter (stdDeviation: 2)

OVERLAY UI (absolute positioned on top of SVG):
  
  Top-left corner:
    "⬤ LIVE SIMULATION" pulsing badge
      (green dot, 12px, bg-oracle-bg/80 pill)
    "Round {currentRound}/{totalRounds}" 
      (JetBrains Mono, 13px, oracle-muted)
    "847 interactions this round" 
      (text-xs oracle-dim, updates live)
  
  Right side (absolute right: 12px, 
    top 50%, transform: translateY(-50%)):
    Vertical sentiment thermometer:
      Width: 20px
      Height: 180px
      Border: 1px solid oracle-border
      Border-radius: 10px
      Background: linear-gradient(to top, 
        #EF4444 0%, #475569 50%, #10B981 100%)
      
      Indicator line (horizontal, 2px, white):
        Position: {(100-bullishPct)/100 * 180}px 
        from top
        Animated: transition top 800ms ease
      
      Labels:
        "BULL" at top (text-xs oracle-green)
        "BEAR" at bottom (text-xs oracle-red)
        "SENTIMENT" vertical text on left
  
  Bottom (full width, absolute bottom: 12px):
    Timeline scrubber:
      bg-oracle-bg/80 rounded-8 p-2 mx-2
      Horizontal progress track
      Round markers as small dots
      Current round indicator
      "Round X" label follows indicator

Node hover tooltip:
  Shows absolute-positioned card:
  Agent Type + Opinion + Influence
  Triggered by SVG circle onMouseEnter

ON PAGE LOAD:
  Simulation auto-starts with initial state 
  (round 5/40, already partway through)
  Use setTimeout to give the impression 
  it was already running when user arrived

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SIMULATION HISTORY (below two-zone layout)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Title: "SIMULATION HISTORY"
Horizontally scrollable row (flex, overflow-x: auto, 
  gap-3, pb-2):

8 history cards from mockSimulations:
Each card (200px wide, flex-shrink: 0, 
  oracle-card style, p-3, cursor-pointer):
  Date+time (text-xs oracle-dim)
  Seed topic (text-sm bold, truncate, max: 2 lines)
  Verdict pill: 
    BULLISH=green, BEARISH=red, NEUTRAL=gray
  Accuracy badge:
    ✓ CORRECT (green) | ✗ WRONG (red) | 
    PENDING (gray)
  "Confidence: XX%" (text-xs JetBrains Mono)

  hover: border-oracle-blue scale(1.01)
  onClick: loads that simulation's seed 
    into the textarea above
🟣 PROMPT 5 — STRATEGY BUILDER
Objectives 4 (AI Features) + 5 (Portfolio Intelligence)
text

Build the STRATEGY BUILDER page at route "/strategy".
Users describe strategies in plain English, ORACLE 
parses them into structured conditions, then runs 
a simulated backtest with visualized results.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE LAYOUT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Page header (full width)
Row 1 (top, 2-column): Input (60%) + Parsed (40%)
Row 2 (full width, appears after backtest): 
  Backtest Results
Row 3 (full width, collapsible): 
  Trade Log + Strategy Library

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE HEADER
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Title: "🧬 ORACLE STRATEGY BUILDER" (24px bold)
Subtitle: "Describe any strategy in plain English. 
  ORACLE parses, backtests, and deploys it."
Right: "SAVED: 8 strategies" pill

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 1 — INPUT SECTION (60% left column)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card: DESCRIBE YOUR STRATEGY

Textarea (6 rows, oracle-input, 
  font-size: 15px, line-height: 1.7, 
  full width):
  
  Placeholder cycles every 4s 
  (AnimatePresence fade, 
  replace placeholder attribute):
  Phrase 1: "Try: 'Buy NVDA when RSI drops below 30 
    AND MiroFish shows >60% bullish sentiment AND 
    Polymarket gives >70% rate hold probability — 
    sell when RSI hits 70 OR swarm turns bearish'"
  Phrase 2: "Try: 'Rotate into TLT and GLD when 
    the swarm simulation shows >70% bearish 
    consensus on equities AND the yield curve 
    is inverted — exit when sentiment reverses'"
  Phrase 3: "Try: 'Mean revert AAPL when it drops 
    >8% in a week AND retail panic is detected in 
    the swarm — take 50% profit at +5%, 
    remainder at +12%'"

Template pills (4 pills, flex-wrap, mt-3, gap-2):
  Each: h-9 text-sm border rounded-8 
    px-3 cursor-pointer
    hover: bg-oracle-surface2
  
  "🛡️ Defensive Rate-Hike" (gold border)
  onClick: fills textarea with:
    "Reduce tech exposure by 20% when 
    Polymarket shows >65% rate hike 
    AND swarm consensus is >60% bearish. 
    Rotate into TLT and GLD. 
    Reverse when swarm turns bullish 
    OR rate hike probability drops below 45%."
  
  "🚀 Momentum + Sentiment" (blue border)
  "⚖️ Mean Reversion + Swarm" (blue border)
  "🔮 Polymarket Arbitrage" (gold border)
  Each fills textarea with relevant strategy text

Backtest configuration row (mt-4):
  Flex row, gap-4, flex-wrap
  
  Date range:
    "FROM" label + date input 
      (value: "2020-01-01", min: "2018-01-01")
    "TO" label + date input 
      (value: today's date)
    Style: oracle-input h-9 text-sm
  
  Starting capital:
    "$" prefix + number input 
      (value: 100000, step: 10000)
    oracle-input h-9 text-sm w-36
  
  Asset universe:
    Select dropdown:
      "US Stocks" | "Crypto" | "ETFs" | 
      "Mixed Portfolio"
    oracle-input h-9 text-sm

BUILD BUTTON (mt-4):
  Full width, h-14, border-radius: 12px
  Background: linear-gradient(135deg, 
    #1D4ED8, #3B82F6)
  Text: "⚡ BUILD & BACKTEST STRATEGY" 
    (bold, white)
  
  LOADING STATES (shows OracleLoadingScreen 
  component with these sequential messages):
  Phase 1 (0-20%): "🧠 Parsing strategy logic..."
  Phase 2 (20-45%): "🔬 Identifying signal layers..."
  Phase 3 (45-75%): "📊 Running 6-year backtest..."
  Phase 4 (75-95%): "📈 Calculating performance..."
  Phase 5 (95-100%): "✅ Strategy complete!"
  
  Total duration: 3.5 seconds
  After completion: 
    setStrategyBuilt(true)
    setShowResults(true)
    Scroll to results section

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 1 — PARSED STRATEGY (40% right column)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card: STRATEGY PARSED
(Shows after Build is clicked)

AnimatePresence:
  initial: { opacity: 0, x: 20 }
  animate: { opacity: 1, x: 0 }
  
Header: 
  "STRATEGY PARSED" (12px uppercase bold)
  "✓ 3 conditions identified" (green, text-xs)

3 condition boxes (stacked, gap-3):

Box 1 — ENTRY CONDITIONS:
  Left border: 3px solid oracle-green
  bg-oracle-surface2 rounded-10 p-3
  Label: "ENTRY CONDITIONS" 
    (10px oracle-green uppercase)
  
  Each condition row:
  Condition icon (⚡ 12px) + 
  Condition text + 
  LayerBadge pill
  
  Conditions:
  ⚡ "RSI < 30" — L4 badge
  ⚡ "Swarm Bullish > 60%" — L6 badge
  ⚡ "Polymarket Rate Hold > 70%" — L5 badge

Box 2 — EXIT CONDITIONS:
  Left border: 3px solid oracle-red
  bg-oracle-surface2 rounded-10 p-3
  Label: "EXIT CONDITIONS" 
    (10px oracle-red uppercase)
  ⚡ "RSI > 70" — L4 badge
  ⚡ "Swarm turns Bearish" — L6 badge

Box 3 — RISK RULES:
  Left border: 3px solid oracle-gold
  bg-oracle-surface2 rounded-10 p-3
  Label: "RISK MANAGEMENT" 
    (10px oracle-gold uppercase)
  ⚡ "Max Position: 10% portfolio"
  ⚡ "Stop Loss: -5%"
  ⚡ "Max 3 concurrent positions"

Layer activation display (mt-3):
  Label: "LAYERS USED:"
  Flex row of 10 layer badges:
  L4, L5, L6 → highlighted oracle-blue, 
    border-oracle-blue, opacity: 1
  L1, L2, L3, L7, L8, L9, L10 → 
    opacity: 0.3, default styling

Action row (mt-3):
  "✏️ Edit" link (oracle-blue text-sm)
  "Looks good ✓" link (oracle-green text-sm)
    Both do nothing (UI state only)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 2 — BACKTEST RESULTS (full width)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AnimatePresence:
  initial: { opacity: 0, y: 30 }
  animate: { opacity: 1, y: 0 }
  transition: { duration: 0.4, ease: "easeOut" }

Only shows when showResults = true

Header: "BACKTEST RESULTS" + 
  "Jan 2020 — Jun 2026 (6.5 years)" pill

Two sub-columns: Left 62% chart, Right 38% stats

LEFT — EQUITY CURVE:
  Recharts ComposedChart, height: 300px
  
  Data: mockEquityCurve (252 points 
    for 1Y, or generate 6-year mock)
  
  Three lines:
  1. "ORACLE Strategy" — Area with gradient fill
     Line: #3B82F6 solid 2px
     Fill: gradient #3B82F6 20%→transparent
     animationDuration: 1500ms (draws left to right)
  
  2. "SPY Benchmark" — Line only
     Stroke: #F59E0B dashed 
     strokeDasharray: "6 3"
     animationDuration: 1500ms
  
  3. "Buy & Hold" — Line only
     Stroke: #475569 dashed
     strokeDasharray: "3 3"
     animationDuration: 1500ms
  
  Custom tooltip (dark card):
    Date | ORACLE: $X | SPY: $X | Diff: +$X

  Chart annotations (ReferenceLine or custom):
    "📊 Earnings" (green arrow at specific date)
    "🔴 Rate Hike" (red arrow)
    "🌊 Swarm Signal" (blue diamond)

  Below main chart: 
    Bar chart (height: 50px, no padding):
      Trade frequency over time
      Bar fill: oracle-blue opacity 0.6

  Legend row:
    "─ ORACLE (+287%)" blue dot
    "- - SPY (+142%)" gold dot
    ".. Buy&Hold" gray dot

RIGHT — PERFORMANCE STATS:
  Stacked cards/rows:
  
  HERO METRIC (large):
    "TOTAL RETURN" (10px oracle-dim)
    "+287.4%" (32px JetBrains Mono bold oracle-green)
    "vs SPY: +142.1%" (oracle-gold 13px)
  
  2-column grid of stats (mt-3):
  Each stat: bg-oracle-surface2 rounded-10 p-3
    Label (10px oracle-dim uppercase)
    Value (18px JetBrains Mono bold)
  
  "SHARPE RATIO" / "2.14" (green)
  "SORTINO RATIO" / "3.07" (green)
  "WIN RATE" / "67.3%" (green)
  "PROFIT FACTOR" / "2.89" (green)
  "MAX DRAWDOWN" / "-8.3%" (red)
  "AVG HOLD" / "12 days" (muted)
  "TOTAL TRADES" / "156" (muted)
  "SWARMS USED" / "89" (blue)
  
  SIGNAL CONTRIBUTION (mt-4):
    Title: "SIGNAL ATTRIBUTION" (12px bold)
    4 bar rows:
    Each: label + horizontal bar + percentage
    
    L6 Swarm Engine: [████████░░] 42% — teal
    L5 Polymarket: [█████░░░░░] 28% — gold
    L4 Technical: [████░░░░░░] 22% — blue
    L3 News NLP: [██░░░░░░░░] 8% — purple
    
    Bars animate width on scroll into view

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 3 — TRADE LOG + DEPLOYMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card: BACKTEST TRADE LOG (collapsible)
  Header with toggle: 
    "BACKTEST TRADE LOG" + "(156 trades)"
    Chevron icon rotates on collapse
  
  When expanded:
  Table (full width):
    Columns (smaller text for all):
    DATE | ASSET | ACTION | ENTRY | 
    EXIT | RETURN | SWARM | REASONING
    
    10 rows from mock data:
    Row color: 
      Profitable: left border oracle-green
      Loss: left border oracle-red
    
    RETURN column: JetBrains Mono, 
      green/red based on value
    SWARM column: "72% Bull" or "58% Bear" 
      in small oracle-muted text
    REASONING column: 
      "View →" link in oracle-blue
      onClick: opens modal with full reasoning
    
    Reasoning Modal:
      Title: "TRADE REASONING — [Date]"
      Sections:
        Signal Inputs (each layer's contribution)
        Risk Assessment
        Entry/Exit logic
        ORACLE Commentary

  "Load more trades" button below table

DEPLOYMENT BAR (sticky bottom of card):
  bg-oracle-bg border-top oracle-border p-3
  Flex row, gap-3:
  
  "💾 SAVE STRATEGY" — outlined gray
    onClick: shows inline form for name + tags
    On save: adds notification "Strategy saved"
  
  "📤 EXPORT" — outlined gray
    onClick: dropdown:
      "Export as JSON"
      "Export as PDF Report" (window.print())
      "Copy Share Link"
  
  "🤖 DEPLOY TO AUTOPILOT" — gold gradient PROMINENT
    onClick: opens confirmation modal:
      Title: "Deploy to Autopilot?"
      Body: strategy name + summary
      "Paper Trading Mode: ON" toggle
      "Require confirmation: ON" toggle
      Buttons: [Cancel] [Deploy Now ▶]
      On Deploy: 
        setAutopilotActive(true) in context
        addNotification('success', 
          'Strategy Deployed',
          'ORACLE Momentum Strategy is now live')
        navigate to War Room

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ROW 4 — STRATEGY LIBRARY (collapsible)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Header: "STRATEGY LIBRARY" + chevron toggle

When expanded:
3-column grid of cards from mockStrategies:
Each card: oracle-card p-4 cursor-pointer
  hover: border-oracle-blue translateY(-2px)
  
  Name (14px bold)
  Description (12px oracle-muted, 2 lines max)
  Performance: "+287% (2020-2026)" 
    (13px oracle-green JetBrains Mono)
  "Sharpe: 2.14" (oracle-gold text-xs)
  Status pill: LIVE (pulsing green) | 
    SAVED (gray) | BACKTESTED (blue)
  
  Footer: 3 icon buttons
    ▶ Run (navigates and fills strategy)
    ✏️ Edit
    🗑️ Delete (confirm dialog)
🟣 PROMPT 6 — MEMORY & LEARNING SCREEN
Objectives 4 (AI) + 5 (Portfolio Intelligence)
text

Build the MEMORY & LEARNING page at route "/memory".
This screen shows ORACLE's persistent knowledge 
graph, investor DNA profile, and learning log.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE LAYOUT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Page header (full width)
Stats pills row (full width)
3-column grid:
  Column 1 (30%): Investor DNA + Behavioral Analytics
  Column 2 (42%): Knowledge Graph Visualization
  Column 3 (28%): Accuracy Tracker + Learning Log
Full-width timeline (bottom)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PAGE HEADER
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Title: "🧠 ORACLE MEMORY" (24px bold)
Subtitle: "ORACLE learns from every simulation, 
  trade, and interaction. Here's what it knows."

Stats pills row (flex, gap-3, mt-3, flex-wrap):
  "MEMORY NODES: 847" — blue pill
  "LESSONS LEARNED: 47" — gold pill
  "GRAPH EDGES: 2,341" — purple pill
  "MEMORY AGE: 3 months" — gray pill

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COLUMN 1 — INVESTOR DNA + BEHAVIORAL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card 1: YOUR INVESTOR DNA

Title: "YOUR INVESTOR DNA"
Subtitle: "(Revealed through behavior, not surveys)"
  (text-xs oracle-muted italic)

RadarChart (Recharts, height: 220px):
  6 axes: 
    Risk Appetite | Patience | Conviction | 
    Diversification | Momentum Bias | 
    Macro Awareness
  
  Two datasets:
  
  1. "Actual Behavior" (blue, 
     fillOpacity: 0.25, 
     stroke: #3B82F6):
     Values: [72, 45, 78, 55, 68, 82]
  
  2. "Stated Preferences" (gold dashed, 
     fillOpacity: 0.1, 
     stroke: #F59E0B, 
     strokeDasharray: "4 2"):
     Values: [85, 60, 80, 65, 75, 70]
  
  PolarGrid: stroke #1E3A5F
  PolarAngleAxis: 
    tick: { fill: '#94A3B8', fontSize: 11 }
  
  Legend below: 
    "● Actual" (blue) | "● Stated" (gold)
  
  animationBegin: 200, animationDuration: 800

3 insight cards below chart (mt-3, gap-2):
Each card: p-3 rounded-10 oracle-input/50
  border-l-4 + flex gap-3

Card 1 (amber left border):
  "⚠️" icon
  "Early Exit Pattern" (13px bold)
  "You've sold winning positions early 3 times. 
  Exit targets auto-adjusted +15%." 
  (text-xs oracle-muted)

Card 2 (green left border):
  "✓" icon
  "Strong Contrarian Instinct" (13px bold)
  "Best trades came against retail panic. 
  Swarm contrarian signals flagged." (text-xs)

Card 3 (blue left border):
  "🔵" icon
  "Macro Awareness: HIGH" (13px bold)
  "L2 macro signals weighted +20% for 
  your profile." (text-xs)

Card 2: BEHAVIORAL ANALYTICS (mt-4)
Title: "BEHAVIORAL ANALYTICS"

4 metric rows:
Each row: label + progress bar + insight text

ROW 1:
  "Avg Hold Time" bold
  Progress bar: 67% (12 days / optimal 18)
  "12 days avg (optimal: 18 days)" oracle-muted text-xs
  Bar color: oracle-amber (suboptimal)

ROW 2:
  "Revealed Risk Tolerance"
  Progress bar: 50% 
  "Actual: MODERATE | Stated: Aggressive"
  oracle-muted text-xs

ROW 3:
  "Best Signal Combo"
  "Swarm + Polymarket" in oracle-blue bold
  "74% accuracy" in oracle-green text-xs

ROW 4:
  "Worst Context"
  "Macro-only, no sentiment" oracle-red
  "43% accuracy" oracle-red text-xs

Card 3: HOW ORACLE ADAPTS (mt-4)
Title: "ACTIVE PERSONALIZATIONS"

5 rows with green checkmark:
Each: ✓ (oracle-green) + text (13px oracle-muted)

✓ "Exit targets +15% (early exit pattern)"
✓ "L2 macro signals weighted +20%"
✓ "Tech sector alerts prioritized"  
✓ "Swarm contrarian signals highlighted"
✓ "Max 12% per position (behavior-based)"

"Reset personalizations" link 
  (text-xs oracle-dim mt-2, underline)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COLUMN 2 — KNOWLEDGE GRAPH
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card: Full column height, 
  bg-oracle-bg border-oracle-border rounded-12

Header (p-3 border-b oracle-border):
  "ORACLE KNOWLEDGE GRAPH" (12px bold)
  "847 nodes · 2,341 relationships" (text-xs oracle-muted)

GRAPH VISUALIZATION:
  Create src/components/KnowledgeGraph.tsx
  
  Pure CSS + SVG animated graph 
  (same approach as Swarm Visualizer)
  
  60 nodes, 5 categories:
  
  NODE DEFINITIONS (generate on mount):
  
  Assets (15 nodes, circles, #3B82F6):
    NVDA, AAPL, MSFT, SPY, QQQ, 
    TLT, GLD, AMZN, TSLA, META,
    BTC, ETH, VIX, DXY, OIL
  
  Events (12 nodes, diamonds, #F59E0B):
    "Fed Meeting Jun'26", "CPI Print", 
    "NVDA Earnings", "Rate Decision", 
    "Jobs Report", "PCE Data",
    "FOMC Minutes", "NFP", 
    "GDP Q1", "PPI", "PMI", "ISM"
  
  Strategies (6 nodes, hexagons, #10B981):
    "Rate Defense", "Momentum+Swarm", 
    "Mean Reversion", "Poly Arb",
    "Macro Hedge", "Earnings Play"
  
  Risk Factors (8 nodes, triangles, #EF4444):
    "Yield Inversion", "VIX Spike",
    "Dollar Strength", "Credit Spread",
    "Recession Risk", "Inflation",
    "Liquidity", "Correlation Break"
  
  Simulations (10+ nodes, stars, #8B5CF6):
    Past swarm simulation results
  
  RENDERING:
  SVG full container
  Each node type uses different shape paths:
    Circle (asset): standard SVG circle
    Diamond (event): polygon rotated 45°
    Hexagon (strategy): 6-point polygon
    Triangle (risk): 3-point polygon
    Star (simulation): star polygon
  
  EDGES:
  Solid lines between related nodes
  Thicker lines (2px) for strong relationships
  Very low opacity (0.15) to avoid clutter
  
  ANIMATION:
  Gentle floating using same requestAnimationFrame 
  loop as Swarm Visualizer
  Slower velocities (0.1-0.2 max)
  
  INTERACTION:
  hover node → 
    Node glows (filter: brightness(2))
    Connected nodes highlight (opacity 1)
    Unconnected nodes dim (opacity 0.15)
    Tooltip shows: name + type + connection count
  
  click node →
    Opens node detail side panel

CONTROLS BAR (below graph, border-t, p-2):
  Filter pills (flex, gap-1, flex-wrap):
    [All ✓] [Assets] [Events] [Strategies] 
    [Risk Factors] [Simulations]
    Each click: toggles visibility of that 
    node category
    Active: bg-oracle-blue, inactive: outlined
  
  Search input (mt-2):
    "🔍 Search nodes..." 
    As user types: highlight matching nodes, 
    dim all others

NODE DETAIL PANEL (slides from right, 
  inside graph card, 260px wide):
  Shows when node clicked
  
  Node name (16px bold)
  Type badge (colored by category)
  
  Stats:
  "Connected to: X nodes"
  "Last updated: 2h ago"
  "Portfolio impact: HIGH/MED/LOW"
  
  Connections list (scrollable):
    Each connection: 
      Connected node name + relationship type
  
  Close button (top right)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COLUMN 3 — ACCURACY + LEARNING LOG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card 1: PREDICTION ACCURACY

Donut chart (Recharts PieChart, 
  height: 180px, center: 90px from top):
  
  Two segments:
  Gold segment: 71% (oracle-gold, 
    fill: #F59E0B)
  Gray segment: 29% (fill: #1E3A5F)
  InnerRadius: 55, OuterRadius: 75
  
  Center label (absolute positioned over chart):
    "71%" (28px JetBrains Mono bold oracle-gold)
    "accuracy" (11px oracle-muted)
  
  animationBegin: 300, animationDuration: 1000

Breakdown table (mt-3):
  Headers: Signal Combo | Accuracy | Count
  5 rows from data:
  
  Each row: accuracy shown as 
    text-colored percentage + small horizontal bar
    (width proportional to accuracy%)
  
  "Swarm + Poly" | 74% 🟢 | 18
  "Swarm + Tech" | 71% 🟢 | 12
  "Swarm + Macro" | 67% 🟡 | 9
  "Tech Only" | 58% 🟡 | 5
  "Macro Only" | 43% 🔴 | 3

Accuracy trend chart (mt-3):
  Recharts LineChart, height: 80px
  No axes labels (clean)
  Grid: none
  Line: oracle-gold, strokeWidth: 2
  10 data points (past 10 simulations)
  Gentle upward trend
  Title above: 
    "ORACLE IS GETTING SMARTER ↑" 
    (10px oracle-gold uppercase)

Card 2: LESSONS LEARNED (mt-4, flex-col flex-1)

Header row:
  "LESSONS LEARNED" + "47 total" pill
  
Search input (mt-2):
  "🔍 Search lessons..." oracle-input h-9

Scrollable list (max-h: 380px overflow-y: auto):
  AnimatePresence for list items

8 lesson cards from mockLessons:
Each card:
  oracle-card p-3 rounded-10 mt-2
  border-l-4 border-oracle-gold
  
  hover: 
    translateY(-1px)
    box-shadow: 0 4px 20px rgba(59,130,246,0.1)
  
  Top row:
    "📚 Lesson #{id}" (11px bold oracle-muted)
    Confidence dots "●●●●○" (oracle-gold, text-xs)
    "{time} ago" (oracle-dim text-xs ml-auto)
  
  Lesson text (mt-1, 12px italic oracle-muted, 
    line-height: 1.5, max 2 lines):
  
  Tags row (mt-2, flex gap-1 flex-wrap):
    Each tag: bg-oracle-surface2 text-oracle-blue 
    text-xs px-2 py-0.5 rounded-full
    "#polymarket" "#rate-hike" etc.

Card 3: MEMORY HEALTH (mt-4)

Title: "MEMORY HEALTH"

4 status rows:
🟢 "Graph Integrity: OPTIMAL" / 
    "0 conflicting nodes" (oracle-muted text-xs)
🟢 "Data Freshness: LIVE" / 
    "Last sync: 2 seconds ago"
🟡 "Coverage: 42%" / 
    Progress bar (oracle-gold, 42% fill) /
    "847 / 2000 target nodes"
🔵 "Learning Rate: +3.2/week" / 
    Tiny upward arrow

3 action buttons (mt-3, flex gap-2):
  "🔄 Force Sync" 
  "📤 Export Memory"
  "🗑️ Reset" (text-red-400, 
    onClick: confirm dialog)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FULL WIDTH BOTTOM — MEMORY TIMELINE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Card: ORACLE MEMORY TIMELINE

Horizontally scrollable timeline:
  bg-oracle-bg, border-oracle-border, 
  rounded-12, p-4

Inner: 
  Relative positioned container, 
  overflow-x: auto, 
  min-width: 100%

Central horizontal line:
  position: absolute, top: 50%, 
  width: 100%, height: 1px, 
  background: oracle-border

Event dots (position: absolute along timeline):
  Each: 12px circle, centered on the line
  
  Types + colors:
  🔵 Blue = simulation run
  🟢 Green = profitable trade
  🔴 Red = loss/correction
  🟡 Gold = lesson learned
  🟣 Purple = strategy deployed
  
  20+ events distributed over 90 days
  
  On hover: 
    dot scales to 20px
    Tooltip card floats above/below line:
      Event type icon + date + description
  
  Date labels below timeline:
    Every 2 weeks: date label
  
  Current moment indicator:
    Glowing white vertical line at right
    "NOW" label above it

X-axis: "3 months ago" → "today"
Overflow: horizontal scroll with 
  overflow-x: auto
  scrollbar styled with oracle scrollbar CSS
🟣 PROMPT 7 — AUTOPILOT + AGENTIC AI + TRANSPARENCY FEED
Objective 6: Agentic AI Trading Agent (/5)
text

Build the Autopilot system, Agentic AI trading 
engine, Transparency Feed, and Voice Command 
experience for ORACLE. This is the agentic layer 
that connects all screens.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART A — AUTOPILOT ACTIVATION MODAL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/components/AutopilotModal.tsx

Appears when AutopilotContext.isActive is set 
to true for the first time (first activation).

Full-screen overlay: 
  rgba(5,8,16,0.95), z-index: 1000

Central card: 520px wide, oracle-card, 
  p-8, border-radius: 16px
  border: 1px solid rgba(245,158,11,0.3)
  box-shadow: 0 0 60px rgba(245,158,11,0.1)

ANIMATION (framer-motion):
  initial: { opacity: 0, scale: 0.9 }
  animate: { opacity: 1, scale: 1 }
  transition: { type: "spring", damping: 20 }

CONTENT:

Large robot icon ring animation:
  Center: "🤖" (48px)
  Surrounding ring: SVG circle
    stroke: oracle-gold
    strokeWidth: 2
    strokeDasharray: 251 (full circumference)
    @keyframes spin-ring:
      strokeDashoffset: 251→0 (draws in)
      then rotates continuously
  Second ring: larger, lower opacity, 
    counter-rotating

Title: "ACTIVATE ORACLE AUTOPILOT" 
  (22px bold, gradient blue→gold)

Warning text (text-sm oracle-muted mt-3, 
  text-center, max-w: 380px mx-auto):
  "ORACLE will monitor all 10 intelligence 
  layers and execute trades autonomously. 
  Every decision is logged to the 
  Transparency Feed with full reasoning."

Config section (mt-6):

3 toggle rows:
Each: flex justify-between items-center py-3 
  border-b oracle-border

Row 1:
  Left: 
    "📄 Paper Trading Mode" (14px bold)
    "No real money used (recommended)" 
      (12px oracle-muted)
  Right: Toggle switch (default ON, locked ON 
    for demo — show tooltip on hover: 
    "Live trading disabled in demo")

Row 2:
  Left:
    "⚠️ Confirm Large Trades" (14px bold)
    "Require confirmation for orders >$5,000"
  Right: Toggle switch (default ON)

Row 3:
  Left:
    "📊 Max Daily Trades" (14px bold)
    "Limit autonomous executions per day"
  Right: 
    Number spinner: [−] [5] [+]
    (min: 1, max: 20, step: 1)

Buttons (mt-8, flex gap-3):
  "Cancel" (outlined oracle-muted flex-1 h-12)
    onClick: autopilotContext.deactivate()
    Closes modal
  
  "ACTIVATE AUTOPILOT ▶" 
    (gold gradient flex-1 h-12 text-base bold)
    Background: linear-gradient(135deg, 
      #92400E, #F59E0B)
    Box-shadow: 0 0 20px rgba(245,158,11,0.3)
    
    onClick:
      Store config in AutopilotContext
      Close modal
      Add notification: 
        type: 'action'
        "⚡ ORACLE Autopilot is now active"
        "Monitoring 10 intelligence layers..."
      Show top bar LIVE badge
      Expand right transparency panel
      Start autopilot feed interval

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PART B — AGENTIC ENGINE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Create src/services/agenticEngine.ts

This service runs when Autopilot is active.
It simulates the 10-layer monitoring loop 
and can trigger real Alpaca orders.

The engine runs a cycle every 45 seconds:

CYCLE FUNCTION: runAgentCycle()

Step 1 — Market Data (L1):
  If Alpaca connected: 
    call getMultipleLatestBars(['NVDA','AAPL','SPY'])
    Calculate price changes
  Add feed entry: 
    "📡 L1: Market data synced — 
    {X} assets updated"

Step 2 — Macro Check (L2):
  Random selection from mock macro signals
  Add feed entry:
    "📊 L2: Macro signal — 
    [signal description]"

Step 3 — News Check (L3):
  Random selection from mock news items
  Add feed entry:
    "📰 L3: [headline] — 
    Sentiment: BEARISH/BULLISH"

Step 4 — Technical Analysis (L4):
  If Alpaca connected: use real price data
  Calculate mock RSI (random 20-80 range):
  If RSI < 30: add "oversold" signal
  If RSI > 70: add "overbought" signal
  Add feed entry:
    "📈 L4: [symbol] RSI=[value] — 
    [interpretation]"

Step 5 — Polymarket (L5):
  Use fixed mock: "Rate hike: 71%"
  Add feed entry:
    "🎲 L5: Polymarket — Rate hike 
    71% probability injected"

Step 6 — Swarm (L6):
  Generate new swarm result 
  (random within ±5% of last result):
  Add feed entry:
    "🌊 L6: Swarm complete — 
    {bullish}% bullish consensus 
    ({agents} agents)"

Step 7 — Agent Debate (L7):
  Add feed entry (pick from mock debate quotes):
    "🤖 L7 Bull: [argument]"
    "🤖 L7 Bear: [counter-argument]"
  
  Mock bull arguments:
    "Earnings momentum still intact"
    "RSI oversold — bounce expected"
    "Institutional accumulation detected"
  
  Mock bear arguments:
    "Yield curve inversion deepening"
    "Rate hike risk elevated: 71%"
    "Retail panic consistent with tops"

Step 8 — Risk Scoring (L8):
  Aggregate signals from above
  Calculate riskLevel: 
    'LOW' | 'MODERATE' | 'ELEVATED' | 'HIGH'
  Add feed entry:
    "⚖️ L8: Portfolio risk — {riskLevel}
    on tech sector"

Step 9 — Memory Check (L9):
  Find relevant lesson from mockLessons
  Add feed entry:
    "📚 L9: Recall Lesson #{id}: 
    {short lesson summary}"

Step 10 — Decision (L10):
  IF swarm bearish > 65% AND 
     risk is ELEVATED or HIGH AND 
     autopilot.paperTradingMode:
    
    Generate trade recommendation:
    symbol = "NVDA" (largest position)
    action = 'sell'
    qty = "5"
    
    Add feed entry:
      "⚡ L10: Recommendation — 
      REDUCE {symbol} by 8%"
    
    IF autopilot.requireConfirmation AND 
       estimatedValue > 5000:
      
      Show trade confirmation toast:
        "ORACLE recommends: 
        SELL 5 NVDA @ Market"
        Buttons: [Confirm] [Skip]
        Auto-confirms after 8 seconds
        unless user cancels
    
    ELSE:
      Execute automatically:
      Call placeOrder({
        symbol: "NVDA",
        qty: "5",
        side: "sell",
        type: "market",
        time_in_force: "day"
      })
      
      On success:
        Add feed entry:
          "✅ EXECUTED: SELL 5 NVDA 
          @ Market — Order {id}"
        Add notification:
          type: 'trade'
          "✅ Autopilot Executed Trade"
          "SELL 5 NVDA — paper trade"
        Refresh positions in context

  
