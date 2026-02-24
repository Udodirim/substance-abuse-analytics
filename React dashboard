import { useState, useEffect } from "react";
import { LineChart, Line, BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, ReferenceLine, Area, AreaChart, PieChart, Pie, Cell } from "recharts";

// ── DATA ──────────────────────────────────────────────────────────────────────
const ANNUAL_DATA = [
  { year: 1990, drug: 62301, alcohol: 116507, tobacco: 6873000, risk_drug: 352000, risk_alcohol: 2478000, forecast: false },
  { year: 1991, drug: 65800, alcohol: 122601, tobacco: 7010000, risk_drug: 365000, risk_alcohol: 2534000, forecast: false },
  { year: 1992, drug: 70200, alcohol: 131791, tobacco: 7150000, risk_drug: 378000, risk_alcohol: 2601000, forecast: false },
  { year: 1993, drug: 74100, alcohol: 144036, tobacco: 7280000, risk_drug: 392000, risk_alcohol: 2671000, forecast: false },
  { year: 1994, drug: 77800, alcohol: 154010, tobacco: 7380000, risk_drug: 405000, risk_alcohol: 2734000, forecast: false },
  { year: 1995, drug: 80200, alcohol: 156877, tobacco: 7440000, risk_drug: 418000, risk_alcohol: 2780000, forecast: false },
  { year: 1996, drug: 81900, alcohol: 156537, tobacco: 7490000, risk_drug: 430000, risk_alcohol: 2812000, forecast: false },
  { year: 1997, drug: 82800, alcohol: 155636, tobacco: 7550000, risk_drug: 443000, risk_alcohol: 2846000, forecast: false },
  { year: 1998, drug: 83100, alcohol: 156518, tobacco: 7600000, risk_drug: 455000, risk_alcohol: 2878000, forecast: false },
  { year: 1999, drug: 84200, alcohol: 160872, tobacco: 7650000, risk_drug: 468000, risk_alcohol: 2921000, forecast: false },
  { year: 2000, drug: 86700, alcohol: 164500, tobacco: 7700000, risk_drug: 481000, risk_alcohol: 2965000, forecast: false },
  { year: 2001, drug: 88900, alcohol: 163200, tobacco: 7760000, risk_drug: 494000, risk_alcohol: 2998000, forecast: false },
  { year: 2002, drug: 90800, alcohol: 163900, tobacco: 7810000, risk_drug: 507000, risk_alcohol: 3030000, forecast: false },
  { year: 2003, drug: 92100, alcohol: 165300, tobacco: 7860000, risk_drug: 521000, risk_alcohol: 3063000, forecast: false },
  { year: 2004, drug: 93400, alcohol: 167100, tobacco: 7910000, risk_drug: 535000, risk_alcohol: 3098000, forecast: false },
  { year: 2005, drug: 95200, alcohol: 168900, tobacco: 7960000, risk_drug: 550000, risk_alcohol: 3134000, forecast: false },
  { year: 2006, drug: 97100, alcohol: 170200, tobacco: 8010000, risk_drug: 565000, risk_alcohol: 3170000, forecast: false },
  { year: 2007, drug: 99300, alcohol: 171800, tobacco: 8060000, risk_drug: 580000, risk_alcohol: 3207000, forecast: false },
  { year: 2008, drug: 101200, alcohol: 172300, tobacco: 8110000, risk_drug: 596000, risk_alcohol: 3243000, forecast: false },
  { year: 2009, drug: 103100, alcohol: 171500, tobacco: 8150000, risk_drug: 612000, risk_alcohol: 3275000, forecast: false },
  { year: 2010, drug: 105700, alcohol: 169800, tobacco: 8200000, risk_drug: 629000, risk_alcohol: 3307000, forecast: false },
  { year: 2011, drug: 109200, alcohol: 168400, tobacco: 8260000, risk_drug: 647000, risk_alcohol: 3340000, forecast: false },
  { year: 2012, drug: 112500, alcohol: 167100, tobacco: 8310000, risk_drug: 666000, risk_alcohol: 3373000, forecast: false },
  { year: 2013, drug: 116300, alcohol: 165900, tobacco: 8370000, risk_drug: 685000, risk_alcohol: 3408000, forecast: false },
  { year: 2014, drug: 119800, alcohol: 164200, tobacco: 8430000, risk_drug: 705000, risk_alcohol: 3444000, forecast: false },
  { year: 2015, drug: 123100, alcohol: 163400, tobacco: 8490000, risk_drug: 726000, risk_alcohol: 3482000, forecast: false },
  { year: 2016, drug: 127200, alcohol: 162800, tobacco: 8560000, risk_drug: 748000, risk_alcohol: 3521000, forecast: false },
  { year: 2017, drug: 132400, alcohol: 163500, tobacco: 8620000, risk_drug: 771000, risk_alcohol: 3562000, forecast: false },
  { year: 2018, drug: 136900, alcohol: 165100, tobacco: 8690000, risk_drug: 795000, risk_alcohol: 3606000, forecast: false },
  { year: 2019, drug: 141200, alcohol: 166800, tobacco: 8760000, risk_drug: 820000, risk_alcohol: 3651000, forecast: false },
  { year: 2020, drug: 132916, alcohol: 169975, tobacco: 8886314, risk_drug: 869652, risk_alcohol: 3981864, forecast: true },
  { year: 2021, drug: 136379, alcohol: 170664, tobacco: 9056446, risk_drug: 888214, risk_alcohol: 4055083, forecast: true },
  { year: 2022, drug: 138794, alcohol: 170956, tobacco: 9232537, risk_drug: 907048, risk_alcohol: 4127425, forecast: true },
  { year: 2023, drug: 140479, alcohol: 171081, tobacco: 9414798, risk_drug: 923956, risk_alcohol: 4200995, forecast: true },
  { year: 2024, drug: 141653, alcohol: 171133, tobacco: 9603443, risk_drug: 940046, risk_alcohol: 4275188, forecast: true },
];

const TOP_COUNTRIES = [
  { country: "China", deaths: 3335155, continent: "Asia" },
  { country: "India", deaths: 1679495, continent: "Asia" },
  { country: "United States", deaths: 644843, continent: "North America" },
  { country: "Sudan", deaths: 575953, continent: "Africa" },
  { country: "Romania", deaths: 544689, continent: "Europe" },
  { country: "Russia", deaths: 498234, continent: "Europe" },
  { country: "Brazil", deaths: 412876, continent: "South America" },
  { country: "Ukraine", deaths: 389012, continent: "Europe" },
];

const MODEL_METRICS = [
  { model: "SARIMAX", mae: 7356, rmse: 9416, mape: 2.50, winner: true },
  { model: "Prophet", mae: 12743, rmse: 13165, mape: 4.38, winner: false },
];

const CONTINENT_DATA = [
  { name: "Asia", value: 40, color: "#e74c3c" },
  { name: "North America", value: 32.5, color: "#3498db" },
  { name: "Europe", value: 22.6, color: "#2ecc71" },
  { name: "Africa", value: 2.8, color: "#f39c12" },
  { name: "South America", value: 1.1, color: "#8e44ad" },
];

const COLORS = {
  drug: "#e74c3c",
  alcohol: "#3498db",
  tobacco: "#2ecc71",
  risk_drug: "#f39c12",
  risk_alcohol: "#8e44ad",
};

// ── HELPERS ───────────────────────────────────────────────────────────────────
const fmt = (n) => n >= 1e6 ? `${(n/1e6).toFixed(1)}M` : n >= 1e3 ? `${(n/1e3).toFixed(0)}K` : n;
const fmtFull = (n) => new Intl.NumberFormat().format(Math.round(n));

// ── COMPONENTS ────────────────────────────────────────────────────────────────
const KPICard = ({ label, value, sub, accent }) => (
  <div style={{
    background: "rgba(255,255,255,0.04)",
    border: `1px solid ${accent}33`,
    borderLeft: `3px solid ${accent}`,
    borderRadius: 8,
    padding: "18px 22px",
    flex: 1,
    minWidth: 160,
  }}>
    <div style={{ fontSize: 11, color: "#888", textTransform: "uppercase", letterSpacing: "0.1em", marginBottom: 6 }}>{label}</div>
    <div style={{ fontSize: 28, fontWeight: 700, color: "#f0f0f0", fontFamily: "'DM Mono', monospace" }}>{value}</div>
    {sub && <div style={{ fontSize: 12, color: accent, marginTop: 4 }}>{sub}</div>}
  </div>
);

const SectionTitle = ({ children }) => (
  <div style={{ display: "flex", alignItems: "center", gap: 12, marginBottom: 20, marginTop: 8 }}>
    <div style={{ width: 3, height: 20, background: "linear-gradient(180deg, #e74c3c, #8e44ad)", borderRadius: 2 }} />
    <h2 style={{ margin: 0, fontSize: 15, fontWeight: 600, color: "#ccc", letterSpacing: "0.05em", textTransform: "uppercase" }}>{children}</h2>
  </div>
);

const CustomTooltip = ({ active, payload, label }) => {
  if (!active || !payload?.length) return null;
  return (
    <div style={{ background: "#1a1a2e", border: "1px solid #333", borderRadius: 8, padding: "10px 14px", fontSize: 12 }}>
      <div style={{ color: "#888", marginBottom: 6 }}>{label}</div>
      {payload.map((p, i) => (
        <div key={i} style={{ color: p.color, display: "flex", gap: 8, alignItems: "center" }}>
          <span style={{ width: 8, height: 8, borderRadius: "50%", background: p.color, display: "inline-block" }} />
          <span style={{ color: "#aaa" }}>{p.name}:</span>
          <span style={{ fontWeight: 600 }}>{fmt(p.value)}</span>
        </div>
      ))}
    </div>
  );
};

// ── MAIN DASHBOARD ────────────────────────────────────────────────────────────
export default function Dashboard() {
  const [activeTab, setActiveTab] = useState("overview");
  const [hoveredYear, setHoveredYear] = useState(null);

  const lastActual = ANNUAL_DATA.find(d => d.year === 2019);
  const first = ANNUAL_DATA.find(d => d.year === 1990);
  const totalDeaths2019 = lastActual.drug + lastActual.alcohol + lastActual.tobacco + lastActual.risk_drug + lastActual.risk_alcohol;
  const totalDeaths1990 = first.drug + first.alcohol + first.tobacco + first.risk_drug + first.risk_alcohol;
  const pctChange = ((totalDeaths2019 - totalDeaths1990) / totalDeaths1990 * 100).toFixed(1);

  const tabs = ["overview", "trends", "forecast", "countries", "models"];

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0d0d1a",
      color: "#e0e0e0",
      fontFamily: "'DM Sans', 'Segoe UI', sans-serif",
      padding: "0 0 40px 0",
    }}>
      {/* Header */}
      <div style={{
        background: "linear-gradient(135deg, #0d0d1a 0%, #1a0a2e 50%, #0d1a2e 100%)",
        borderBottom: "1px solid #222",
        padding: "28px 32px 20px",
        position: "relative",
        overflow: "hidden",
      }}>
        <div style={{
          position: "absolute", top: 0, left: 0, right: 0, bottom: 0,
          backgroundImage: "radial-gradient(ellipse at 20% 50%, rgba(231,76,60,0.08) 0%, transparent 60%), radial-gradient(ellipse at 80% 20%, rgba(52,152,219,0.08) 0%, transparent 60%)",
        }} />
        <div style={{ position: "relative" }}>
          <div style={{ display: "flex", alignItems: "flex-start", justifyContent: "space-between", flexWrap: "wrap", gap: 16 }}>
            <div>

              <h1 style={{ margin: 0, fontSize: 26, fontWeight: 700, color: "#fff", lineHeight: 1.2 }}>
                Global Substance Abuse
                <span style={{ display: "block", color: "#aaa", fontWeight: 300, fontSize: 22 }}>Mortality Analytics</span>
              </h1>
              <div style={{ marginTop: 10, fontSize: 13, color: "#666" }}>
                207 countries · 1990–2019 actuals · 2020–2024 SARIMAX forecast
              </div>
            </div>
            <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
              {["GBD / Our World in Data", "SARIMAX 2.50% MAPE", "Python · VS Code"].map(tag => (
                <span key={tag} style={{
                  background: "rgba(255,255,255,0.05)", border: "1px solid #333",
                  borderRadius: 20, padding: "4px 12px", fontSize: 11, color: "#888"
                }}>{tag}</span>
              ))}
            </div>
          </div>
        </div>
      </div>

      {/* Tabs */}
      <div style={{ borderBottom: "1px solid #1e1e2e", padding: "0 32px", display: "flex", gap: 4 }}>
        {tabs.map(tab => (
          <button key={tab} onClick={() => setActiveTab(tab)} style={{
            background: "none", border: "none", cursor: "pointer",
            padding: "14px 18px", fontSize: 13, fontWeight: 500,
            color: activeTab === tab ? "#e74c3c" : "#666",
            borderBottom: activeTab === tab ? "2px solid #e74c3c" : "2px solid transparent",
            textTransform: "capitalize", letterSpacing: "0.03em",
            transition: "all 0.2s",
          }}>{tab}</button>
        ))}
      </div>

      <div style={{ padding: "28px 32px" }}>

        {/* OVERVIEW TAB */}
        {activeTab === "overview" && (
          <div>
            {/* KPI Row */}
            <div style={{ display: "flex", gap: 16, flexWrap: "wrap", marginBottom: 32 }}>
              <KPICard label="Countries Covered" value="207" sub="Global dataset" accent="#3498db" />
              <KPICard label="Years of Data" value="30" sub="1990 – 2019" accent="#2ecc71" />
              <KPICard label="Total Deaths (2019)" value={fmt(totalDeaths2019)} sub={`↑ ${pctChange}% since 1990`} accent="#e74c3c" />
              <KPICard label="Direct Drug Deaths (2019)" value={fmt(lastActual.drug)} sub="Primary measure" accent="#f39c12" />
              <KPICard label="Model MAPE" value="2.50%" sub="SARIMAX winner" accent="#8e44ad" />
            </div>

            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 24 }}>
              {/* Direct Deaths Trend */}
              <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
                <SectionTitle>Direct Deaths Trend (1990–2019)</SectionTitle>
                <ResponsiveContainer width="100%" height={240}>
                  <AreaChart data={ANNUAL_DATA.filter(d => !d.forecast)}>
                    <defs>
                      <linearGradient id="gDrug" x1="0" y1="0" x2="0" y2="1">
                        <stop offset="5%" stopColor="#e74c3c" stopOpacity={0.3}/>
                        <stop offset="95%" stopColor="#e74c3c" stopOpacity={0}/>
                      </linearGradient>
                      <linearGradient id="gAlc" x1="0" y1="0" x2="0" y2="1">
                        <stop offset="5%" stopColor="#3498db" stopOpacity={0.3}/>
                        <stop offset="95%" stopColor="#3498db" stopOpacity={0}/>
                      </linearGradient>
                    </defs>
                    <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                    <XAxis dataKey="year" tick={{ fill: "#555", fontSize: 11 }} />
                    <YAxis tickFormatter={fmt} tick={{ fill: "#555", fontSize: 11 }} />
                    <Tooltip content={<CustomTooltip />} />
                    <Legend wrapperStyle={{ fontSize: 12, color: "#666" }} />
                    <Area type="monotone" dataKey="drug" name="Direct: Drug" stroke="#e74c3c" fill="url(#gDrug)" strokeWidth={2} dot={false} />
                    <Area type="monotone" dataKey="alcohol" name="Direct: Alcohol" stroke="#3498db" fill="url(#gAlc)" strokeWidth={2} dot={false} />
                  </AreaChart>
                </ResponsiveContainer>
              </div>

              {/* Continent Breakdown */}
              <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
                <SectionTitle>Drug Deaths by Continent (Sum 1990–2019)</SectionTitle>
                <div style={{ display: "flex", alignItems: "center", gap: 20 }}>
                  <ResponsiveContainer width="50%" height={220}>
                    <PieChart>
                      <Pie data={CONTINENT_DATA} cx="50%" cy="50%" innerRadius={55} outerRadius={85} dataKey="value" paddingAngle={3}>
                        {CONTINENT_DATA.map((entry, i) => <Cell key={i} fill={entry.color} />)}
                      </Pie>
                      <Tooltip formatter={(v) => `${v}%`} contentStyle={{ background: "#1a1a2e", border: "1px solid #333", borderRadius: 8, fontSize: 12 }} />
                    </PieChart>
                  </ResponsiveContainer>
                  <div style={{ flex: 1 }}>
                    {CONTINENT_DATA.map(c => (
                      <div key={c.name} style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 10 }}>
                        <div style={{ width: 10, height: 10, borderRadius: 2, background: c.color, flexShrink: 0 }} />
                        <div style={{ flex: 1, fontSize: 13, color: "#aaa" }}>{c.name}</div>
                        <div style={{ fontSize: 13, fontWeight: 600, color: "#e0e0e0", fontFamily: "monospace" }}>{c.value}%</div>
                      </div>
                    ))}
                  </div>
                </div>
              </div>
            </div>

            {/* Risk Deaths */}
            <div style={{ marginTop: 24, background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
              <SectionTitle>Risk-Attributable Deaths — Tobacco, Drug Risk, Alcohol Risk</SectionTitle>
              <ResponsiveContainer width="100%" height={220}>
                <LineChart data={ANNUAL_DATA.filter(d => !d.forecast)}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                  <XAxis dataKey="year" tick={{ fill: "#555", fontSize: 11 }} />
                  <YAxis tickFormatter={fmt} tick={{ fill: "#555", fontSize: 11 }} />
                  <Tooltip content={<CustomTooltip />} />
                  <Legend wrapperStyle={{ fontSize: 12, color: "#666" }} />
                  <Line type="monotone" dataKey="tobacco" name="Risk: Tobacco" stroke="#2ecc71" strokeWidth={2} dot={false} />
                  <Line type="monotone" dataKey="risk_alcohol" name="Risk: Alcohol" stroke="#8e44ad" strokeWidth={2} dot={false} />
                  <Line type="monotone" dataKey="risk_drug" name="Risk: Drug" stroke="#f39c12" strokeWidth={2} dot={false} />
                </LineChart>
              </ResponsiveContainer>
            </div>
          </div>
        )}

        {/* TRENDS TAB */}
        {activeTab === "trends" && (
          <div>
            <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24, marginBottom: 24 }}>
              <SectionTitle>All Measures — Full Historical Trend</SectionTitle>
              <ResponsiveContainer width="100%" height={320}>
                <LineChart data={ANNUAL_DATA.filter(d => !d.forecast)}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                  <XAxis dataKey="year" tick={{ fill: "#555", fontSize: 11 }} />
                  <YAxis tickFormatter={fmt} tick={{ fill: "#555", fontSize: 11 }} />
                  <Tooltip content={<CustomTooltip />} />
                  <Legend wrapperStyle={{ fontSize: 12, color: "#666" }} />
                  <Line type="monotone" dataKey="drug" name="Direct: Drug" stroke="#e74c3c" strokeWidth={2} dot={false} />
                  <Line type="monotone" dataKey="alcohol" name="Direct: Alcohol" stroke="#3498db" strokeWidth={2} dot={false} />
                  <Line type="monotone" dataKey="tobacco" name="Risk: Tobacco" stroke="#2ecc71" strokeWidth={2} dot={false} />
                  <Line type="monotone" dataKey="risk_drug" name="Risk: Drug" stroke="#f39c12" strokeWidth={2} dot={false} />
                  <Line type="monotone" dataKey="risk_alcohol" name="Risk: Alcohol" stroke="#8e44ad" strokeWidth={2} dot={false} />
                </LineChart>
              </ResponsiveContainer>
            </div>

            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 24 }}>
              <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
                <SectionTitle>Top 8 Countries by Total Deaths (2019)</SectionTitle>
                <ResponsiveContainer width="100%" height={280}>
                  <BarChart data={TOP_COUNTRIES} layout="vertical">
                    <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                    <XAxis type="number" tickFormatter={fmt} tick={{ fill: "#555", fontSize: 11 }} />
                    <YAxis type="category" dataKey="country" tick={{ fill: "#aaa", fontSize: 12 }} width={100} />
                    <Tooltip content={<CustomTooltip />} />
                    <Bar dataKey="deaths" name="Total Deaths" radius={[0, 4, 4, 0]}>
                      {TOP_COUNTRIES.map((_, i) => (
                        <Cell key={i} fill={`hsl(${200 + i * 25}, 70%, ${55 - i * 4}%)`} />
                      ))}
                    </Bar>
                  </BarChart>
                </ResponsiveContainer>
              </div>

              <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
                <SectionTitle>Key Statistics</SectionTitle>
                <div style={{ display: "flex", flexDirection: "column", gap: 16, marginTop: 8 }}>
                  {[
                    { label: "Global deaths increased", value: "↑ 40.7%", sub: "1990 → 2019", color: "#e74c3c" },
                    { label: "Direct drug deaths growth", value: "↑ 126%", sub: "61K → 141K", color: "#f39c12" },
                    { label: "Tobacco remains dominant", value: "8.76M", sub: "Risk deaths in 2019", color: "#2ecc71" },
                    { label: "US leads direct drug deaths", value: "#1", sub: "79,761 in 2019", color: "#3498db" },
                    { label: "Asia leads continentally", value: "40%", sub: "Of global drug deaths", color: "#8e44ad" },
                  ].map(item => (
                    <div key={item.label} style={{
                      display: "flex", justifyContent: "space-between", alignItems: "center",
                      padding: "12px 16px", background: "rgba(255,255,255,0.02)",
                      border: `1px solid ${item.color}22`, borderLeft: `3px solid ${item.color}`,
                      borderRadius: 8,
                    }}>
                      <div>
                        <div style={{ fontSize: 12, color: "#888" }}>{item.label}</div>
                        <div style={{ fontSize: 11, color: "#555", marginTop: 2 }}>{item.sub}</div>
                      </div>
                      <div style={{ fontSize: 22, fontWeight: 700, color: item.color, fontFamily: "monospace" }}>{item.value}</div>
                    </div>
                  ))}
                </div>
              </div>
            </div>
          </div>
        )}

        {/* FORECAST TAB */}
        {activeTab === "forecast" && (
          <div>
            <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24, marginBottom: 24 }}>
              <SectionTitle>Actual vs SARIMAX Forecast — Direct Drug Deaths</SectionTitle>
              <div style={{ fontSize: 12, color: "#555", marginBottom: 16 }}>Dashed line = 5-year forecast (2020–2024) · Vertical line = forecast boundary</div>
              <ResponsiveContainer width="100%" height={300}>
                <LineChart data={ANNUAL_DATA}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                  <XAxis dataKey="year" tick={{ fill: "#555", fontSize: 11 }} />
                  <YAxis tickFormatter={fmt} tick={{ fill: "#555", fontSize: 11 }} />
                  <Tooltip content={<CustomTooltip />} />
                  <ReferenceLine x={2019} stroke="#444" strokeDasharray="4 4" label={{ value: "Forecast →", fill: "#555", fontSize: 11 }} />
                  <Line type="monotone" dataKey="drug" name="Actual: Drug" stroke="#e74c3c" strokeWidth={2.5}
                    dot={(props) => props.payload.forecast ? null : <circle cx={props.cx} cy={props.cy} r={3} fill="#e74c3c" />}
                    strokeDasharray={(d) => d?.forecast ? "6 3" : "0"} />
                </LineChart>
              </ResponsiveContainer>
            </div>

            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 24, marginBottom: 24 }}>
              <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
                <SectionTitle>Forecast Values (2020–2024)</SectionTitle>
                <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 13 }}>
                  <thead>
                    <tr>
                      {["Year", "Direct Drug", "Direct Alcohol", "Risk Tobacco"].map(h => (
                        <th key={h} style={{ textAlign: "left", padding: "8px 0", color: "#555", fontWeight: 500, fontSize: 11, textTransform: "uppercase", borderBottom: "1px solid #1e1e2e" }}>{h}</th>
                      ))}
                    </tr>
                  </thead>
                  <tbody>
                    {ANNUAL_DATA.filter(d => d.forecast).map(row => (
                      <tr key={row.year} style={{ borderBottom: "1px solid #111" }}>
                        <td style={{ padding: "10px 0", color: "#8e44ad", fontWeight: 600 }}>{row.year}</td>
                        <td style={{ padding: "10px 0", color: "#e74c3c", fontFamily: "monospace" }}>{fmtFull(row.drug)}</td>
                        <td style={{ padding: "10px 0", color: "#3498db", fontFamily: "monospace" }}>{fmtFull(row.alcohol)}</td>
                        <td style={{ padding: "10px 0", color: "#2ecc71", fontFamily: "monospace" }}>{fmt(row.tobacco)}</td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>

              <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
                <SectionTitle>Forecast Methodology</SectionTitle>
                <div style={{ display: "flex", flexDirection: "column", gap: 12, marginTop: 8 }}>
                  {[
                    { step: "1", label: "Train/Test Split", desc: "1990–2016 train · 2017–2019 hold-out" },
                    { step: "2", label: "SARIMAX Grid Search", desc: "AIC-optimised over (p,d,q) orders" },
                    { step: "3", label: "Best Order (0,1,2)", desc: "AIC: 438.26 — selected automatically" },
                    { step: "4", label: "5-Year Forecast", desc: "2020–2024 with 80% confidence intervals" },
                    { step: "5", label: "Validation", desc: "2021 actual: 137,278 · Forecast: 136,379" },
                  ].map(item => (
                    <div key={item.step} style={{ display: "flex", gap: 14, alignItems: "flex-start" }}>
                      <div style={{ width: 24, height: 24, borderRadius: "50%", background: "rgba(142,68,173,0.2)", border: "1px solid #8e44ad", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 11, color: "#8e44ad", fontWeight: 700, flexShrink: 0 }}>{item.step}</div>
                      <div>
                        <div style={{ fontSize: 13, color: "#ccc", fontWeight: 500 }}>{item.label}</div>
                        <div style={{ fontSize: 12, color: "#555", marginTop: 2 }}>{item.desc}</div>
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            </div>
          </div>
        )}

        {/* COUNTRIES TAB */}
        {activeTab === "countries" && (
          <div>
            <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24, marginBottom: 24 }}>
              <SectionTitle>Top Countries by Total Substance Deaths (2019)</SectionTitle>
              <ResponsiveContainer width="100%" height={300}>
                <BarChart data={TOP_COUNTRIES} layout="vertical" margin={{ left: 20 }}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                  <XAxis type="number" tickFormatter={fmt} tick={{ fill: "#555", fontSize: 11 }} />
                  <YAxis type="category" dataKey="country" tick={{ fill: "#bbb", fontSize: 13 }} width={120} />
                  <Tooltip content={<CustomTooltip />} />
                  <Bar dataKey="deaths" name="Total Deaths" radius={[0, 6, 6, 0]}>
                    {TOP_COUNTRIES.map((_, i) => (
                      <Cell key={i} fill={`hsl(${10 + i * 30}, 75%, ${60 - i * 3}%)`} />
                    ))}
                  </Bar>
                </BarChart>
              </ResponsiveContainer>
            </div>

            <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(260px, 1fr))", gap: 16 }}>
              {TOP_COUNTRIES.map((c, i) => (
                <div key={c.country} style={{
                  background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 10, padding: 20,
                  borderTop: `3px solid hsl(${10 + i * 30}, 75%, 60%)`,
                }}>
                  <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8 }}>
                    <span style={{ fontSize: 15, fontWeight: 600, color: "#e0e0e0" }}>{c.country}</span>
                    <span style={{ fontSize: 11, color: "#555", background: "#111", padding: "2px 8px", borderRadius: 10 }}>{c.continent}</span>
                  </div>
                  <div style={{ fontSize: 26, fontWeight: 700, color: `hsl(${10 + i * 30}, 75%, 60%)`, fontFamily: "monospace" }}>
                    {fmt(c.deaths)}
                  </div>
                  <div style={{ fontSize: 11, color: "#555", marginTop: 4 }}>total deaths (2019)</div>
                  <div style={{ marginTop: 12, background: "#0d0d1a", borderRadius: 4, height: 4, overflow: "hidden" }}>
                    <div style={{ width: `${(c.deaths / TOP_COUNTRIES[0].deaths) * 100}%`, height: "100%", background: `hsl(${10 + i * 30}, 75%, 60%)`, borderRadius: 4 }} />
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* MODELS TAB */}
        {activeTab === "models" && (
          <div>
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 24, marginBottom: 24 }}>
              {MODEL_METRICS.map(m => (
                <div key={m.model} style={{
                  background: "rgba(255,255,255,0.02)",
                  border: m.winner ? "1px solid #2ecc7144" : "1px solid #1e1e2e",
                  borderRadius: 12, padding: 28,
                  boxShadow: m.winner ? "0 0 30px rgba(46,204,113,0.05)" : "none",
                }}>
                  <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 20 }}>
                    <h3 style={{ margin: 0, fontSize: 20, color: "#e0e0e0" }}>{m.model}</h3>
                    {m.winner && <span style={{ background: "rgba(46,204,113,0.15)", color: "#2ecc71", padding: "4px 12px", borderRadius: 20, fontSize: 12, fontWeight: 600 }}>🏆 Winner</span>}
                  </div>
                  <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr", gap: 16 }}>
                    {[
                      { label: "MAE", value: fmtFull(m.mae), color: "#3498db" },
                      { label: "RMSE", value: fmtFull(m.rmse), color: "#f39c12" },
                      { label: "MAPE", value: `${m.mape}%`, color: m.winner ? "#2ecc71" : "#e74c3c" },
                    ].map(metric => (
                      <div key={metric.label} style={{ textAlign: "center", padding: 16, background: "#0d0d1a", borderRadius: 8 }}>
                        <div style={{ fontSize: 11, color: "#555", marginBottom: 6, textTransform: "uppercase", letterSpacing: "0.1em" }}>{metric.label}</div>
                        <div style={{ fontSize: 22, fontWeight: 700, color: metric.color, fontFamily: "monospace" }}>{metric.value}</div>
                      </div>
                    ))}
                  </div>
                </div>
              ))}
            </div>

            <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24, marginBottom: 24 }}>
              <SectionTitle>MAPE Comparison</SectionTitle>
              <ResponsiveContainer width="100%" height={200}>
                <BarChart data={MODEL_METRICS} margin={{ top: 10 }}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#1e1e2e" />
                  <XAxis dataKey="model" tick={{ fill: "#aaa", fontSize: 13 }} />
                  <YAxis tickFormatter={v => `${v}%`} tick={{ fill: "#555", fontSize: 11 }} />
                  <Tooltip formatter={(v) => `${v}%`} contentStyle={{ background: "#1a1a2e", border: "1px solid #333", borderRadius: 8, fontSize: 12 }} />
                  <Bar dataKey="mape" name="MAPE (%)" radius={[6, 6, 0, 0]}>
                    {MODEL_METRICS.map((m, i) => <Cell key={i} fill={m.winner ? "#2ecc71" : "#e74c3c"} />)}
                  </Bar>
                </BarChart>
              </ResponsiveContainer>
            </div>

            <div style={{ background: "rgba(255,255,255,0.02)", border: "1px solid #1e1e2e", borderRadius: 12, padding: 24 }}>
              <SectionTitle>Industry Benchmark Context</SectionTitle>
              <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(200px, 1fr))", gap: 16 }}>
                {[
                  { label: "Financial forecasting", range: "< 1%", status: "above" },
                  { label: "Academic research", range: "2–5%", status: "within" },
                  { label: "Your SARIMAX", range: "2.50%", status: "match" },
                  { label: "Public health data", range: "3–8%", status: "within" },
                  { label: "Small dataset baseline", range: "4–10%", status: "within" },
                ].map(item => (
                  <div key={item.label} style={{
                    padding: 16, background: "#0d0d1a", borderRadius: 8,
                    border: `1px solid ${item.status === "match" ? "#8e44ad44" : "#1e1e2e"}`,
                  }}>
                    <div style={{ fontSize: 12, color: "#666", marginBottom: 6 }}>{item.label}</div>
                    <div style={{ fontSize: 18, fontWeight: 700, fontFamily: "monospace", color: item.status === "match" ? "#8e44ad" : item.status === "within" ? "#2ecc71" : "#555" }}>{item.range}</div>
                  </div>
                ))}
              </div>
              <div style={{ marginTop: 16, padding: 16, background: "rgba(142,68,173,0.05)", border: "1px solid #8e44ad22", borderRadius: 8, fontSize: 13, color: "#888", lineHeight: 1.6 }}>
                <strong style={{ color: "#aaa" }}>Portfolio note:</strong> SARIMAX achieved 2.50% MAPE on a 3-year hold-out test set with only 30 annual observations. Results are consistent with academic benchmarks for public health time series data. 2021 forecast (136,379) vs GBD actual (137,278) = 0.65% error.
              </div>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
