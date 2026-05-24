# daily-learning-app
git clone https://github.com/abrawrkhan71/daily-learning-app.git
import { useState, useEffect } from "react";

const lessons = [
  {
    id: 1,
    category: "Valuation",
    tag: "FINANCE",
    title: "EBITDA",
    subtitle: "Earnings Before Interest, Taxes, Depreciation & Amortization",
    body: "EBITDA strips away financing decisions, accounting choices, and tax environments to show raw operating profitability. It's the closest proxy to cash a business generates from its core operations — and why investors use it to compare companies across industries and capital structures.",
    formula: "Net Income + Interest + Taxes + D&A = EBITDA",
    example: "A company earns $2M net income, pays $500K interest, $300K taxes, and has $200K D&A → EBITDA = $3M",
    insight: "EV/EBITDA multiples of 6–10× are common in mature industries; 15–25× signals high growth expectations.",
    color: "#00FF87",
  },
  {
    id: 2,
    category: "Markets",
    tag: "MACRO",
    title: "Yield Curve",
    subtitle: "The Shape That Predicts Recessions",
    body: "The yield curve plots interest rates across maturities (3-month to 30-year Treasuries). Normally it slopes upward — longer = riskier = higher yield. When short-term rates exceed long-term, the curve 'inverts.' Every U.S. recession since 1955 has been preceded by an inverted yield curve.",
    formula: "Spread = 10-Year Treasury Yield − 2-Year Treasury Yield",
    example: "If 2-year yields 5.2% and 10-year yields 4.8%, the spread is −0.4% (inverted) — a recession signal.",
    insight: "The curve doesn't predict timing well — recessions typically follow inversion by 6–24 months.",
    color: "#FFD700",
  },
  {
    id: 3,
    category: "Accounting",
    tag: "FUNDAMENTALS",
    title: "Free Cash Flow",
    subtitle: "The Real Measure of Company Health",
    body: "FCF is what's left after a company pays for operations and capital expenditures. Unlike net income, it can't be easily manipulated with accounting. Warren Buffett calls it 'owner earnings' — it's the actual cash available to grow the business, pay dividends, buy back stock, or reduce debt.",
    formula: "FCF = Operating Cash Flow − Capital Expenditures",
    example: "Operating CF = $10M, CapEx = $3M → FCF = $7M. This $7M is truly 'free.'",
    insight: "A company can show positive net income but negative FCF — a red flag often hiding in footnotes.",
    color: "#FF6B6B",
  },
  {
    id: 4,
    category: "Risk",
    tag: "PORTFOLIO",
    title: "Sharpe Ratio",
    subtitle: "Return Per Unit of Risk",
    body: "The Sharpe Ratio tells you how much excess return you're earning for each unit of volatility you're absorbing. A higher ratio means better risk-adjusted performance. It's the foundational metric for comparing investments that have different risk profiles.",
    formula: "(Portfolio Return − Risk-Free Rate) ÷ Standard Deviation",
    example: "Fund returns 12%, risk-free rate is 4%, std dev is 10% → Sharpe = (12−4)/10 = 0.8",
    insight: "Below 1 is acceptable, 1–2 is good, above 2 is excellent. Anything above 3 warrants deep skepticism.",
    color: "#A78BFA",
  },
  {
    id: 5,
    category: "Debt",
    tag: "LEVERAGE",
    title: "Debt-to-EBITDA",
    subtitle: "How Long to Pay Off All Debt",
    body: "Debt/EBITDA measures how many years of operating earnings it would take to retire all debt, assuming every dollar goes to repayment. Lenders use this as a covenant benchmark. Private equity firms watch it obsessively when structuring leveraged buyouts.",
    formula: "Total Debt ÷ EBITDA = Years to Repay",
    example: "Total debt = $15M, EBITDA = $5M → 3× leverage. Most lenders get nervous above 4–5×.",
    insight: "During the 2008 crisis, many companies had 8–12× leverage. At 5×, one bad quarter becomes existential.",
    color: "#38BDF8",
  },
  {
    id: 6,
    category: "Psychology",
    tag: "BEHAVIORAL",
    title: "Loss Aversion",
    subtitle: "Why Losses Hurt Twice as Much as Gains Feel Good",
    body: "Kahneman & Tversky proved that humans feel the pain of a $1,000 loss roughly twice as intensely as the pleasure of a $1,000 gain. This asymmetry causes investors to hold losers too long (avoiding realizing the loss) and sell winners too early — the exact opposite of optimal behavior.",
    formula: "Pain of Loss ≈ 2× Joy of Equivalent Gain",
    example: "You hold a stock down 40% hoping to 'break even,' while selling a stock up 15% to 'lock in gains.'",
    insight: "The antidote: pre-commit to rules. 'I sell at −20% or +50%' removes emotion from the decision.",
    color: "#FB923C",
  },
  {
    id: 7,
    category: "Real Assets",
    tag: "ALTERNATIVE",
    title: "Cap Rate",
    subtitle: "The Core Metric of Real Estate Valuation",
    body: "The Capitalization Rate tells you the unlevered yield of a property — what you'd earn if you bought it in cash. It's how real estate investors quickly assess and compare properties without getting distracted by financing. A higher cap rate = more income relative to price (but often higher risk).",
    formula: "Cap Rate = Net Operating Income ÷ Property Value",
    example: "NOI = $80,000/year, Property = $1,000,000 → Cap Rate = 8%. You earn 8% unlevered.",
    insight: "Class A urban multifamily might trade at 4–5% cap rates; Class C suburban at 7–9% — priced for risk.",
    color: "#34D399",
  },
];

const categoryColors = {
  Valuation: "#00FF87",
  Markets: "#FFD700",
  Accounting: "#FF6B6B",
  Risk: "#A78BFA",
  Debt: "#38BDF8",
  Psychology: "#FB923C",
  "Real Assets": "#34D399",
};

export default function DailyLearn() {
  const todayIndex = new Date().getDate() % lessons.length;
  const [current, setCurrent] = useState(todayIndex);
  const [revealed, setRevealed] = useState(false);
  const [viewed, setViewed] = useState(new Set([todayIndex]));

  const lesson = lessons[current];
  const color = lesson.color;

  useEffect(() => {
    setRevealed(false);
    setTimeout(() => setRevealed(true), 80);
  }, [current]);

  const go = (dir) => {
    const next = (current + dir + lessons.length) % lessons.length;
    setCurrent(next);
    setViewed((v) => new Set([...v, next]));
  };

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0A0A0F",
      fontFamily: "'Georgia', 'Times New Roman', serif",
      color: "#E8E4DC",
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
      padding: "40px 20px",
      position: "relative",
      overflow: "hidden",
    }}>
      {/* Background grid */}
      <div style={{
        position: "fixed", inset: 0, zIndex: 0,
        backgroundImage: `linear-gradient(rgba(255,255,255,0.02) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px)`,
        backgroundSize: "60px 60px",
        pointerEvents: "none",
      }} />

      {/* Glow behind card */}
      <div style={{
        position: "fixed",
        top: "30%", left: "50%",
        transform: "translate(-50%, -50%)",
        width: 600, height: 600,
        borderRadius: "50%",
        background: `radial-gradient(circle, ${color}18 0%, transparent 70%)`,
        transition: "background 0.8s ease",
        pointerEvents: "none",
        zIndex: 0,
      }} />

      <div style={{ position: "relative", zIndex: 1, width: "100%", maxWidth: 680 }}>

        {/* Header */}
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 40 }}>
          <div>
            <div style={{ fontSize: 11, letterSpacing: 4, color: "#555", textTransform: "uppercase", fontFamily: "monospace" }}>
              Daily Briefing
            </div>
            <div style={{ fontSize: 22, fontWeight: "normal", color: "#E8E4DC", marginTop: 4 }}>
              Finance & Investing
            </div>
          </div>
          <div style={{
            fontFamily: "monospace", fontSize: 11, color: "#444", textAlign: "right", lineHeight: 1.8
          }}>
            <div>{new Date().toLocaleDateString("en-US", { weekday: "long" }).toUpperCase()}</div>
            <div style={{ color: color }}>{new Date().toLocaleDateString("en-US", { month: "short", day: "numeric", year: "numeric" })}</div>
          </div>
        </div>

        {/* Lesson selector dots */}
        <div style={{ display: "flex", gap: 8, marginBottom: 32, flexWrap: "wrap" }}>
          {lessons.map((l, i) => (
            <button
              key={i}
              onClick={() => { setCurrent(i); setViewed(v => new Set([...v, i])); }}
              title={l.title}
              style={{
                width: 10, height: 10,
                borderRadius: "50%",
                border: "none",
                background: i === current
                  ? categoryColors[l.category]
                  : viewed.has(i) ? "#333" : "#222",
                cursor: "pointer",
                transition: "all 0.3s",
                transform: i === current ? "scale(1.5)" : "scale(1)",
                outline: "none",
              }}
            />
          ))}
        </div>

        {/* Main Card */}
        <div style={{
          background: "#111118",
          border: `1px solid ${color}33`,
          borderRadius: 2,
          padding: "40px",
          opacity: revealed ? 1 : 0,
          transform: revealed ? "translateY(0)" : "translateY(12px)",
          transition: "opacity 0.4s ease, transform 0.4s ease",
          boxShadow: `0 0 60px ${color}0A, inset 0 1px 0 ${color}22`,
        }}>

          {/* Tag + category */}
          <div style={{ display: "flex", gap: 12, marginBottom: 24, alignItems: "center" }}>
            <span style={{
              background: color,
              color: "#000",
              fontSize: 9,
              fontFamily: "monospace",
              letterSpacing: 3,
              padding: "4px 10px",
              fontWeight: "bold",
            }}>
              {lesson.tag}
            </span>
            <span style={{ fontSize: 11, color: "#555", fontFamily: "monospace", letterSpacing: 2 }}>
              {lesson.category.toUpperCase()}
            </span>
            <span style={{ marginLeft: "auto", fontSize: 11, color: "#333", fontFamily: "monospace" }}>
              {current + 1} / {lessons.length}
            </span>
          </div>

          {/* Title block */}
          <div style={{ borderLeft: `3px solid ${color}`, paddingLeft: 20, marginBottom: 32 }}>
            <h1 style={{
              fontSize: 42,
              margin: 0,
              fontWeight: "normal",
              letterSpacing: -1,
              lineHeight: 1,
              color: "#F5F0E8",
            }}>
              {lesson.title}
            </h1>
            <p style={{
              margin: "8px 0 0",
              fontSize: 14,
              color: "#666",
              fontFamily: "'Georgia', serif",
              fontStyle: "italic",
            }}>
              {lesson.subtitle}
            </p>
          </div>

          {/* Body */}
          <p style={{
            fontSize: 16,
            lineHeight: 1.85,
            color: "#C8C4BC",
            margin: "0 0 36px",
            fontFamily: "'Georgia', serif",
          }}>
            {lesson.body}
          </p>

          {/* Formula */}
          <div style={{
            background: "#0D0D14",
            border: `1px solid ${color}44`,
            borderRadius: 1,
            padding: "18px 24px",
            marginBottom: 20,
            fontFamily: "monospace",
          }}>
            <div style={{ fontSize: 9, color: "#444", letterSpacing: 3, marginBottom: 10, textTransform: "uppercase" }}>
              Formula
            </div>
            <div style={{ fontSize: 14, color: color, letterSpacing: 1 }}>
              {lesson.formula}
            </div>
          </div>

          {/* Example */}
          <div style={{
            background: "#0D0D14",
            border: "1px solid #222",
            borderRadius: 1,
            padding: "18px 24px",
            marginBottom: 20,
          }}>
            <div style={{ fontSize: 9, color: "#444", fontFamily: "monospace", letterSpacing: 3, marginBottom: 10, textTransform: "uppercase" }}>
              Example
            </div>
            <div style={{ fontSize: 14, color: "#888", lineHeight: 1.7 }}>
              {lesson.example}
            </div>
          </div>

          {/* Insight */}
          <div style={{
            display: "flex",
            gap: 16,
            alignItems: "flex-start",
            padding: "18px 0 0",
            borderTop: "1px solid #1a1a22",
          }}>
            <span style={{ color: color, fontSize: 18, marginTop: 1, flexShrink: 0 }}>◆</span>
            <p style={{
              margin: 0,
              fontSize: 13,
              color: "#777",
              fontFamily: "'Georgia', serif",
              fontStyle: "italic",
              lineHeight: 1.8,
            }}>
              {lesson.insight}
            </p>
          </div>
        </div>

        {/* Navigation */}
        <div style={{ display: "flex", justifyContent: "space-between", marginTop: 28, gap: 16 }}>
          <button onClick={() => go(-1)} style={{
            flex: 1,
            padding: "14px 24px",
            background: "transparent",
            border: "1px solid #222",
            color: "#555",
            fontFamily: "monospace",
            fontSize: 11,
            letterSpacing: 3,
            cursor: "pointer",
            transition: "all 0.2s",
            textTransform: "uppercase",
          }}
            onMouseEnter={e => { e.target.style.borderColor = "#444"; e.target.style.color = "#888"; }}
            onMouseLeave={e => { e.target.style.borderColor = "#222"; e.target.style.color = "#555"; }}
          >
            ← Prev
          </button>
          <button onClick={() => go(1)} style={{
            flex: 1,
            padding: "14px 24px",
            background: color,
            border: `1px solid ${color}`,
            color: "#000",
            fontFamily: "monospace",
            fontSize: 11,
            fontWeight: "bold",
            letterSpacing: 3,
            cursor: "pointer",
            transition: "all 0.2s",
            textTransform: "uppercase",
          }}
            onMouseEnter={e => e.target.style.opacity = "0.85"}
            onMouseLeave={e => e.target.style.opacity = "1"}
          >
            Next →
          </button>
        </div>

        {/* Topic index */}
        <div style={{ marginTop: 40, paddingTop: 28, borderTop: "1px solid #111" }}>
          <div style={{ fontSize: 10, fontFamily: "monospace", letterSpacing: 3, color: "#333", marginBottom: 16, textTransform: "uppercase" }}>
            All Topics
          </div>
          <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
            {lessons.map((l, i) => (
              <button key={i} onClick={() => { setCurrent(i); setViewed(v => new Set([...v, i])); }}
                style={{
                  display: "flex", alignItems: "center", gap: 16,
                  background: "transparent", border: "none", cursor: "pointer",
                  padding: "8px 0", textAlign: "left",
                  borderBottom: "1px solid #111",
                  transition: "all 0.2s",
                }}
              >
                <span style={{
                  width: 6, height: 6, borderRadius: "50%", flexShrink: 0,
                  background: i === current ? categoryColors[l.category] : "#333",
                  transition: "background 0.3s",
                }} />
                <span style={{
                  fontSize: 9, fontFamily: "monospace", letterSpacing: 2,
                  color: i === current ? categoryColors[l.category] : "#444",
                  width: 80, textTransform: "uppercase",
                }}>
                  {l.category}
                </span>
                <span style={{
                  fontSize: 14,
                  color: i === current ? "#E8E4DC" : "#555",
                  fontFamily: "'Georgia', serif",
                }}>
                  {l.title}
                </span>
                {viewed.has(i) && i !== current && (
                  <span style={{ marginLeft: "auto", fontSize: 9, fontFamily: "monospace", color: "#333" }}>READ</span>
                )}
              </button>
            ))}
          </div>
        </div>

      </div>
    </div>
  );
}
