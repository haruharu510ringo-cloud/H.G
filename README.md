/*
 * La-Vita!!! イベントまとめページ（シンプル版）
 * Design: Clean & Simple — Light Blue × White × Black Text
 * Target: NAMIMATI学生団体の仲間向け企画レポートページ
 * Source: La-Vita!!!企画まとめ.pdf (2024.7.7 鎌倉 材木座海岸)
 */

import { useEffect, useRef, useState } from "react";

// ─── スクロールアニメーション用フック ─────────────────────────────────────
function useFadeInUp() {
  const ref = useRef<HTMLDivElement>(null);
  useEffect(() => {
    const el = ref.current;
    if (!el) return;
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          el.classList.add("visible");
          observer.disconnect();
        }
      },
      { threshold: 0.1 }
    );
    observer.observe(el);
    return () => observer.disconnect();
  }, []);
  return ref;
}

// ─── ナビゲーション ────────────────────────────────────────────────────────
function Nav() {
  const [scrolled, setScrolled] = useState(false);
  const [menuOpen, setMenuOpen] = useState(false);

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 60);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  const links = [
    { href: "#concept", label: "コンセプト" },
    { href: "#contents", label: "コンテンツ" },
    { href: "#sponsors", label: "協賛" },
    { href: "#review", label: "振り返り" },
    { href: "#voices", label: "メンバーの声" },
  ];

  return (
    <header
      className="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
      style={{
        background: scrolled ? "rgba(173, 216, 230, 0.95)" : "transparent",
        backdropFilter: scrolled ? "blur(12px)" : "none",
        boxShadow: scrolled ? "0 2px 8px rgba(0,0,0,0.1)" : "none",
      }}
    >
      <div className="container flex items-center justify-between py-4">
        <a href="#top" className="flex items-center gap-2">
          <span
            className="font-bold text-2xl tracking-wide"
            style={{
              fontFamily: "'Noto Serif JP', serif",
              color: "#333",
            }}
          >
            La-Vita!!!
          </span>
        </a>

        {/* Desktop nav */}
        <nav className="hidden md:flex items-center gap-8">
          {links.map((l) => (
            <a
              key={l.href}
              href={l.href}
              className="text-sm font-medium transition-colors hover:opacity-70"
              style={{ color: "#333" }}
            >
              {l.label}
            </a>
          ))}
        </nav>

        {/* Mobile menu button */}
        <button
          className="md:hidden text-2xl"
          style={{ color: "#333" }}
          onClick={() => setMenuOpen(!menuOpen)}
        >
          ☰
        </button>
      </div>

      {/* Mobile menu */}
      {menuOpen && (
        <nav
          className="md:hidden border-t"
          style={{
            background: "rgba(173, 216, 230, 0.98)",
            borderColor: "rgba(0,0,0,0.1)",
          }}
        >
          <div className="container py-4 flex flex-col gap-4">
            {links.map((l) => (
              <a
                key={l.href}
                href={l.href}
                className="text-sm font-medium"
                style={{ color: "#333" }}
                onClick={() => setMenuOpen(false)}
              >
                {l.label}
              </a>
            ))}
          </div>
        </nav>
      )}
    </header>
  );
}

// ─── ヒーロー ──────────────────────────────────────────────────────────────
function HeroSection() {
  return (
    <section
      className="pt-24 pb-16 md:pt-32 md:pb-24"
      style={{ background: "linear-gradient(135deg, #ADD8E6 0%, #E0F6FF 100%)" }}
    >
      <div className="container text-center">
        <div className="mb-6">
          <span
            className="inline-block px-4 py-2 rounded-full text-sm font-bold"
            style={{
              background: "rgba(255,255,255,0.8)",
              color: "#333",
            }}
          >
            📅 2024.7.7 鎌倉 材木座海岸
          </span>
        </div>

        <h1
          className="text-5xl md:text-7xl font-bold mb-6"
          style={{
            fontFamily: "'Noto Serif JP', serif",
            color: "#333",
          }}
        >
          La-Vita!!!
        </h1>

        <p
          className="text-lg md:text-xl mb-4"
          style={{
            fontFamily: "'Noto Serif JP', serif",
            color: "#555",
            fontStyle: "italic",
          }}
        >
          NAMIMATI BEACH CLEAN w/ mammababy & HiLife Beach House
        </p>

        <p
          className="text-base md:text-lg max-w-2xl mx-auto mb-6"
          style={{ color: "#555", lineHeight: "1.8" }}
        >
          忙しい大学生に、リフレッシュとビタミンチャージを。
        </p>

        <p
          className="text-sm md:text-base max-w-2xl mx-auto"
          style={{ color: "#666", lineHeight: "1.8" }}
        >
          このページは、La-Vita!!!の企画意図・実施内容・苦労した点・協賛情報を仲間に伝えるためのまとめです。次の企画に活かしてください。
        </p>

        <p
          className="text-xs mt-8"
          style={{ color: "#888" }}
        >
          Written by Haruka Goto（NAMIMATI 2年）
        </p>
      </div>
    </section>
  );
}

// ─── コンセプト ────────────────────────────────────────────────────────────
function ConceptSection() {
  const ref = useFadeInUp();

  return (
    <section id="concept" className="py-16 md:py-24" style={{ background: "#fff" }}>
      <div className="container max-w-3xl" ref={ref}>
        <h2
          className="text-3xl md:text-4xl font-bold mb-8"
          style={{
            fontFamily: "'Noto Serif JP', serif",
            color: "#333",
          }}
        >
          La-Vita!!!とは
        </h2>

        <div className="space-y-6" style={{ color: "#555", lineHeight: "1.9" }}>
          <p>
            <strong>企画名の由来：</strong>
            「La Vita」はイタリア語で「人生」という意味。「人生を楽しむ」というコンセプトで、大学生活の中で忙しさに追われている仲間たちに、海でのリフレッシュとビタミンチャージの時間を提供する企画です。
          </p>

          <p>
            <strong>実施日時：</strong>
            2024年7月7日（日）午前9:00～午後3:00
          </p>

          <p>
            <strong>実施場所：</strong>
            鎌倉 材木座海岸
          </p>

          <p>
            <strong>参加者数：</strong>
            約50名（NAMIMATI学生団体メンバー）
          </p>

          <p>
            <strong>企画の目的：</strong>
            <br />
            ① ビーチクリーンを通じた社会貢献
            <br />
            ② 海でのスポーツ・音楽・食事を通じたメンバー間の交流
            <br />
            ③ 忙しい大学生活の中でのリフレッシュ
            <br />
            ④ 企業との連携による信頼関係構築
          </p>
        </div>
      </div>
    </section>
  );
}

// ─── コンテンツ詳細 ────────────────────────────────────────────────────────
function ContentsSection() {
  const ref = useFadeInUp();

  const contents = [
    {
      title: "① ビーチクリーン",
      description:
        "朝9:00から1時間、材木座海岸のビーチクリーンを実施。ゴミ袋を配布し、参加者全員で海岸のゴミを回収。社会貢献活動を通じて、環境への意識を高めた。",
    },
    {
      title: "② バレーボール大会",
      description:
        "ビーチクリーン後、ビーチバレーボール大会を開催。チーム分けをして、楽しく競い合った。参加者から『大学生活で久しぶりにスポーツができた』という声が多く聞かれた。",
    },
    {
      title: "③ ドリンク＆スナック",
      description:
        "HiLife Beach Houseのご協力により、冷たいドリンクとスナックを提供。疲れた体をリフレッシュ。mammababyのビタミンドリンクも配布し、栄養補給をサポート。",
    },
    {
      title: "④ 音楽＆キャンドルナイト",
      description:
        "夕方、ビーチでキャンドルを灯し、音楽を流しながらリラックスタイム。参加者同士で会話を楽しみ、海の夕陽を眺めながら、ゆったりとした時間を過ごした。",
    },
    {
      title: "⑤ オリジナルステッカー配布",
      description:
        "La-Vita!!!のオリジナルステッカーをデザイン・制作。参加者全員に配布し、イベントの記念品とした。デザインは海・太陽・人のシルエットをモチーフに、企画のコンセプトを表現。",
    },
  ];

  return (
    <section id="contents" className="py-16 md:py-24" style={{ background: "#f9fafb" }}>
      <div className="container max-w-3xl" ref={ref}>
        <h2
          className="text-3xl md:text-4xl font-bold mb-12"
          style={{
            fontFamily: "'Noto Serif JP', serif",
            color: "#333",
          }}
        >
          5つのコンテンツ
        </h2>

        <div className="space-y-8">
          {contents.map((c, i) => (
            <div
              key={i}
              className="p-6 rounded-lg"
              style={{
                background: "#fff",
                border: "1px solid rgba(0,0,0,0.1)",
              }}
            >
              <h3
                className="text-xl font-bold mb-3"
                style={{ color: "#333" }}
              >
                {c.title}
              </h3>
              <p style={{ color: "#666", lineHeight: "1.8" }}>
                {c.description}
              </p>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}

// ─── 協賛企業 ──────────────────────────────────────────────────────────────
function SponsorsSection() {
  const ref = useFadeInUp();

  return (
    <section id="sponsors" className="py-16 md:py-24" style={{ background: "#fff" }}>
      <div className="container max-w-3xl" ref={ref}>
        <h2
          className="text-3xl md:text-4xl font-bold mb-12"
          style={{
            fontFamily: "'Noto Serif JP', serif",
            color: "#333",
          }}
        >
          協賛企業
        </h2>

        <div className="space-y-10">
          {/* mammababy */}
          <div
            className="p-8 rounded-lg"
            style={{
              background: "rgba(173, 216, 230, 0.2)",
              border: "2px solid #ADD8E6",
            }}
          >
            <h3
              className="text-2xl font-bold mb-4"
              style={{ color: "#333" }}
            >
              🌿 mammababy
            </h3>
            <p style={{ color: "#666", lineHeight: "1.8", marginBottom: "1rem" }}>
              <strong>協賛内容：</strong>
              ビタミンドリンク「Vitamin Charge」を50本提供。参加者全員に配布し、海での活動後の栄養補給をサポート。
            </p>
            <p style={{ color: "#666", lineHeight: "1.8" }}>
              <strong>企業紹介：</strong>
              自然派ビタミンドリンクメーカー。健康と美容をサポートする商品を展開。大学生向けのリフレッシュドリンクとして人気。
            </p>
          </div>

          {/* HiLife Beach House */}
          <div
            className="p-8 rounded-lg"
            style={{
              background: "rgba(173, 216, 230, 0.2)",
              border: "2px solid #ADD8E6",
            }}
          >
            <h3
              className="text-2xl font-bold mb-4"
              style={{ color: "#333" }}
            >
              🏖️ HiLife Beach House
            </h3>
            <p style={{ color: "#666", lineHeight: "1.8", marginBottom: "1rem" }}>
              <strong>協賛内容：</strong>
              冷たいドリンク（アイスティー・ジュース）とスナック（ポテトチップス・クッキー）を提供。イベント中盤の休憩時間に配布。
            </p>
            <p style={{ color: "#666", lineHeight: "1.8" }}>
              <strong>企業紹介：</strong>
              材木座海岸にあるビーチハウス。カフェ・バー・イベント施設として地域に根ざした運営をしている。地元の学生団体を積極的にサポート。
            </p>
          </div>
        </div>

        <p
          className="mt-10 text-center text-sm"
          style={{ color: "#999" }}
        >
          両企業のご協力により、参加者に最高のリフレッシュ体験を提供できました。心より感謝申し上げます。
        </p>
      </div>
    </section>
  );
}

// ─── 振り返り ──────────────────────────────────────────────────────────────
function ReviewSection() {
  const ref = useFadeInUp();
  const [activeTab, setActiveTab] = useState<"good" | "challenges">("good");

  const good = [
    "参加者が50名と予想を上回り、企画の需要の高さを実感した",
    "ビーチクリーン→スポーツ→リラックスという流れが自然で、参加者の満足度が高かった",
    "協賛企業との連携がスムーズで、企業側からも『また協力したい』というお言葉をいただいた",
    "天気に恵まれ、夕陽が美しく、参加者が『最高の思い出になった』とコメント",
    "SNS投稿が自然に増え、企画のバイラル効果が期待できる",
    "メンバー間の交流が深まり、団体の結束力が高まった",
  ];

  const challenges = [
    "事前準備の時間が想定より長く、企画者の負担が大きかった",
    "ゴミ袋の数が足りず、途中で追加で用意する必要があった",
    "天気予報が不確実で、雨天時の対応を想定できていなかった",
    "参加者の年齢層が幅広く、全員が楽しめるコンテンツの設計に工夫が必要だった",
    "協賛企業との調整が複数あり、スケジュール管理が複雑だった",
    "帰宅時の交通手段の案内が不十分で、参加者から質問が多かった",
  ];

  return (
    <section id="review" className="py-16 md:py-24" style={{ background: "#f9fafb" }}>
      <div className="container max-w-3xl" ref={ref}>
        <h2
          className="text-3xl md:text-4xl font-bold mb-12"
          style={{
            fontFamily: "'Noto Serif JP', serif",
            color: "#333",
          }}
        >
          振り返り
        </h2>

        {/* Tab buttons */}
        <div className="flex gap-4 mb-8">
          <button
            onClick={() => setActiveTab("good")}
            className="px-6 py-3 rounded-lg font-bold transition-all"
            style={{
              background: activeTab === "good" ? "#ADD8E6" : "#e0e0e0",
              color: "#333",
            }}
          >
            ✅ 良かった点
          </button> 
(Content truncated due to size limit. Use line ranges to read remaining content)
