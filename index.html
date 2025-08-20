import React, { useEffect, useMemo, useRef, useState } from "react";
import { Coins, Bolt, Bell, Gift, Trophy, PlusCircle, Shield, Users, Wallet, Clock, ChevronRight, Gem } from "lucide-react";
import { motion, AnimatePresence } from "framer-motion";

/**
 * BitcoinX — Tap-to-Earn demo
 * ---------------------------------------------------------
 * • Single-file React app with TailwindCSS
 * • LocalStorage persistence
 * • Active tap earnings + passive income per hour
 * • Upgrades, tasks, daily reward, simple shop
 * • Combo meter, notifications, basic achievements
 * ---------------------------------------------------------
 * How to use:
 * 1) Drop into any React project (e.g., Vite, CRA, Next.js Client Component)
 * 2) Ensure TailwindCSS is enabled
 * 3) Default export is <BitcoinXApp />
 */

const STORAGE_KEY = "bitcoinx_save_v1";

const defaultSave = {
  username: "amd_dda",
  level: 4,
  levelProgress: 0.4,
  balance: 100390,
  perTap: 10_904, // Inspired by mock
  perHour: 200,
  claimCooldownMs: 2 * 60 * 60 * 1000, // 2 hours
  lastClaimAt: 0,
  lastOnlineAt: Date.now(),
  upgrades: {
    equipment: 0,
    mining: 0,
    infra: 0,
    security: 0,
  },
  tasks: {
    dailyClaimedAt: 0,
    joinTelegram: false,
    invite20: 0, // count of invited friends
  },
  achievements: {
    firstTap: false,
    rich100k: false,
    combo100: false,
  },
  notifications: 14,
};

function loadSave() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return defaultSave;
    return { ...defaultSave, ...JSON.parse(raw) };
  } catch {
    return defaultSave;
  }
}

function saveSave(s) {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(s));
  } catch {}
}

function format(n) {
  if (n >= 1_000_000_000) return (n / 1_000_000_000).toFixed(2) + "B";
  if (n >= 1_000_000) return (n / 1_000_000).toFixed(2) + "M";
  if (n >= 1_000) return (n / 1_000).toFixed(2) + "K";
  return n.toLocaleString();
}

function usePassiveIncome(save, setSave) {
  // Convert offline time to earnings and live accrue
  useEffect(() => {
    const now = Date.now();
    const elapsedMs = now - (save.lastOnlineAt || now);
    const earned = Math.floor((elapsedMs / 3600000) * save.perHour);
    if (earned > 0) {
      setSave((s) => ({ ...s, balance: s.balance + earned, lastOnlineAt: now }));
    } else {
      setSave((s) => ({ ...s, lastOnlineAt: now }));
    }
    const t = setInterval(() => {
      setSave((s) => ({ ...s, balance: s.balance + Math.floor(s.perHour / 3600) }));
    }, 1000);
    return () => clearInterval(t);
  }, []); // run once
}

function ProgressBar({ value }) {
  return (
    <div className="w-full h-2 bg-white/10 rounded-full overflow-hidden">
      <div className="h-full bg-cyan-400" style={{ width: `${Math.min(100, value * 100)}%` }} />
    </div>
  );
}

function TopBar({ save }) {
  return (
    <div className="flex items-center justify-between py-2">
      <div className="text-cyan-300 text-sm">Cancel</div>
      <div className="text-cyan-100 font-semibold">BitcoinX</div>
      <div className="relative">
        <Bell className="w-5 h-5" />
        {save.notifications > 0 && (
          <span className="absolute -top-1 -right-1 bg-pink-500 text-white text-[10px] rounded-full px-1">
            {save.notifications}
          </span>
        )}
      </div>
    </div>
  );
}

function StatChip({ icon: Icon, label, value }) {
  return (
    <div className="flex items-center gap-2 bg-white/10 rounded-xl px-3 py-2">
      <Icon className="w-4 h-4" />
      <div className="text-xs opacity-80">{label}</div>
      <div className="text-sm font-semibold">{value}</div>
    </div>
  );
}

function UpgradeCard({ title, desc, cost, onBuy, disabled, icon: Icon }) {
  return (
    <div className={`rounded-2xl p-4 bg-white/5 backdrop-blur border border-white/10 flex items-center justify-between ${disabled ? "opacity-60" : ""}`}>
      <div className="flex items-center gap-3">
        <div className="p-2 rounded-xl bg-white/10">
          <Icon className="w-6 h-6" />
        </div>
        <div>
          <div className="font-semibold">{title}</div>
          <div className="text-xs opacity-80">{desc}</div>
        </div>
      </div>
      <button
        onClick={onBuy}
        disabled={disabled}
        className="px-3 py-2 rounded-xl bg-cyan-500/90 hover:bg-cyan-400 active:scale-95 transition text-sm font-semibold">
        Buy • {format(cost)}
      </button>
    </div>
  );
}

function TaskRow({ title, reward, done, onClaim, icon: Icon }) {
  return (
    <div className={`rounded-2xl p-4 bg-white/5 border border-white/10 flex items-center justify-between ${done ? "opacity-60" : ""}`}>
      <div className="flex items-center gap-3">
        <div className="p-2 rounded-xl bg-white/10">
          <Icon className="w-5 h-5" />
        </div>
        <div>
          <div className="font-semibold">{title}</div>
          <div className="text-xs opacity-80">+ {format(reward)} coins</div>
        </div>
      </div>
      <button
        onClick={onClaim}
        disabled={done}
        className="px-3 py-2 rounded-xl bg-pink-500/90 hover:bg-pink-400 active:scale-95 transition text-sm font-semibold">
        {done ? "Claimed" : "Claim"}
      </button>
    </div>
  );
}

function BigTapButton({ onTap, label = "Tap" }) {
  return (
    <motion.button
      whileTap={{ scale: 0.95 }}
      onClick={onTap}
      className="select-none mx-auto mt-6 mb-4 w-52 h-52 rounded-full bg-gradient-to-br from-cyan-400 to-blue-600 shadow-xl shadow-cyan-900/40 flex items-center justify-center text-xl font-extrabold">
      {label}
    </motion.button>
  );
}

function Countdown({ until }) {
  const [now, setNow] = useState(Date.now());
  useEffect(() => {
    const t = setInterval(() => setNow(Date.now()), 1000);
    return () => clearInterval(t);
  }, []);
  const left = Math.max(0, until - now);
  const h = Math.floor(left / 3600000);
  const m = Math.floor((left % 3600000) / 60000);
  const s = Math.floor((left % 60000) / 1000);
  return <span>{h.toString().padStart(2, "0")}:{m.toString().padStart(2, "0")}:{s.toString().padStart(2, "0")}</span>;
}

export default function BitcoinXApp() {
  const [save, setSave] = useState(loadSave());
  const [combo, setCombo] = useState(0);
  const [tapBurst, setTapBurst] = useState(0);
  const [activeTab, setActiveTab] = useState("earn");
  const claimReadyAt = (save.lastClaimAt || 0) + save.claimCooldownMs;

  usePassiveIncome(save, setSave);

  useEffect(() => saveSave(save), [save]);

  // Combo drains slowly
  useEffect(() => {
    const t = setInterval(() => setCombo((c) => Math.max(0, c - 1)), 800);
    return () => clearInterval(t);
  }, []);

  const perTapEffective = useMemo(() => Math.floor(save.perTap * (1 + combo / 1000)), [save.perTap, combo]);

  const handleTap = () => {
    setTapBurst((n) => n + 1);
    setCombo((c) => Math.min(1000, c + 12));
    setSave((s) => {
      const next = { ...s, balance: s.balance + perTapEffective };
      if (!s.achievements.firstTap) next.achievements = { ...s.achievements, firstTap: true };
      if (!s.achievements.rich100k && next.balance >= 100000) next.achievements = { ...next.achievements, rich100k: true };
      return next;
    });
  };

  const buyUpgrade = (type) => {
    const baseCosts = { equipment: 200, mining: 800, infra: 2500, security: 500 };
    const scale = { equipment: 1.25, mining: 1.35, infra: 1.45, security: 1.3 };
    const gains = { equipment: { perTap: 250 }, mining: { perHour: 140 }, infra: { perTap: 1500 }, security: { perHour: 140 } };

    const level = save.upgrades[type] || 0;
    const cost = Math.floor(baseCosts[type] * Math.pow(scale[type], level));
    if (save.balance < cost) return;

    setSave((s) => {
      const upgraded = { ...s };
      upgraded.balance -= cost;
      upgraded.upgrades[type] = level + 1;
      upgraded.perTap += gains[type].perTap || 0;
      upgraded.perHour += gains[type].perHour || 0;
      upgraded.levelProgress = Math.min(1, upgraded.levelProgress + 0.08);
      if (upgraded.levelProgress >= 1) {
        upgraded.level += 1;
        upgraded.levelProgress = 0;
      }
      return upgraded;
    });
  };

  const claimHourly = () => {
    if (Date.now() < claimReadyAt) return;
    const reward = save.perHour * 2; // juicy claim
    setSave((s) => ({ ...s, balance: s.balance + reward, lastClaimAt: Date.now() }));
  };

  const claimDaily = () => {
    const now = Date.now();
    const day = 24 * 3600000;
    if (now - (save.tasks.dailyClaimedAt || 0) < day) return;
    setSave((s) => ({ ...s, balance: s.balance + 500, tasks: { ...s.tasks, dailyClaimedAt: now } }));
  };

  const claimTelegram = () => {
    if (save.tasks.joinTelegram) return;
    setSave((s) => ({ ...s, balance: s.balance + 500, tasks: { ...s.tasks, joinTelegram: true } }));
  };

  const inviteFriend = () => {
    setSave((s) => ({ ...s, balance: s.balance + 75, tasks: { ...s.tasks, invite20: Math.min(20, s.tasks.invite20 + 1) } }));
  };

  useEffect(() => {
    if (combo >= 100 && !save.achievements.combo100) {
      setSave((s) => ({ ...s, achievements: { ...s.achievements, combo100: true } }));
    }
  }, [combo]);

  return (
    <div className="min-h-screen w-full bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-cyan-900 via-slate-900 to-slate-950 text-white">
      <div className="max-w-md mx-auto px-4 pb-28">
        <TopBar save={save} />

        {/* Profile + progress */}
        <div className="rounded-3xl p-4 bg-white/5 border border-white/10 mb-3">
          <div className="flex items-center justify-between mb-2">
            <div className="flex items-center gap-2">
              <div className="w-9 h-9 rounded-full bg-gradient-to-br from-orange-400 to-pink-500 flex items-center justify-center font-bold">B</div>
              <div>
                <div className="text-sm opacity-80">@{save.username}</div>
                <div className="text-xs opacity-70">LVL {save.level}/10</div>
              </div>
            </div>
            <StatChip icon={Bolt} label="/hour" value={`+${format(save.perHour)}`} />
          </div>
          <ProgressBar value={save.levelProgress} />
        </div>

        {/* KPI row */}
        <div className="flex items-center gap-2 mb-3">
          <StatChip icon={Gem} label="per tap" value={format(perTapEffective)} />
          <StatChip icon={Clock} label="claim" value={Date.now() >= claimReadyAt ? "Ready" : <Countdown until={claimReadyAt} />} />
          <StatChip icon={Shield} label="combo" value={`${combo}`} />
        </div>

        {/* Balance big */}
        <div className="text-center">
          <div className="text-sm opacity-80 mb-1">Coins</div>
          <div className="text-5xl font-extrabold tracking-tight flex items-center justify-center gap-2">
            <Coins className="w-8 h-8" /> {format(save.balance)}
          </div>
        </div>

        {/* Tap area */}
        <BigTapButton onTap={handleTap} label={`+${format(perTapEffective)}`} />

        {/* Animated floating gain bubbles */}
        <AnimatePresence initial={false}>
          {[...Array(Math.min(6, tapBurst)).keys()].map((i) => (
            <motion.div
              key={i}
              initial={{ opacity: 0, y: 0 }}
              animate={{ opacity: 1, y: -60 }}
              exit={{ opacity: 0 }}
              onAnimationComplete={() => setTapBurst((n) => Math.max(0, n - 1))}
              className="pointer-events-none fixed left-1/2 -translate-x-1/2 text-cyan-200">
              +{format(perTapEffective)}
            </motion.div>
          ))}
        </AnimatePresence>

        {/* Quick nav chips */}
        <div className="grid grid-cols-4 gap-2 my-4">
          {[
            { id: "earn", icon: Wallet, label: "Earn" },
            { id: "cards", icon: Gift, label: "Cards" },
            { id: "shop", icon: PlusCircle, label: "Shop" },
            { id: "friends", icon: Users, label: "Friends" },
          ].map((t) => (
            <button
              key={t.id}
              onClick={() => setActiveTab(t.id)}
              className={`flex items-center justify-center gap-2 p-3 rounded-2xl border ${activeTab === t.id ? "bg-cyan-500/20 border-cyan-400/40" : "bg-white/5 border-white/10"}`}>
              <t.icon className="w-5 h-5" />
              <span className="text-sm">{t.label}</span>
            </button>
          ))}
        </div>

        {/* Tab content */}
        {activeTab === "earn" && (
          <div className="space-y-3">
            <div className="rounded-2xl p-4 bg-white/5 border border-white/10">
              <div className="flex items-center justify-between">
                <div>
                  <div className="text-lg font-semibold">Claim Booster</div>
                  <div className="text-xs opacity-80">Claim every 2 hours for bonus</div>
                </div>
                <button
                  onClick={claimHourly}
                  disabled={Date.now() < claimReadyAt}
                  className="px-3 py-2 rounded-xl bg-emerald-500/90 disabled:bg-white/10 transition font-semibold">
                  {Date.now() >= claimReadyAt ? `Claim ${format(save.perHour * 2)}` : <Countdown until={claimReadyAt} />}
                </button>
              </div>
            </div>

            <div className="rounded-2xl p-4 bg-white/5 border border-white/10">
              <div className="text-lg font-semibold mb-2">Tasks</div>
              <div className="space-y-2">
                <TaskRow title="Daily Reward" reward={500} done={Date.now() - (save.tasks.dailyClaimedAt||0) < 24*3600000} onClaim={claimDaily} icon={Gift} />
                <TaskRow title="Join Telegram" reward={500} done={save.tasks.joinTelegram} onClaim={claimTelegram} icon={Users} />
                <div className="rounded-2xl p-4 bg-white/5 border border-white/10">
                  <div className="flex items-center justify-between">
                    <div className="flex items-center gap-3">
                      <div className="p-2 rounded-xl bg-white/10"><Users className="w-5 h-5" /></div>
                      <div>
                        <div className="font-semibold">Invite 20 friends</div>
                        <div className="text-xs opacity-80">Progress: {save.tasks.invite20}/20 • +1500 coins</div>
                      </div>
                    </div>
                    <button onClick={inviteFriend} className="px-3 py-2 rounded-xl bg-pink-500/90 hover:bg-pink-400 font-semibold">Invite</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        )}

        {activeTab === "shop" && (
          <div className="space-y-3">
            <UpgradeCard title="Equipment" desc="Boost per tap" cost={Math.floor(200 * Math.pow(1.25, save.upgrades.equipment||0))} icon={Bolt} disabled={save.balance < Math.floor(200 * Math.pow(1.25, save.upgrades.equipment||0))} onBuy={() => buyUpgrade("equipment")} />
            <UpgradeCard title="Mining Rig" desc="Boost per hour" cost={Math.floor(800 * Math.pow(1.35, save.upgrades.mining||0))} icon={Gem} disabled={save.balance < Math.floor(800 * Math.pow(1.35, save.upgrades.mining||0))} onBuy={() => buyUpgrade("mining")} />
            <UpgradeCard title="Infrastructure" desc="Big per tap gains" cost={Math.floor(2500 * Math.pow(1.45, save.upgrades.infra||0))} icon={Coins} disabled={save.balance < Math.floor(2500 * Math.pow(1.45, save.upgrades.infra||0))} onBuy={() => buyUpgrade("infra")} />
            <UpgradeCard title="Security Update" desc="Steady hourly boost" cost={Math.floor(500 * Math.pow(1.3, save.upgrades.security||0))} icon={Shield} disabled={save.balance < Math.floor(500 * Math.pow(1.3, save.upgrades.security||0))} onBuy={() => buyUpgrade("security")} />
          </div>
        )}

        {activeTab === "cards" && (
          <div className="space-y-3">
            <div className="rounded-2xl p-4 bg-white/5 border border-white/10">
              <div className="text-lg font-semibold mb-1">Achievements</div>
              <div className="grid grid-cols-2 gap-2">
                {[
                  { id: "firstTap", label: "First Tap" },
                  { id: "rich100k", label: "100K Balance" },
                  { id: "combo100", label: "Combo 100" },
                ].map((a) => (
                  <div key={a.id} className={`rounded-xl p-3 border ${save.achievements[a.id] ? "bg-emerald-500/10 border-emerald-500/40" : "bg-white/5 border-white/10"}`}>
                    <div className="font-semibold text-sm">{a.label}</div>
                    <div className="text-xs opacity-80">{save.achievements[a.id] ? "Unlocked" : "Locked"}</div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}

        {activeTab === "friends" && (
          <div className="space-y-3">
            <div className="rounded-2xl p-4 bg-white/5 border border-white/10">
              <div className="text-lg font-semibold">Refer & Earn</div>
              <div className="text-sm opacity-80 mb-3">Share link with friends. Each join gives +75 coins (demo).</div>
              <button onClick={inviteFriend} className="px-4 py-2 rounded-xl bg-cyan-500/90 hover:bg-cyan-400 font-semibold flex items-center gap-2">
                <Users className="w-5 h-5" /> Copy Invite Link
              </button>
            </div>
          </div>
        )}
      </div>

      {/* Bottom Nav bar */}
      <div className="fixed bottom-0 left-0 right-0 border-t border-white/10 bg-slate-950/80 backdrop-blur">
        <div className="max-w-md mx-auto px-4 py-3 grid grid-cols-4 gap-2">
          {[
            { id: "earn", icon: Wallet, label: "Earn" },
            { id: "cards", icon: Gift, label: "Cards" },
            { id: "shop", icon: PlusCircle, label: "Shop" },
            { id: "friends", icon: Users, label: "Friends" },
          ].map((t) => (
            <button
              key={t.id}
              onClick={() => setActiveTab(t.id)}
              className={`flex flex-col items-center justify-center gap-1 py-1 rounded-xl ${activeTab === t.id ? "bg-white/5" : ""}`}>
              <t.icon className="w-5 h-5" />
              <span className="text-xs">{t.label}</span>
            </button>
          ))}
        </div>
      </div>
    </div>
  );
}
