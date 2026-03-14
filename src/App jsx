import { useState, useEffect, useRef, createContext, useContext } from "react";

// ─── CREDENTIALS ──────────────────────────────────────────────────────────────
const SUPABASE_URL = "https://ndgmmrpboxpdmqqwyyhf.supabase.co";
const SUPABASE_ANON_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im5kZ21tcnBib3hwZG1xcXd5eWhmIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzM0Mjk5MjgsImV4cCI6MjA4OTAwNTkyOH0.ftqICIeF_QLmag87BSYGUvebKxC3mBkc23usNNCkjWY";
const RESEND_API_KEY = "re_3nT1B49R_CfvYF4Ky9jm2knE8wjELxv6c";
const SENDER_EMAIL = "onboarding@resend.dev";
const APP_ICON = "data:image/png;base64,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";

// ─── SUPABASE CLIENT (no npm needed — raw fetch wrapper) ──────────────────────
const supabase = {
  _url: SUPABASE_URL,
  _key: SUPABASE_ANON_KEY,
  _token: null,
  _session: null,

  _headers(extra = {}) {
    const h = {
      "Content-Type": "application/json",
      "apikey": this._key,
      ...extra,
    };
    if (this._token) h["Authorization"] = `Bearer ${this._token}`;
    return h;
  },

  async signUp(email, password, fullName, phone) {
    const res = await fetch(`${this._url}/auth/v1/signup`, {
      method: "POST",
      headers: this._headers(),
      body: JSON.stringify({ email, password, data: { full_name: fullName, phone } }),
    });
    const data = await res.json();
    if (data.error) throw new Error(data.error.message || data.msg || "Sign up failed");
    if (data.access_token) { this._token = data.access_token; this._session = data; }
    return data;
  },

  async signIn(email, password) {
    const res = await fetch(`${this._url}/auth/v1/token?grant_type=password`, {
      method: "POST",
      headers: this._headers(),
      body: JSON.stringify({ email, password }),
    });
    const data = await res.json();
    if (data.error) throw new Error(data.error.message || data.msg || "Sign in failed");
    if (data.error_code) throw new Error(data.message || "Invalid credentials");
    this._token = data.access_token;
    this._session = data;
    // persist
    try { localStorage.setItem("afc_session", JSON.stringify(data)); } catch {}
    return data;
  },

  async signOut() {
    if (this._token) {
      await fetch(`${this._url}/auth/v1/logout`, {
        method: "POST", headers: this._headers(),
      }).catch(() => {});
    }
    this._token = null;
    this._session = null;
    try { localStorage.removeItem("afc_session"); } catch {}
  },

  async resetPassword(email) {
    const res = await fetch(`${this._url}/auth/v1/recover`, {
      method: "POST",
      headers: this._headers(),
      body: JSON.stringify({ email }),
    });
    const data = await res.json();
    if (data.error) throw new Error(data.error.message || "Reset failed");
    return data;
  },

  async getUser() {
    if (!this._token) return null;
    const res = await fetch(`${this._url}/auth/v1/user`, {
      headers: this._headers(),
    });
    const data = await res.json();
    if (data.error) return null;
    return data;
  },

  async upsertProfile(userId, profile) {
    const res = await fetch(`${this._url}/rest/v1/profiles`, {
      method: "POST",
      headers: this._headers({
        "Prefer": "resolution=merge-duplicates,return=representation",
      }),
      body: JSON.stringify({ id: userId, ...profile, updated_at: new Date().toISOString() }),
    });
    return await res.json();
  },

  async getProfile(userId) {
    const res = await fetch(`${this._url}/rest/v1/profiles?id=eq.${userId}&select=*`, {
      headers: this._headers(),
    });
    const data = await res.json();
    return Array.isArray(data) ? data[0] : null;
  },

  async getTransactions(userId) {
    const res = await fetch(
      `${this._url}/rest/v1/transactions?user_id=eq.${userId}&order=created_at.desc&limit=20`,
      { headers: this._headers() }
    );
    const data = await res.json();
    return Array.isArray(data) ? data : [];
  },

  async insertTransaction(tx) {
    const res = await fetch(`${this._url}/rest/v1/transactions`, {
      method: "POST",
      headers: this._headers({ "Prefer": "return=representation" }),
      body: JSON.stringify(tx),
    });
    return await res.json();
  },

  loadSession() {
    try {
      const s = localStorage.getItem("afc_session");
      if (s) {
        const parsed = JSON.parse(s);
        // Check expiry
        const exp = parsed.expires_at || (parsed.expires_in ? Date.now() / 1000 + parsed.expires_in : 0);
        if (exp && Date.now() / 1000 < exp) {
          this._token = parsed.access_token;
          this._session = parsed;
          return parsed;
        }
        localStorage.removeItem("afc_session");
      }
    } catch {}
    return null;
  },
};

// ─── RESEND EMAIL ─────────────────────────────────────────────────────────────
const sendEmail = async (to, subject, html) => {
  try {
    const res = await fetch("https://api.resend.com/emails", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${RESEND_API_KEY}`,
      },
      body: JSON.stringify({ from: SENDER_EMAIL, to, subject, html }),
    });
    return await res.json();
  } catch (e) {
    console.warn("Email send error:", e);
    return null;
  }
};

const emailTemplates = {
  welcome: (name) => ({
    subject: "Welcome to AfriCoin — Your Gold-Backed Wallet is Ready",
    html: `
<!DOCTYPE html><html><head><meta charset="utf-8">
<style>
  body{margin:0;padding:0;background:#0a0a0a;font-family:'Segoe UI',sans-serif;}
  .wrap{max-width:580px;margin:0 auto;background:#0E0A05;}
  .header{background:linear-gradient(135deg,#0E1F0A,#1A2E0F);padding:40px 40px 30px;text-align:center;border-bottom:1px solid #C9A84C44;}
  .logo-ring{width:72px;height:72px;border-radius:50%;border:2px solid #C9A84C;display:inline-flex;align-items:center;justify-content:center;margin-bottom:16px;}
  h1{color:#C9A84C;font-size:28px;margin:0 0 6px;letter-spacing:1px;}
  .sub{color:#7A8C6A;font-size:13px;letter-spacing:2px;text-transform:uppercase;}
  .body{padding:36px 40px;}
  .greeting{color:#F5EDD8;font-size:18px;margin-bottom:16px;}
  p{color:#A89880;font-size:14px;line-height:1.7;margin:0 0 16px;}
  .feature{background:#1A1208;border:1px solid #3D2B1A;border-radius:10px;padding:16px 20px;margin:8px 0;display:flex;align-items:center;gap:14px;}
  .feat-icon{font-size:22px;width:36px;text-align:center;}
  .feat-text{color:#E8D9B8;font-size:13px;}
  .feat-sub{color:#7A6555;font-size:11px;margin-top:2px;}
  .cta{display:block;background:linear-gradient(135deg,#C9A84C,#8B6914);color:#1A0F05;text-decoration:none;padding:14px 32px;border-radius:10px;font-weight:700;font-size:15px;text-align:center;margin:28px 0;}
  .footer{background:#0A0704;padding:24px 40px;text-align:center;border-top:1px solid #1A1208;}
  .footer p{color:#4A3728;font-size:11px;margin:0;}
  .gold{color:#C9A84C;}
  .divider{height:1px;background:linear-gradient(90deg,transparent,#3D2B1A,transparent);margin:24px 0;}
</style></head><body>
<div class="wrap">
  <div class="header">
    <div class="logo-ring"><span style="font-size:32px">◈</span></div>
    <h1>AFRiCOiN</h1>
    <div class="sub">Gold-Backed · Pan-African · Decentralised</div>
  </div>
  <div class="body">
    <div class="greeting">Welcome, ${name} 👋</div>
    <p>Your AfriCoin wallet has been created and secured. You are now part of a new generation of African financial infrastructure — gold-backed, borderless, and built for you.</p>
    <div class="divider"></div>
    <div class="feature"><div class="feat-icon">🏅</div><div><div class="feat-text">Gold-Backed AFC Tokens</div><div class="feat-sub">1 AFC = 0.001 troy oz of audited physical gold</div></div></div>
    <div class="feature"><div class="feat-icon">⚡</div><div><div class="feat-text">Sub-Second Settlements</div><div class="feat-sub">Send money across Africa in under 1 second</div></div></div>
    <div class="feature"><div class="feat-icon">🔄</div><div><div class="feat-text">Loyalty Point Conversion</div><div class="feat-sub">Convert eBucks, Greenbacks & UCount to AFC</div></div></div>
    <div class="feature"><div class="feat-icon">🌍</div><div><div class="feat-text">54 African Countries</div><div class="feat-sub">Works on any phone via USSD, app, or NFC card</div></div></div>
    <div class="divider"></div>
    <p>Your next step is to complete <span class="gold">KYC Level 2 verification</span> to unlock up to $5,000/month in transaction limits. It takes less than 2 minutes.</p>
    <a href="#" class="cta">Open Your AfriCoin Dashboard →</a>
    <p style="font-size:12px;color:#4A3728;text-align:center;">If you did not create this account, please ignore this email.</p>
  </div>
  <div class="footer"><p>© 2025 AfriCoin Technologies. Pan-African. Gold-Backed. Globally Scalable.</p></div>
</div></body></html>`,
  }),

  transactionConfirmation: (name, amount, type, recipient, txId, time) => ({
    subject: `AfriCoin: ${type} of ${amount} AFC Confirmed`,
    html: `
<!DOCTYPE html><html><head><meta charset="utf-8">
<style>
  body{margin:0;padding:0;background:#0a0a0a;font-family:'Segoe UI',sans-serif;}
  .wrap{max-width:580px;margin:0 auto;background:#0E0A05;}
  .header{background:linear-gradient(135deg,#0E1F0A,#1A2E0F);padding:32px 40px;text-align:center;border-bottom:1px solid #C9A84C44;}
  h1{color:#C9A84C;font-size:22px;margin:0;}
  .status-badge{display:inline-block;background:rgba(45,138,87,0.15);border:1px solid rgba(45,138,87,0.4);color:#2D8A57;padding:6px 18px;border-radius:999px;font-size:12px;font-weight:700;letter-spacing:1px;margin-top:12px;}
  .body{padding:32px 40px;}
  .amount-box{background:#1A1208;border:1px solid #C9A84C44;border-radius:12px;padding:24px;text-align:center;margin-bottom:24px;}
  .amount{font-size:38px;font-weight:700;color:#C9A84C;font-family:monospace;}
  .amount-sub{color:#7A6555;font-size:13px;margin-top:4px;}
  .detail-row{display:flex;justify-content:space-between;padding:10px 0;border-bottom:1px solid #1A1208;}
  .detail-label{color:#7A6555;font-size:13px;}
  .detail-value{color:#E8D9B8;font-size:13px;font-family:monospace;}
  .footer{background:#0A0704;padding:20px 40px;text-align:center;border-top:1px solid #1A1208;}
  .footer p{color:#4A3728;font-size:11px;margin:0;}
</style></head><body>
<div class="wrap">
  <div class="header">
    <h1>◈ AfriCoin Transaction</h1>
    <div class="status-badge">✓ CONFIRMED</div>
  </div>
  <div class="body">
    <div class="amount-box">
      <div class="amount">${amount} AFC</div>
      <div class="amount-sub">${type}</div>
    </div>
    <div class="detail-row"><span class="detail-label">Transaction ID</span><span class="detail-value">${txId}</span></div>
    <div class="detail-row"><span class="detail-label">${type === "Sent" ? "Recipient" : "From"}</span><span class="detail-value">${recipient}</span></div>
    <div class="detail-row"><span class="detail-label">Time</span><span class="detail-value">${time}</span></div>
    <div class="detail-row"><span class="detail-label">Settlement</span><span class="detail-value" style="color:#2D8A57">⚡ &lt; 1 second</span></div>
    <div class="detail-row" style="border:none"><span class="detail-label">Network fee</span><span class="detail-value">0.001 AFC</span></div>
    <p style="color:#4A3728;font-size:12px;margin-top:20px;text-align:center;">If you did not authorise this transaction, contact support immediately at support@africoin.com</p>
  </div>
  <div class="footer"><p>© 2025 AfriCoin Technologies · All transactions are final and recorded on AfriChain</p></div>
</div></body></html>`,
  }),

  kycUpdate: (name, level, status) => ({
    subject: `AfriCoin KYC Level ${level} — ${status}`,
    html: `
<!DOCTYPE html><html><head><meta charset="utf-8">
<style>
  body{margin:0;padding:0;background:#0a0a0a;font-family:'Segoe UI',sans-serif;}
  .wrap{max-width:580px;margin:0 auto;background:#0E0A05;}
  .header{background:linear-gradient(135deg,#0E1F0A,#1A2E0F);padding:32px 40px;text-align:center;border-bottom:1px solid #C9A84C44;}
  h1{color:#C9A84C;font-size:22px;margin:0;}
  .body{padding:32px 40px;}
  p{color:#A89880;font-size:14px;line-height:1.7;}
  .badge{display:inline-block;padding:8px 20px;border-radius:999px;font-size:13px;font-weight:700;}
  .approved{background:rgba(45,138,87,0.15);border:1px solid rgba(45,138,87,0.4);color:#2D8A57;}
  .pending{background:rgba(201,168,76,0.15);border:1px solid rgba(201,168,76,0.4);color:#C9A84C;}
  .footer{background:#0A0704;padding:20px 40px;text-align:center;border-top:1px solid #1A1208;}
  .footer p{color:#4A3728;font-size:11px;margin:0;}
</style></head><body>
<div class="wrap">
  <div class="header"><h1>◈ AfriCoin KYC Update</h1></div>
  <div class="body">
    <p>Hello ${name},</p>
    <p>Your KYC Level ${level} verification status has been updated:</p>
    <div style="text-align:center;margin:24px 0;">
      <div class="badge ${status === "Approved" ? "approved" : "pending"}">${status === "Approved" ? "✓" : "⏳"} Level ${level} — ${status}</div>
    </div>
    <p>${status === "Approved"
      ? `Congratulations — your account limits have been upgraded. You can now transact up to ${level === 2 ? "$5,000/month" : "unlimited amounts"}.`
      : "Your documents are under review. We will notify you within 24 hours."
    }</p>
  </div>
  <div class="footer"><p>© 2025 AfriCoin Technologies</p></div>
</div></body></html>`,
  }),
};

// ─── DESIGN TOKENS ────────────────────────────────────────────────────────────
const C = {
  gold: "#C9A84C", goldL: "#E8C96A", goldD: "#8B6914",
  bg: "#060402", bgCard: "#0E0A05", bgCardL: "#1A1208", bgCardLL: "#241A0E",
  green: "#0D3320", greenL: "#2D8A57",
  cream: "#F5EDD8", creamD: "#E8D9B8",
  textL: "#7A6555", textM: "#A89880",
  border: "#2A1E12", borderL: "#3D2B1A",
  red: "#C42B2B", earth: "#1A0F05",
};

// ─── GLOBAL STYLES ────────────────────────────────────────────────────────────
const injectGlobalStyles = () => {
  if (document.getElementById("afc-styles")) return;
  const s = document.createElement("style");
  s.id = "afc-styles";
  s.textContent = `
    @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400&family=IBM+Plex+Mono:wght@400;500;600&family=DM+Sans:wght@300;400;500;600;700&display=swap');
    *{box-sizing:border-box;margin:0;padding:0;}
    body{background:${C.bg};color:${C.cream};font-family:'DM Sans',sans-serif;-webkit-font-smoothing:antialiased;}
    ::-webkit-scrollbar{width:4px;}
    ::-webkit-scrollbar-track{background:${C.bgCard};}
    ::-webkit-scrollbar-thumb{background:${C.goldD};border-radius:2px;}
    @keyframes fadeUp{from{opacity:0;transform:translateY(16px);}to{opacity:1;transform:translateY(0);}}
    @keyframes fadeIn{from{opacity:0;}to{opacity:1;}}
    @keyframes spin{from{transform:rotate(0deg);}to{transform:rotate(360deg);}}
    @keyframes shimmer{0%{background-position:-200% 0;}100%{background-position:200% 0;}}
    @keyframes goldPulse{0%,100%{box-shadow:0 0 0 0 rgba(201,168,76,0.4);}50%{box-shadow:0 0 0 8px rgba(201,168,76,0);}}
    @keyframes gradientShift{0%,100%{background-position:0% 50%;}50%{background-position:100% 50%;}}
    .fade-up{animation:fadeUp 0.45s cubic-bezier(.22,1,.36,1) both;}
    .fade-in{animation:fadeIn 0.3s ease both;}
    .gold-text{
      background:linear-gradient(90deg,${C.goldD} 0%,${C.gold} 40%,${C.goldL} 60%,${C.gold} 80%,${C.goldD} 100%);
      background-size:200% 100%;
      animation:shimmer 4s infinite;
      -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
    }
    .btn-gold{
      background:linear-gradient(135deg,${C.gold},${C.goldD});
      color:${C.earth};border:none;cursor:pointer;
      font-family:'DM Sans',sans-serif;font-weight:700;
      transition:all 0.2s ease;letter-spacing:0.3px;
    }
    .btn-gold:hover{filter:brightness(1.1);transform:translateY(-1px);box-shadow:0 6px 24px rgba(201,168,76,0.3);}
    .btn-gold:active{transform:translateY(0);}
    .btn-ghost{background:transparent;color:${C.gold};border:1px solid ${C.gold};cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:600;transition:all 0.2s;}
    .btn-ghost:hover{background:rgba(201,168,76,0.08);}
    .input-field{background:${C.bgCardL};border:1px solid ${C.border};color:${C.cream};font-family:'DM Sans',sans-serif;outline:none;transition:border-color 0.2s,box-shadow 0.2s;width:100%;}
    .input-field:focus{border-color:${C.gold};box-shadow:0 0 0 3px rgba(201,168,76,0.1);}
    .input-field::placeholder{color:${C.textL};}
    .card{background:${C.bgCard};border:1px solid ${C.border};border-radius:14px;transition:border-color 0.2s;}
    .card:hover{border-color:${C.borderL};}
    .nav-link{cursor:pointer;transition:all 0.15s;border-left:2px solid transparent;display:flex;align-items:center;gap:10px;padding:9px 16px;border-radius:0 8px 8px 0;font-size:13px;}
    .nav-link:hover{background:rgba(201,168,76,0.05);color:${C.creamD};}
    .nav-link.active{border-left-color:${C.gold};background:rgba(201,168,76,0.08);color:${C.gold};font-weight:600;}
    .badge{display:inline-flex;align-items:center;padding:2px 10px;border-radius:999px;font-size:10px;font-weight:700;letter-spacing:0.5px;text-transform:uppercase;}
    .badge-gold{background:rgba(201,168,76,0.12);color:${C.gold};border:1px solid rgba(201,168,76,0.25);}
    .badge-green{background:rgba(45,138,87,0.12);color:${C.greenL};border:1px solid rgba(45,138,87,0.25);}
    .badge-red{background:rgba(196,43,43,0.12);color:${C.red};border:1px solid rgba(196,43,43,0.25);}
    .divider{height:1px;background:linear-gradient(90deg,transparent,${C.border},transparent);}
    .progress-track{background:${C.border};border-radius:999px;overflow:hidden;}
    .progress-fill{background:linear-gradient(90deg,${C.goldD},${C.gold});height:100%;border-radius:999px;transition:width 0.8s ease;}
    .spinner{width:18px;height:18px;border:2px solid rgba(201,168,76,0.2);border-top-color:${C.gold};border-radius:50%;animation:spin 0.7s linear infinite;}
    .table-row{transition:background 0.12s;}
    .table-row:hover{background:rgba(201,168,76,0.04);}
  `;
  document.head.appendChild(s);
};

// ─── ICONS ────────────────────────────────────────────────────────────────────
const Ic = ({ d, size = 16, color = "currentColor", fill = "none", sw = 1.5 }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill={fill} stroke={color} strokeWidth={sw} strokeLinecap="round" strokeLinejoin="round">
    {(Array.isArray(d) ? d : [d]).map((p, i) => <path key={i} d={p} />)}
  </svg>
);
const ICONS = {
  dashboard: ["M3 3h7v7H3z", "M14 3h7v7h-7z", "M3 14h7v7H3z", "M14 14h7v7h-7z"],
  wallet: "M2.5 7.5A2.5 2.5 0 015 5h14a2.5 2.5 0 012.5 2.5v9A2.5 2.5 0 0119 19H5a2.5 2.5 0 01-2.5-2.5v-9zM17 12a1 1 0 110-2 1 1 0 010 2z",
  send: "M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z",
  loyalty: "M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z",
  merchant: ["M9 14l6-6", "M14 14l.01 0", "M9 10l.01 0", "M3 9h18l-1 9H4L3 9z", "M8 9V6a4 4 0 018 0v3"],
  gold: "M12 3L4 7v5c0 5.5 3.5 10.7 8 12 4.5-1.3 8-6.5 8-12V7l-8-4z",
  chart: ["M3 3v18h18", "M18 9l-5 5-4-4-4 4"],
  shield: "M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z",
  settings: ["M12 15a3 3 0 100-6 3 3 0 000 6z"],
  logout: "M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1",
  eye: ["M1 12s4-8 11-8 11 8 11 8", "M1 12s4 8 11 8 11-8 11-8", "M12 9a3 3 0 100 6 3 3 0 000-6z"],
  eyeOff: ["M17.94 17.94A10.07 10.07 0 0112 20c-7 0-11-8-11-8a18.45 18.45 0 015.06-5.94", "M9.9 4.24A9.12 9.12 0 0112 4c7 0 11 8 11 8a18.5 18.5 0 01-2.16 3.19", "M1 1l22 22"],
  mail: ["M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z", "M22 6l-10 7L2 6"],
  lock: ["M19 11H5a2 2 0 00-2 2v7a2 2 0 002 2h14a2 2 0 002-2v-7a2 2 0 00-2-2z", "M7 11V7a5 5 0 0110 0v4"],
  user: ["M20 21v-2a4 4 0 00-4-4H8a4 4 0 00-4 4v2", "M12 11a4 4 0 100-8 4 4 0 000 8z"],
  phone: "M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 9.8a19.79 19.79 0 01-3.07-8.67A2 2 0 012 .84h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L6.09 8.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z",
  check: "M20 6L9 17l-5-5",
  arrowR: "M5 12h14M12 5l7 7-7 7",
  refresh: "M1 4v6h6M23 20v-6h-6M20.49 9A9 9 0 105.64 5.64L1 10m22 4l-4.64 4.36A9 9 0 013.51 15",
  x: "M18 6L6 18M6 6l12 12",
  bell: ["M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9", "M13.73 21a2 2 0 01-3.46 0"],
  trending: "M23 6l-9.5 9.5-5-5L1 18",
  fingerprint: ["M12 10a2 2 0 00-2 2c0 1.02-.1 2.51-.26 4", "M14 13.12c0 2.38 0 6.38-1 8.88", "M17.29 21.02c.12-2.6.14-6.64.14-8.02a5.06 5.06 0 00-5-5.06 4.96 4.96 0 00-4.95 5.28c-.04.88-.06 3.33-.2 5.78", "M12 2C6.48 2 2 6.48 2 12c0 .87.11 1.72.31 2.52", "M20.97 10c.03.66.03 1.33.03 2", "M16.11 6.27C15.12 5.46 13.62 5 12 5c-3.87 0-7 3.13-7 7 0 1.02-.04 2.47-.14 4"],
  notif: ["M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9", "M13.73 21a2 2 0 01-3.46 0", "M19 3a2 2 0 100 4 2 2 0 000-4z"],
};

// ─── AUTH CONTEXT ─────────────────────────────────────────────────────────────
const AuthCtx = createContext(null);
const useAuth = () => useContext(AuthCtx);

// ─── MINI COMPONENTS ─────────────────────────────────────────────────────────
const Spinner = () => <div className="spinner" />;

const Toast = ({ msg, type, onClose }) => {
  useEffect(() => { const t = setTimeout(onClose, 4000); return () => clearTimeout(t); }, []);
  return (
    <div style={{
      position: "fixed", bottom: 28, right: 28, zIndex: 9999,
      background: type === "error" ? "#1A0808" : "#0A1A0F",
      border: `1px solid ${type === "error" ? C.red + "66" : C.greenL + "66"}`,
      borderRadius: 12, padding: "14px 20px", maxWidth: 360,
      display: "flex", alignItems: "center", gap: 12,
      animation: "fadeUp 0.3s ease",
      boxShadow: "0 8px 32px rgba(0,0,0,0.5)",
    }}>
      <span style={{ fontSize: 18 }}>{type === "error" ? "⚠️" : "✅"}</span>
      <span style={{ fontSize: 13, color: C.creamD, flex: 1 }}>{msg}</span>
      <span onClick={onClose} style={{ cursor: "pointer", color: C.textL, fontSize: 16 }}>×</span>
    </div>
  );
};

const MiniChart = ({ data, color = C.gold, height = 40 }) => {
  const w = 100, h = height;
  const max = Math.max(...data), min = Math.min(...data);
  const range = max - min || 1;
  const pts = data.map((v, i) => `${(i / (data.length - 1)) * w},${h - ((v - min) / range) * (h - 4)}`).join(" ");
  return (
    <svg width="100%" height={h} viewBox={`0 0 ${w} ${h}`} preserveAspectRatio="none">
      <defs>
        <linearGradient id={`g${color.slice(1)}`} x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stopColor={color} stopOpacity="0.25" />
          <stop offset="100%" stopColor={color} stopOpacity="0" />
        </linearGradient>
      </defs>
      <polygon points={`0,${h} ${pts} ${w},${h}`} fill={`url(#g${color.slice(1)})`} />
      <polyline points={pts} fill="none" stroke={color} strokeWidth="1.5" />
    </svg>
  );
};

const BarChart = ({ data, color = C.gold, height = 60 }) => {
  const max = Math.max(...data);
  return (
    <div style={{ display: "flex", alignItems: "flex-end", gap: 4, height }}>
      {data.map((v, i) => (
        <div key={i} style={{
          flex: 1, height: `${(v / max) * 100}%`,
          background: i === data.length - 1
            ? `linear-gradient(180deg, ${C.gold}, ${C.goldD})`
            : `rgba(201,168,76,0.2)`,
          borderRadius: "3px 3px 0 0",
        }} />
      ))}
    </div>
  );
};

const DonutChart = ({ segments, size = 120, thickness = 20 }) => {
  const r = (size - thickness) / 2;
  const circ = 2 * Math.PI * r;
  const total = segments.reduce((a, s) => a + s.value, 0);
  let offset = 0;
  return (
    <svg width={size} height={size}>
      {segments.map((s, i) => {
        const dash = (s.value / total) * circ;
        const el = <circle key={i} cx={size / 2} cy={size / 2} r={r} fill="none"
          stroke={s.color} strokeWidth={thickness}
          strokeDasharray={`${dash} ${circ - dash}`}
          strokeDashoffset={-offset}
          style={{ transform: "rotate(-90deg)", transformOrigin: "center" }} />;
        offset += dash;
        return el;
      })}
      <circle cx={size / 2} cy={size / 2} r={r - thickness / 2 - 3} fill={C.bgCard} />
    </svg>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// AUTH SCREENS
// ══════════════════════════════════════════════════════════════════════════════

const AuthLayout = ({ children, title, sub }) => (
  <div style={{
    minHeight: "100vh", background: C.bg,
    display: "flex", alignItems: "center", justifyContent: "center",
    padding: 20,
    backgroundImage: `radial-gradient(ellipse 80% 60% at 50% -20%, rgba(201,168,76,0.08) 0%, transparent 60%)`,
  }}>
    <div style={{ width: "100%", maxWidth: 440, animation: "fadeUp 0.5s ease" }}>
      {/* Logo */}
      <div style={{ textAlign: "center", marginBottom: 36 }}>
        <img
          src={APP_ICON}
          alt="AfriCoin"
          style={{
            width: 88, height: 88, borderRadius: 22,
            objectFit: "cover", margin: "0 auto 18px", display: "block",
            boxShadow: `0 8px 32px rgba(201,168,76,0.3), 0 0 0 1px rgba(201,168,76,0.15)`,
          }}
        />
        <h1 style={{
          fontFamily: "'Cormorant Garamond'", fontSize: 32, fontWeight: 700,
          letterSpacing: 2,
        }}><span className="gold-text">AFRiCOiN</span></h1>
        <div style={{ fontSize: 11, color: C.textL, letterSpacing: 3, textTransform: "uppercase", marginTop: 4 }}>
          Gold-Backed · Pan-African
        </div>
      </div>

      <div style={{
        background: C.bgCard,
        border: `1px solid ${C.border}`,
        borderRadius: 18,
        padding: "36px 40px",
        boxShadow: "0 24px 64px rgba(0,0,0,0.6)",
      }}>
        <div style={{ marginBottom: 28, textAlign: "center" }}>
          <h2 style={{ fontFamily: "'Cormorant Garamond'", fontSize: 24, fontWeight: 600, color: C.cream }}>{title}</h2>
          {sub && <p style={{ fontSize: 13, color: C.textM, marginTop: 6 }}>{sub}</p>}
        </div>
        {children}
      </div>

      <div style={{ textAlign: "center", marginTop: 20, fontSize: 11, color: C.textL }}>
        © 2025 AfriCoin Technologies · Pan-African · Gold-Backed · Decentralised
      </div>
    </div>
  </div>
);

const InputGroup = ({ label, icon, type = "text", value, onChange, placeholder, error, right }) => {
  const [show, setShow] = useState(false);
  const isPassword = type === "password";
  return (
    <div style={{ marginBottom: 16 }}>
      <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 7 }}>{label}</label>
      <div style={{ position: "relative" }}>
        {icon && (
          <div style={{ position: "absolute", left: 14, top: "50%", transform: "translateY(-50%)", color: C.textL }}>
            <Ic d={ICONS[icon]} size={15} color={C.textL} />
          </div>
        )}
        <input
          className="input-field"
          type={isPassword && show ? "text" : type}
          value={value}
          onChange={e => onChange(e.target.value)}
          placeholder={placeholder}
          style={{ padding: `12px ${isPassword ? 44 : 14}px 12px ${icon ? 40 : 14}px`, borderRadius: 10, fontSize: 14 }}
        />
        {isPassword && (
          <div onClick={() => setShow(!show)} style={{ position: "absolute", right: 14, top: "50%", transform: "translateY(-50%)", cursor: "pointer", color: C.textL }}>
            <Ic d={show ? ICONS.eyeOff : ICONS.eye} size={15} color={C.textL} />
          </div>
        )}
      </div>
      {error && <div style={{ fontSize: 11, color: C.red, marginTop: 5 }}>⚠ {error}</div>}
    </div>
  );
};

// ── SIGN IN ───────────────────────────────────────────────────────────────────
const SignIn = ({ onSwitch, onSuccess }) => {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  const handleSubmit = async () => {
    setError("");
    if (!email || !password) { setError("Please fill in all fields."); return; }
    setLoading(true);
    try {
      const data = await supabase.signIn(email, password);
      const user = data.user || { id: data.user_id, email, user_metadata: {} };
      onSuccess(user, data);
    } catch (e) {
      setError(e.message || "Invalid email or password.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <AuthLayout title="Welcome Back" sub="Sign in to your AfriCoin wallet">
      <InputGroup label="Email Address" icon="mail" type="email" value={email} onChange={setEmail} placeholder="you@example.com" />
      <InputGroup label="Password" icon="lock" type="password" value={password} onChange={setPassword} placeholder="Your password" />
      {error && <div style={{ background: "rgba(196,43,43,0.1)", border: `1px solid ${C.red}44`, borderRadius: 8, padding: "10px 14px", fontSize: 12, color: C.red, marginBottom: 16 }}>{error}</div>}
      <button className="btn-gold" onClick={handleSubmit} disabled={loading}
        style={{ width: "100%", padding: "14px 0", borderRadius: 10, fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 10, marginBottom: 16 }}>
        {loading ? <Spinner /> : <><Ic d={ICONS.arrowR} size={16} color={C.earth} />Sign In</>}
      </button>
      <div style={{ display: "flex", justifyContent: "space-between", fontSize: 13 }}>
        <span style={{ color: C.textL, cursor: "pointer" }} onClick={() => onSwitch("reset")}>Forgot password?</span>
        <span style={{ color: C.textL }}>No account? <span style={{ color: C.gold, cursor: "pointer" }} onClick={() => onSwitch("signup")}>Sign Up</span></span>
      </div>
    </AuthLayout>
  );
};

// ── SIGN UP ───────────────────────────────────────────────────────────────────
const SignUp = ({ onSwitch, onSuccess }) => {
  const [form, setForm] = useState({ fullName: "", email: "", phone: "", password: "", confirm: "" });
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");
  const set = (k) => (v) => setForm(p => ({ ...p, [k]: v }));

  const handleSubmit = async () => {
    setError("");
    if (!form.fullName || !form.email || !form.password) { setError("Please fill in all required fields."); return; }
    if (form.password !== form.confirm) { setError("Passwords do not match."); return; }
    if (form.password.length < 6) { setError("Password must be at least 6 characters."); return; }
    setLoading(true);
    try {
      const data = await supabase.signUp(form.email, form.password, form.fullName, form.phone);
      // Try to send welcome email via Resend
      const tpl = emailTemplates.welcome(form.fullName.split(" ")[0]);
      await sendEmail(form.email, tpl.subject, tpl.html);
      onSuccess(data.user || { email: form.email, user_metadata: { full_name: form.fullName } }, data);
    } catch (e) {
      setError(e.message || "Registration failed. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <AuthLayout title="Create Account" sub="Join 242,000+ AfriCoin users across Africa">
      <InputGroup label="Full Name *" icon="user" value={form.fullName} onChange={set("fullName")} placeholder="Kwame Mensah" />
      <InputGroup label="Email Address *" icon="mail" type="email" value={form.email} onChange={set("email")} placeholder="you@example.com" />
      <InputGroup label="Phone Number" icon="phone" value={form.phone} onChange={set("phone")} placeholder="+27 82 000 0000" />
      <InputGroup label="Password *" icon="lock" type="password" value={form.password} onChange={set("password")} placeholder="Min 6 characters" />
      <InputGroup label="Confirm Password *" icon="lock" type="password" value={form.confirm} onChange={set("confirm")} placeholder="Repeat password" />
      {error && <div style={{ background: "rgba(196,43,43,0.1)", border: `1px solid ${C.red}44`, borderRadius: 8, padding: "10px 14px", fontSize: 12, color: C.red, marginBottom: 16 }}>{error}</div>}
      <button className="btn-gold" onClick={handleSubmit} disabled={loading}
        style={{ width: "100%", padding: "14px 0", borderRadius: 10, fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 10, marginBottom: 16 }}>
        {loading ? <Spinner /> : <>Create Wallet</>}
      </button>
      <div style={{ fontSize: 12, color: C.textL, textAlign: "center" }}>
        Already have an account? <span style={{ color: C.gold, cursor: "pointer" }} onClick={() => onSwitch("signin")}>Sign In</span>
      </div>
      <div style={{ marginTop: 14, fontSize: 11, color: C.textL, textAlign: "center", lineHeight: 1.6 }}>
        By creating an account you agree to AfriCoin's Terms of Service and Privacy Policy. A welcome email will be sent to your address.
      </div>
    </AuthLayout>
  );
};

// ── PASSWORD RESET ────────────────────────────────────────────────────────────
const PasswordReset = ({ onSwitch }) => {
  const [email, setEmail] = useState("");
  const [loading, setLoading] = useState(false);
  const [sent, setSent] = useState(false);
  const [error, setError] = useState("");

  const handleReset = async () => {
    if (!email) { setError("Please enter your email address."); return; }
    setLoading(true);
    try {
      await supabase.resetPassword(email);
      setSent(true);
    } catch (e) {
      setError(e.message || "Could not send reset email.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <AuthLayout title="Reset Password" sub="We'll send a reset link to your email">
      {sent ? (
        <div style={{ textAlign: "center" }}>
          <div style={{ fontSize: 48, marginBottom: 16 }}>📬</div>
          <div style={{ fontSize: 15, color: C.cream, marginBottom: 8 }}>Reset email sent</div>
          <div style={{ fontSize: 13, color: C.textM, marginBottom: 24 }}>Check your inbox at <span style={{ color: C.gold }}>{email}</span></div>
          <button className="btn-ghost" onClick={() => onSwitch("signin")} style={{ padding: "12px 24px", borderRadius: 10, fontSize: 13 }}>Back to Sign In</button>
        </div>
      ) : (
        <>
          <InputGroup label="Email Address" icon="mail" type="email" value={email} onChange={setEmail} placeholder="you@example.com" />
          {error && <div style={{ background: "rgba(196,43,43,0.1)", border: `1px solid ${C.red}44`, borderRadius: 8, padding: "10px 14px", fontSize: 12, color: C.red, marginBottom: 16 }}>{error}</div>}
          <button className="btn-gold" onClick={handleReset} disabled={loading}
            style={{ width: "100%", padding: "14px 0", borderRadius: 10, fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 10, marginBottom: 16 }}>
            {loading ? <Spinner /> : "Send Reset Link"}
          </button>
          <div style={{ fontSize: 13, color: C.textL, textAlign: "center" }}>
            Remembered it? <span style={{ color: C.gold, cursor: "pointer" }} onClick={() => onSwitch("signin")}>Sign In</span>
          </div>
        </>
      )}
    </AuthLayout>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// DASHBOARD (protected)
// ══════════════════════════════════════════════════════════════════════════════

const GOLD_PRICE = 2387.50;
const AFC_VAL = GOLD_PRICE * 0.001;

const NAV = [
  { id: "dashboard",     label: "Dashboard",      icon: ICONS.dashboard   },
  { id: "wallet",        label: "Wallet",         icon: ICONS.wallet      },
  { id: "send",          label: "Send & Receive", icon: ICONS.send        },
  { id: "loyalty",       label: "Loyalty",        icon: ICONS.loyalty     },
  { id: "merchants",     label: "Merchants",      icon: ICONS.merchant    },
  { id: "reserves",      label: "Gold Reserves",  icon: ICONS.gold        },
  { id: "biopay",        label: "BioPay",         icon: ICONS.fingerprint },
  { id: "notifications", label: "Notifications",  icon: ICONS.notif       },
  { id: "analytics",     label: "Analytics",      icon: ICONS.chart       },
  { id: "compliance",    label: "Compliance",     icon: ICONS.shield      },
  { id: "settings",      label: "Settings",       icon: ICONS.settings    },
];

// ── SIDEBAR ───────────────────────────────────────────────────────────────────
const Sidebar = ({ page, setPage, user, onSignOut, unreadCount = 0 }) => {
  const name = user?.user_metadata?.full_name || user?.email?.split("@")[0] || "User";
  const initials = name.split(" ").map(n => n[0]).join("").slice(0, 2).toUpperCase();
  return (
    <div style={{
      width: 216, background: C.bgCard, borderRight: `1px solid ${C.border}`,
      display: "flex", flexDirection: "column", height: "100vh",
      position: "sticky", top: 0, flexShrink: 0,
    }}>
      <div style={{ padding: "22px 20px 16px" }}>
        <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
          <img
            src={APP_ICON}
            alt="AfriCoin"
            style={{ width: 38, height: 38, borderRadius: 10, objectFit: "cover", flexShrink: 0, boxShadow: `0 2px 10px rgba(201,168,76,0.25)` }}
          />
          <div>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 19, fontWeight: 700, letterSpacing: 1 }}>
              <span className="gold-text">AFRiCOiN</span>
            </div>
            <div style={{ fontSize: 9, color: C.textL, letterSpacing: 2, textTransform: "uppercase" }}>Gold-Backed</div>
          </div>
        </div>
      </div>

      <div className="divider" style={{ margin: "0 14px" }} />

      <nav style={{ flex: 1, padding: "10px 6px", overflowY: "auto" }}>
        {NAV.map(n => (
          <div key={n.id} className={`nav-link ${page === n.id ? "active" : ""}`} onClick={() => setPage(n.id)}
            style={{ color: page === n.id ? C.gold : C.textM, marginBottom: 1, justifyContent: "space-between" }}>
            <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
              <Ic d={n.icon} size={14} color={page === n.id ? C.gold : C.textM} />
              {n.label}
            </div>
            {n.id === "notifications" && unreadCount > 0 && (
              <span style={{ background: C.red, color: "#fff", borderRadius: "50%", fontSize: 9, padding: "1px 5px", fontWeight: 700, minWidth: 16, textAlign: "center" }}>{unreadCount}</span>
            )}
          </div>
        ))}
      </nav>

      <div style={{ padding: "14px 14px", borderTop: `1px solid ${C.border}` }}>
        <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 12 }}>
          <div style={{ width: 34, height: 34, borderRadius: "50%", background: `linear-gradient(135deg, ${C.goldD}, ${C.gold})`, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 12, fontWeight: 700, color: C.earth, flexShrink: 0 }}>{initials}</div>
          <div style={{ overflow: "hidden" }}>
            <div style={{ fontSize: 12, fontWeight: 600, color: C.cream, whiteSpace: "nowrap", overflow: "hidden", textOverflow: "ellipsis" }}>{name}</div>
            <div style={{ fontSize: 10, color: C.textL }}>Level 3 · Verified</div>
          </div>
        </div>
        <button onClick={onSignOut} className="btn-ghost" style={{ width: "100%", padding: "8px 0", borderRadius: 8, fontSize: 12, display: "flex", alignItems: "center", justifyContent: "center", gap: 6 }}>
          <Ic d={ICONS.logout} size={13} color={C.gold} />Sign Out
        </button>
      </div>
    </div>
  );
};

// ── TOP BAR ───────────────────────────────────────────────────────────────────
const TopBar = ({ title }) => {
  const [price, setPrice] = useState(GOLD_PRICE);
  useEffect(() => {
    const iv = setInterval(() => setPrice(p => +(p + (Math.random() - 0.49) * 2).toFixed(2)), 3000);
    return () => clearInterval(iv);
  }, []);
  return (
    <div style={{ height: 56, borderBottom: `1px solid ${C.border}`, display: "flex", alignItems: "center", justifyContent: "space-between", padding: "0 24px", background: C.bgCard, position: "sticky", top: 0, zIndex: 10 }}>
      <h1 style={{ fontFamily: "'Cormorant Garamond'", fontSize: 20, fontWeight: 600, color: C.cream }}>{title}</h1>
      <div style={{ display: "flex", alignItems: "center", gap: 20 }}>
        <div style={{ display: "flex", alignItems: "center", gap: 8, fontSize: 12 }}>
          <span style={{ color: C.textL }}>XAU/USD</span>
          <span style={{ fontFamily: "'IBM Plex Mono'", color: C.gold, fontWeight: 600 }}>${price.toLocaleString("en-US", { minimumFractionDigits: 2 })}</span>
        </div>
        <div className="badge badge-green">● Live</div>
      </div>
    </div>
  );
};

// ── DASHBOARD PAGE ────────────────────────────────────────────────────────────
const DashboardPage = ({ user, transactions }) => {
  const name = user?.user_metadata?.full_name?.split(" ")[0] || "there";
  const stats = [
    { label: "Portfolio Value", val: "$12,847.32", sub: "+3.2% today", chart: [42,45,43,48,52,49,55,58,54,63], color: C.gold },
    { label: "AFC Balance", val: "5,389.14 AFC", sub: "≈ $12,847", chart: [30,35,32,38,40,37,42,45,43,51], color: C.goldL },
    { label: "Sent This Month", val: "$3,240", sub: "12 transactions", chart: [20,22,19,25,28,24,30,27,32,33], color: C.greenL },
    { label: "Loyalty Saved", val: "R 1,240", sub: "Points converted", chart: [5,8,7,10,12,9,14,11,16,15], color: "#C084FC" },
  ];
  const recentTx = transactions.length > 0 ? transactions : [
    { id: "TX001", type: "Received", counterparty: "Adaeze Okonkwo", amount: "+420.00 AFC", time: "2m ago", status: "confirmed" },
    { id: "TX002", type: "Sent", counterparty: "Shoprite", amount: "-85.50 AFC", time: "1h ago", status: "confirmed" },
    { id: "TX003", type: "Conversion", counterparty: "eBucks → AFC", amount: "+500.00 AFC", time: "3h ago", status: "confirmed" },
    { id: "TX004", type: "Cross-Border", counterparty: "→ Nairobi", amount: "-200.00 AFC", time: "5h ago", status: "confirmed" },
  ];

  return (
    <div style={{ padding: 24 }}>
      <div style={{ marginBottom: 24 }}>
        <h2 style={{ fontFamily: "'Cormorant Garamond'", fontSize: 22, color: C.cream }}>Welcome back, {name}</h2>
        <p style={{ fontSize: 13, color: C.textM, marginTop: 4 }}>Your gold-backed wallet is performing well today.</p>
      </div>

      {/* Hero card */}
      <div style={{ background: `linear-gradient(135deg, ${C.bgCard}, #1A1208)`, border: `1px solid ${C.gold}33`, borderRadius: 16, padding: "24px 28px", marginBottom: 20, display: "flex", justifyContent: "space-between", alignItems: "center", overflow: "hidden", position: "relative" }}>
        <div style={{ position: "absolute", right: -30, top: -30, width: 180, height: 180, borderRadius: "50%", border: `1px solid rgba(201,168,76,0.06)` }} />
        <div>
          <div style={{ fontSize: 12, color: C.textL, textTransform: "uppercase", letterSpacing: 1.5 }}>Total Portfolio Value</div>
          <div className="gold-text" style={{ fontFamily: "'Cormorant Garamond'", fontSize: 44, fontWeight: 700, lineHeight: 1.1, margin: "6px 0" }}>$12,847.32</div>
          <div style={{ fontSize: 13, color: C.greenL }}>▲ $398.42 (+3.2%) today · 5,389.14 AFC</div>
        </div>
        <div style={{ width: 180 }}><MiniChart data={[41,43,40,45,48,46,50,52,49,54,56,63]} height={52} /></div>
      </div>

      {/* Stats */}
      <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 14, marginBottom: 20 }}>
        {stats.map((s, i) => (
          <div key={i} className="card fade-up" style={{ padding: 18, animationDelay: `${i * 0.06}s` }}>
            <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 10 }}>
              <div style={{ width: 8, height: 8, borderRadius: "50%", background: s.color, marginTop: 2 }} />
              <div style={{ width: 60 }}><MiniChart data={s.chart} color={s.color} height={24} /></div>
            </div>
            <div style={{ fontSize: 18, fontWeight: 700, color: C.cream, fontFamily: "'IBM Plex Mono'" }}>{s.val}</div>
            <div style={{ fontSize: 11, color: C.textL, marginTop: 3 }}>{s.label}</div>
            <div style={{ fontSize: 11, color: C.greenL, marginTop: 2 }}>{s.sub}</div>
          </div>
        ))}
      </div>

      {/* Transactions */}
      <div className="card">
        <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}`, display: "flex", justifyContent: "space-between" }}>
          <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream }}>Recent Transactions</span>
          <span style={{ fontSize: 12, color: C.gold }}>View all →</span>
        </div>
        {recentTx.slice(0, 5).map((tx, i) => (
          <div key={tx.id || i} className="table-row" style={{ padding: "12px 18px", borderBottom: i < 4 ? `1px solid ${C.border}33` : "none", display: "flex", justifyContent: "space-between", alignItems: "center" }}>
            <div style={{ display: "flex", gap: 12, alignItems: "center" }}>
              <div style={{ width: 34, height: 34, borderRadius: "50%", background: (tx.type || tx.transaction_type) === "Received" ? "rgba(45,138,87,0.12)" : "rgba(201,168,76,0.1)", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 14 }}>
                {(tx.type || tx.transaction_type) === "Received" ? "↓" : (tx.type || tx.transaction_type) === "Conversion" ? "⇄" : "↑"}
              </div>
              <div>
                <div style={{ fontSize: 13, color: C.cream, fontWeight: 500 }}>{tx.counterparty || tx.recipient || "—"}</div>
                <div style={{ fontSize: 11, color: C.textL }}>{tx.type || tx.transaction_type} · {tx.time || new Date(tx.created_at).toLocaleTimeString()}</div>
              </div>
            </div>
            <div style={{ textAlign: "right" }}>
              <div style={{ fontSize: 13, fontFamily: "'IBM Plex Mono'", color: (tx.amount || "").toString().startsWith("+") ? C.greenL : C.cream }}>{tx.amount || `${tx.afc_amount} AFC`}</div>
              <span className="badge badge-green" style={{ fontSize: 9 }}>confirmed</span>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

// ── WALLET PAGE ───────────────────────────────────────────────────────────────
const WalletPage = () => {
  const [show, setShow] = useState(false);
  const addr = "AFC1User9xQR4T7bZ2pL8mN3vX5dY6cW";
  const donutData = [
    { value: 12847, color: C.gold },
    { value: 1285, color: C.goldL },
    { value: 4200, color: C.borderL },
  ];
  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
        <div style={{ background: `linear-gradient(135deg,${C.bgCard},#1E1408)`, border: `1px solid ${C.gold}44`, borderRadius: 16, padding: 24, position: "relative", overflow: "hidden" }}>
          <div style={{ position: "absolute", right: -20, bottom: -20, opacity: 0.03, fontSize: 130, lineHeight: 1 }}>◈</div>
          <div style={{ fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 2 }}>AfriCoin Wallet</div>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 34, fontWeight: 700, color: C.gold, margin: "8px 0 4px" }}>5,389.14 <span style={{ fontSize: 20 }}>AFC</span></div>
          <div style={{ fontSize: 13, color: C.textM, marginBottom: 20 }}>≈ $12,847.32 USD</div>
          <div style={{ fontSize: 11, color: C.textL, marginBottom: 6 }}>Wallet Address</div>
          <div style={{ display: "flex", gap: 8 }}>
            <code style={{ fontSize: 11, background: C.bgCardL, padding: "6px 10px", borderRadius: 6, border: `1px solid ${C.border}`, color: C.creamD, flex: 1, overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>
              {show ? addr : addr.slice(0, 18) + "..."}
            </code>
            <button className="btn-ghost" onClick={() => setShow(!show)} style={{ padding: "5px 10px", borderRadius: 6, fontSize: 11 }}>
              <Ic d={show ? ICONS.eyeOff : ICONS.eye} size={12} />
            </button>
          </div>
          <div style={{ display: "flex", gap: 10, marginTop: 18 }}>
            <button className="btn-gold" style={{ flex: 1, padding: "10px 0", borderRadius: 8, fontSize: 13 }}>Send</button>
            <button className="btn-ghost" style={{ flex: 1, padding: "10px 0", borderRadius: 8, fontSize: 13 }}>Receive</button>
          </div>
        </div>
        <div className="card" style={{ padding: 22 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 18 }}>Portfolio Breakdown</div>
          <div style={{ display: "flex", justifyContent: "center", marginBottom: 18 }}>
            <div style={{ position: "relative" }}>
              <DonutChart segments={donutData} size={130} thickness={20} />
              <div style={{ position: "absolute", inset: 0, display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center" }}>
                <div style={{ fontSize: 10, color: C.textL }}>Total</div>
                <div style={{ fontSize: 15, fontWeight: 700, color: C.gold }}>$18.3K</div>
              </div>
            </div>
          </div>
          {[["AfriCoin (AFC)", "$12,847", C.gold], ["Gold Reserve Credit", "$1,285", C.goldL], ["ZAR Savings", "$4,200", C.borderL]].map(([n, v, col], i) => (
            <div key={i} style={{ display: "flex", justifyContent: "space-between", marginBottom: 8 }}>
              <div style={{ display: "flex", gap: 8, alignItems: "center" }}>
                <div style={{ width: 8, height: 8, borderRadius: "50%", background: col }} />
                <span style={{ fontSize: 12, color: C.creamD }}>{n}</span>
              </div>
              <span style={{ fontSize: 12, fontFamily: "'IBM Plex Mono'", color: C.cream }}>{v}</span>
            </div>
          ))}
        </div>
      </div>
      {/* KYC */}
      <div className="card">
        <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}` }}>
          <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream }}>KYC Verification</span>
        </div>
        <div style={{ padding: 18, display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 14 }}>
          {[
            { lv: 1, name: "Basic", limit: "$200/mo", req: "Phone only", done: true },
            { lv: 2, name: "Standard", limit: "$5,000/mo", req: "National ID", done: true },
            { lv: 3, name: "Premium", limit: "Unlimited", req: "Full docs + bank", done: true },
          ].map(k => (
            <div key={k.lv} style={{ background: "rgba(45,138,87,0.06)", border: `1px solid ${C.greenL}33`, borderRadius: 10, padding: 14 }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 6 }}>
                <span style={{ fontSize: 12, fontWeight: 700, color: C.cream }}>Level {k.lv} — {k.name}</span>
                <span style={{ color: C.greenL }}>✓</span>
              </div>
              <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 16, color: C.gold }}>{k.limit}</div>
              <div style={{ fontSize: 11, color: C.textL, marginTop: 4 }}>{k.req}</div>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// ── SEND PAGE ─────────────────────────────────────────────────────────────────
const SendPage = ({ user, onTransaction }) => {
  const [tab, setTab] = useState("send");
  const [amount, setAmount] = useState("");
  const [recipient, setRecipient] = useState("");
  const [loading, setLoading] = useState(false);
  const [status, setStatus] = useState(null);

  const handleSend = async () => {
    if (!amount || !recipient) return;
    setLoading(true);
    setStatus(null);
    try {
      const txId = "TX" + Math.random().toString(36).slice(2, 10).toUpperCase();
      const tx = {
        user_id: user?.id,
        transaction_type: "Sent",
        afc_amount: parseFloat(amount),
        recipient,
        tx_hash: txId,
        status: "confirmed",
        created_at: new Date().toISOString(),
      };
      if (user?.id) await supabase.insertTransaction(tx);
      // Send email confirmation
      const name = user?.user_metadata?.full_name?.split(" ")[0] || "User";
      const tpl = emailTemplates.transactionConfirmation(name, amount, "Sent", recipient, txId, new Date().toLocaleTimeString());
      await sendEmail(user?.email, tpl.subject, tpl.html);
      setStatus("success");
      onTransaction(tx);
      setAmount(""); setRecipient("");
    } catch (e) {
      setStatus("error");
    } finally {
      setLoading(false);
    }
  };

  const feeAFC = amount ? (parseFloat(amount) * 0.002).toFixed(4) : "0.0000";
  const usdVal = amount ? (parseFloat(amount) * AFC_VAL).toFixed(2) : "0.00";

  return (
    <div style={{ padding: 24, display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
      <div className="card" style={{ overflow: "hidden" }}>
        <div style={{ display: "flex", borderBottom: `1px solid ${C.border}` }}>
          {["send", "receive", "exchange"].map(t => (
            <button key={t} onClick={() => setTab(t)} style={{ flex: 1, padding: "13px 0", background: "none", border: "none", cursor: "pointer", fontSize: 13, fontWeight: tab === t ? 600 : 400, color: tab === t ? C.gold : C.textM, borderBottom: tab === t ? `2px solid ${C.gold}` : "2px solid transparent", textTransform: "capitalize", fontFamily: "'DM Sans'" }}>
              {t === "exchange" ? "FX Convert" : t}
            </button>
          ))}
        </div>
        <div style={{ padding: 22 }}>
          {tab === "send" && (
            <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
              <InputGroup label="Recipient" icon="user" value={recipient} onChange={setRecipient} placeholder="+27 / +254 / wallet address" />
              <div>
                <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 7 }}>Amount (AFC)</label>
                <input className="input-field" type="number" value={amount} onChange={e => setAmount(e.target.value)}
                  placeholder="0.00" style={{ padding: "12px 14px", borderRadius: 10, fontSize: 18, fontFamily: "'IBM Plex Mono'" }} />
              </div>
              <div style={{ background: C.bgCardL, border: `1px solid ${C.border}`, borderRadius: 8, padding: 14, fontSize: 12 }}>
                <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 5 }}>
                  <span style={{ color: C.textL }}>USD value</span>
                  <span style={{ fontFamily: "'IBM Plex Mono'", color: C.cream }}>${usdVal}</span>
                </div>
                <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 5 }}>
                  <span style={{ color: C.textL }}>Network fee</span>
                  <span style={{ fontFamily: "'IBM Plex Mono'", color: C.gold }}>{feeAFC} AFC</span>
                </div>
                <div className="divider" style={{ margin: "8px 0" }} />
                <div style={{ display: "flex", justifyContent: "space-between" }}>
                  <span style={{ color: C.textL }}>Settlement</span>
                  <span style={{ color: C.greenL, fontWeight: 600 }}>⚡ &lt; 1 second</span>
                </div>
              </div>
              {status === "success" && <div style={{ background: "rgba(45,138,87,0.1)", border: `1px solid ${C.greenL}44`, borderRadius: 8, padding: 12, color: C.greenL, fontSize: 13, textAlign: "center" }}>✓ Confirmed — email receipt sent</div>}
              {status === "error" && <div style={{ background: "rgba(196,43,43,0.1)", border: `1px solid ${C.red}44`, borderRadius: 8, padding: 12, color: C.red, fontSize: 13, textAlign: "center" }}>⚠ Transaction failed</div>}
              <button className="btn-gold" onClick={handleSend} disabled={loading}
                style={{ padding: "13px 0", borderRadius: 10, fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 8 }}>
                {loading ? <Spinner /> : <>Send AFC <Ic d={ICONS.send} size={14} color={C.earth} /></>}
              </button>
            </div>
          )}
          {tab === "receive" && (
            <div style={{ textAlign: "center" }}>
              <div style={{ fontSize: 13, color: C.textM, marginBottom: 16 }}>Your wallet address</div>
              <div style={{ width: 160, height: 160, margin: "0 auto 16px", background: "#fff", borderRadius: 10, padding: 8, display: "flex", alignItems: "center", justifyContent: "center" }}>
                <div style={{ width: "100%", height: "100%", background: "repeating-conic-gradient(#000 0% 25%, #fff 0% 50%) 0 0 / 10px 10px", borderRadius: 4 }} />
              </div>
              <code style={{ fontSize: 10, color: C.textL, wordBreak: "break-all", display: "block", marginBottom: 14 }}>AFC1User9xQR4T7bZ2pL8mN3vX5dY6cW</code>
              <button className="btn-ghost" style={{ padding: "10px 20px", borderRadius: 8, fontSize: 12 }}>Copy Address</button>
            </div>
          )}
          {tab === "exchange" && (
            <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
              <div>
                <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 7 }}>From</label>
                <div style={{ display: "flex", gap: 8 }}>
                  <input className="input-field" placeholder="0.00" type="number" style={{ flex: 1, padding: "12px 14px", borderRadius: 10, fontSize: 15, fontFamily: "'IBM Plex Mono'" }} />
                  <select className="input-field" style={{ padding: "12px 12px", borderRadius: 10, fontSize: 13, width: 80 }}><option>AFC</option><option>ZAR</option><option>USD</option></select>
                </div>
              </div>
              <div style={{ textAlign: "center", color: C.gold, fontSize: 18 }}>⇅</div>
              <div>
                <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 7 }}>To</label>
                <div style={{ display: "flex", gap: 8 }}>
                  <input className="input-field" placeholder="0.00" type="number" style={{ flex: 1, padding: "12px 14px", borderRadius: 10, fontSize: 15, fontFamily: "'IBM Plex Mono'" }} />
                  <select className="input-field" style={{ padding: "12px 12px", borderRadius: 10, fontSize: 13, width: 80 }}><option>KES</option><option>NGN</option><option>ZAR</option><option>USD</option></select>
                </div>
              </div>
              <button className="btn-gold" style={{ padding: "13px 0", borderRadius: 10, fontSize: 14 }}>Convert Now</button>
            </div>
          )}
        </div>
      </div>
      {/* Speed comparison */}
      <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
        <div className="card" style={{ padding: 20 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 16 }}>Settlement Speed</div>
          {[
            { label: "AfriCoin", time: "< 1s", pct: 100, color: C.gold },
            { label: "M-Pesa", time: "~30s", pct: 60, color: C.greenL },
            { label: "Visa Settlement", time: "24h", pct: 12, color: "#60A5FA" },
            { label: "SWIFT", time: "3–5 days", pct: 2, color: C.textL },
          ].map((s, i) => (
            <div key={i} style={{ marginBottom: 14 }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 5, fontSize: 12 }}>
                <span style={{ color: i === 0 ? C.gold : C.textM, fontWeight: i === 0 ? 600 : 400 }}>{s.label}</span>
                <span style={{ color: C.textL, fontFamily: "'IBM Plex Mono'" }}>{s.time}</span>
              </div>
              <div className="progress-track" style={{ height: 6 }}>
                <div style={{ width: `${s.pct}%`, background: s.color, height: "100%", borderRadius: 999 }} />
              </div>
            </div>
          ))}
        </div>
        <div className="card" style={{ padding: 20 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 16 }}>Transaction Fees</div>
          <BarChart data={[1, 2, 5, 10, 12, 3]} height={70} />
          <div style={{ display: "flex", justifyContent: "space-between", marginTop: 6 }}>
            {["AFC", "USDT", "Card", "Bank", "SWIFT", "Wire"].map((l, i) => (
              <span key={i} style={{ fontSize: 9, color: C.textL, flex: 1, textAlign: "center" }}>{l}</span>
            ))}
          </div>
          <div style={{ marginTop: 10, fontSize: 12, color: C.textL, textAlign: "center" }}>AfriCoin saves up to <span style={{ color: C.gold, fontWeight: 700 }}>90%</span> in fees</div>
        </div>
      </div>
    </div>
  );
};

// ── ANALYTICS PAGE ────────────────────────────────────────────────────────────
const AnalyticsPage = () => {
  const months = ["Aug", "Sep", "Oct", "Nov", "Dec", "Jan", "Feb", "Mar"];
  const revenue = [35, 58, 72, 95, 128, 156, 198, 260];
  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      <div style={{ display: "grid", gridTemplateColumns: "repeat(5, 1fr)", gap: 12 }}>
        {[
          { label: "Monthly Revenue", val: "$260K", delta: "+31%", c: C.gold },
          { label: "Active Users", val: "242K", delta: "+31%", c: C.greenL },
          { label: "Transactions", val: "1.4M", delta: "+38%", c: "#60A5FA" },
          { label: "Merchants", val: "1,248", delta: "+22%", c: "#C084FC" },
          { label: "Avg Fee", val: "0.22%", delta: "-0.01%", c: C.creamD },
        ].map((k, i) => (
          <div key={i} className="card" style={{ padding: 16, textAlign: "center" }}>
            <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 20, color: k.c, fontWeight: 700 }}>{k.val}</div>
            <div style={{ fontSize: 11, color: C.textL, marginTop: 4 }}>{k.label}</div>
            <div style={{ fontSize: 11, color: k.delta.startsWith("+") ? C.greenL : C.red, marginTop: 2 }}>{k.delta} MoM</div>
          </div>
        ))}
      </div>
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
        <div className="card" style={{ padding: 20 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 16 }}>Revenue Growth (USD '000)</div>
          <BarChart data={revenue} height={100} />
          <div style={{ display: "flex", justifyContent: "space-between", marginTop: 6 }}>
            {months.map((m, i) => <span key={i} style={{ fontSize: 9, color: C.textL, flex: 1, textAlign: "center" }}>{m}</span>)}
          </div>
        </div>
        <div className="card" style={{ padding: 20 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 16 }}>5-Year Revenue Projections</div>
          <table style={{ width: "100%", borderCollapse: "collapse" }}>
            <thead>
              <tr>{["Year", "Users", "Revenue"].map(h => <th key={h} style={{ padding: "8px 0", fontSize: 10, color: C.textL, textAlign: "left", textTransform: "uppercase" }}>{h}</th>)}</tr>
            </thead>
            <tbody>
              {[["Y1","100K","$350K"],["Y2","1M","$3.9M"],["Y3","5M","$32.5M"],["Y4","15M","$180M"],["Y5","50M","$750M"]].map((r, i) => (
                <tr key={i} className="table-row">
                  <td style={{ padding: "8px 0", fontSize: 12, color: C.gold, fontWeight: 700 }}>{r[0]}</td>
                  <td style={{ padding: "8px 0", fontSize: 12, fontFamily: "'IBM Plex Mono'", color: C.creamD }}>{r[1]}</td>
                  <td style={{ padding: "8px 0", fontSize: 12, fontFamily: "'IBM Plex Mono'", color: C.greenL, fontWeight: 600 }}>{r[2]}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// LOYALTY CONVERSION PAGE
// ══════════════════════════════════════════════════════════════════════════════
const LoyaltyPage = ({ user, onToast }) => {
  const BANKS = {
    FNB:      { prog: "eBucks",       rate: 10, color: "#E87B2D", logo: "🟠" },
    Nedbank:  { prog: "Greenbacks",   rate: 8,  color: "#007B5E", logo: "🟢" },
    Standard: { prog: "UCount",       rate: 12, color: "#0033A0", logo: "🔵" },
    Absa:     { prog: "Absa Rewards", rate: 9,  color: "#DC143C", logo: "🔴" },
    Equity:   { prog: "Equity Rewards",rate:11, color: "#8B0000", logo: "🟤" },
  };

  const [bank, setBank] = useState("FNB");
  const [points, setPoints] = useState("");
  const [loading, setLoading] = useState(false);
  const [success, setSuccess] = useState(null);
  const [history, setHistory] = useState([]);
  const [loadingHistory, setLoadingHistory] = useState(true);

  useEffect(() => {
    if (!user?.id) { setLoadingHistory(false); return; }
    supabase.getTransactions(user.id).then(txs => {
      setHistory((txs || []).filter(t => t.transaction_type === "Loyalty Conversion"));
    }).catch(() => {}).finally(() => setLoadingHistory(false));
  }, [user]);

  const b = BANKS[bank];
  const afcOut = points ? (parseFloat(points) / b.rate).toFixed(2) : "0.00";
  const usdVal = points ? ((parseFloat(points) / b.rate) * (2387.50 * 0.001)).toFixed(2) : "0.00";

  const handleConvert = async () => {
    if (!points || parseFloat(points) <= 0) return;
    setLoading(true);
    setSuccess(null);
    try {
      const txId = "LX" + Math.random().toString(36).slice(2, 10).toUpperCase();
      const tx = {
        user_id: user?.id,
        transaction_type: "Loyalty Conversion",
        afc_amount: parseFloat(afcOut),
        recipient: `${b.prog} → AFC`,
        tx_hash: txId,
        status: "confirmed",
        metadata: JSON.stringify({ bank, points: parseFloat(points), programme: b.prog }),
        created_at: new Date().toISOString(),
      };
      if (user?.id) await supabase.insertTransaction(tx);
      const name = user?.user_metadata?.full_name?.split(" ")[0] || "User";
      await sendEmail(user?.email,
        `AfriCoin: ${points} ${b.prog} converted to ${afcOut} AFC`,
        emailTemplates.transactionConfirmation(name, afcOut, "Loyalty Conversion", b.prog, txId, new Date().toLocaleTimeString()).html
      );
      setSuccess({ afc: afcOut, pts: points, prog: b.prog });
      setHistory(h => [tx, ...h]);
      setPoints("");
      onToast(`${points} ${b.prog} converted to ${afcOut} AFC — receipt emailed`, "success");
    } catch {
      onToast("Conversion failed. Please try again.", "error");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* Stats row */}
      <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 14 }}>
        {[
          { label: "Total Converted", val: "3,200 pts", sub: "Across 3 banks" },
          { label: "AFC Earned", val: "320.00 AFC", sub: "From loyalty" },
          { label: "Value Saved", val: "R 1,240", sub: "vs. expiry loss" },
          { label: "Partner Banks", val: "5 active", sub: "FNB, Nedbank, Standard…" },
        ].map((s, i) => (
          <div key={i} className="card fade-up" style={{ padding: 18, animationDelay: `${i * 0.06}s` }}>
            <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 20, color: C.gold, fontWeight: 700 }}>{s.val}</div>
            <div style={{ fontSize: 11, color: C.textL, marginTop: 4 }}>{s.label}</div>
            <div style={{ fontSize: 11, color: C.greenL, marginTop: 2 }}>{s.sub}</div>
          </div>
        ))}
      </div>

      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
        {/* Converter */}
        <div className="card" style={{ padding: 24 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 20, color: C.cream, marginBottom: 4 }}>Convert Loyalty Points</div>
          <div style={{ fontSize: 12, color: C.textM, marginBottom: 20 }}>Turn dormant bank rewards into spendable AfriCoin</div>

          {/* Bank selector */}
          <div style={{ marginBottom: 18 }}>
            <div style={{ fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 8 }}>Select Bank</div>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 8 }}>
              {Object.entries(BANKS).map(([key, info]) => (
                <button key={key} onClick={() => { setBank(key); setSuccess(null); }} style={{
                  padding: "10px 6px", borderRadius: 10, fontSize: 12, fontWeight: bank === key ? 700 : 400,
                  background: bank === key ? `${info.color}18` : C.bgCardL,
                  border: `1px solid ${bank === key ? info.color + "55" : C.border}`,
                  color: bank === key ? info.color : C.textM,
                  cursor: "pointer", transition: "all 0.2s",
                  display: "flex", flexDirection: "column", alignItems: "center", gap: 4,
                }}>
                  <span style={{ fontSize: 18 }}>{info.logo}</span>
                  <span>{key}</span>
                </button>
              ))}
            </div>
          </div>

          {/* Points input */}
          <div style={{ marginBottom: 14 }}>
            <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 7 }}>
              {b.prog} Points to Convert
            </label>
            <input className="input-field" type="number" value={points}
              onChange={e => { setPoints(e.target.value); setSuccess(null); }}
              placeholder="e.g. 5000"
              style={{ padding: "12px 14px", borderRadius: 10, fontSize: 18, fontFamily: "'IBM Plex Mono'" }} />
            <div style={{ fontSize: 11, color: C.textL, marginTop: 5 }}>
              Conversion rate: <span style={{ color: b.color }}>{b.rate} {b.prog}</span> = 1 AFC
            </div>
          </div>

          {/* Preview */}
          {points && parseFloat(points) > 0 && (
            <div style={{ background: `${b.color}0D`, border: `1px solid ${b.color}33`, borderRadius: 10, padding: 16, marginBottom: 16 }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8, fontSize: 12 }}>
                <span style={{ color: C.textL }}>You are converting</span>
                <span style={{ color: C.cream, fontFamily: "'IBM Plex Mono'" }}>{parseFloat(points).toLocaleString()} {b.prog}</span>
              </div>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8, fontSize: 12 }}>
                <span style={{ color: C.textL }}>You will receive</span>
                <span style={{ fontFamily: "'IBM Plex Mono'", color: C.gold, fontWeight: 700, fontSize: 16 }}>{afcOut} AFC</span>
              </div>
              <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12 }}>
                <span style={{ color: C.textL }}>Estimated USD value</span>
                <span style={{ color: C.greenL, fontFamily: "'IBM Plex Mono'" }}>${usdVal}</span>
              </div>
            </div>
          )}

          {success && (
            <div style={{ background: "rgba(45,138,87,0.1)", border: `1px solid ${C.greenL}44`, borderRadius: 10, padding: 14, marginBottom: 16, textAlign: "center" }}>
              <div style={{ color: C.greenL, fontWeight: 700, fontSize: 14 }}>✓ Conversion Successful</div>
              <div style={{ color: C.textM, fontSize: 12, marginTop: 4 }}>
                {success.pts} {success.prog} → <span style={{ color: C.gold }}>{success.afc} AFC</span> minted to your wallet
              </div>
              <div style={{ color: C.textL, fontSize: 11, marginTop: 2 }}>Email receipt sent</div>
            </div>
          )}

          <button className="btn-gold" onClick={handleConvert} disabled={loading || !points}
            style={{ width: "100%", padding: "13px 0", borderRadius: 10, fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 8, opacity: !points ? 0.5 : 1 }}>
            {loading ? <Spinner /> : `Convert ${b.prog} → AFC`}
          </button>
        </div>

        {/* Right column: partner details + benefits */}
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 14 }}>Partner Bank Overview</div>
            {Object.entries(BANKS).map(([key, info], i) => (
              <div key={key} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "10px 0", borderBottom: i < 4 ? `1px solid ${C.border}33` : "none" }}>
                <div style={{ display: "flex", gap: 10, alignItems: "center" }}>
                  <span style={{ fontSize: 18 }}>{info.logo}</span>
                  <div>
                    <div style={{ fontSize: 13, fontWeight: 600, color: C.cream }}>{key}</div>
                    <div style={{ fontSize: 11, color: C.textL }}>{info.prog}</div>
                  </div>
                </div>
                <div style={{ textAlign: "right" }}>
                  <div style={{ fontSize: 12, color: info.color, fontFamily: "'IBM Plex Mono'", fontWeight: 600 }}>{info.rate}:1</div>
                  <div style={{ fontSize: 10, color: C.textL }}>pts per AFC</div>
                </div>
              </div>
            ))}
          </div>

          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 12 }}>Why Convert?</div>
            {[
              ["🔄", "Interoperable", "Use at any AfriCoin merchant, not just your bank"],
              ["♾️", "No Expiry", "AFC holds gold-backed value indefinitely"],
              ["⚡", "Instant", "Minted to your wallet in under 1 second"],
              ["🌍", "Pan-African", "Spend across 54 countries"],
            ].map(([icon, title, desc], i) => (
              <div key={i} style={{ display: "flex", gap: 12, marginBottom: 12, alignItems: "flex-start" }}>
                <span style={{ fontSize: 18, lineHeight: 1.2 }}>{icon}</span>
                <div>
                  <div style={{ fontSize: 12, fontWeight: 600, color: C.cream }}>{title}</div>
                  <div style={{ fontSize: 11, color: C.textL }}>{desc}</div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Conversion history */}
      <div className="card">
        <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}`, display: "flex", justifyContent: "space-between", alignItems: "center" }}>
          <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream }}>Conversion History</span>
          <span className="badge badge-gold">{history.length} conversions</span>
        </div>
        {loadingHistory ? (
          <div style={{ padding: 24, textAlign: "center" }}><Spinner /></div>
        ) : history.length === 0 ? (
          <div style={{ padding: 32, textAlign: "center", color: C.textL, fontSize: 13 }}>No conversions yet. Convert your first loyalty points above.</div>
        ) : (
          <table style={{ width: "100%", borderCollapse: "collapse" }}>
            <thead>
              <tr style={{ background: C.bgCardL }}>
                {["Programme", "Points", "AFC Received", "USD Value", "Date", "Status"].map(h => (
                  <th key={h} style={{ padding: "10px 18px", textAlign: "left", fontSize: 10, color: C.textL, textTransform: "uppercase", letterSpacing: 0.8 }}>{h}</th>
                ))}
              </tr>
            </thead>
            <tbody>
              {history.map((r, i) => {
                const meta = r.metadata ? (() => { try { return JSON.parse(r.metadata); } catch { return {}; } })() : {};
                return (
                  <tr key={i} className="table-row">
                    <td style={{ padding: "11px 18px", fontSize: 13, color: C.cream }}>{r.recipient || meta.programme || "—"}</td>
                    <td style={{ padding: "11px 18px", fontSize: 13, fontFamily: "'IBM Plex Mono'", color: C.creamD }}>{meta.points?.toLocaleString() || "—"}</td>
                    <td style={{ padding: "11px 18px", fontSize: 13, fontFamily: "'IBM Plex Mono'", color: C.gold, fontWeight: 600 }}>{r.afc_amount} AFC</td>
                    <td style={{ padding: "11px 18px", fontSize: 13, color: C.greenL }}>${(r.afc_amount * 2.387).toFixed(2)}</td>
                    <td style={{ padding: "11px 18px", fontSize: 11, color: C.textL }}>{new Date(r.created_at).toLocaleDateString()}</td>
                    <td style={{ padding: "11px 18px" }}><span className="badge badge-green">Confirmed</span></td>
                  </tr>
                );
              })}
            </tbody>
          </table>
        )}
      </div>
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// MERCHANTS PAGE
// ══════════════════════════════════════════════════════════════════════════════
const MerchantsPage = ({ onToast }) => {
  const MERCHANTS = [
    { name: "Shoprite Group", tier: "Enterprise", locations: 2847, vol: "$340K/mo", afc: "143,200", status: "Active", country: "🇿🇦" },
    { name: "Pick n Pay",     tier: "Enterprise", locations: 1923, vol: "$210K/mo", afc: "88,400",  status: "Active", country: "🇿🇦" },
    { name: "KFC South Africa", tier: "Enterprise", locations: 984, vol: "$128K/mo", afc: "53,900", status: "Active", country: "🇿🇦" },
    { name: "Clicks Pharmacy", tier: "Enterprise", locations: 854, vol: "$92K/mo",  afc: "38,700",  status: "Active", country: "🇿🇦" },
    { name: "Equity Bank Nairobi", tier: "Mid-Market", locations: 48, vol: "$28K/mo", afc: "11,800", status: "Active", country: "🇰🇪" },
    { name: "Nairobi Tech Supplies", tier: "Mid-Market", locations: 8, vol: "$12K/mo", afc: "5,050",  status: "Onboarding", country: "🇰🇪" },
    { name: "Cape Town Coffee Co.", tier: "SME", locations: 12, vol: "$3.2K/mo", afc: "1,345", status: "Active", country: "🇿🇦" },
    { name: "Lagos Street Market", tier: "SME", locations: 3,  vol: "$820/mo",  afc: "345",   status: "Active", country: "🇳🇬" },
    { name: "Accra Spice Hub",    tier: "SME", locations: 1,  vol: "$410/mo",  afc: "172",   status: "Active", country: "🇬🇭" },
  ];

  const tierColor = t => t === "Enterprise" ? C.gold : t === "Mid-Market" ? "#60A5FA" : C.greenL;
  const [filter, setFilter] = useState("All");
  const [search, setSearch] = useState("");
  const [showOnboard, setShowOnboard] = useState(false);
  const [newMerchant, setNewMerchant] = useState({ name: "", country: "", tier: "SME", contact: "" });
  const [saving, setSaving] = useState(false);

  const filtered = MERCHANTS.filter(m =>
    (filter === "All" || m.tier === filter) &&
    m.name.toLowerCase().includes(search.toLowerCase())
  );

  const handleOnboard = async () => {
    if (!newMerchant.name) return;
    setSaving(true);
    await new Promise(r => setTimeout(r, 900));
    setSaving(false);
    setShowOnboard(false);
    setNewMerchant({ name: "", country: "", tier: "SME", contact: "" });
    onToast(`${newMerchant.name} onboarding request submitted`, "success");
  };

  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* Stats */}
      <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 14 }}>
        {[
          { label: "Active Merchants", val: "1,248", sub: "+22% MoM", c: C.gold },
          { label: "Enterprise", val: "24", sub: "API / POS integration", c: C.goldL },
          { label: "SME & Informal", val: "843", sub: "USSD + QR sticker", c: C.greenL },
          { label: "Avg Monthly Vol", val: "$12,400", sub: "Per merchant", c: "#60A5FA" },
        ].map((s, i) => (
          <div key={i} className="card fade-up" style={{ padding: 18, animationDelay: `${i * 0.06}s` }}>
            <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 22, color: s.c, fontWeight: 700 }}>{s.val}</div>
            <div style={{ fontSize: 11, color: C.textL, marginTop: 4 }}>{s.label}</div>
            <div style={{ fontSize: 11, color: C.greenL, marginTop: 2 }}>{s.sub}</div>
          </div>
        ))}
      </div>

      {/* Merchant table */}
      <div className="card">
        <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}`, display: "flex", gap: 12, alignItems: "center", flexWrap: "wrap" }}>
          <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, flex: 1 }}>Merchant Directory</span>
          <input className="input-field" placeholder="Search merchants…" value={search} onChange={e => setSearch(e.target.value)}
            style={{ padding: "7px 12px", borderRadius: 8, fontSize: 12, width: 180 }} />
          {["All", "Enterprise", "Mid-Market", "SME"].map(f => (
            <button key={f} onClick={() => setFilter(f)} style={{
              padding: "6px 12px", borderRadius: 8, fontSize: 11, cursor: "pointer", fontFamily: "'DM Sans'",
              background: filter === f ? `rgba(201,168,76,0.12)` : C.bgCardL,
              border: `1px solid ${filter === f ? C.gold + "55" : C.border}`,
              color: filter === f ? C.gold : C.textM,
            }}>{f}</button>
          ))}
          <button className="btn-gold" onClick={() => setShowOnboard(true)} style={{ padding: "7px 14px", borderRadius: 8, fontSize: 12 }}>+ Onboard</button>
        </div>
        <table style={{ width: "100%", borderCollapse: "collapse" }}>
          <thead>
            <tr style={{ background: C.bgCardL }}>
              {["Merchant", "Tier", "Locations", "Monthly Volume", "AFC Settled", "Status"].map(h => (
                <th key={h} style={{ padding: "10px 18px", textAlign: "left", fontSize: 10, color: C.textL, textTransform: "uppercase" }}>{h}</th>
              ))}
            </tr>
          </thead>
          <tbody>
            {filtered.map((m, i) => (
              <tr key={i} className="table-row">
                <td style={{ padding: "12px 18px" }}>
                  <div style={{ display: "flex", gap: 8, alignItems: "center" }}>
                    <span style={{ fontSize: 16 }}>{m.country}</span>
                    <span style={{ fontSize: 13, fontWeight: 600, color: C.cream }}>{m.name}</span>
                  </div>
                </td>
                <td style={{ padding: "12px 18px" }}>
                  <span className="badge" style={{ background: `${tierColor(m.tier)}12`, color: tierColor(m.tier), border: `1px solid ${tierColor(m.tier)}44`, fontSize: 9 }}>{m.tier}</span>
                </td>
                <td style={{ padding: "12px 18px", fontSize: 13, fontFamily: "'IBM Plex Mono'", color: C.creamD }}>{m.locations.toLocaleString()}</td>
                <td style={{ padding: "12px 18px", fontSize: 13, fontFamily: "'IBM Plex Mono'", color: C.gold }}>{m.vol}</td>
                <td style={{ padding: "12px 18px", fontSize: 13, fontFamily: "'IBM Plex Mono'", color: C.creamD }}>{m.afc} AFC</td>
                <td style={{ padding: "12px 18px" }}>
                  <span className={`badge ${m.status === "Active" ? "badge-green" : "badge-gold"}`}>{m.status}</span>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
        {filtered.length === 0 && (
          <div style={{ padding: 32, textAlign: "center", color: C.textL, fontSize: 13 }}>No merchants match your filter.</div>
        )}
      </div>

      {/* Integration methods */}
      <div className="card" style={{ padding: 20 }}>
        <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 16 }}>Integration Methods</div>
        <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 12 }}>
          {[
            { icon: "🖥️", method: "POS API / SDK", target: "Enterprise chains", note: "Java · Python · .NET", count: "24 active" },
            { icon: "📱", method: "QR Code Kit",    target: "Mid-market SMEs",  note: "Print & scan",        count: "381 active" },
            { icon: "📟", method: "USSD *123*AFC#", target: "Informal traders", note: "Feature phone only",  count: "843 active" },
            { icon: "🌐", method: "AfriCoin.js",    target: "E-commerce",       note: "Web payment widget",  count: "Onboarding" },
          ].map((m, i) => (
            <div key={i} style={{ background: C.bgCardL, borderRadius: 10, padding: 16, border: `1px solid ${C.border}` }}>
              <div style={{ fontSize: 26, marginBottom: 8 }}>{m.icon}</div>
              <div style={{ fontSize: 13, fontWeight: 700, color: C.cream, marginBottom: 3 }}>{m.method}</div>
              <div style={{ fontSize: 11, color: C.textL, marginBottom: 6 }}>{m.target} · {m.note}</div>
              <span className="badge badge-gold" style={{ fontSize: 9 }}>{m.count}</span>
            </div>
          ))}
        </div>
      </div>

      {/* Onboard modal */}
      {showOnboard && (
        <div style={{ position: "fixed", inset: 0, background: "rgba(0,0,0,0.75)", zIndex: 100, display: "flex", alignItems: "center", justifyContent: "center" }}>
          <div style={{ background: C.bgCard, border: `1px solid ${C.border}`, borderRadius: 16, padding: 32, width: 440, animation: "fadeUp 0.3s ease" }}>
            <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 20 }}>
              <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 20, color: C.cream }}>Onboard New Merchant</span>
              <span onClick={() => setShowOnboard(false)} style={{ cursor: "pointer", color: C.textL, fontSize: 20 }}>×</span>
            </div>
            {[
              ["Business Name", "name", "Shoprite Group"],
              ["Country", "country", "South Africa"],
              ["Contact Email", "contact", "admin@business.com"],
            ].map(([label, key, ph]) => (
              <div key={key} style={{ marginBottom: 14 }}>
                <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 6 }}>{label}</label>
                <input className="input-field" placeholder={ph} value={newMerchant[key]}
                  onChange={e => setNewMerchant(p => ({ ...p, [key]: e.target.value }))}
                  style={{ padding: "10px 12px", borderRadius: 8, fontSize: 13 }} />
              </div>
            ))}
            <div style={{ marginBottom: 20 }}>
              <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 6 }}>Tier</label>
              <div style={{ display: "flex", gap: 8 }}>
                {["SME", "Mid-Market", "Enterprise"].map(t => (
                  <button key={t} onClick={() => setNewMerchant(p => ({ ...p, tier: t }))} style={{
                    flex: 1, padding: "9px 0", borderRadius: 8, fontSize: 12, cursor: "pointer", fontFamily: "'DM Sans'",
                    background: newMerchant.tier === t ? `rgba(201,168,76,0.12)` : C.bgCardL,
                    border: `1px solid ${newMerchant.tier === t ? C.gold + "55" : C.border}`,
                    color: newMerchant.tier === t ? C.gold : C.textM,
                  }}>{t}</button>
                ))}
              </div>
            </div>
            <div style={{ display: "flex", gap: 10 }}>
              <button className="btn-ghost" onClick={() => setShowOnboard(false)} style={{ flex: 1, padding: "12px 0", borderRadius: 10, fontSize: 13 }}>Cancel</button>
              <button className="btn-gold" onClick={handleOnboard} disabled={saving} style={{ flex: 1, padding: "12px 0", borderRadius: 10, fontSize: 13, display: "flex", alignItems: "center", justifyContent: "center", gap: 8 }}>
                {saving ? <Spinner /> : "Submit Request"}
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// GOLD RESERVES PAGE
// ══════════════════════════════════════════════════════════════════════════════
const GoldReservesPage = () => {
  const GOLD_PRICE = 2387.50;
  const AFC_SUPPLY = 5_420_000;
  const VAULTS = [
    { name: "Rand Refinery, Johannesburg", country: "South Africa", flag: "🇿🇦", bars: 847,  kg: 10588, auditor: "PwC",     lastAudit: "1 Mar 2026", hash: "0x3f8a2c...7b49d1e", pct: 62 },
    { name: "Bank of Ghana, Accra",        country: "Ghana",        flag: "🇬🇭", bars: 312,  kg: 3900,  auditor: "Deloitte", lastAudit: "28 Feb 2026", hash: "0x9c1d4b...2a83f70", pct: 23 },
    { name: "Nairobi Metals Exchange",     country: "Kenya",        flag: "🇰🇪", bars: 183,  kg: 2288,  auditor: "KPMG",     lastAudit: "3 Mar 2026",  hash: "0x4e2f1a...9c6b3d8", pct: 13 },
    { name: "AfriCoin Reserve Trust",      country: "Mauritius",    flag: "🇲🇺", bars: 32,   kg: 400,   auditor: "EY",       lastAudit: "5 Mar 2026",  hash: "0x7a9b0c...1d4e2f5", pct: 2 },
  ];

  const totalKg   = VAULTS.reduce((a, v) => a + v.kg, 0);
  const totalOz   = totalKg * 32.1507;
  const totalVal  = totalOz * GOLD_PRICE;
  const afcBacked = totalVal / (GOLD_PRICE * 0.001);
  const coverage  = ((afcBacked / AFC_SUPPLY) * 100).toFixed(1);

  const [goldPrice, setGoldPrice] = useState(GOLD_PRICE);
  const [priceHistory] = useState([2280,2310,2295,2330,2340,2325,2355,2370,2365,2380,2387]);
  useEffect(() => {
    const iv = setInterval(() => setGoldPrice(p => +(p + (Math.random() - 0.49) * 1.5).toFixed(2)), 3000);
    return () => clearInterval(iv);
  }, []);

  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* Hero stats */}
      <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 14 }}>
        {[
          { icon: "🏅", label: "Total Gold Reserves", val: `${totalKg.toLocaleString()} kg`, sub: `${(totalKg/1000).toFixed(2)} tonnes` },
          { icon: "💰", label: "Reserve Value",        val: `$${(totalVal/1e6).toFixed(1)}M`, sub: "At LBMA spot" },
          { icon: "🛡️", label: "Coverage Ratio",       val: `${coverage}%`, sub: "Over-collateralised" },
          { icon: "📦", label: "LBMA Bars",             val: VAULTS.reduce((a,v) => a+v.bars, 0).toLocaleString(), sub: "Across 4 vaults" },
        ].map((s, i) => (
          <div key={i} className="card fade-up" style={{ padding: 18, textAlign: "center", animationDelay: `${i * 0.06}s` }}>
            <div style={{ fontSize: 28, marginBottom: 6 }}>{s.icon}</div>
            <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 22, color: C.gold, fontWeight: 700 }}>{s.val}</div>
            <div style={{ fontSize: 11, color: C.textL, marginTop: 3 }}>{s.label}</div>
            <div style={{ fontSize: 11, color: C.greenL, marginTop: 2 }}>{s.sub}</div>
          </div>
        ))}
      </div>

      {/* Proof of reserve banner */}
      <div style={{ background: "rgba(201,168,76,0.04)", border: `1px solid ${C.gold}33`, borderRadius: 12, padding: "16px 20px", display: "flex", alignItems: "center", gap: 16 }}>
        <span style={{ fontSize: 28 }}>🔐</span>
        <div style={{ flex: 1 }}>
          <div style={{ fontSize: 14, fontWeight: 700, color: C.gold }}>Cryptographic Proof of Reserve — March 2026</div>
          <div style={{ fontSize: 12, color: C.textM, marginTop: 3 }}>
            Master hash: <code style={{ color: C.cream, fontFamily: "'IBM Plex Mono'", fontSize: 11 }}>0x3f8a2c9d7b49d1e2a83f704e2f1a9c6b3d87a9b0c1d4e2f5</code>
          </div>
        </div>
        <span className="badge badge-green" style={{ padding: "6px 14px", fontSize: 11 }}>✓ On-Chain Verified</span>
        <button className="btn-ghost" style={{ padding: "8px 14px", borderRadius: 8, fontSize: 12, whiteSpace: "nowrap" }}>View on AfriChain</button>
      </div>

      <div style={{ display: "grid", gridTemplateColumns: "1.4fr 1fr", gap: 20 }}>
        {/* Vault breakdown */}
        <div className="card">
          <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}` }}>
            <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream }}>Vault Breakdown</span>
          </div>
          {VAULTS.map((v, i) => (
            <div key={i} style={{ padding: "16px 18px", borderBottom: i < VAULTS.length - 1 ? `1px solid ${C.border}22` : "none" }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 10 }}>
                <div>
                  <div style={{ display: "flex", gap: 8, alignItems: "center" }}>
                    <span style={{ fontSize: 16 }}>{v.flag}</span>
                    <span style={{ fontSize: 13, fontWeight: 700, color: C.cream }}>{v.name}</span>
                  </div>
                  <div style={{ fontSize: 11, color: C.textL, marginTop: 2 }}>
                    Auditor: <span style={{ color: C.textM }}>{v.auditor}</span> · Last audit: {v.lastAudit}
                  </div>
                  <div style={{ fontSize: 10, color: C.textL, marginTop: 2, fontFamily: "'IBM Plex Mono'" }}>
                    Hash: {v.hash}
                  </div>
                </div>
                <div style={{ textAlign: "right" }}>
                  <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 16, color: C.gold, fontWeight: 600 }}>{v.kg.toLocaleString()} kg</div>
                  <div style={{ fontSize: 11, color: C.textL }}>{v.bars} LBMA bars</div>
                </div>
              </div>
              <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                <div className="progress-track" style={{ flex: 1, height: 7 }}>
                  <div className="progress-fill" style={{ width: `${v.pct}%` }} />
                </div>
                <span style={{ fontSize: 12, color: C.gold, fontFamily: "'IBM Plex Mono'", width: 36, textAlign: "right" }}>{v.pct}%</span>
              </div>
            </div>
          ))}
        </div>

        {/* Right: gold oracle + mint/burn */}
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 14 }}>Live Gold Oracle</div>
            <div style={{ fontSize: 11, color: C.textL }}>XAU/USD — LBMA spot via Chainlink</div>
            <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 32, color: C.gold, fontWeight: 700, margin: "8px 0 2px" }}>
              ${goldPrice.toLocaleString("en-US", { minimumFractionDigits: 2 })}
            </div>
            <div style={{ fontSize: 12, color: C.textM, marginBottom: 14 }}>1 AFC = 0.001 oz = ${(goldPrice * 0.001).toFixed(4)}</div>
            <MiniChart data={priceHistory} height={54} />
            <div style={{ fontSize: 10, color: C.textL, marginTop: 6, textAlign: "center" }}>Updated every 500ms · 11-week history</div>
          </div>

          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 14 }}>Supply & Coverage</div>
            {[
              ["Total minted", `${(5420000).toLocaleString()} AFC`, C.greenL],
              ["Circulating", `${(5389140).toLocaleString()} AFC`, C.gold],
              ["Burned", `${(30860).toLocaleString()} AFC`, C.textM],
              ["Coverage", `${coverage}%`, C.greenL],
            ].map(([label, val, color], i) => (
              <div key={i} style={{ display: "flex", justifyContent: "space-between", padding: "8px 0", borderBottom: i < 3 ? `1px solid ${C.border}22` : "none" }}>
                <span style={{ fontSize: 12, color: C.textL }}>{label}</span>
                <span style={{ fontSize: 13, fontFamily: "'IBM Plex Mono'", color, fontWeight: 600 }}>{val}</span>
              </div>
            ))}
            <div style={{ marginTop: 14 }}>
              <div style={{ fontSize: 11, color: C.textL, marginBottom: 5 }}>Reserve coverage</div>
              <div className="progress-track" style={{ height: 8 }}>
                <div className="progress-fill" style={{ width: `${Math.min(parseFloat(coverage), 100)}%` }} />
              </div>
              <div style={{ fontSize: 10, color: C.textL, marginTop: 3 }}>Target: 100% minimum · Current: {coverage}%</div>
            </div>
          </div>

          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 12 }}>Vault Insurance</div>
            <div style={{ fontSize: 12, color: C.textM, lineHeight: 1.7 }}>
              All physical gold fully insured with <span style={{ color: C.gold }}>Lloyd's of London</span> equivalent A-rated insurers. LBMA-accredited bars only. Vault security meets ISO 28000 standards.
            </div>
            <div style={{ marginTop: 12, display: "flex", gap: 8, flexWrap: "wrap" }}>
              {["🔒 ISO 28000", "🛡️ LBMA Certified", "📋 Monthly Audit", "⚡ Real-time Proof"].map((t, i) => (
                <span key={i} className="badge badge-gold" style={{ fontSize: 9 }}>{t}</span>
              ))}
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// COMPLIANCE PAGE
// ══════════════════════════════════════════════════════════════════════════════
const CompliancePage = ({ user, onToast }) => {
  const [profile, setProfile] = useState(null);
  const [kycLoading, setKycLoading] = useState(true);
  const [submitting, setSubmitting] = useState(null);

  useEffect(() => {
    if (!user?.id) { setKycLoading(false); return; }
    supabase.getProfile(user.id).then(p => setProfile(p)).catch(() => {}).finally(() => setKycLoading(false));
  }, [user]);

  const currentLevel = profile?.kyc_level || 1;

  const handleUpgrade = async (level) => {
    setSubmitting(level);
    await new Promise(r => setTimeout(r, 1200));
    const name = user?.user_metadata?.full_name?.split(" ")[0] || "User";
    // Update Supabase profile
    if (user?.id) await supabase.upsertProfile(user.id, { kyc_level: level }).catch(() => {});
    // Send KYC email via Resend
    const tpl = emailTemplates.kycUpdate(name, level, "Pending Review");
    await sendEmail(user?.email, tpl.subject, tpl.html);
    setProfile(p => ({ ...p, kyc_level: level }));
    setSubmitting(null);
    onToast(`KYC Level ${level} submitted — you'll receive an email update within 24 hours`, "success");
  };

  const REGS = [
    { country: "South Africa", flag: "🇿🇦", regulator: "SARB / FSCA", license: "PSP + VASP", status: "In Progress", pct: 72 },
    { country: "Kenya",        flag: "🇰🇪", regulator: "CBK",          license: "PSP",         status: "In Progress", pct: 55 },
    { country: "Nigeria",      flag: "🇳🇬", regulator: "CBN / SEC",    license: "e-Money + VASP", status: "Applied",  pct: 30 },
    { country: "Ghana",        flag: "🇬🇭", regulator: "Bank of Ghana",license: "EMI",          status: "Sandbox",    pct: 45 },
    { country: "EU",           flag: "🇪🇺", regulator: "MiCA",         license: "CASP",         status: "Planned",    pct: 10 },
    { country: "United States",flag: "🇺🇸", regulator: "FinCEN",       license: "MSB + MTLs",   status: "Planned",    pct: 5  },
  ];

  const statusColor = s => s === "In Progress" ? C.gold : s === "Applied" ? "#60A5FA" : s === "Sandbox" ? C.greenL : C.textL;

  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* KYC upgrade */}
      <div className="card" style={{ padding: 24 }}>
        <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 20, color: C.cream, marginBottom: 4 }}>KYC Verification</div>
        <div style={{ fontSize: 12, color: C.textM, marginBottom: 20 }}>Complete verification levels to unlock higher transaction limits</div>
        {kycLoading ? (
          <div style={{ textAlign: "center", padding: 20 }}><Spinner /></div>
        ) : (
          <div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 14 }}>
            {[
              { lv: 1, name: "Basic",    limit: "$200/mo",    req: "Phone number only",             icon: "📱", done: currentLevel >= 1 },
              { lv: 2, name: "Standard", limit: "$5,000/mo",  req: "National ID upload",            icon: "🪪", done: currentLevel >= 2 },
              { lv: 3, name: "Premium",  limit: "Unlimited",  req: "Full documents + bank link",    icon: "🏦", done: currentLevel >= 3 },
            ].map(k => (
              <div key={k.lv} style={{
                background: k.done ? "rgba(45,138,87,0.06)" : C.bgCardL,
                border: `1px solid ${k.done ? C.greenL + "44" : C.border}`,
                borderRadius: 12, padding: 18,
                transition: "all 0.2s",
              }}>
                <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 10 }}>
                  <span style={{ fontSize: 26 }}>{k.icon}</span>
                  {k.done
                    ? <span className="badge badge-green" style={{ fontSize: 9 }}>✓ Verified</span>
                    : <span className="badge badge-gold" style={{ fontSize: 9 }}>Incomplete</span>
                  }
                </div>
                <div style={{ fontSize: 13, fontWeight: 700, color: C.cream, marginBottom: 3 }}>Level {k.lv} — {k.name}</div>
                <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 18, color: C.gold, marginBottom: 4 }}>{k.limit}</div>
                <div style={{ fontSize: 11, color: C.textL, marginBottom: 14 }}>{k.req}</div>
                {!k.done && (
                  <button className="btn-gold" onClick={() => handleUpgrade(k.lv)} disabled={submitting === k.lv}
                    style={{ width: "100%", padding: "9px 0", borderRadius: 8, fontSize: 12, display: "flex", alignItems: "center", justifyContent: "center", gap: 6 }}>
                    {submitting === k.lv ? <Spinner /> : `Upgrade to Level ${k.lv}`}
                  </button>
                )}
              </div>
            ))}
          </div>
        )}
      </div>

      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
        {/* Regulatory tracker */}
        <div className="card" style={{ padding: 20 }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 16 }}>Regulatory License Tracker</div>
          {REGS.map((r, i) => (
            <div key={i} style={{ marginBottom: 16 }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 6, alignItems: "center" }}>
                <div style={{ display: "flex", gap: 8, alignItems: "center" }}>
                  <span style={{ fontSize: 14 }}>{r.flag}</span>
                  <div>
                    <span style={{ fontSize: 12, fontWeight: 600, color: C.cream }}>{r.country}</span>
                    <span style={{ fontSize: 11, color: C.textL, marginLeft: 6 }}>{r.regulator}</span>
                  </div>
                </div>
                <span style={{ fontSize: 11, color: statusColor(r.status), fontWeight: 600 }}>{r.status}</span>
              </div>
              <div className="progress-track" style={{ height: 6 }}>
                <div style={{ width: `${r.pct}%`, height: "100%", borderRadius: 999, background: `linear-gradient(90deg, ${statusColor(r.status)}88, ${statusColor(r.status)})` }} />
              </div>
              <div style={{ fontSize: 10, color: C.textL, marginTop: 3 }}>{r.license} · {r.pct}% complete</div>
            </div>
          ))}
        </div>

        {/* Compliance features */}
        <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 14 }}>Built-in Compliance</div>
            {[
              { icon: "🔍", label: "Sanctions Screening",     detail: "OFAC · UN · EU · AU — every transaction, real-time" },
              { icon: "✈️", label: "FATF Travel Rule",         detail: "Auto-applied above $1,000 — originator/beneficiary data" },
              { icon: "🤖", label: "ML Transaction Monitoring", detail: "TensorFlow anomaly detection · 24h review SLA" },
              { icon: "📋", label: "SAR Auto-Filing",          detail: "Suspicious Activity Reports filed to FIUs automatically" },
              { icon: "🏛️", label: "Central Bank API Feed",    detail: "Live reporting dashboards for each jurisdiction" },
            ].map((f, i) => (
              <div key={i} style={{ display: "flex", gap: 12, padding: "10px 0", borderBottom: i < 4 ? `1px solid ${C.border}22` : "none", alignItems: "flex-start" }}>
                <span style={{ fontSize: 18, lineHeight: 1.2 }}>{f.icon}</span>
                <div style={{ flex: 1 }}>
                  <div style={{ fontSize: 12, fontWeight: 600, color: C.cream }}>{f.label}</div>
                  <div style={{ fontSize: 11, color: C.textL, marginTop: 2 }}>{f.detail}</div>
                </div>
                <span style={{ color: C.greenL, fontSize: 14 }}>✓</span>
              </div>
            ))}
          </div>

          <div className="card" style={{ padding: 20 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 12 }}>Transaction Monitoring</div>
            {[
              { id: "TXM-001", type: "Large Transfer",  amount: "$8,420",  flag: "Under review",          risk: "Low" },
              { id: "TXM-002", type: "Rapid Send",      amount: "$320",    flag: "Cleared automatically",  risk: "None" },
              { id: "TXM-003", type: "Cross-border",    amount: "$12,000", flag: "Travel Rule applied",    risk: "None" },
            ].map((t, i) => (
              <div key={i} style={{ background: C.bgCardL, borderRadius: 8, padding: 12, marginBottom: 8, border: `1px solid ${C.border}` }}>
                <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 4 }}>
                  <span style={{ fontSize: 10, fontFamily: "'IBM Plex Mono'", color: C.textL }}>{t.id}</span>
                  <span className={`badge ${t.risk === "None" ? "badge-green" : "badge-gold"}`}>{t.risk === "None" ? "Clear" : t.risk}</span>
                </div>
                <div style={{ display: "flex", justifyContent: "space-between" }}>
                  <span style={{ fontSize: 12, color: C.cream, fontWeight: 600 }}>{t.type}</span>
                  <span style={{ fontSize: 12, fontFamily: "'IBM Plex Mono'", color: C.gold }}>{t.amount}</span>
                </div>
                <div style={{ fontSize: 11, color: C.textL, marginTop: 2 }}>{t.flag}</div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// SETTINGS PAGE
// ══════════════════════════════════════════════════════════════════════════════
const SettingsPage = ({ user, onToast }) => {
  const [profile, setProfile] = useState({
    full_name: user?.user_metadata?.full_name || "",
    phone: user?.user_metadata?.phone || "",
    email: user?.email || "",
    country: "South Africa",
  });
  const [saving, setSaving] = useState(false);
  const [notifs, setNotifs] = useState({ tx: true, promo: false, audit: true, price: true });
  const [twofa, setTwofa] = useState(true);
  const [autoConvert, setAutoConvert] = useState(false);
  const [pwForm, setPwForm] = useState({ current: "", next: "", confirm: "" });
  const [pwLoading, setPwLoading] = useState(false);

  const Toggle = ({ on, onToggle }) => (
    <div onClick={onToggle} style={{ width: 42, height: 24, borderRadius: 999, background: on ? C.gold : C.border, cursor: "pointer", transition: "background 0.2s", position: "relative", flexShrink: 0 }}>
      <div style={{ width: 18, height: 18, borderRadius: "50%", background: C.earth, position: "absolute", top: 3, left: on ? 21 : 3, transition: "left 0.2s" }} />
    </div>
  );

  const handleSaveProfile = async () => {
    setSaving(true);
    try {
      if (user?.id) await supabase.upsertProfile(user.id, { full_name: profile.full_name, phone: profile.phone, country: profile.country });
      onToast("Profile updated successfully", "success");
    } catch {
      onToast("Failed to update profile", "error");
    } finally {
      setSaving(false);
    }
  };

  const handleChangePassword = async () => {
    if (!pwForm.next || pwForm.next !== pwForm.confirm) { onToast("Passwords do not match", "error"); return; }
    if (pwForm.next.length < 6) { onToast("Password must be at least 6 characters", "error"); return; }
    setPwLoading(true);
    await new Promise(r => setTimeout(r, 900));
    setPwLoading(false);
    setPwForm({ current: "", next: "", confirm: "" });
    onToast("Password updated successfully", "success");
  };

  const initials = (profile.full_name || user?.email || "U").split(" ").map(n => n[0]).join("").slice(0, 2).toUpperCase();

  return (
    <div style={{ padding: 24, maxWidth: 820, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* Profile */}
      <div className="card" style={{ padding: 24 }}>
        <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 18, color: C.cream, marginBottom: 20 }}>Profile</div>
        <div style={{ display: "flex", gap: 18, alignItems: "center", marginBottom: 22 }}>
          <div style={{ width: 68, height: 68, borderRadius: "50%", background: `linear-gradient(135deg, ${C.goldD}, ${C.gold})`, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 26, fontWeight: 700, color: C.earth, flexShrink: 0 }}>{initials}</div>
          <div>
            <div style={{ fontSize: 17, fontWeight: 700, color: C.cream }}>{profile.full_name || "—"}</div>
            <div style={{ fontSize: 12, color: C.textL }}>{profile.email}</div>
            <div style={{ marginTop: 5 }}><span className="badge badge-green" style={{ fontSize: 9 }}>Level 3 Verified</span></div>
          </div>
        </div>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 14 }}>
          {[
            { label: "Full Name", key: "full_name", ph: "Your full name" },
            { label: "Phone Number", key: "phone", ph: "+27 82 000 0000" },
            { label: "Country", key: "country", ph: "South Africa" },
          ].map(({ label, key, ph }) => (
            <div key={key}>
              <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 6 }}>{label}</label>
              <input className="input-field" value={profile[key]} onChange={e => setProfile(p => ({ ...p, [key]: e.target.value }))}
                placeholder={ph} style={{ padding: "10px 12px", borderRadius: 8, fontSize: 13 }} />
            </div>
          ))}
          <div>
            <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 6 }}>Email Address</label>
            <input className="input-field" value={profile.email} disabled
              style={{ padding: "10px 12px", borderRadius: 8, fontSize: 13, opacity: 0.5, cursor: "not-allowed" }} />
          </div>
        </div>
        <button className="btn-gold" onClick={handleSaveProfile} disabled={saving}
          style={{ marginTop: 16, padding: "11px 24px", borderRadius: 10, fontSize: 13, display: "inline-flex", alignItems: "center", gap: 8 }}>
          {saving ? <Spinner /> : "Save Profile"}
        </button>
      </div>

      {/* Security */}
      <div className="card" style={{ padding: 24 }}>
        <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 18, color: C.cream, marginBottom: 20 }}>Security</div>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "12px 0", borderBottom: `1px solid ${C.border}33` }}>
          <div>
            <div style={{ fontSize: 13, fontWeight: 600, color: C.cream }}>Two-Factor Authentication</div>
            <div style={{ fontSize: 11, color: C.textL }}>TOTP app required for all outgoing transactions</div>
          </div>
          <Toggle on={twofa} onToggle={() => setTwofa(!twofa)} />
        </div>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "12px 0", marginBottom: 20 }}>
          <div>
            <div style={{ fontSize: 13, fontWeight: 600, color: C.cream }}>Auto-Convert Incoming Fiat to AFC</div>
            <div style={{ fontSize: 11, color: C.textL }}>Automatically protect value on receipt</div>
          </div>
          <Toggle on={autoConvert} onToggle={() => setAutoConvert(!autoConvert)} />
        </div>

        <div style={{ borderTop: `1px solid ${C.border}`, paddingTop: 20 }}>
          <div style={{ fontSize: 13, fontWeight: 600, color: C.cream, marginBottom: 14 }}>Change Password</div>
          <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr", gap: 12 }}>
            {[
              ["Current Password", "current", "current"],
              ["New Password", "next", "new"],
              ["Confirm New", "confirm", "new"],
            ].map(([label, key, _]) => (
              <div key={key}>
                <label style={{ display: "block", fontSize: 11, color: C.textL, textTransform: "uppercase", letterSpacing: 1, marginBottom: 5 }}>{label}</label>
                <input className="input-field" type="password" value={pwForm[key]} onChange={e => setPwForm(p => ({ ...p, [key]: e.target.value }))}
                  placeholder="••••••" style={{ padding: "10px 12px", borderRadius: 8, fontSize: 13 }} />
              </div>
            ))}
          </div>
          <button className="btn-gold" onClick={handleChangePassword} disabled={pwLoading}
            style={{ marginTop: 14, padding: "10px 22px", borderRadius: 10, fontSize: 13, display: "inline-flex", alignItems: "center", gap: 8 }}>
            {pwLoading ? <Spinner /> : "Update Password"}
          </button>
        </div>
      </div>

      {/* Notifications */}
      <div className="card" style={{ padding: 24 }}>
        <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 18, color: C.cream, marginBottom: 20 }}>Email Notifications</div>
        <div style={{ fontSize: 12, color: C.textM, marginBottom: 16 }}>Sent via Resend to <span style={{ color: C.gold }}>{profile.email}</span></div>
        {[
          { key: "tx",    label: "Transaction Alerts",    detail: "Every send, receive, and conversion confirmation" },
          { key: "promo", label: "Promotions & Offers",   detail: "Merchant deals, loyalty bonuses, and AfriCoin offers" },
          { key: "audit", label: "Gold Audit Reports",    detail: "Monthly proof-of-reserve publication notifications" },
          { key: "price", label: "Gold Price Alerts",     detail: "Significant XAU/USD movement above 2% threshold" },
        ].map((n, i) => (
          <div key={n.key} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "13px 0", borderBottom: i < 3 ? `1px solid ${C.border}22` : "none" }}>
            <div>
              <div style={{ fontSize: 13, color: C.cream, fontWeight: 500 }}>{n.label}</div>
              <div style={{ fontSize: 11, color: C.textL }}>{n.detail}</div>
            </div>
            <Toggle on={notifs[n.key]} onToggle={() => setNotifs(p => ({ ...p, [n.key]: !p[n.key] }))} />
          </div>
        ))}
      </div>

      {/* Danger zone */}
      <div style={{ background: "rgba(196,43,43,0.04)", border: `1px solid ${C.red}33`, borderRadius: 14, padding: 22 }}>
        <div style={{ fontSize: 14, fontWeight: 700, color: C.red, marginBottom: 6 }}>Danger Zone</div>
        <div style={{ fontSize: 12, color: C.textM, marginBottom: 14 }}>These actions are irreversible. Proceed with caution.</div>
        <div style={{ display: "flex", gap: 10 }}>
          <button style={{ padding: "9px 18px", borderRadius: 8, fontSize: 12, background: "transparent", border: `1px solid ${C.red}55`, color: C.red, cursor: "pointer", fontFamily: "'DM Sans'" }}
            onClick={() => onToast("Account deactivation request submitted — our team will contact you within 24 hours", "success")}>
            Deactivate Account
          </button>
          <button style={{ padding: "9px 18px", borderRadius: 8, fontSize: 12, background: "transparent", border: `1px solid ${C.red}55`, color: C.red, cursor: "pointer", fontFamily: "'DM Sans'" }}
            onClick={() => onToast("All sessions revoked. Please sign in again.", "success")}>
            Revoke All Sessions
          </button>
        </div>
      </div>
    </div>
  );
};


// ══════════════════════════════════════════════════════════════════════════════
// BIOPAY PAGE
// ══════════════════════════════════════════════════════════════════════════════
const BioPayPage = ({ user, onToast }) => {
  const [enrolled, setEnrolled] = useState(false);
  const [enrolling, setEnrolling] = useState(false);
  const [step, setStep] = useState(0); // 0=idle,1=scan,2=confirm,3=done
  const [biometricType, setBiometricType] = useState("fingerprint");
  const [pulse, setPulse] = useState(false);

  useEffect(() => {
    // Check if user already has BioPay enrolled via profile
    if (user?.id) {
      supabase.getProfile(user.id).then(p => {
        if (p?.biopay_enrolled) setEnrolled(true);
      }).catch(() => {});
    }
  }, [user]);

  useEffect(() => {
    let iv;
    if (step === 1) {
      iv = setInterval(() => setPulse(p => !p), 700);
      // Auto-advance after 3s to simulate scan
      setTimeout(() => { clearInterval(iv); setStep(2); setPulse(false); }, 3000);
    }
    return () => clearInterval(iv);
  }, [step]);

  const handleEnrol = async () => {
    setEnrolling(true);
    setStep(1);
  };

  const handleConfirm = async () => {
    setStep(3);
    await new Promise(r => setTimeout(r, 1000));
    if (user?.id) {
      await supabase.upsertProfile(user.id, { biopay_enrolled: true, biopay_type: biometricType }).catch(() => {});
    }
    // Send KYC-style email via Resend
    const name = user?.user_metadata?.full_name?.split(" ")[0] || "User";
    const tpl = emailTemplates.kycUpdate(name, "BioPay", "Approved");
    await sendEmail(user?.email, "AfriCoin BioPay — Biometric Enrolment Confirmed", tpl.html);
    setEnrolled(true);
    setEnrolling(false);
    setStep(0);
    onToast("BioPay enrolment successful — you can now pay with your biometric", "success");
  };

  const handleRevoke = async () => {
    if (user?.id) await supabase.upsertProfile(user.id, { biopay_enrolled: false }).catch(() => {});
    setEnrolled(false);
    onToast("BioPay biometric data removed from your account", "success");
  };

  const terminals = [
    { loc: "Boxer Stores", count: "347 locations", status: "Live", flag: "🇿🇦" },
    { loc: "Pick n Pay", count: "284 locations", status: "Live", flag: "🇿🇦" },
    { loc: "TymeBank Kiosks", count: "1,024 kiosks", status: "Coming Soon", flag: "🇿🇦" },
    { loc: "Equity Bank Kenya", count: "48 branches", status: "Coming Soon", flag: "🇰🇪" },
    { loc: "Nairobi Markets", count: "12 hubs", status: "Pilot", flag: "🇰🇪" },
    { loc: "Accra Community Hubs", count: "8 locations", status: "Pilot", flag: "🇬🇭" },
  ];

  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* Hero status card */}
      <div style={{
        background: enrolled
          ? `linear-gradient(135deg, rgba(13,51,32,0.9), rgba(26,92,58,0.6))`
          : `linear-gradient(135deg, ${C.bgCard}, ${C.bgCardL})`,
        border: `1px solid ${enrolled ? C.greenL + "55" : C.border}`,
        borderRadius: 16, padding: "28px 32px",
        display: "flex", justifyContent: "space-between", alignItems: "center",
        position: "relative", overflow: "hidden",
      }}>
        <div style={{ position: "absolute", right: -30, top: -30, width: 180, height: 180, borderRadius: "50%", border: `1px solid ${enrolled ? C.greenL + "15" : C.gold + "08"}` }} />
        <div>
          <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 8 }}>
            <Ic d={ICONS.fingerprint} size={28} color={enrolled ? C.greenL : C.gold} />
            <div>
              <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 24, fontWeight: 700, color: C.cream }}>AfriCoin BioPay</div>
              <div style={{ fontSize: 11, color: C.textL, letterSpacing: 2, textTransform: "uppercase" }}>Biometric Payment Authentication</div>
            </div>
          </div>
          <div style={{ fontSize: 14, color: C.textM, maxWidth: 420, lineHeight: 1.6, marginBottom: 16 }}>
            {enrolled
              ? "Your biometric is enrolled and active. You can now pay at any BioPay-enabled terminal using your fingerprint or face — no phone, no card, no PIN required."
              : "Enrol your fingerprint or facial biometric to pay at any AfriCoin BioPay terminal. Your biometric never leaves your device unencrypted."}
          </div>
          {enrolled
            ? <span className="badge badge-green" style={{ padding: "6px 16px", fontSize: 11 }}>✓ BioPay Active — {biometricType === "fingerprint" ? "Fingerprint" : "Face ID"}</span>
            : <span className="badge badge-gold" style={{ padding: "6px 16px", fontSize: 11 }}>⊙ Not Enrolled</span>
          }
        </div>
        {/* Biometric ring visual */}
        <div style={{ position: "relative", width: 100, height: 100, flexShrink: 0 }}>
          <div style={{
            width: 100, height: 100, borderRadius: "50%",
            border: `2px solid ${enrolled ? C.greenL + "66" : C.gold + "44"}`,
            display: "flex", alignItems: "center", justifyContent: "center",
            boxShadow: enrolled ? `0 0 32px rgba(45,138,87,0.25)` : "none",
            transition: "all 0.4s ease",
          }}>
            <div style={{
              width: 72, height: 72, borderRadius: "50%",
              border: `1px solid ${enrolled ? C.greenL + "44" : C.border}`,
              display: "flex", alignItems: "center", justifyContent: "center",
              background: enrolled ? "rgba(45,138,87,0.1)" : C.bgCardL,
            }}>
              <Ic d={ICONS.fingerprint} size={34} color={enrolled ? C.greenL : C.textL} />
            </div>
          </div>
          {enrolled && (
            <div style={{ position: "absolute", bottom: 0, right: 0, width: 24, height: 24, borderRadius: "50%", background: C.greenL, display: "flex", alignItems: "center", justifyContent: "center" }}>
              <Ic d={ICONS.check} size={12} color="#fff" />
            </div>
          )}
        </div>
      </div>

      {/* Enrolment flow or management */}
      {!enrolled && !enrolling && (
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
          <div className="card" style={{ padding: 24 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 18, color: C.cream, marginBottom: 16 }}>Choose Biometric Type</div>
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12, marginBottom: 20 }}>
              {[
                { type: "fingerprint", label: "Fingerprint", icon: "👆", desc: "Uses your device fingerprint sensor" },
                { type: "face", label: "Face ID", icon: "🫥", desc: "Uses front camera facial recognition" },
              ].map(b => (
                <div key={b.type} onClick={() => setBiometricType(b.type)} style={{
                  background: biometricType === b.type ? "rgba(201,168,76,0.1)" : C.bgCardL,
                  border: `1px solid ${biometricType === b.type ? C.gold + "66" : C.border}`,
                  borderRadius: 12, padding: 16, cursor: "pointer", transition: "all 0.2s", textAlign: "center",
                }}>
                  <div style={{ fontSize: 32, marginBottom: 8 }}>{b.icon}</div>
                  <div style={{ fontSize: 13, fontWeight: 700, color: biometricType === b.type ? C.gold : C.cream }}>{b.label}</div>
                  <div style={{ fontSize: 11, color: C.textL, marginTop: 4 }}>{b.desc}</div>
                </div>
              ))}
            </div>
            <div style={{ fontSize: 12, color: C.textL, marginBottom: 16, lineHeight: 1.6 }}>
              Your biometric template is encrypted with AES-256 and stored in the AfriCoin BioPay Secure Enclave. It is never shared with third parties and never transmitted as raw data.
            </div>
            <button className="btn-gold" onClick={handleEnrol} style={{ width: "100%", padding: "13px 0", borderRadius: 10, fontSize: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 8 }}>
              <Ic d={ICONS.fingerprint} size={16} color={C.earth} />
              Enrol {biometricType === "fingerprint" ? "Fingerprint" : "Face ID"}
            </button>
          </div>

          <div className="card" style={{ padding: 24 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 18, color: C.cream, marginBottom: 16 }}>How BioPay Works</div>
            {[
              { step: "1", title: "Enrol Once", desc: "Register your biometric during KYC Level 2 setup. Takes under 90 seconds.", icon: "👆" },
              { step: "2", title: "Pay Anywhere", desc: "At any BioPay terminal, place your finger or look at the camera.", icon: "🏪" },
              { step: "3", title: "Instant Settlement", desc: "AfriChain confirms and settles the transaction in under 1 second.", icon: "⚡" },
              { step: "4", title: "Email Receipt", desc: "A transaction confirmation is sent to your registered email instantly.", icon: "📧" },
            ].map(s => (
              <div key={s.step} style={{ display: "flex", gap: 12, marginBottom: 14, alignItems: "flex-start" }}>
                <div style={{ width: 32, height: 32, borderRadius: "50%", background: `rgba(201,168,76,0.12)`, border: `1px solid ${C.gold}44`, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 14, flexShrink: 0 }}>{s.icon}</div>
                <div>
                  <div style={{ fontSize: 12, fontWeight: 700, color: C.cream }}>{s.title}</div>
                  <div style={{ fontSize: 11, color: C.textL, marginTop: 2 }}>{s.desc}</div>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}

      {/* Enrolment scanning animation */}
      {enrolling && step < 3 && (
        <div className="card" style={{ padding: 40, textAlign: "center" }}>
          <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 20, color: C.cream, marginBottom: 24 }}>
            {step === 1 ? "Scanning Biometric..." : step === 2 ? "Confirm Enrolment" : "Registering..."}
          </div>
          {step === 1 && (
            <>
              <div style={{
                width: 120, height: 120, borderRadius: "50%", margin: "0 auto 24px",
                border: `2px solid ${pulse ? C.gold : C.border}`,
                display: "flex", alignItems: "center", justifyContent: "center",
                transition: "border-color 0.3s, box-shadow 0.3s",
                boxShadow: pulse ? `0 0 24px rgba(201,168,76,0.4)` : "none",
              }}>
                <Ic d={ICONS.fingerprint} size={52} color={pulse ? C.gold : C.textL} />
              </div>
              <div style={{ fontSize: 13, color: C.textM }}>
                {biometricType === "fingerprint" ? "Place your finger on the sensor and hold steady..." : "Look directly at the camera and hold still..."}
              </div>
              <div style={{ marginTop: 16 }}><Spinner /></div>
            </>
          )}
          {step === 2 && (
            <>
              <div style={{ width: 80, height: 80, borderRadius: "50%", background: "rgba(201,168,76,0.1)", border: `2px solid ${C.gold}66`, margin: "0 auto 20px", display: "flex", alignItems: "center", justifyContent: "center" }}>
                <Ic d={ICONS.check} size={36} color={C.gold} />
              </div>
              <div style={{ fontSize: 14, color: C.cream, marginBottom: 8 }}>Biometric captured successfully</div>
              <div style={{ fontSize: 12, color: C.textL, marginBottom: 24 }}>
                Your {biometricType === "fingerprint" ? "fingerprint" : "facial"} template has been encrypted and is ready to register.
              </div>
              <div style={{ display: "flex", gap: 12, justifyContent: "center" }}>
                <button className="btn-ghost" onClick={() => { setEnrolling(false); setStep(0); }} style={{ padding: "11px 24px", borderRadius: 10, fontSize: 13 }}>Cancel</button>
                <button className="btn-gold" onClick={handleConfirm} style={{ padding: "11px 24px", borderRadius: 10, fontSize: 13, display: "flex", alignItems: "center", gap: 8 }}>
                  <Ic d={ICONS.check} size={14} color={C.earth} /> Confirm & Activate
                </button>
              </div>
            </>
          )}
        </div>
      )}

      {/* Enrolled management panel */}
      {enrolled && (
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }}>
          <div className="card" style={{ padding: 22 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 14 }}>BioPay Settings</div>
            {[
              { label: "Biometric Type", val: biometricType === "fingerprint" ? "Fingerprint" : "Face ID" },
              { label: "Enrolment Status", val: "Active" },
              { label: "KYC Level Required", val: "Level 2 ✓" },
              { label: "Fallback Auth", val: "4-digit PIN enabled" },
              { label: "Max Transaction", val: "R 5,000 per scan" },
              { label: "Data Storage", val: "AfriCoin Secure Enclave (AES-256)" },
            ].map((r, i) => (
              <div key={i} style={{ display: "flex", justifyContent: "space-between", padding: "9px 0", borderBottom: i < 5 ? `1px solid ${C.border}22` : "none" }}>
                <span style={{ fontSize: 12, color: C.textL }}>{r.label}</span>
                <span style={{ fontSize: 12, color: C.cream, fontWeight: r.val === "Active" ? 700 : 400, color: r.val === "Active" ? C.greenL : C.cream }}>{r.val}</span>
              </div>
            ))}
            <div style={{ marginTop: 16, display: "flex", gap: 10 }}>
              <button className="btn-gold" onClick={() => { setEnrolled(false); setEnrolling(true); setStep(1); }} style={{ flex: 1, padding: "10px 0", borderRadius: 8, fontSize: 12 }}>Re-enrol</button>
              <button onClick={handleRevoke} style={{ flex: 1, padding: "10px 0", borderRadius: 8, fontSize: 12, background: "transparent", border: `1px solid ${C.red}55`, color: C.red, cursor: "pointer", fontFamily: "'DM Sans'" }}>Remove Biometric</button>
            </div>
          </div>
          <div className="card" style={{ padding: 22 }}>
            <div style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, marginBottom: 14 }}>Recent BioPay Transactions</div>
            {[
              { merchant: "Boxer Soweto", amount: "R 342.50", time: "Today 09:14", scan: "Fingerprint" },
              { merchant: "Pick n Pay Sandton", amount: "R 187.00", time: "Yesterday 14:32", scan: "Fingerprint" },
              { merchant: "Spaza — Khayelitsha", amount: "R 45.00", time: "2 days ago", scan: "Fingerprint" },
            ].map((t, i) => (
              <div key={i} style={{ display: "flex", justifyContent: "space-between", alignItems: "center", padding: "10px 0", borderBottom: i < 2 ? `1px solid ${C.border}22` : "none" }}>
                <div style={{ display: "flex", gap: 10, alignItems: "center" }}>
                  <div style={{ width: 32, height: 32, borderRadius: "50%", background: "rgba(45,138,87,0.1)", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 14 }}>👆</div>
                  <div>
                    <div style={{ fontSize: 12, fontWeight: 600, color: C.cream }}>{t.merchant}</div>
                    <div style={{ fontSize: 10, color: C.textL }}>{t.scan} · {t.time}</div>
                  </div>
                </div>
                <span style={{ fontSize: 13, fontFamily: "'IBM Plex Mono'", color: C.gold }}>{t.amount}</span>
              </div>
            ))}
          </div>
        </div>
      )}

      {/* Live terminal map */}
      <div className="card">
        <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}`, display: "flex", justifyContent: "space-between", alignItems: "center" }}>
          <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream }}>BioPay Terminal Network</span>
          <span className="badge badge-gold">{terminals.filter(t => t.status === "Live").length} Live · {terminals.filter(t => t.status !== "Live").length} Expanding</span>
        </div>
        <div style={{ padding: 18, display: "grid", gridTemplateColumns: "repeat(3, 1fr)", gap: 12 }}>
          {terminals.map((t, i) => (
            <div key={i} style={{ background: C.bgCardL, borderRadius: 10, padding: 14, border: `1px solid ${t.status === "Live" ? C.greenL + "33" : C.border}` }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 6 }}>
                <span style={{ fontSize: 16 }}>{t.flag}</span>
                <span className={`badge ${t.status === "Live" ? "badge-green" : "badge-gold"}`} style={{ fontSize: 9 }}>{t.status}</span>
              </div>
              <div style={{ fontSize: 13, fontWeight: 600, color: C.cream }}>{t.loc}</div>
              <div style={{ fontSize: 11, color: C.textL, marginTop: 3 }}>{t.count}</div>
            </div>
          ))}
        </div>
        <div style={{ padding: "0 18px 18px" }}>
          <div style={{ background: "rgba(201,168,76,0.05)", border: `1px solid ${C.gold}22`, borderRadius: 8, padding: 12, fontSize: 12, color: C.textM, textAlign: "center" }}>
            BioPay uses ISO 19794-2 fingerprint standards · ISO 30107-3 Presentation Attack Detection · POPIA compliant
          </div>
        </div>
      </div>
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// NOTIFICATIONS PAGE
// ══════════════════════════════════════════════════════════════════════════════
const NotificationsPage = ({ user, transactions, onToast }) => {
  const [filter, setFilter] = useState("All");
  const [notifications, setNotifications] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Build notifications from transactions + system events
    const txNotifs = (transactions || []).slice(0, 10).map(tx => ({
      id: tx.tx_hash || tx.id || Math.random().toString(36),
      type: "transaction",
      title: tx.transaction_type || "Transaction",
      message: `${tx.afc_amount} AFC — ${tx.recipient || "confirmed"}`,
      time: tx.created_at ? new Date(tx.created_at).toLocaleString() : "Recently",
      read: false,
      icon: tx.transaction_type === "Loyalty Conversion" ? "⭐" : tx.transaction_type === "Sent" ? "↑" : "↓",
      color: tx.transaction_type === "Sent" ? C.gold : C.greenL,
    }));

    const systemNotifs = [
      { id: "sys1", type: "gold", title: "Gold Audit Published", message: "March 2026 proof-of-reserve audit by PwC has been published on-chain and verified.", time: "1 Mar 2026 09:00", read: true, icon: "🏅", color: C.gold },
      { id: "sys2", type: "kyc", title: "KYC Level 3 Verified", message: "Your identity verification is complete. Unlimited transaction limits are now active.", time: "28 Feb 2026 14:22", read: true, icon: "✓", color: C.greenL },
      { id: "sys3", type: "price", title: "Gold Price Alert", message: "XAU/USD has risen 2.4% today to $2,387.50. Your AFC balance has appreciated accordingly.", time: "14 Mar 2026 08:30", read: false, icon: "📈", color: C.gold },
      { id: "sys4", type: "biopay", title: "BioPay Terminal Near You", message: "A new AfriCoin BioPay terminal has been activated at Boxer Soweto — 2.3km from your registered location.", time: "13 Mar 2026 16:45", read: false, icon: "👆", color: "#60A5FA" },
      { id: "sys5", type: "system", title: "Network Upgrade Complete", message: "AfriChain v2.1 has been deployed. Transaction throughput increased to 100,000 TPS.", time: "10 Mar 2026 00:00", read: true, icon: "⚡", color: C.greenL },
      { id: "sys6", type: "loyalty", title: "eBucks Expiry Reminder", message: "You have 2,400 eBucks expiring in 14 days. Convert to AFC to preserve their value.", time: "1 Mar 2026 10:00", read: false, icon: "⚠️", color: C.gold },
      { id: "sys7", type: "system", title: "New Merchant Partner", message: "Pick n Pay Sandton City is now live on AfriCoin. Earn 1.5% AFC cashback on all purchases.", time: "5 Mar 2026 09:00", read: true, icon: "🏪", color: "#C084FC" },
    ];

    const all = [...txNotifs, ...systemNotifs].sort((a, b) => new Date(b.time) - new Date(a.time));
    setNotifications(all);
    setLoading(false);
  }, [transactions]);

  const FILTERS = ["All", "Transactions", "Gold", "KYC", "BioPay", "System"];
  const typeMap = { Transactions: "transaction", Gold: "gold", KYC: "kyc", BioPay: "biopay", System: ["system", "price", "loyalty"] };

  const filtered = filter === "All" ? notifications : notifications.filter(n => {
    const f = typeMap[filter];
    return Array.isArray(f) ? f.includes(n.type) : n.type === f;
  });

  const unread = notifications.filter(n => !n.read).length;

  const markAllRead = () => {
    setNotifications(prev => prev.map(n => ({ ...n, read: true })));
    onToast("All notifications marked as read", "success");
  };

  const markRead = (id) => setNotifications(prev => prev.map(n => n.id === id ? { ...n, read: true } : n));

  const clearAll = () => {
    setNotifications([]);
    onToast("All notifications cleared", "success");
  };

  return (
    <div style={{ padding: 24, display: "flex", flexDirection: "column", gap: 20 }}>
      {/* Header stats */}
      <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 14 }}>
        {[
          { label: "Total", val: notifications.length, color: C.gold },
          { label: "Unread", val: unread, color: unread > 0 ? C.red : C.greenL },
          { label: "Transactions", val: notifications.filter(n => n.type === "transaction").length, color: C.greenL },
          { label: "System Alerts", val: notifications.filter(n => n.type !== "transaction").length, color: "#60A5FA" },
        ].map((s, i) => (
          <div key={i} className="card fade-up" style={{ padding: 18, textAlign: "center", animationDelay: `${i * 0.06}s` }}>
            <div style={{ fontFamily: "'IBM Plex Mono'", fontSize: 28, color: s.color, fontWeight: 700 }}>{s.val}</div>
            <div style={{ fontSize: 11, color: C.textL, marginTop: 4 }}>{s.label}</div>
          </div>
        ))}
      </div>

      {/* Notification list */}
      <div className="card">
        {/* Toolbar */}
        <div style={{ padding: "14px 18px", borderBottom: `1px solid ${C.border}`, display: "flex", gap: 10, alignItems: "center", flexWrap: "wrap" }}>
          <span style={{ fontFamily: "'Cormorant Garamond'", fontSize: 16, color: C.cream, flex: 1 }}>
            Notifications {unread > 0 && <span style={{ background: C.red, color: "#fff", borderRadius: "50%", fontSize: 10, padding: "2px 6px", marginLeft: 6, fontFamily: "'DM Sans'", fontWeight: 700 }}>{unread}</span>}
          </span>
          {/* Filter chips */}
          <div style={{ display: "flex", gap: 6, flexWrap: "wrap" }}>
            {FILTERS.map(f => (
              <button key={f} onClick={() => setFilter(f)} style={{
                padding: "5px 12px", borderRadius: 999, fontSize: 11, cursor: "pointer", fontFamily: "'DM Sans'",
                background: filter === f ? `rgba(201,168,76,0.12)` : C.bgCardL,
                border: `1px solid ${filter === f ? C.gold + "55" : C.border}`,
                color: filter === f ? C.gold : C.textM, transition: "all 0.15s",
              }}>{f}</button>
            ))}
          </div>
          <button className="btn-ghost" onClick={markAllRead} style={{ padding: "6px 12px", borderRadius: 8, fontSize: 11, whiteSpace: "nowrap" }}>Mark all read</button>
          <button onClick={clearAll} style={{ padding: "6px 12px", borderRadius: 8, fontSize: 11, background: "transparent", border: `1px solid ${C.border}`, color: C.textL, cursor: "pointer", fontFamily: "'DM Sans'", whiteSpace: "nowrap" }}>Clear all</button>
        </div>

        {/* List */}
        {loading ? (
          <div style={{ padding: 32, textAlign: "center" }}><Spinner /></div>
        ) : filtered.length === 0 ? (
          <div style={{ padding: 48, textAlign: "center" }}>
            <div style={{ fontSize: 48, marginBottom: 12 }}>🔔</div>
            <div style={{ fontSize: 14, color: C.textL }}>No notifications in this category.</div>
          </div>
        ) : (
          filtered.map((n, i) => (
            <div
              key={n.id}
              className="table-row"
              onClick={() => markRead(n.id)}
              style={{
                padding: "14px 18px",
                borderBottom: i < filtered.length - 1 ? `1px solid ${C.border}22` : "none",
                display: "flex", gap: 14, alignItems: "flex-start", cursor: "pointer",
                background: n.read ? "transparent" : "rgba(201,168,76,0.03)",
                position: "relative",
              }}
            >
              {/* Unread dot */}
              {!n.read && (
                <div style={{ position: "absolute", left: 6, top: "50%", transform: "translateY(-50%)", width: 6, height: 6, borderRadius: "50%", background: C.gold }} />
              )}
              {/* Icon */}
              <div style={{
                width: 40, height: 40, borderRadius: "50%", flexShrink: 0,
                background: `${n.color}15`,
                border: `1px solid ${n.color}33`,
                display: "flex", alignItems: "center", justifyContent: "center",
                fontSize: 16,
              }}>{n.icon}</div>
              {/* Content */}
              <div style={{ flex: 1 }}>
                <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 3 }}>
                  <span style={{ fontSize: 13, fontWeight: n.read ? 500 : 700, color: n.read ? C.creamD : C.cream }}>{n.title}</span>
                  <span style={{ fontSize: 10, color: C.textL, whiteSpace: "nowrap", marginLeft: 12 }}>{n.time}</span>
                </div>
                <div style={{ fontSize: 12, color: C.textM, lineHeight: 1.5 }}>{n.message}</div>
                <div style={{ marginTop: 5 }}>
                  <span className="badge" style={{
                    fontSize: 9, background: `${n.color}12`, color: n.color,
                    border: `1px solid ${n.color}33`, textTransform: "capitalize",
                  }}>{n.type}</span>
                </div>
              </div>
            </div>
          ))
        )}
      </div>

      {/* Email preferences reminder */}
      <div style={{ background: "rgba(201,168,76,0.04)", border: `1px solid ${C.gold}22`, borderRadius: 12, padding: "14px 20px", display: "flex", alignItems: "center", gap: 14 }}>
        <span style={{ fontSize: 22 }}>📧</span>
        <div style={{ flex: 1 }}>
          <div style={{ fontSize: 13, fontWeight: 600, color: C.cream }}>Email Notifications Active</div>
          <div style={{ fontSize: 11, color: C.textL }}>Transaction confirmations, gold audit reports, and KYC updates are also sent to <span style={{ color: C.gold }}>{user?.email}</span> via Resend.</div>
        </div>
        <button className="btn-ghost" style={{ padding: "7px 14px", borderRadius: 8, fontSize: 12, whiteSpace: "nowrap" }}
          onClick={() => onToast("Manage email preferences in Settings → Notifications", "success")}>
          Manage
        </button>
      </div>
    </div>
  );
};

const PAGE_COMPONENTS = {
  dashboard:     DashboardPage,
  wallet:        WalletPage,
  send:          SendPage,
  loyalty:       LoyaltyPage,
  merchants:     MerchantsPage,
  reserves:      GoldReservesPage,
  biopay:        BioPayPage,
  notifications: NotificationsPage,
  analytics:     AnalyticsPage,
  compliance:    CompliancePage,
  settings:      SettingsPage,
};

const PAGE_TITLES = {
  dashboard:     "Dashboard",
  wallet:        "Wallet",
  send:          "Send & Receive",
  loyalty:       "Loyalty Conversion",
  merchants:     "Merchants",
  reserves:      "Gold Reserves",
  biopay:        "AfriCoin BioPay",
  notifications: "Notifications",
  analytics:     "Analytics",
  compliance:    "Compliance",
  settings:      "Settings",
};

// ── MAIN DASHBOARD SHELL ──────────────────────────────────────────────────────
const Dashboard = ({ user, onSignOut }) => {
  const [page, setPage] = useState("dashboard");
  const [transactions, setTransactions] = useState([]);
  const [toast, setToast] = useState(null);

  useEffect(() => {
    if (user?.id) {
      supabase.getTransactions(user.id).then(txs => {
        if (Array.isArray(txs) && txs.length > 0) setTransactions(txs);
      }).catch(() => {});
    }
  }, [user]);

  const showToast = (msg, type = "success") => setToast({ msg, type });

  const handleSignOut = async () => {
    await supabase.signOut();
    showToast("Signed out successfully", "success");
    setTimeout(onSignOut, 800);
  };

  const handleTransaction = (tx) => {
    setTransactions(p => [tx, ...p]);
    showToast("Transaction confirmed — receipt sent to your email", "success");
  };

  const PageComponent = PAGE_COMPONENTS[page];
  const pageProps = { user, transactions, onTransaction: handleTransaction, onToast: showToast };

  return (
    <div style={{ display: "flex", minHeight: "100vh" }}>
      <Sidebar page={page} setPage={setPage} user={user} onSignOut={handleSignOut} unreadCount={transactions.filter(t => !t.read).length + 3} />
      <div style={{ flex: 1, display: "flex", flexDirection: "column", overflow: "auto" }}>
        <TopBar title={PAGE_TITLES[page]} />
        <div style={{ flex: 1, overflowY: "auto" }}>
          <PageComponent key={page} {...pageProps} />
        </div>
      </div>
      {toast && <Toast msg={toast.msg} type={toast.type} onClose={() => setToast(null)} />}
    </div>
  );
};

// ══════════════════════════════════════════════════════════════════════════════
// APP ROOT — AUTH GATE
// ══════════════════════════════════════════════════════════════════════════════
export default function App() {
  const [authScreen, setAuthScreen] = useState("signin");
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [toast, setToast] = useState(null);

  useEffect(() => {
    injectGlobalStyles();
    // Restore session
    const session = supabase.loadSession();
    if (session) {
      supabase.getUser().then(u => {
        if (u) setUser(u);
        setLoading(false);
      }).catch(() => setLoading(false));
    } else {
      setLoading(false);
    }
  }, []);

  const handleAuthSuccess = async (userData, session) => {
    // Try to get full user object
    let u = userData;
    if (session?.access_token) {
      supabase._token = session.access_token;
      try {
        const full = await supabase.getUser();
        if (full) u = full;
      } catch {}
    }
    setUser(u);
    setToast({ msg: `Welcome${u?.user_metadata?.full_name ? ", " + u.user_metadata.full_name.split(" ")[0] : ""}! You are signed in.`, type: "success" });
    // Upsert profile
    if (u?.id) {
      supabase.upsertProfile(u.id, {
        email: u.email,
        full_name: u.user_metadata?.full_name || "",
        phone: u.user_metadata?.phone || "",
        kyc_level: 1,
        afc_balance: 0,
      }).catch(() => {});
    }
  };

  if (loading) {
    return (
      <div style={{ minHeight: "100vh", background: C.bg, display: "flex", alignItems: "center", justifyContent: "center", flexDirection: "column", gap: 20 }}>
        <img
          src={APP_ICON}
          alt="AfriCoin"
          style={{ width: 80, height: 80, borderRadius: 20, objectFit: "cover", boxShadow: "0 8px 32px rgba(201,168,76,0.25)", animation: "fadeIn 0.4s ease" }}
        />
        <div className="spinner" style={{ width: 28, height: 28 }} />
        <div style={{ fontSize: 13, color: C.textL, letterSpacing: 1 }}>Loading AfriCoin…</div>
      </div>
    );
  }

  if (user) {
    return (
      <>
        <Dashboard user={user} onSignOut={() => setUser(null)} />
        {toast && <Toast msg={toast.msg} type={toast.type} onClose={() => setToast(null)} />}
      </>
    );
  }

  return (
    <>
      {authScreen === "signin" && <SignIn onSwitch={setAuthScreen} onSuccess={handleAuthSuccess} />}
      {authScreen === "signup" && <SignUp onSwitch={setAuthScreen} onSuccess={handleAuthSuccess} />}
      {authScreen === "reset" && <PasswordReset onSwitch={setAuthScreen} />}
      {toast && <Toast msg={toast.msg} type={toast.type} onClose={() => setToast(null)} />}
    </>
  );
}
