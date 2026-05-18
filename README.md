import React, { useMemo, useState } from "react";
import { motion } from "framer-motion";
import {
  ArrowRight,
  CheckCircle2,
  ShieldCheck,
  Smartphone,
  Clock3,
  FileCheck2,
  Wallet,
  Menu,
  LockKeyhole,
  Sparkles,
} from "lucide-react";

const money = new Intl.NumberFormat("es-CO", {
  style: "currency",
  currency: "COP",
  maximumFractionDigits: 0,
});

const brand = {
  blue: "#4148f5",
  mint: "#7fffc9",
  navy: "#003153",
  soft: "#f5f8ff",
};

function formatShort(value) {
  return money.format(value).replace("COP", "$").replace(/\s/g, "");
}

function Logo({ light = false }) {
  return (
    <div className="leading-none">
      <div className={`font-poppins text-[30px] md:text-[34px] font-extrabold tracking-[-0.06em] ${light ? "text-white" : "text-[#4148f5]"}`}>
        RapiCredit<span className="align-top text-[20px]">▦</span>
      </div>
      <div className={`mt-1 text-center font-barlow text-[13px] tracking-[0.25em] ${light ? "text-white/80" : "text-[#4148f5]/80"}`}>
        Contigo siempre
      </div>
    </div>
  );
}

function RapiflexLogo({ className = "" }) {
  return (
    <div className={`font-poppins font-black tracking-[-0.08em] leading-none ${className}`}>
      Rapi<span className="relative inline-block">F<span className="absolute left-[38%] top-[10%] h-[24%] w-[65%] rounded-full bg-current opacity-100" /></span>lex
    </div>
  );
}

function GraphicRings({ className = "" }) {
  return (
    <div className={`pointer-events-none absolute ${className}`}>
      {[0, 1, 2, 3, 4].map((i) => (
        <div
          key={i}
          className="absolute rounded-full border-[5px] border-white/80"
          style={{
            width: 110 + i * 28,
            height: 110 + i * 28,
            left: -i * 14,
            top: -i * 14,
            clipPath: "polygon(0 0, 100% 0, 100% 85%, 0 85%)",
          }}
        />
      ))}
    </div>
  );
}

function Starburst({ className = "", color = brand.mint }) {
  return (
    <div className={`absolute h-20 w-20 ${className}`}>
      {Array.from({ length: 16 }).map((_, i) => (
        <span
          key={i}
          className="absolute left-1/2 top-1/2 h-10 w-3 origin-bottom rounded-full"
          style={{
            background: color,
            transform: `translate(-50%, -100%) rotate(${i * 22.5}deg)`,
          }}
        />
      ))}
    </div>
  );
}

function Dots({ className = "" }) {
  return (
    <div className={`absolute grid grid-cols-7 gap-2 opacity-60 ${className}`}>
      {Array.from({ length: 49 }).map((_, i) => (
        <span key={i} className="h-1 w-1 rounded-full bg-white" />
      ))}
    </div>
  );
}

function PhoneMock({ amount, days }) {
  return (
    <motion.div
      initial={{ y: 20, opacity: 0 }}
      animate={{ y: 0, opacity: 1 }}
      transition={{ duration: 0.7, delay: 0.2 }}
      className="relative mx-auto h-[420px] w-[218px] rounded-[34px] border-[8px] border-[#071c32] bg-white shadow-2xl md:h-[455px] md:w-[236px]"
    >
      <div className="absolute left-1/2 top-3 h-6 w-24 -translate-x-1/2 rounded-full bg-[#071c32]" />
      <div className="rounded-t-[25px] bg-[#4148f5] px-5 pb-16 pt-12 text-center text-white">
        <RapiflexLogo className="text-[26px]" />
      </div>
      <div className="-mt-10 mx-4 rounded-[24px] bg-white px-4 pb-5 pt-6 text-center shadow-xl">
        <motion.div
          key={`${amount}-${days}`}
          initial={{ scale: 0.85 }}
          animate={{ scale: 1 }}
          className="mx-auto flex h-20 w-20 items-center justify-center rounded-full bg-[#7fffc9] text-[#003153]"
        >
          <CheckCircle2 size={48} strokeWidth={2.6} />
        </motion.div>
        <p className="mt-4 font-poppins text-lg font-extrabold text-[#003153]">¡Solicitud aprobada!</p>
        <p className="mx-auto mt-2 max-w-[150px] font-barlow text-sm leading-tight text-[#38506c]">Tu dinero, listo cuando lo necesites.</p>
        <div className="mt-5 rounded-2xl border border-slate-100 bg-slate-50 p-3">
          <span className="font-barlow text-xs font-bold text-slate-500">Monto aprobado</span>
          <motion.div key={amount} initial={{ y: 8, opacity: 0 }} animate={{ y: 0, opacity: 1 }} className="mt-1 rounded-xl bg-[#7fffc9] py-2 font-poppins text-xl font-black text-[#003153]">
            {formatShort(amount)}
          </motion.div>
        </div>
        <div className="mt-3 rounded-2xl border border-slate-100 bg-white p-3">
          <span className="font-barlow text-xs font-bold text-slate-500">Plazo</span>
          <motion.div key={days} initial={{ y: 8, opacity: 0 }} animate={{ y: 0, opacity: 1 }} className="font-poppins text-lg font-black text-[#003153]">
            {days} días
          </motion.div>
        </div>
        <button className="mt-4 w-full rounded-full bg-[#003153] py-3 font-poppins text-sm font-bold text-white">Ver detalle</button>
      </div>
    </motion.div>
  );
}

function SimulatorCard({ amount, setAmount, days, setDays }) {
  const progressAmount = ((amount - 100000) / 900000) * 100;
  const progressDays = ((days - 5) / 25) * 100;
  const estimated = useMemo(() => Math.round(amount / days), [amount, days]);

  return (
    <motion.div
      initial={{ x: 40, opacity: 0 }}
      animate={{ x: 0, opacity: 1 }}
      transition={{ duration: 0.7, delay: 0.3 }}
      className="relative z-20 w-full rounded-[30px] bg-white/95 p-5 shadow-[0_24px_70px_rgba(0,0,0,0.22)] backdrop-blur md:max-w-[410px] md:p-7"
    >
      <div className="mb-5 flex items-start justify-between gap-4">
        <div>
          <p className="font-poppins text-2xl font-black tracking-[-0.04em] text-[#003153]">Simula tu préstamo</p>
          <p className="mt-1 font-barlow text-sm font-semibold text-slate-500">Elige monto y plazo en segundos.</p>
        </div>
        <div className="rounded-2xl bg-[#eefcf7] p-3 text-[#003153]"><Sparkles size={24} /></div>
      </div>

      <div className="space-y-6">
        <div>
          <div className="mb-2 flex items-center justify-between font-poppins">
            <label className="text-sm font-bold text-[#003153]">Monto a solicitar</label>
            <motion.span key={amount} initial={{ scale: 0.9 }} animate={{ scale: 1 }} className="rounded-full bg-[#7fffc9] px-4 py-2 text-lg font-black text-[#003153]">
              {formatShort(amount)}
            </motion.span>
          </div>
          <input
            aria-label="Monto a solicitar"
            type="range"
            min="100000"
            max="1000000"
            step="50000"
            value={amount}
            onChange={(e) => setAmount(Number(e.target.value))}
            className="range w-full"
            style={{ background: `linear-gradient(90deg, ${brand.mint} ${progressAmount}%, #d9e2ee ${progressAmount}%)` }}
          />
          <div className="mt-2 flex justify-between font-barlow text-xs font-bold text-slate-400"><span>$100.000</span><span>$1.000.000</span></div>
        </div>

        <div>
          <div className="mb-2 flex items-center justify-between font-poppins">
            <label className="text-sm font-bold text-[#003153]">Plazo de pago</label>
            <motion.span key={days} initial={{ scale: 0.9 }} animate={{ scale: 1 }} className="rounded-full bg-[#003153] px-4 py-2 text-lg font-black text-white">
              {days} días
            </motion.span>
          </div>
          <input
            aria-label="Plazo de pago"
            type="range"
            min="5"
            max="30"
            step="1"
            value={days}
            onChange={(e) => setDays(Number(e.target.value))}
            className="range w-full"
            style={{ background: `linear-gradient(90deg, ${brand.blue} ${progressDays}%, #d9e2ee ${progressDays}%)` }}
          />
          <div className="mt-2 flex justify-between font-barlow text-xs font-bold text-slate-400"><span>5 días</span><span>30 días</span></div>
        </div>
      </div>

      <div className="mt-6 grid grid-cols-2 gap-3">
        <div className="rounded-3xl bg-[#f4f7fb] p-4">
          <p className="font-barlow text-xs font-bold uppercase tracking-wide text-slate-400">Monto</p>
          <p className="mt-1 font-poppins text-xl font-black text-[#003153]">{formatShort(amount)}</p>
        </div>
        <div className="rounded-3xl bg-[#f4f7fb] p-4">
          <p className="font-barlow text-xs font-bold uppercase tracking-wide text-slate-400">Estimado diario</p>
          <p className="mt-1 font-poppins text-xl font-black text-[#003153]">{formatShort(estimated)}</p>
        </div>
      </div>

      <button className="group mt-5 flex w-full items-center justify-center gap-3 rounded-2xl bg-[#7fffc9] px-6 py-4 font-poppins text-lg font-black text-[#003153] shadow-lg shadow-emerald-200/60 transition hover:-translate-y-0.5 hover:bg-white focus:outline-none focus:ring-4 focus:ring-[#7fffc9]/50">
        Quiero mi préstamo <ArrowRight className="transition group-hover:translate-x-1" />
      </button>
      <div className="mt-4 flex items-center justify-center gap-2 font-barlow text-sm font-semibold text-slate-500"><LockKeyhole size={16} /> Tu información está segura y protegida.</div>
    </motion.div>
  );
}

function BenefitCard({ icon: Icon, title, text, delay = 0 }) {
  return (
    <motion.div
      initial={{ y: 28, opacity: 0 }}
      whileInView={{ y: 0, opacity: 1 }}
      viewport={{ once: true, amount: 0.3 }}
      transition={{ duration: 0.55, delay }}
      className="group rounded-[28px] border border-slate-100 bg-white p-6 shadow-[0_18px_45px_rgba(0,49,83,0.08)] transition hover:-translate-y-1 hover:shadow-[0_24px_60px_rgba(65,72,245,0.16)]"
    >
      <div className="mb-5 flex h-16 w-16 items-center justify-center rounded-3xl bg-[#effff9] text-[#003153] ring-2 ring-[#7fffc9] transition group-hover:rotate-3 group-hover:scale-105">
        <Icon size={32} />
      </div>
      <h3 className="font-poppins text-lg font-black text-[#003153]">{title}</h3>
      <p className="mt-2 font-barlow text-base leading-relaxed text-slate-600">{text}</p>
    </motion.div>
  );
}

function Step({ n, icon: Icon, title, text }) {
  return (
    <div className="relative rounded-[28px] bg-white p-6 shadow-[0_18px_45px_rgba(0,49,83,0.07)]">
      <div className="absolute -top-4 left-6 flex h-9 w-9 items-center justify-center rounded-full bg-[#7fffc9] font-poppins text-sm font-black text-[#003153]">{n}</div>
      <div className="mb-5 mt-3 flex h-16 w-16 items-center justify-center rounded-full border-2 border-[#7fffc9] bg-[#f1fffa] text-[#003153]">
        <Icon size={30} />
      </div>
      <h3 className="font-poppins text-xl font-black text-[#003153]">{title}</h3>
      <p className="mt-2 font-barlow text-base text-slate-600">{text}</p>
    </div>
  );
}

function CtaButton({ children = "Solicítalo ahora", variant = "primary" }) {
  const primary = variant === "primary";
  return (
    <button className={`group inline-flex min-h-[52px] items-center justify-center gap-3 rounded-2xl px-6 py-3 font-poppins text-base font-black transition focus:outline-none focus:ring-4 ${primary ? "bg-[#7fffc9] text-[#003153] shadow-lg shadow-emerald-300/30 hover:-translate-y-0.5 hover:bg-white focus:ring-[#7fffc9]/50" : "border-2 border-white/40 bg-white/10 text-white hover:bg-white hover:text-[#003153] focus:ring-white/30"}`}>
      {children}
      <span className={`flex h-8 w-8 items-center justify-center rounded-full transition group-hover:translate-x-1 ${primary ? "bg-[#003153] text-white" : "bg-white text-[#003153]"}`}>
        <ArrowRight size={18} />
      </span>
    </button>
  );
}

export default function RapiFlexLandingPage() {
  const [amount, setAmount] = useState(750000);
  const [days, setDays] = useState(15);

  return (
    <main className="min-h-screen bg-white text-[#003153]">
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Barlow:wght@400;500;600;700;800&family=Poppins:wght@500;600;700;800;900&display=swap');
        .font-poppins{font-family:'Poppins',system-ui,sans-serif}.font-barlow{font-family:'Barlow',system-ui,sans-serif}
        .range{height:12px;border-radius:999px;appearance:none;outline:none}.range::-webkit-slider-thumb{appearance:none;height:28px;width:28px;border-radius:999px;background:#fff;border:7px solid #003153;box-shadow:0 8px 25px rgba(0,49,83,.25);cursor:pointer}.range::-moz-range-thumb{height:28px;width:28px;border-radius:999px;background:#fff;border:7px solid #003153;box-shadow:0 8px 25px rgba(0,49,83,.25);cursor:pointer}
        .urban{font-family:'Poppins',system-ui,sans-serif;font-style:italic;letter-spacing:-.085em;text-shadow:0 3px 0 rgba(255,255,255,.18)}
        html{scroll-behavior:smooth}
      `}</style>

      <section className="relative overflow-hidden bg-[#003153] text-white">
        <div className="mx-auto flex max-w-7xl items-center justify-center gap-2 px-5 py-3 font-barlow text-sm font-semibold md:text-base">
          <Starburst className="static !h-5 !w-5 scale-[.25]" />
          <span>Tu préstamo, a tu manera. <strong className="text-[#7fffc9]">Rápido, 100% en línea y sin complicaciones.</strong></span>
        </div>
      </section>

      <header className="sticky top-0 z-50 border-b border-white/10 bg-white/85 backdrop-blur-xl">
        <div className="mx-auto flex max-w-7xl items-center justify-between px-5 py-4">
          <Logo />
          <nav className="hidden items-center gap-8 font-barlow text-[15px] font-bold text-[#003153] lg:flex">
            <a href="#beneficios" className="hover:text-[#4148f5]">Beneficios</a>
            <a href="#funciona" className="hover:text-[#4148f5]">Cómo funciona</a>
            <a href="#seguridad" className="hover:text-[#4148f5]">Seguridad</a>
            <a href="#guia" className="hover:text-[#4148f5]">UI Kit</a>
          </nav>
          <div className="hidden md:block"><CtaButton /></div>
          <button className="rounded-xl bg-[#f1f4ff] p-3 text-[#003153] lg:hidden"><Menu /></button>
        </div>
      </header>

      <section className="relative overflow-hidden bg-[#4148f5]">
        <Dots className="left-[23%] top-24 hidden md:grid" />
        <Dots className="right-16 top-28 hidden md:grid" />
        <Starburst className="left-[44%] top-24 hidden md:block" />
        <GraphicRings className="right-[9%] top-[16%] hidden h-[260px] w-[260px] md:block" />
        <motion.div className="absolute -bottom-10 left-0 h-24 w-[65%] rounded-full border-[18px] border-[#7fffc9] opacity-80" animate={{ x: [0, 35, 0] }} transition={{ duration: 7, repeat: Infinity, ease: "easeInOut" }} />

        <div className="relative mx-auto grid max-w-7xl gap-8 px-5 pb-14 pt-10 md:grid-cols-[1.05fr_.95fr] md:pb-20 md:pt-14">
          <div className="relative z-10 flex flex-col justify-center text-white">
            <motion.p initial={{ y: 18, opacity: 0 }} animate={{ y: 0, opacity: 1 }} className="urban text-[76px] font-black leading-[0.9] md:text-[112px]">Llegó</motion.p>
            <motion.div initial={{ y: 18, opacity: 0 }} animate={{ y: 0, opacity: 1 }} transition={{ delay: 0.08 }}>
              <RapiflexLogo className="mt-1 text-[72px] text-white md:text-[124px]" />
            </motion.div>

            <motion.div initial={{ y: 16, opacity: 0 }} animate={{ y: 0, opacity: 1 }} transition={{ delay: 0.16 }} className="mt-5 w-fit rounded-2xl bg-[#003153] px-5 py-3 font-poppins text-2xl font-black md:text-3xl">
              Tu dinero, <span className="text-[#7fffc9]">a tu manera.</span>
            </motion.div>

            <motion.p initial={{ y: 16, opacity: 0 }} animate={{ y: 0, opacity: 1 }} transition={{ delay: 0.23 }} className="mt-6 max-w-[560px] font-barlow text-xl font-semibold leading-tight text-white/95 md:text-2xl">
              Préstamos desde <strong className="text-[#7fffc9]">$100.000 hasta $1.000.000</strong> a 5 - 30 días. 100% en línea y con respuesta en minutos.
            </motion.p>

            <div className="mt-8 flex flex-col gap-4 sm:flex-row sm:items-center">
              <CtaButton />
              <a href="#funciona" className="group inline-flex items-center gap-3 font-poppins text-base font-bold text-white underline-offset-8 hover:underline">
                Conoce cómo funciona <ArrowRight className="transition group-hover:translate-x-1" size={20} />
              </a>
            </div>

            <div className="mt-8 flex flex-wrap items-center gap-5 font-barlow text-sm font-semibold text-white/85">
              <span className="flex items-center gap-2"><ShieldCheck size={24} /> Vigilado por Superintendencia Financiera de Colombia</span>
              <span>*Aplican TyC.</span>
            </div>
          </div>

          <div className="relative z-10 grid gap-6 lg:grid-cols-[.85fr_1fr] lg:items-center">
            <div className="relative order-2 lg:order-1">
              <div className="mx-auto max-w-[290px] rounded-t-full bg-gradient-to-b from-white/30 to-transparent p-4">
                <PhoneMock amount={amount} days={days} />
              </div>
            </div>
            <div className="order-1 lg:order-2">
              <SimulatorCard amount={amount} setAmount={setAmount} days={days} setDays={setDays} />
            </div>
          </div>
        </div>
      </section>

      <section className="bg-white py-14 md:py-18" id="beneficios">
        <div className="mx-auto max-w-7xl px-5">
          <div className="mx-auto max-w-3xl text-center">
            <h2 className="font-poppins text-4xl font-black tracking-[-0.05em] text-[#003153] md:text-5xl">Así de fácil, <span className="text-[#4148f5]">así de RapiFlex</span></h2>
            <p className="mt-4 font-barlow text-lg font-medium text-slate-600">Beneficios claros, rápidos de entender y pensados para convertir tráfico en solicitudes reales.</p>
          </div>

          <div className="mt-10 grid gap-5 md:grid-cols-2 lg:grid-cols-4">
            <BenefitCard icon={Smartphone} title="100% en línea" text="Haz tu solicitud desde tu celular o computador, donde estés." />
            <BenefitCard icon={Clock3} title="Respuesta en minutos" text="Una experiencia rápida para que sigas con tu día sin complicarte." delay={0.05} />
            <BenefitCard icon={FileCheck2} title="Sin filas ni papeleo" text="Olvídate del trámite tradicional y completa todo digitalmente." delay={0.1} />
            <BenefitCard icon={ShieldCheck} title="Seguro y confiable" text="Protegemos tu información en cada paso del proceso." delay={0.15} />
          </div>
        </div>
      </section>

      <section className="bg-[#f5f8ff] py-14" id="funciona">
        <div className="mx-auto max-w-7xl px-5">
          <h2 className="text-center font-poppins text-4xl font-black tracking-[-0.05em] text-[#003153] md:text-5xl">Pídelo fácil, <span className="text-[#4148f5]">recíbelo rápido</span></h2>
          <div className="mt-12 grid gap-6 md:grid-cols-3">
            <Step n="1" icon={FileCheck2} title="Completa tus datos" text="Diligencia la información básica desde el formulario de solicitud." />
            <Step n="2" icon={Clock3} title="Recibe respuesta" text="Te respondemos en minutos según la validación de tu información." />
            <Step n="3" icon={Wallet} title="Usa tu dinero" text="Si eres aprobado, úsalo como quieras y cuando lo necesites." />
          </div>
        </div>
      </section>

      <section className="bg-white py-14" id="seguridad">
        <div className="mx-auto max-w-7xl px-5">
          <div className="relative overflow-hidden rounded-[38px] bg-[#003153] p-6 text-white shadow-2xl md:p-10">
            <GraphicRings className="left-20 top-16 h-[200px] w-[200px] opacity-70" />
            <Dots className="right-16 top-16 hidden md:grid" />
            <motion.div className="absolute -bottom-8 right-8 h-24 w-[48%] rounded-full border-[13px] border-[#7fffc9] opacity-80" animate={{ x: [0, -20, 0] }} transition={{ duration: 6, repeat: Infinity, ease: "easeInOut" }} />
            <div className="relative z-10 grid items-center gap-8 md:grid-cols-[.85fr_1.15fr]">
              <div className="min-h-[300px] overflow-hidden rounded-[30px] bg-gradient-to-br from-[#7fffc9] to-[#4148f5] p-4">
                <div className="flex h-full min-h-[270px] items-end justify-center rounded-[24px] bg-white/10 p-6 text-center backdrop-blur">
                  <div className="rounded-[28px] bg-white/95 p-5 text-[#003153] shadow-xl">
                    <div className="mx-auto mb-4 flex h-20 w-20 items-center justify-center rounded-full bg-[#7fffc9]"><Smartphone size={40} /></div>
                    <p className="font-poppins text-xl font-black">Solicitud protegida</p>
                    <p className="mt-2 font-barlow text-sm text-slate-600">Proceso digital seguro y acompañado.</p>
                  </div>
                </div>
              </div>
              <div>
                <div className="mb-5 flex h-20 w-20 items-center justify-center rounded-[28px] border-2 border-[#7fffc9] text-[#7fffc9]"><ShieldCheck size={46} /></div>
                <h2 className="font-poppins text-4xl font-black tracking-[-0.05em] md:text-6xl">Tu tranquilidad es <span className="text-[#7fffc9]">nuestra prioridad.</span></h2>
                <p className="mt-5 max-w-2xl font-barlow text-lg leading-relaxed text-white/82">En RapiCredit protegemos tu información y te acompañamos durante el proceso para que solicites tu préstamo con confianza, claridad y seguridad.</p>
                <div className="mt-7 flex flex-wrap gap-3">
                  {["Datos protegidos", "Proceso 100% digital", "Acompañamiento claro"].map((t) => <span key={t} className="rounded-full bg-white/10 px-4 py-2 font-barlow text-sm font-bold text-white ring-1 ring-white/15">{t}</span>)}
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section className="bg-white pb-16">
        <div className="mx-auto max-w-7xl px-5">
          <div className="overflow-hidden rounded-[32px] bg-gradient-to-r from-[#4148f5] via-[#7fffc9] to-[#7fffc9] p-6 md:p-8">
            <div className="flex flex-col items-start justify-between gap-6 md:flex-row md:items-center">
              <div className="flex items-center gap-5">
                <div className="flex h-16 w-16 items-center justify-center rounded-full bg-[#003153] text-white"><ArrowRight size={34} /></div>
                <div>
                  <h2 className="font-poppins text-4xl font-black tracking-[-0.05em] text-[#003153] md:text-5xl">Solicítalo ahora</h2>
                  <p className="mt-1 font-barlow text-lg font-bold text-[#003153]/80">Fácil, rápido y 100% en línea. Tu dinero, a tu manera.</p>
                </div>
              </div>
              <CtaButton>Empezar solicitud</CtaButton>
            </div>
          </div>
        </div>
      </section>

      <section className="bg-[#f5f8ff] py-14" id="guia">
        <div className="mx-auto max-w-7xl px-5">
          <div className="mb-8">
            <p className="font-barlow text-sm font-black uppercase tracking-[0.18em] text-[#4148f5]">Guía de estilos UI</p>
            <h2 className="mt-2 font-poppins text-4xl font-black tracking-[-0.05em] text-[#003153]">Definición de botones y sistema visual</h2>
          </div>
          <div className="grid gap-6 lg:grid-cols-3">
            <div className="rounded-[28px] bg-white p-6 shadow-lg">
              <h3 className="font-poppins text-xl font-black">Colores accesibles</h3>
              <div className="mt-5 space-y-3">
                {[
                  ["Azul verdadero", "#4148f5", "text-white"],
                  ["Verde confiable", "#7fffc9", "text-[#003153]"],
                  ["Azul experiencia", "#003153", "text-white"],
                ].map(([name, hex, cls]) => <div key={hex} className={`rounded-2xl p-4 font-poppins font-black ${cls}`} style={{ background: hex }}>{name}<span className="float-right font-barlow font-bold">{hex}</span></div>)}
              </div>
            </div>
            <div className="rounded-[28px] bg-white p-6 shadow-lg">
              <h3 className="font-poppins text-xl font-black">Botones CTA</h3>
              <div className="mt-5 space-y-4">
                <CtaButton>Solicítalo ahora</CtaButton>
                <button className="inline-flex min-h-[52px] items-center justify-center rounded-2xl border-2 border-[#4148f5] px-6 py-3 font-poppins font-black text-[#4148f5] transition hover:bg-[#4148f5] hover:text-white focus:outline-none focus:ring-4 focus:ring-[#4148f5]/30">Conoce cómo funciona</button>
                <button className="inline-flex min-h-[52px] items-center justify-center rounded-2xl bg-slate-200 px-6 py-3 font-poppins font-black text-slate-500" disabled>Estado deshabilitado</button>
              </div>
              <p className="mt-4 font-barlow text-sm text-slate-500">Altura mínima 52px, foco visible, contraste alto y texto directo orientado a conversión.</p>
            </div>
            <div className="rounded-[28px] bg-white p-6 shadow-lg">
              <h3 className="font-poppins text-xl font-black">Tipografía</h3>
              <div className="mt-5 space-y-4">
                <div><p className="font-barlow text-xs font-bold uppercase text-slate-400">H1 / Poppins Black</p><p className="font-poppins text-4xl font-black tracking-[-0.05em]">Llegó RapiFlex</p></div>
                <div><p className="font-barlow text-xs font-bold uppercase text-slate-400">Body / Barlow</p><p className="font-barlow text-lg text-slate-600">Texto claro, cercano y fácil de leer en web y mobile.</p></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <footer className="bg-[#003153] py-10 text-white">
        <div className="mx-auto grid max-w-7xl gap-8 px-5 md:grid-cols-[1fr_1fr_1fr] md:items-center">
          <Logo light />
          <div className="font-barlow text-sm font-semibold text-white/75 md:text-center">Términos y condiciones · Política de privacidad · Síguenos</div>
          <div className="font-barlow text-sm font-semibold text-white/75 md:text-right">Vigilado por Superintendencia Financiera de Colombia<br />*Aplican TyC.</div>
        </div>
      </footer>

      <div className="fixed inset-x-3 bottom-3 z-50 md:hidden">
        <button className="flex w-full items-center justify-center gap-3 rounded-2xl bg-[#7fffc9] px-6 py-4 font-poppins text-lg font-black text-[#003153] shadow-2xl">
          Solicítalo ahora <ArrowRight />
        </button>
      </div>
    </main>
  );
}
