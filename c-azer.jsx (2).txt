import React, { useState, useRef, useEffect, useCallback } from "react";

/* ---------------------------------- ICONS (custom, consistent 1.75px stroke family) ---------------------------------- */

const iconProps = { viewBox: "0 0 24 24", fill: "none", stroke: "currentColor", strokeWidth: 1.75, strokeLinecap: "round", strokeLinejoin: "round" };

const IconMenu = (p) => (
  <svg {...iconProps} {...p}><path d="M3 6h18" /><path d="M3 12h18" /><path d="M3 18h12" /></svg>
);
const IconPlus = (p) => (
  <svg {...iconProps} {...p}><path d="M12 5v14" /><path d="M5 12h14" /></svg>
);
const IconTrash = (p) => (
  <svg {...iconProps} {...p}><path d="M4 7h16" /><path d="M9 7V5a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2" /><path d="M6 7l1 13a1 1 0 0 0 1 1h8a1 1 0 0 0 1-1l1-13" /><path d="M10 11v6" /><path d="M14 11v6" /></svg>
);
const IconChat = (p) => (
  <svg viewBox="0 0 24 24" fill="currentColor" {...p}>
    <path d="M12 3C6.9 3 3 6.4 3 10.6c0 2.5 1.4 4.7 3.6 6.1-.1.9-.5 2.1-1.3 3.2-.2.3 0 .7.4.6 1.7-.4 3.1-1.1 4-1.7.7.2 1.5.3 2.3.3 5.1 0 9-3.4 9-7.6S17.1 3 12 3z" />
  </svg>
);
const IconSparkle = (p) => (
  <svg viewBox="0 0 24 24" fill="currentColor" {...p}>
    <path d="M11 3.2c.15-.5.85-.5 1 0l1.2 3.9a4.6 4.6 0 0 0 3 3l3.9 1.2c.5.15.5.85 0 1L16.2 13.5a4.6 4.6 0 0 0-3 3L12 20.4c-.15.5-.85.5-1 0l-1.2-3.9a4.6 4.6 0 0 0-3-3L2.9 12.3c-.5-.15-.5-.85 0-1l3.9-1.2a4.6 4.6 0 0 0 3-3L11 3.2z" />
    <path d="M18.5 2.3c.1-.4.6-.4.7 0l.4 1.4c.1.4.4.7.8.8l1.4.4c.4.1.4.6 0 .7l-1.4.4c-.4.1-.7.4-.8.8l-.4 1.4c-.1.4-.6.4-.7 0l-.4-1.4a1.2 1.2 0 0 0-.8-.8l-1.4-.4c-.4-.1-.4-.6 0-.7l1.4-.4c.4-.1.7-.4.8-.8l.4-1.4z" />
  </svg>
);
const IconCode = (p) => (
  <svg {...iconProps} {...p}><path d="M8 8l-4 4 4 4" /><path d="M16 8l4 4-4 4" /><path d="M13.5 5.5l-3 13" /></svg>
);
const IconImage = (p) => (
  <svg {...iconProps} {...p}><rect x="3" y="4" width="18" height="16" rx="2" /><circle cx="8.5" cy="9.5" r="1.5" /><path d="M21 15l-5.5-5.5L5 20" /></svg>
);
const IconSettings = (p) => (
  <svg {...iconProps} {...p}><circle cx="12" cy="12" r="3" /><path d="M19.4 13a7.7 7.7 0 0 0 0-2l2-1.5-2-3.4-2.3.6a7.7 7.7 0 0 0-1.7-1L15 3h-4l-.4 2.7a7.7 7.7 0 0 0-1.7 1l-2.3-.6-2 3.4L6.6 11a7.7 7.7 0 0 0 0 2l-2 1.5 2 3.4 2.3-.6c.5.45 1.1.8 1.7 1L11 21h4l.4-2.7c.6-.2 1.2-.55 1.7-1l2.3.6 2-3.4-2-1.5z" /></svg>
);
const IconSend = (p) => (
  <svg viewBox="0 0 24 24" fill="currentColor" {...p}>
    <path d="M21.5 2.5 2.7 10.1c-.9.4-.8 1.7.1 2l6.1 2 2 6.1c.3.9 1.6 1 2 .1L20.5 2.9c.3-.6-.4-1.3-1-1z" opacity="0.35" />
    <path d="M21.5 2.5 10.2 13.7l2.7 6.6c.3.9 1.6 1 2 .1L22.5 3.5c.2-.6-.4-1.3-1-1z" />
  </svg>
);
const IconClose = (p) => (
  <svg {...iconProps} {...p}><path d="M6 6l12 12" /><path d="M18 6L6 18" /></svg>
);
const IconStore = (p) => (
  <svg {...iconProps} {...p}><path d="M4 9l1-5h14l1 5" /><path d="M4 9h16v10a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V9z" /><path d="M9 13a3 3 0 0 0 6 0" /></svg>
);
const IconCrown = (p) => (
  <svg {...iconProps} {...p}><path d="M4 18h16" /><path d="M4 18l-1-9 5 4 4-6 4 6 5-4-1 9" /></svg>
);
const IconCheck = (p) => (
  <svg {...iconProps} {...p}><path d="M5 13l4 4 10-10" /></svg>
);
const IconBell = (p) => (
  <svg {...iconProps} {...p}><path d="M6 10a6 6 0 0 1 12 0c0 4 1.5 5.5 1.5 5.5H4.5S6 14 6 10z" /><path d="M10 19a2 2 0 0 0 4 0" /></svg>
);
const IconUser = (p) => (
  <svg {...iconProps} {...p}><circle cx="12" cy="8" r="3.5" /><path d="M5 20c1-4 4-6 7-6s6 2 7 6" /></svg>
);

const IconPaperclip = (p) => (
  <svg {...iconProps} {...p}><path d="M8 12.5 15 5.6a3.2 3.2 0 0 1 4.5 4.5l-8 8a5 5 0 1 1-7-7l7.3-7.3" /></svg>
);
const IconChevron = (p) => (
  <svg {...iconProps} {...p}><path d="M6 9l6 6 6-6" /></svg>
);

const Logo = ({ size = 26 }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none">
    <circle cx="12" cy="12" r="11" stroke="#22d3ee" strokeWidth="1.5" />
    <path d="M15.2 7.2a5.4 5.4 0 1 0 0 9.6" stroke="#22d3ee" strokeWidth="1.9" strokeLinecap="round" fill="none" />
    <path d="M13.6 9.4l1 1.5-1.7.5" stroke="#facc15" strokeWidth="1.3" strokeLinecap="round" strokeLinejoin="round" fill="none" />
  </svg>
);

/* ---------------------------------- helpers ---------------------------------- */

const uid = () => Math.random().toString(36).slice(2, 10);

function seedFromString(str) {
  let h = 1779033703 ^ str.length;
  for (let i = 0; i < str.length; i++) {
    h = Math.imul(h ^ str.charCodeAt(i), 3432918353);
    h = (h << 13) | (h >>> 19);
  }
  return () => {
    h = Math.imul(h ^ (h >>> 16), 2246822507);
    h = Math.imul(h ^ (h >>> 13), 3266489909);
    h ^= h >>> 16;
    return (h >>> 0) / 4294967296;
  };
}

const PALETTES = [
  { name: "aurora", stops: ["#22d3ee", "#3b82f6", "#a78bfa"] },
  { name: "sunset", stops: ["#fb923c", "#f472b6", "#a855f7"] },
  { name: "forest", stops: ["#34d399", "#22d3ee", "#0ea5e9"] },
  { name: "gold", stops: ["#facc15", "#fb923c", "#ef4444"] },
  { name: "ocean", stops: ["#0ea5e9", "#22d3ee", "#6366f1"] },
];

const DENSITY_MULT = { sparse: 0.6, medium: 1, dense: 1.6 };

function generateArt(prompt, pro = false, aiPlan = null) {
  const rand = seedFromString(prompt || "c-azer");
  const colors = aiPlan?.colors?.length >= 2 ? aiPlan.colors : PALETTES[Math.floor(rand() * PALETTES.length)].stops;
  const densityMult = DENSITY_MULT[aiPlan?.density] || 1;
  const blobs = [];
  const count = Math.round(((pro ? 8 : 4) + Math.floor(rand() * (pro ? 5 : 3))) * densityMult);
  for (let i = 0; i < count; i++) {
    blobs.push({
      id: i,
      cx: 10 + rand() * 80,
      cy: 10 + rand() * 80,
      rx: (pro ? 16 : 22) + rand() * (pro ? 26 : 30),
      ry: (pro ? 16 : 22) + rand() * (pro ? 26 : 30),
      rot: rand() * 360,
      color: colors[Math.floor(rand() * colors.length)],
      op: (pro ? 0.35 : 0.45) + rand() * 0.35,
    });
  }
  const dots = [];
  const dotCount = Math.round(((pro ? 40 : 18) + Math.floor(rand() * (pro ? 30 : 14))) * densityMult);
  for (let i = 0; i < dotCount; i++) {
    dots.push({ id: i, x: rand() * 100, y: rand() * 100, r: 0.25 + rand() * (pro ? 1 : 0.8), op: 0.12 + rand() * 0.35 });
  }
  return { blobs, dots, palette: colors, pro, mood: aiPlan?.mood };
}

async function planArt(prompt) {
  const system =
    "Sen bir görsel sanat yönetmenisin. Kullanıcının verdiği görsel açıklamasını oku ve buna uygun soyut bir kompozisyon öner. " +
    "SADECE şu formatta JSON döndür, başka hiçbir açıklama ekleme: " +
    '{"colors":["#hex1","#hex2","#hex3"],"density":"sparse|medium|dense","mood":"kısa bir kelime"} ' +
    "Renkleri açıklamanın ruh haline göre seç (ör. gün batımı -> turuncu/pembe/kırmızı, orman -> yeşil tonları, uzay -> lacivert/mor, deniz -> mavi tonları).";
  try {
    const raw = await callClaude([{ role: "user", content: prompt }], system);
    const clean = raw.replace(/```json|```/g, "").trim();
    const parsed = JSON.parse(clean);
    if (Array.isArray(parsed.colors) && parsed.colors.length >= 2) return parsed;
  } catch (e) {
    /* aşağıda yerel palete düşülüyor */
  }
  return null;
}

async function callClaude(messages, systemPrompt) {
  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "claude-sonnet-4-6",
      max_tokens: 1000,
      system: systemPrompt,
      messages: messages.map((m) => {
        if (m.attachment?.isImage) {
          return {
            role: m.role,
            content: [
              { type: "image", source: { type: "base64", media_type: m.attachment.mediaType, data: m.attachment.base64 } },
              { type: "text", text: m.content || "Bu görseli değerlendirir misin?" },
            ],
          };
        }
        if (m.attachment) {
          return { role: m.role, content: `${m.content}\n\n[Ek dosya: ${m.attachment.name}]` };
        }
        return { role: m.role, content: m.content };
      }),
    }),
  });
  const data = await response.json();
  const text = (data.content || []).map((c) => c.text || "").join("\n").trim();
  return text || "Bir yanıt üretilemedi, tekrar dener misin?";
}

// NOTE: bu anahtar tarayıcıdan doğrudan çağrıldığı için kod içinde ve ağ isteklerinde
// görünür durumda. Üretime alırken bunu bir sunucu tarafına taşımanı öneririm.
const GEMINI_API_KEY = "AQ.Ab8RN6JUwyOhgmSqFTS7lyC9mfgOits7AjyTw9lPF9AYZvthIw";

// TODO: Gerçek bir OpenAI anahtarın varsa buraya koy. Bu artifact ortamı yalnızca
// api.anthropic.com'a erişebildiği için burada gerçek bir istek atmıyor — aynı callGemini
// gibi ileride kendi sunucunda proxy'leyeceğin senaryo için referans olarak duruyor.
const OPENAI_API_KEY = "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";

async function callOpenAI(messages, systemPrompt) {
  const response = await fetch("https://api.openai.com/v1/chat/completions", {
    method: "POST",
    headers: { "Content-Type": "application/json", Authorization: `Bearer ${OPENAI_API_KEY}` },
    body: JSON.stringify({
      model: "gpt-4o-mini",
      messages: [{ role: "system", content: systemPrompt }, ...messages.map((m) => ({ role: m.role, content: m.content }))],
    }),
  });
  const data = await response.json();
  return data.choices?.[0]?.message?.content?.trim() || "Bir yanıt üretilemedi, tekrar dener misin?";
}

// TODO: Buraya gerçek ödeme sayfanın linkini koy — ör. bir Stripe Payment Link
// ("https://buy.stripe.com/..."), iyzico/PayTR checkout linki ya da mağaza sayfan.
// Boş bırakılırsa "Yükselt" butonu demo modda kalır ve gerçek ödeme almaz.
const PAYMENT_URL = "";

async function callGemini(messages, systemPrompt) {
  const response = await fetch(
    "https://generativelanguage.googleapis.com/v1beta/models/gemini-flash-latest:generateContent",
    {
      method: "POST",
      headers: { "Content-Type": "application/json", "X-goog-api-key": GEMINI_API_KEY },
      body: JSON.stringify({
        systemInstruction: { parts: [{ text: systemPrompt }] },
        contents: messages.map((m) => ({
          role: m.role === "assistant" ? "model" : "user",
          parts: [{ text: m.content }],
        })),
      }),
    }
  );
  const data = await response.json();
  const text = (data.candidates?.[0]?.content?.parts || []).map((p) => p.text || "").join("\n").trim();
  return text || "Bir yanıt üretilemedi, tekrar dener misin?";
}

// NOT: Bu artifact ortamı yalnızca api.anthropic.com'a ağ erişimine izin veriyor.
// Dış servislere (ör. generativelanguage.googleapis.com, api.openai.com) yapılan istekler
// bu sanal alan tarafından engellendiği için Gemini/OpenAI anahtarları burada gerçek bir
// istek atamıyor. callGemini/callOpenAI fonksiyonları ileride kendi sunucun üzerinden
// proxy'leyeceğin senaryo için referans olarak bırakıldı, şu an kullanılmıyor.
async function callModel(model, messages, systemPrompt) {
  return callClaude(messages, systemPrompt);
}

/* ---------------------------------- chat panel (shared by Sohbet & Kod) ---------------------------------- */

function ChatPanel({ chat, onSend, loading, placeholder, emptyTitle, emptyHint, mono, model, onOpenModelPicker }) {
  const [text, setText] = useState("");
  const [attachment, setAttachment] = useState(null);
  const bottomRef = useRef(null);
  const fileRef = useRef(null);

  useEffect(() => {
    bottomRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [chat?.messages?.length, loading]);

  const submit = () => {
    const t = text.trim();
    if ((!t && !attachment) || loading) return;
    onSend(t, attachment);
    setText("");
    setAttachment(null);
  };

  const handleFile = (e) => {
    const file = e.target.files?.[0];
    e.target.value = "";
    if (!file) return;
    if (file.type.startsWith("image/")) {
      const reader = new FileReader();
      reader.onload = () => {
        const base64 = String(reader.result).split(",")[1];
        setAttachment({ name: file.name, isImage: true, mediaType: file.type, base64, previewUrl: String(reader.result) });
      };
      reader.readAsDataURL(file);
    } else {
      setAttachment({ name: file.name, isImage: false });
    }
  };

  return (
    <div className="flex flex-col h-full">
      <div className="flex-1 overflow-y-auto overscroll-contain px-4 py-4 space-y-3">
        {(!chat || chat.messages.length === 0) && (
          <div className="h-full flex flex-col items-center justify-center text-center px-6 text-slate-500">
            <p className="text-slate-300 font-semibold text-base mb-1">{emptyTitle}</p>
            <p className="text-sm">{emptyHint}</p>
          </div>
        )}
        {chat?.messages.map((m, i) => (
          <div key={i} className={`flex ${m.role === "user" ? "justify-end" : "justify-start"}`}>
            <div
              className={`max-w-[85%] rounded-2xl px-4 py-2.5 text-sm leading-relaxed whitespace-pre-wrap ${
                m.role === "user"
                  ? "bg-gradient-to-br from-blue-500 to-blue-600 text-white rounded-br-sm"
                  : "bg-slate-800 text-slate-100 rounded-bl-sm"
              } ${mono && m.role !== "user" ? "font-mono text-[13px]" : ""}`}
            >
              {m.attachment?.isImage && (
                <img src={m.attachment.previewUrl} alt={m.attachment.name} className="rounded-lg mb-2 max-h-40 object-cover" />
              )}
              {m.attachment && !m.attachment.isImage && (
                <div className="flex items-center gap-1.5 bg-black/15 rounded-lg px-2 py-1 mb-2 text-xs">
                  <IconPaperclip className="w-3.5 h-3.5" /> {m.attachment.name}
                </div>
              )}
              {m.content}
            </div>
          </div>
        ))}
        {loading && (
          <div className="flex justify-start">
            <div className="bg-slate-800 text-slate-400 rounded-2xl rounded-bl-sm px-4 py-2.5 text-sm">
              yazıyor…
            </div>
          </div>
        )}
        <div ref={bottomRef} />
      </div>

      <div className="border-t border-slate-800 p-3 bg-slate-950 space-y-2">
        {attachment && (
          <div className="flex items-center gap-2 bg-slate-900 border border-slate-800 rounded-xl px-3 py-1.5 w-fit">
            {attachment.isImage ? (
              <img src={attachment.previewUrl} alt="" className="w-6 h-6 rounded object-cover" />
            ) : (
              <IconPaperclip className="w-3.5 h-3.5 text-slate-400" />
            )}
            <span className="text-xs text-slate-300 max-w-[140px] truncate">{attachment.name}</span>
            <button onClick={() => setAttachment(null)} className="text-slate-500 hover:text-red-400">
              <IconClose className="w-3.5 h-3.5" />
            </button>
          </div>
        )}
        <textarea
          value={text}
          onChange={(e) => setText(e.target.value)}
          onKeyDown={(e) => {
            if (e.key === "Enter" && !e.shiftKey) {
              e.preventDefault();
              submit();
            }
          }}
          placeholder={placeholder}
          rows={1}
          className="w-full resize-none bg-slate-900 border border-slate-700 rounded-2xl px-3.5 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500 max-h-28"
        />
        <div className="flex items-center justify-between">
          <div className="flex items-center gap-1.5">
            <input ref={fileRef} type="file" accept="image/*,.pdf,.txt,.doc,.docx" className="hidden" onChange={handleFile} />
            <button
              onClick={() => fileRef.current?.click()}
              className="w-8 h-8 flex items-center justify-center rounded-full bg-slate-900 border border-slate-800 text-slate-400 active:scale-90 transition"
              aria-label="Dosya ekle"
            >
              <IconPaperclip className="w-4 h-4" />
            </button>
            <button
              onClick={onOpenModelPicker}
              className="flex items-center gap-1 h-8 px-2.5 rounded-full bg-slate-900 border border-slate-800 text-slate-300 text-xs font-medium active:scale-95 transition"
            >
              {model !== "c-azer" &&
                (() => {
                  const Icon = MODELS[model].icon;
                  const a = ACCENT_CLASSES[MODELS[model].accent];
                  return <Icon className={`w-3 h-3 ${a.text}`} />;
                })()}
              {MODELS[model].name}
              <IconChevron className="w-3 h-3 text-slate-500" />
            </button>
          </div>
          <button
            onClick={submit}
            disabled={loading || (!text.trim() && !attachment)}
            className="shrink-0 w-10 h-10 rounded-full bg-gradient-to-br from-blue-400 to-blue-600 disabled:from-slate-800 disabled:to-slate-800 disabled:text-slate-600 text-white flex items-center justify-center shadow-lg shadow-blue-500/25 active:scale-90 transition"
          >
            <IconSend className="w-4 h-4" />
          </button>
        </div>
      </div>
    </div>
  );
}

const IconAmd = (p) => (
  <svg viewBox="0 0 24 24" fill="currentColor" {...p}>
    <path d="M12 2 3 7v10l9 5 9-5V7l-9-5zm0 2.3 6.7 3.7L12 11.7 5.3 8 12 4.3zM5 9.7l6 3.3v6.7l-6-3.3V9.7zm8 10v-6.7l6-3.3v6.7l-6 3.3z" />
  </svg>
);
const IconEye = (p) => (
  <svg {...iconProps} {...p}><path d="M2 12s3.5-7 10-7 10 7 10 7-3.5 7-10 7-10-7-10-7z" /><circle cx="12" cy="12" r="3" /></svg>
);
const IconEyeOff = (p) => (
  <svg {...iconProps} {...p}><path d="M3 3l18 18" /><path d="M10.6 5.2A10.6 10.6 0 0 1 12 5c6.5 0 10 7 10 7a15.6 15.6 0 0 1-3.2 4.1M6.6 6.6C4 8.3 2 12 2 12s3.5 7 10 7c1.4 0 2.6-.3 3.7-.8" /><path d="M9.9 9.9a3 3 0 0 0 4.2 4.2" /></svg>
);
const IconMail = (p) => (
  <svg {...iconProps} {...p}><rect x="3" y="5" width="18" height="14" rx="2" /><path d="M3 7l9 6 9-6" /></svg>
);
const IconLock = (p) => (
  <svg {...iconProps} {...p}><rect x="5" y="11" width="14" height="9" rx="2" /><path d="M8 11V7a4 4 0 0 1 8 0v4" /></svg>
);
const IconGoogle = (p) => (
  <svg viewBox="0 0 24 24" {...p}>
    <path fill="#4285F4" d="M22.5 12.2c0-.8-.1-1.5-.2-2.2H12v4.3h5.9c-.3 1.4-1 2.6-2.2 3.4v2.8h3.6c2.1-1.9 3.2-4.8 3.2-8.3z" />
    <path fill="#34A853" d="M12 23c3 0 5.4-1 7.3-2.6l-3.6-2.8c-1 .7-2.2 1.1-3.7 1.1-2.8 0-5.2-1.9-6.1-4.4H2.2v2.8C4.1 20.6 7.8 23 12 23z" />
    <path fill="#FBBC05" d="M5.9 14.3a6.6 6.6 0 0 1 0-4.6V6.9H2.2a11 11 0 0 0 0 10.2l3.7-2.8z" />
    <path fill="#EA4335" d="M12 5.4c1.6 0 3.1.6 4.3 1.6l3.2-3.2C17.4 1.9 15 1 12 1 7.8 1 4.1 3.4 2.2 6.9l3.7 2.8c.9-2.5 3.3-4.3 6.1-4.3z" />
  </svg>
);

/* ---------------------------------- login screen ---------------------------------- */

function LoginScreen({ onLogin }) {
  const [mode, setMode] = useState("login"); // 'login' | 'signup'
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [confirm, setConfirm] = useState("");
  const [showPw, setShowPw] = useState(false);
  const [agree, setAgree] = useState(false);
  const [error, setError] = useState("");
  const [busy, setBusy] = useState(false);

  const validate = () => {
    if (mode === "signup" && name.trim().length < 2) return "Adını gir.";
    if (!/^\S+@\S+\.\S+$/.test(email)) return "Geçerli bir e-posta adresi gir.";
    if (password.length < 6) return "Şifre en az 6 karakter olmalı.";
    if (mode === "signup" && password !== confirm) return "Şifreler uyuşmuyor.";
    if (mode === "signup" && !agree) return "Devam etmek için kullanım şartlarını onaylamalısın.";
    return "";
  };

  const submit = (e) => {
    e.preventDefault();
    const err = validate();
    if (err) {
      setError(err);
      return;
    }
    setError("");
    setBusy(true);
    // TODO(Firebase): mode === "signup" -> createUserWithEmailAndPassword
    // mode === "login"  -> signInWithEmailAndPassword
    setTimeout(() => {
      setBusy(false);
      onLogin({ name: name || email.split("@")[0], email });
    }, 500);
  };

  const googleLogin = () => {
    setBusy(true);
    // TODO(Firebase): signInWithPopup(auth, new GoogleAuthProvider())
    setTimeout(() => {
      setBusy(false);
      onLogin({ name: "Google Kullanıcısı", email: "google@ornek.com" });
    }, 500);
  };

  return (
    <div className="w-full h-full overflow-y-auto overscroll-contain flex flex-col items-center justify-center px-6 py-10 bg-slate-950">
      <Logo size={44} />
      <h1 className="text-lg font-semibold mt-3 tracking-tight">
        {mode === "login" ? "Tekrar hoş geldin" : "Hesap oluştur"}
      </h1>
      <p className="text-xs text-slate-500 mb-7 text-center">
        {mode === "login" ? "Devam etmek için giriş yap" : "C-Azer'i kullanmaya birkaç adımda başla"}
      </p>

      <form key={mode} onSubmit={submit} className="w-full max-w-xs space-y-3 animate-tabIn">
        {mode === "signup" && (
          <div className="relative">
            <IconUser className="w-4 h-4 text-slate-500 absolute left-3 top-1/2 -translate-y-1/2" />
            <input
              value={name}
              onChange={(e) => setName(e.target.value)}
              placeholder="Ad Soyad"
              className="w-full bg-slate-900 border border-slate-700 rounded-xl pl-9 pr-3.5 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
          </div>
        )}
        <div className="relative">
          <IconMail className="w-4 h-4 text-slate-500 absolute left-3 top-1/2 -translate-y-1/2" />
          <input
            value={email}
            onChange={(e) => setEmail(e.target.value)}
            type="email"
            placeholder="E-posta"
            className="w-full bg-slate-900 border border-slate-700 rounded-xl pl-9 pr-3.5 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div className="relative">
          <IconLock className="w-4 h-4 text-slate-500 absolute left-3 top-1/2 -translate-y-1/2" />
          <input
            value={password}
            onChange={(e) => setPassword(e.target.value)}
            type={showPw ? "text" : "password"}
            placeholder="Şifre (en az 6 karakter)"
            className="w-full bg-slate-900 border border-slate-700 rounded-xl pl-9 pr-9 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
          <button
            type="button"
            onClick={() => setShowPw((v) => !v)}
            className="absolute right-3 top-1/2 -translate-y-1/2 text-slate-500"
          >
            {showPw ? <IconEyeOff className="w-4 h-4" /> : <IconEye className="w-4 h-4" />}
          </button>
        </div>
        {mode === "signup" && (
          <div className="relative">
            <IconLock className="w-4 h-4 text-slate-500 absolute left-3 top-1/2 -translate-y-1/2" />
            <input
              value={confirm}
              onChange={(e) => setConfirm(e.target.value)}
              type={showPw ? "text" : "password"}
              placeholder="Şifreyi tekrar gir"
              className="w-full bg-slate-900 border border-slate-700 rounded-xl pl-9 pr-3.5 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
          </div>
        )}
        {mode === "signup" && (
          <label className="flex items-start gap-2 text-[11px] text-slate-400 pt-1 cursor-pointer">
            <input
              type="checkbox"
              checked={agree}
              onChange={(e) => setAgree(e.target.checked)}
              className="mt-0.5 accent-blue-500"
            />
            Kullanım şartlarını ve gizlilik politikasını okudum, kabul ediyorum.
          </label>
        )}
        {error && <p className="text-xs text-red-400">{error}</p>}
        {mode === "login" && (
          <div className="text-right">
            <button type="button" className="text-[11px] text-blue-400">Şifremi unuttum</button>
          </div>
        )}
        <button
          type="submit"
          disabled={busy}
          className="w-full py-2.5 rounded-xl bg-gradient-to-br from-blue-400 to-blue-600 disabled:opacity-60 text-white text-sm font-semibold active:scale-95 transition shadow-lg shadow-blue-500/25"
        >
          {busy ? "Bir saniye…" : mode === "login" ? "Giriş Yap" : "Kayıt Ol"}
        </button>
      </form>

      <div className="w-full max-w-xs flex items-center gap-3 my-5">
        <div className="flex-1 h-px bg-slate-800" />
        <span className="text-[11px] text-slate-600">veya</span>
        <div className="flex-1 h-px bg-slate-800" />
      </div>

      <button
        onClick={googleLogin}
        disabled={busy}
        className="w-full max-w-xs flex items-center justify-center gap-2 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm font-medium active:scale-95 transition disabled:opacity-60"
      >
        <IconGoogle className="w-4 h-4" /> Google ile devam et
      </button>

      <button
        onClick={() => {
          setMode((m) => (m === "login" ? "signup" : "login"));
          setError("");
        }}
        className="text-xs text-slate-500 mt-6"
      >
        {mode === "login" ? "Hesabın yok mu? " : "Zaten hesabın var mı? "}
        <span className="text-blue-400 font-medium">{mode === "login" ? "Kayıt ol" : "Giriş yap"}</span>
      </button>
    </div>
  );
}

const MODELS = {
  "c-azer": {
    id: "c-azer",
    name: "C-Azer",
    tag: "Standart",
    desc: "Günlük sohbet ve kod için hızlı, dengeli model.",
    icon: Logo,
    accent: "cyan",
  },
  "c-wq": {
    id: "c-wq",
    name: "C-Wq",
    tag: "ÜST DÜZEY",
    desc: "Daha derin akıl yürütür. Ücretsizde sınırlı önizleme — tam gücü Plus'ta açılır.",
    icon: IconCrown,
    accent: "amber",
  },
  "c-amd": {
    id: "c-amd",
    name: "C-Amd",
    tag: "ALTERNATİF",
    desc: "Daha yaratıcı ve doğal bir sohbet tarzı sunan alternatif model.",
    icon: IconAmd,
    accent: "emerald",
  },
};

const ACCENT_CLASSES = {
  cyan: { bg: "bg-cyan-500/15", text: "text-cyan-400", border: "border-cyan-500", ring: "bg-cyan-500/5" },
  amber: { bg: "bg-amber-400/15", text: "text-amber-400", border: "border-amber-400", ring: "bg-amber-400/5" },
  emerald: { bg: "bg-emerald-400/15", text: "text-emerald-400", border: "border-emerald-400", ring: "bg-emerald-400/5" },
};

const WQ_FREE_LIMIT = 4;
const ART_FREE_LIMIT = 3;

export default function CAzerApp() {
  const [user, setUser] = useState(null); // { name, email } | null
  const [tab, setTab] = useState("sohbet");
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const [isPlus, setIsPlus] = useState(false);
  const [notify, setNotify] = useState(true);
  const [purchaseMsg, setPurchaseMsg] = useState("");
  const [model, setModel] = useState("c-azer");
  const [modelPickerOpen, setModelPickerOpen] = useState(false);
  const [wqCount, setWqCount] = useState(0);
  const [artFreeCount, setArtFreeCount] = useState(0);
  const [upgradeReason, setUpgradeReason] = useState(null); // 'wq' | 'gorsel' | null

  // Sayfanın kaydırılıp zıplamasını (rubber-band) engelle
  useEffect(() => {
    const prevBody = document.body.style.overflow;
    const prevHtml = document.documentElement.style.overflow;
    document.body.style.overflow = "hidden";
    document.documentElement.style.overflow = "hidden";
    return () => {
      document.body.style.overflow = prevBody;
      document.documentElement.style.overflow = prevHtml;
    };
  }, []);

  const mkChat = (title) => ({ id: uid(), title, messages: [] });

  const [sections, setSections] = useState({
    sohbet: { chats: [mkChat("Yeni Sohbet")], activeId: null },
    kod: { chats: [mkChat("Yeni Kod Oturumu")], activeId: null },
  });
  useEffect(() => {
    setSections((s) => ({
      sohbet: { ...s.sohbet, activeId: s.sohbet.chats[0].id },
      kod: { ...s.kod, activeId: s.kod.chats[0].id },
    }));
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);

  const [loading, setLoading] = useState(false);
  const [artPrompt, setArtPrompt] = useState("");
  const [artItems, setArtItems] = useState([]);
  const [artLoading, setArtLoading] = useState(false);

  const activeSection = tab === "kod" ? "kod" : "sohbet";
  const secData = sections[activeSection];
  const activeChat = secData?.chats.find((c) => c.id === secData.activeId) || null;

  const newChat = (section) => {
    const title = section === "kod" ? "Yeni Kod Oturumu" : "Yeni Sohbet";
    setSections((s) => {
      const chat = mkChat(title);
      return { ...s, [section]: { chats: [chat, ...s[section].chats], activeId: chat.id } };
    });
    setSidebarOpen(false);
  };

  const deleteChat = (section, id) => {
    setSections((s) => {
      const remaining = s[section].chats.filter((c) => c.id !== id);
      const chats = remaining.length ? remaining : [mkChat(section === "kod" ? "Yeni Kod Oturumu" : "Yeni Sohbet")];
      const activeId = s[section].activeId === id ? chats[0].id : s[section].activeId;
      return { ...s, [section]: { chats, activeId } };
    });
  };

  const selectChat = (section, id) => {
    setSections((s) => ({ ...s, [section]: { ...s[section], activeId: id } }));
    setSidebarOpen(false);
  };

  const send = useCallback(
    async (section, text, attachment) => {
      if (model === "c-wq" && !isPlus && wqCount >= WQ_FREE_LIMIT) {
        setUpgradeReason("wq");
        return;
      }
      const chatId = sections[section].activeId;
      const userMsg = { role: "user", content: text, attachment: attachment || undefined };

      setSections((s) => ({
        ...s,
        [section]: {
          ...s[section],
          chats: s[section].chats.map((c) =>
            c.id === chatId
              ? { ...c, title: c.messages.length === 0 ? (text || attachment?.name || "Sohbet").slice(0, 28) : c.title, messages: [...c.messages, userMsg] }
              : c
          ),
        },
      }));
      if (model === "c-wq" && !isPlus) setWqCount((n) => n + 1);
      setLoading(true);
      try {
        const history = [...(sections[section].chats.find((c) => c.id === chatId)?.messages || []), userMsg];
        const base =
          section === "kod"
            ? "Sadece programlama, kod yazma, hata ayıklama ve teknik konularda yardım ediyorsun. Kod bloklarını net ver, kısa açıklamalar ekle."
            : "Türkçe konuşan, samimi ve yardımsever bir yapay zeka sohbet asistanısın.";
        let system;
        if (model === "c-wq" && isPlus) {
          system = `Sen C-Wq isimli, C-Azer Plus'ın en üst düzey modelisin. ${base} Yanıt vermeden önce konuyu birkaç açıdan değerlendir, olası hataları ve alternatifleri düşün, ardından en derinlemesine, gerekçeli ve kapsamlı yanıtı ver. Türkçe yanıt ver.`;
        } else if (model === "c-wq") {
          system = `Sen C-Wq isimli modelin ücretsiz önizleme moduysun — tam gücün Plus üyelikte açılıyor. ${base} Orta uzunlukta, standart bir yanıt ver, Plus'taki kadar derinlemesine analiz yapma. Türkçe yanıt ver.`;
        } else if (model === "c-amd") {
          system = `Sen C-Amd isimli bir yapay zeka asistanısın. ${base} Daha sohbet havasında, yaratıcı ve akıcı bir üslup kullan; örnekler ve benzetmelerle anlat. Türkçe yanıt ver.`;
        } else {
          system = `Sen C-Azer isimli bir yapay zeka asistanısın. ${base} Kısa ve net yanıtlar ver. Türkçe yanıt ver.`;
        }
        const reply = await callModel(model, history, system);
        setSections((s) => ({
          ...s,
          [section]: {
            ...s[section],
            chats: s[section].chats.map((c) =>
              c.id === chatId ? { ...c, messages: [...c.messages, { role: "assistant", content: reply }] } : c
            ),
          },
        }));
      } catch (e) {
        setSections((s) => ({
          ...s,
          [section]: {
            ...s[section],
            chats: s[section].chats.map((c) =>
              c.id === chatId
                ? { ...c, messages: [...c.messages, { role: "assistant", content: "Bağlantı hatası oluştu. Lütfen tekrar dene." }] }
                : c
            ),
          },
        }));
      } finally {
        setLoading(false);
      }
    },
    [sections, model, isPlus, wqCount]
  );

  const generateImage = async () => {
    if (!artPrompt.trim() || artLoading) return;
    if (!isPlus && artFreeCount >= ART_FREE_LIMIT) {
      setUpgradeReason("gorsel");
      return;
    }
    const promptText = artPrompt.trim();
    setArtLoading(true);
    setArtPrompt("");
    try {
      const aiPlan = await planArt(promptText);
      const art = generateArt(promptText, isPlus, aiPlan);
      setArtItems((prev) => [{ id: uid(), prompt: promptText, ...art }, ...prev]);
      if (!isPlus) setArtFreeCount((n) => n + 1);
    } finally {
      setArtLoading(false);
    }
  };

  const buyPlus = () => {
    if (PAYMENT_URL) {
      window.open(PAYMENT_URL, "_blank");
      return;
    }
    setIsPlus(true);
    setPurchaseMsg("Demo modu: ödeme linki henüz tanımlı değil (PAYMENT_URL). Gerçek link eklenince buradan yönlendirme yapılacak.");
    setTimeout(() => setPurchaseMsg(""), 5000);
  };

  const tabs = [
    { key: "sohbet", label: "Sohbet", icon: IconChat },
    { key: "kod", label: "Kod", icon: IconCode },
    { key: "gorsel", label: "Görsel", icon: IconImage },
    { key: "ayarlar", label: "Ayarlar", icon: IconSettings },
  ];

  const headerTitle = tabs.find((t) => t.key === tab)?.label || "";

  if (!user) {
    return (
      <div style={{ position: "fixed", inset: 0, height: "100dvh" }}>
        <LoginScreen onLogin={setUser} />
      </div>
    );
  }

  return (
    <div
      className="bg-slate-950 text-slate-100 flex flex-col overflow-hidden overscroll-none"
      style={{ fontFamily: "'Sora', ui-sans-serif, system-ui", position: "fixed", inset: 0, height: "100dvh" }}
    >
      {/* Header */}
      <div className="flex items-center gap-3 px-4 h-14 border-b border-slate-800 shrink-0 bg-slate-950 z-20">
        <button
          onClick={() => setSidebarOpen(true)}
          className="w-9 h-9 flex items-center justify-center rounded-lg hover:bg-slate-900 active:scale-95 transition"
          aria-label="Menü"
        >
          <IconMenu className="w-5 h-5 text-slate-300" />
        </button>
        <Logo size={22} />
        <div className="flex flex-col leading-tight">
          <span className="font-semibold text-[15px] tracking-tight">C-Azer</span>
          <span className="text-[11px] text-slate-500 -mt-0.5">{headerTitle}</span>
        </div>
        {isPlus && (
          <span className="ml-auto flex items-center gap-1 text-[11px] font-medium text-amber-400 bg-amber-400/10 px-2 py-1 rounded-full">
            <IconCrown className="w-3 h-3" /> Plus
          </span>
        )}
      </div>

      {/* Content */}
      <div key={tab} className="flex-1 min-h-0 animate-tabIn">
        {tab === "sohbet" && (
          <ChatPanel
            chat={activeChat}
            loading={loading}
            onSend={(t, a) => send("sohbet", t, a)}
            placeholder="C-Azer'e bir şey sor…"
            emptyTitle="Sohbete başla"
            emptyHint="Aklındaki her şeyi C-Azer'e sorabilirsin."
            model={model}
            onOpenModelPicker={() => setModelPickerOpen(true)}
          />
        )}
        {tab === "kod" && (
          <ChatPanel
            chat={activeChat}
            loading={loading}
            onSend={(t, a) => send("kod", t, a)}
            placeholder="Bir kod isteği yaz…"
            emptyTitle="Kod modu"
            emptyHint="Fonksiyon, hata ayıklama veya kod açıklaması iste."
            mono
            model={model}
            onOpenModelPicker={() => setModelPickerOpen(true)}
          />
        )}
        {tab === "gorsel" && (
          <div className="flex flex-col h-full">
            <div className="flex-1 overflow-y-auto overscroll-contain p-4">
              {artItems.length === 0 && !artLoading && (
                <div className="h-full flex flex-col items-center justify-center text-center px-6 text-slate-500">
                  <IconSparkle className="w-8 h-8 mb-2 text-blue-400/60" />
                  <p className="text-slate-300 font-semibold text-base mb-1">Görsel oluştur</p>
                  <p className="text-sm">Bir tanım yaz, C-Azer senin için soyut bir kompozisyon üretsin.</p>
                </div>
              )}
              <div className="grid grid-cols-2 gap-3">
                {artLoading && (
                  <div className="aspect-square rounded-2xl bg-slate-900 border border-slate-800 animate-pulse" />
                )}
                {artItems.map((art) => (
                  <div key={art.id} className="relative rounded-2xl overflow-hidden border border-slate-800 bg-slate-900">
                    {art.pro && (
                      <span className="absolute top-1.5 right-1.5 z-10 flex items-center gap-0.5 text-[9px] font-semibold text-amber-300 bg-slate-950/70 backdrop-blur px-1.5 py-0.5 rounded-full">
                        <IconCrown className="w-2.5 h-2.5" /> PLUS
                      </span>
                    )}
                    <svg viewBox="0 0 100 100" className="w-full aspect-square">
                      <defs>
                        <filter id={`blur-${art.id}`} x="-50%" y="-50%" width="200%" height="200%">
                          <feGaussianBlur stdDeviation={art.pro ? 6 : 9} />
                        </filter>
                      </defs>
                      <rect width="100" height="100" fill="#0b1220" />
                      <g filter={`url(#blur-${art.id})`}>
                        {art.blobs.map((b) => (
                          <ellipse
                            key={b.id}
                            cx={b.cx}
                            cy={b.cy}
                            rx={b.rx}
                            ry={b.ry}
                            fill={b.color}
                            opacity={b.op}
                            transform={`rotate(${b.rot} ${b.cx} ${b.cy})`}
                          />
                        ))}
                      </g>
                      {art.dots.map((d) => (
                        <circle key={d.id} cx={d.x} cy={d.y} r={d.r} fill="#fff" opacity={d.op} />
                      ))}
                    </svg>
                    <p className="text-[11px] text-slate-400 px-2 py-1.5 truncate">
                      {art.prompt}
                      {art.mood && <span className="text-slate-600"> · {art.mood}</span>}
                    </p>
                  </div>
                ))}
              </div>
              {!isPlus && (
                <p className="text-[11px] text-slate-500 text-center mt-3">
                  {Math.max(ART_FREE_LIMIT - artFreeCount, 0)}/{ART_FREE_LIMIT} ücretsiz görsel hakkı kaldı ·{" "}
                  <button onClick={() => setUpgradeReason("gorsel")} className="text-amber-400 underline underline-offset-2">
                    Plus ile sınırsız ve daha detaylı
                  </button>
                </p>
              )}
            </div>
            <div className="border-t border-slate-800 p-3 flex items-end gap-2 bg-slate-950">
              <input
                value={artPrompt}
                onChange={(e) => setArtPrompt(e.target.value)}
                onKeyDown={(e) => e.key === "Enter" && generateImage()}
                placeholder="Örn: uzayda gün batımı"
                className="flex-1 bg-slate-900 border border-slate-700 rounded-xl px-3 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500"
              />
              <button
                onClick={generateImage}
                disabled={artLoading || !artPrompt.trim()}
                className="shrink-0 h-10 px-4 rounded-xl bg-gradient-to-br from-blue-400 to-blue-600 disabled:from-slate-800 disabled:to-slate-800 disabled:text-slate-600 text-white text-sm font-medium flex items-center gap-1.5 active:scale-95 transition"
              >
                <IconSparkle className="w-4 h-4" /> Oluştur
              </button>
            </div>
          </div>
        )}
        {tab === "ayarlar" && (
          <div className="h-full overflow-y-auto overscroll-contain p-4 space-y-6">
            {/* Profil */}
            <div>
              <p className="text-xs font-semibold text-slate-500 uppercase tracking-wide mb-2">Profil</p>
              <div className="flex items-center gap-3 bg-slate-900 border border-slate-800 rounded-2xl p-4">
                <div className="w-11 h-11 rounded-full bg-cyan-500/15 text-cyan-400 flex items-center justify-center">
                  <IconUser className="w-5 h-5" />
                </div>
                <div className="flex-1 min-w-0">
                  <p className="text-sm font-medium truncate">{user.name}</p>
                  <p className="text-xs text-slate-500">{isPlus ? "C-Azer Plus üye" : "Ücretsiz plan"}</p>
                </div>
                <button onClick={() => setUser(null)} className="text-xs text-slate-500 hover:text-red-400 shrink-0">
                  Çıkış yap
                </button>
              </div>
            </div>

            {/* Genel */}
            <div>
              <p className="text-xs font-semibold text-slate-500 uppercase tracking-wide mb-2">Genel</p>
              <div className="bg-slate-900 border border-slate-800 rounded-2xl divide-y divide-slate-800">
                <div className="flex items-center justify-between px-4 py-3">
                  <div className="flex items-center gap-2.5">
                    <IconBell className="w-4 h-4 text-slate-400" />
                    <span className="text-sm">Bildirimler</span>
                  </div>
                  <button
                    onClick={() => setNotify((v) => !v)}
                    className={`w-10 h-6 rounded-full transition relative ${notify ? "bg-cyan-500" : "bg-slate-700"}`}
                  >
                    <span className={`absolute top-0.5 w-5 h-5 rounded-full bg-white transition ${notify ? "left-4.5" : "left-0.5"}`} style={{ left: notify ? "18px" : "2px" }} />
                  </button>
                </div>
                <div className="flex items-center justify-between px-4 py-3">
                  <span className="text-sm">Karanlık mod</span>
                  <span className="text-xs text-slate-500">Aktif</span>
                </div>
                <button
                  onClick={() => setModelPickerOpen(true)}
                  className="w-full flex items-center justify-between px-4 py-3 active:bg-slate-800/60 transition"
                >
                  <span className="text-sm">Yapay zeka modeli</span>
                  <span className="flex items-center gap-1 text-xs text-slate-400">
                    {model !== "c-azer" &&
                      (() => {
                        const Icon = MODELS[model].icon;
                        const a = ACCENT_CLASSES[MODELS[model].accent];
                        return <Icon className={`w-3.5 h-3.5 ${a.text}`} />;
                      })()}
                    {MODELS[model].name}
                  </span>
                </button>
              </div>
            </div>

            {/* Mağaza */}
            <div>
              <p className="text-xs font-semibold text-slate-500 uppercase tracking-wide mb-2 flex items-center gap-1.5">
                <IconStore className="w-3.5 h-3.5" /> Mağaza
              </p>
              <div className="bg-gradient-to-br from-slate-900 to-slate-900 border border-amber-400/30 rounded-2xl p-5 relative overflow-hidden">
                <div className="flex items-center gap-2 mb-3">
                  <div className="w-9 h-9 rounded-xl bg-amber-400/15 text-amber-400 flex items-center justify-center">
                    <IconCrown className="w-5 h-5" />
                  </div>
                  <div>
                    <p className="font-semibold text-sm">C-Azer Plus</p>
                    <p className="text-xs text-slate-500">Yıllık üyelik</p>
                  </div>
                  <p className="ml-auto text-lg font-bold text-amber-400">980₺</p>
                </div>
                <ul className="space-y-1.5 mb-4">
                  {[
                    "C-Wq'nun tam gücü, sınırsız kullanım",
                    "Sınırsız ve daha detaylı görsel oluşturma",
                    "Gelişmiş kod modeli",
                    "Öncelikli destek",
                  ].map((f) => (
                    <li key={f} className="flex items-center gap-2 text-xs text-slate-300">
                      <IconCheck className="w-3.5 h-3.5 text-amber-400 shrink-0" /> {f}
                    </li>
                  ))}
                </ul>
                {isPlus ? (
                  <button disabled className="w-full py-2.5 rounded-xl bg-slate-800 text-slate-400 text-sm font-medium flex items-center justify-center gap-1.5">
                    <IconCheck className="w-4 h-4" /> Plus Üyesiniz
                  </button>
                ) : (
                  <button
                    onClick={buyPlus}
                    className="w-full py-2.5 rounded-xl bg-amber-400 text-slate-950 text-sm font-semibold active:scale-95 transition"
                  >
                    {PAYMENT_URL ? "Satın Al — 980₺/yıl" : "Yükselt — 980₺/yıl"}
                  </button>
                )}
                {!PAYMENT_URL && !isPlus && (
                  <p className="text-[10.5px] text-slate-600 mt-2 text-center">Ödeme sistemi henüz bağlanmadı — şu an demo modda</p>
                )}
                {purchaseMsg && <p className="text-[11px] text-amber-300 mt-2 text-center">{purchaseMsg}</p>}
              </div>
            </div>
          </div>
        )}
      </div>

      {/* Bottom nav — floating glass pill */}
      <div className="px-4 pb-3 pt-2 bg-slate-950 shrink-0 z-20">
        <div className="relative flex items-center justify-around rounded-full px-2 py-1.5 border border-blue-300/25 bg-blue-500/10 backdrop-blur-xl shadow-lg shadow-blue-500/20">
          <div className="pointer-events-none absolute inset-0 rounded-full bg-gradient-to-b from-white/10 to-transparent" />
          {tabs.map((t) => {
            const Icon = t.icon;
            const active = tab === t.key;
            return (
              <button
                key={t.key}
                onClick={() => setTab(t.key)}
                className="relative flex flex-col items-center justify-center gap-0.5 py-1.5 px-3 active:scale-90 transition"
              >
                <span
                  className={`flex items-center justify-center w-9 h-9 rounded-full transition ${
                    active ? "bg-blue-400/25" : "bg-transparent"
                  }`}
                >
                  <Icon className={`w-[18px] h-[18px] ${active ? "text-blue-300" : "text-slate-400"}`} />
                </span>
                <span className={`text-[10px] ${active ? "text-blue-300 font-medium" : "text-slate-500"}`}>{t.label}</span>
              </button>
            );
          })}
        </div>
      </div>

      {/* Sidebar drawer */}
      {sidebarOpen && (
        <div className="absolute inset-0 z-30 flex">
          <div className="absolute inset-0 bg-black/60" onClick={() => setSidebarOpen(false)} />
          <div className="relative w-[78%] max-w-xs h-full bg-slate-900 border-r border-slate-800 flex flex-col animate-[slideIn_0.2s_ease-out]">
            <div className="flex items-center justify-between px-4 h-14 border-b border-slate-800">
              <div className="flex items-center gap-2">
                <Logo size={20} />
                <span className="font-semibold text-sm">C-Azer</span>
              </div>
              <button onClick={() => setSidebarOpen(false)} className="w-8 h-8 flex items-center justify-center rounded-lg hover:bg-slate-800">
                <IconClose className="w-4 h-4 text-slate-400" />
              </button>
            </div>

            {(tab === "sohbet" || tab === "kod") ? (
              <>
                <div className="p-3">
                  <button
                    onClick={() => newChat(activeSection)}
                    className="w-full flex items-center gap-2 justify-center bg-cyan-500 text-slate-950 text-sm font-medium rounded-xl py-2.5 active:scale-95 transition"
                  >
                    <IconPlus className="w-4 h-4" /> Yeni {activeSection === "kod" ? "Kod Oturumu" : "Sohbet"}
                  </button>
                </div>
                <div className="flex-1 overflow-y-auto overscroll-contain px-2 pb-3 space-y-1">
                  <p className="px-2 py-1 text-[11px] font-semibold text-slate-500 uppercase tracking-wide">Geçmiş</p>
                  {secData.chats.map((c) => (
                    <div
                      key={c.id}
                      className={`group flex items-center gap-2 rounded-xl px-3 py-2.5 cursor-pointer ${
                        c.id === secData.activeId ? "bg-slate-800" : "hover:bg-slate-800/60"
                      }`}
                      onClick={() => selectChat(activeSection, c.id)}
                    >
                      <span className="flex-1 text-sm truncate text-slate-200">{c.title}</span>
                      <button
                        onClick={(e) => {
                          e.stopPropagation();
                          deleteChat(activeSection, c.id);
                        }}
                        className="opacity-60 hover:opacity-100 text-slate-500 hover:text-red-400 transition"
                        aria-label="Sohbeti sil"
                      >
                        <IconTrash className="w-4 h-4" />
                      </button>
                    </div>
                  ))}
                </div>
              </>
            ) : (
              <div className="flex-1 flex items-center justify-center text-center px-6 text-sm text-slate-500">
                Bu sekmede sohbet geçmişi bulunmuyor.
              </div>
            )}
          </div>
        </div>
      )}

      {/* Model seçim ekranı */}
      {modelPickerOpen && (
        <div className="absolute inset-0 z-40 flex items-end sm:items-center justify-center">
          <div className="absolute inset-0 bg-black/70" onClick={() => setModelPickerOpen(false)} />
          <div className="relative w-full sm:max-w-sm bg-slate-900 border border-slate-800 rounded-t-3xl sm:rounded-3xl p-4 pb-6 animate-modalIn">
            <div className="flex items-center justify-between mb-1 px-1">
              <p className="font-semibold text-base">Yapay zeka seç</p>
              <button onClick={() => setModelPickerOpen(false)} className="w-8 h-8 flex items-center justify-center rounded-lg hover:bg-slate-800">
                <IconClose className="w-4 h-4 text-slate-400" />
              </button>
            </div>
            <p className="text-xs text-slate-500 px-1 mb-4">Sohbet ve Kod modunda hangi model yanıt versin?</p>
            <div className="space-y-2.5">
              {Object.values(MODELS).map((m) => {
                const active = model === m.id;
                const a = ACCENT_CLASSES[m.accent];
                const Icon = m.icon;
                return (
                  <button
                    key={m.id}
                    onClick={() => {
                      setModel(m.id);
                      setModelPickerOpen(false);
                    }}
                    className={`w-full text-left rounded-2xl p-4 border transition active:scale-[0.98] ${
                      active ? `${a.border} ${a.ring}` : "border-slate-800 bg-slate-950 hover:bg-slate-800/40"
                    }`}
                  >
                    <div className="flex items-center gap-3">
                      <div className={`w-10 h-10 rounded-xl flex items-center justify-center shrink-0 ${a.bg} ${a.text}`}>
                        {m.id === "c-azer" ? <Logo size={20} /> : <Icon className="w-5 h-5" />}
                      </div>
                      <div className="flex-1 min-w-0">
                        <div className="flex items-center gap-2">
                          <span className="font-semibold text-sm">{m.name}</span>
                          <span className={`text-[9.5px] font-semibold px-1.5 py-0.5 rounded-full ${a.bg} ${a.text}`}>
                            {m.tag}
                          </span>
                        </div>
                        <p className="text-xs text-slate-500 mt-0.5 leading-snug">{m.desc}</p>
                      </div>
                      {active && (
                        <div className={`w-5 h-5 rounded-full ${a.text.replace("text-", "bg-")} text-slate-950 flex items-center justify-center shrink-0`}>
                          <IconCheck className="w-3 h-3" />
                        </div>
                      )}
                    </div>
                  </button>
                );
              })}
            </div>
          </div>
        </div>
      )}

      {/* Yükseltme (paywall) ekranı */}
      {upgradeReason && (
        <div className="absolute inset-0 z-40 flex items-end sm:items-center justify-center">
          <div className="absolute inset-0 bg-black/70" onClick={() => setUpgradeReason(null)} />
          <div className="relative w-full sm:max-w-sm bg-slate-900 border border-amber-400/30 rounded-t-3xl sm:rounded-3xl p-5 pb-6 animate-modalIn text-center">
            <button onClick={() => setUpgradeReason(null)} className="absolute top-3 right-3 w-8 h-8 flex items-center justify-center rounded-lg hover:bg-slate-800">
              <IconClose className="w-4 h-4 text-slate-400" />
            </button>
            <div className="w-14 h-14 rounded-2xl bg-amber-400/15 text-amber-400 flex items-center justify-center mx-auto mb-3">
              <IconCrown className="w-7 h-7" />
            </div>
            <p className="font-semibold text-base mb-1">
              {upgradeReason === "wq" ? "C-Wq önizleme hakkın doldu" : "Ücretsiz görsel hakkın doldu"}
            </p>
            <p className="text-xs text-slate-400 leading-relaxed mb-5 px-2">
              {upgradeReason === "wq"
                ? "C-Wq'nun tam gücü — en derin, en kapsamlı yanıtlar — sadece C-Azer Plus'ta. Plus'a geçince C-Wq sınırsız ve tam kapasiteyle çalışır."
                : "Plus'ta görsel oluşturma sınırsız ve çok daha detaylı, katmanlı bir motorla çalışır."}
            </p>
            <button
              onClick={() => {
                if (PAYMENT_URL) {
                  window.open(PAYMENT_URL, "_blank");
                } else {
                  setUpgradeReason(null);
                  setTab("ayarlar");
                }
              }}
              className="w-full py-2.5 rounded-xl bg-amber-400 text-slate-950 text-sm font-semibold active:scale-95 transition mb-2"
            >
              {PAYMENT_URL ? "Satın al" : "Plus'a bak"} — 980₺/yıl
            </button>
            <button onClick={() => setUpgradeReason(null)} className="text-xs text-slate-500">
              Şimdi değil
            </button>
          </div>
        </div>
      )}

      <style>{`
        @keyframes slideIn { from { transform: translateX(-100%);} to { transform: translateX(0);} }
        @keyframes modalIn { from { opacity: 0; transform: translateY(12px) scale(0.98);} to { opacity: 1; transform: translateY(0) scale(1);} }
        @keyframes tabIn { from { opacity: 0; transform: translateY(4px);} to { opacity: 1; transform: translateY(0);} }
        .animate-modalIn { animation: modalIn 0.22s ease-out; }
        .animate-tabIn { animation: tabIn 0.16s ease-out; }
      `}</style>
    </div>
  );
}
