/**
 * La-Vita!!! イベントまとめページ
 * Design: Coastal Editorial — Sunset Gold × Deep Navy × Warm White
 * Target: NAMIMATI学生団体の仲間向け企画レポートページ
 * Source: La-Vita!!!企画まとめ.pdf (2024.7.7 鎌倉 材木座海岸)
 */

import { useEffect, useRef, useState } from "react";

// ─── 画像URL（manus-upload-file --webdev でアップロード済み） ───────────────
const IMAGES = {
  logo: "https://d2xsxph8kpxj0f.cloudfront.net/310519663782321279/HKZUNetSZ9AVRcQT97cpf2/logo_lavita-h2rd4aPjkHYvZXbz3tFAZw.webp",
  heroBg: "https://d2xsxph8kpxj0f.cloudfront.net/310519663782321279/HKZUNetSZ9AVRcQT97cpf2/hero_bg-Q2Y4sRt8w9MRzgj3yqm8Qf.webp",
  heroGroup: "/manus-storage/photo_hero_group_47059afe.jpg",
  mammababyProduct: "/manus-storage/photo_mammababy_product_0e4e3f63.jpg",
  clean1: "/manus-storage/photo_clean_1_1546720f.jpg",
  clean2: "/manus-storage/photo_clean_2_1f409fc6.jpg",
  clean3: "/manus-storage/photo_clean_3_48d953dd.jpg",
  volley1: "/manus-storage/photo_volley_1_7fc44cc4.jpg",
  volley2: "/manus-storage/photo_volley_2_d9af247c.jpg",
  volley3: "/manus-storage/photo_volley_3_bd0cd538.jpg",
  drinks1: "/manus-storage/photo_drinks_1_69aaa9ea.jpg",
  drinks2: "/manus-storage/photo_drinks_2_3ca8285a.jpg",
  music: "/manus-storage/photo_music_c9ff9fbe.jpg",
  candle: "/manus-storage/photo_candle_9656b192.jpg",
  sticker1: "/manus-storage/photo_sticker_1_c1966ca4.jpg",
  sticker2: "/manus-storage/photo_sticker_2_29fcede4.jpg",
  stickerDesigns: "/manus-storage/photo_sticker_designs_676132ca.jpg",
  sponsorUv: "/manus-storage/photo_sponsor_uv_30322675.jpg",
  sponsorDrinks: "/manus-storage/photo_sponsor_drinks_4342a50e.jpg",
};

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
        background: scrolled
          ? "rgba(26, 46, 59, 0.95)"
          : "transparent",
        backdropFilter: scrolled ? "blur(12px)" : "none",
        boxShadow: scrolled ? "0 2px 20px rgba(0,0,0,0.3)" : "none",
      }}
    >
      <div className="container flex items-center justify-between py-3">
        <a href="#top" className="flex items-center gap-2">
          <img src={IMAGES.logo} alt="La-Vita logo" className="w-9 h-9" />
          <span
            className="font-bold text-lg tracking-wide"
            style={{
              fontFamily: "'Noto Serif JP', serif",
              color: "#E8A04A",
            }}
          >
            La-Vita!!!
          </span>
        </a>

        {/* Desktop nav */}
        <nav className="hidden md:flex items-center gap-6">
          {links.map((l) => (
            <a
              key={l.href}
              href={l.href}
              className="text-sm font-medium transition-colors duration-200 hover:text-amber-400"
              style={{ color: scrolled ? "#FBF8F3" : "rgba(255,255,255,0.9)" }}
            >
              {l.label}
            </a>
          ))}
        </nav>

        {/* Mobile hamburger */}
        <button
          className="md:hidden flex flex-col gap-1.5 p-2"
          onClick={() => setMenuOpen(!menuOpen)}
          aria-label="メニュー"
        >
          {[0, 1, 2].map((i) => (
            <span
              key={i}
              className="block w-6 h-0.5 transition-all duration-200"
              style={{ background: "#E8A04A" }}
            />
          ))}
        </button>
      </div>

      {/* Mobile menu */}
      {menuOpen && (
        <div
          className="md:hidden px-4 pb-4 pt-2 flex flex-col gap-3"
          style={{ background: "rgba(26, 46, 59, 0.98)" }}
        >
          {links.map((l) => (
            <a
              key={l.href}
              href={l.href}
              className="text-sm font-medium py-2 border-b border-white/10"
              style={{ color: "#FBF8F3" }}
              onClick={() => setMenuOpen(false)}
            >
              {l.label}
            </a>
          ))}
        </div>
      )}
    </header>
  );
}

// ─── ヒーローセクション ───────────────────────────────────────────────────
function Hero() {
  return (
    <section
      id="top"
      className="relative min-h-screen flex items-end overflow-hidden"
      style={{ background: "#1A2E3B" }}
    >
      {/* 背景画像 */}
      <div className="absolute inset-0">
        <img
          src={IMAGES.heroBg}
          alt="材木座海岸の夕暮れ"
          className="w-full h-full object-cover"
        />
        <div
          className="absolute inset-0"
          style={{
            background:
              "linear-gradient(to top, rgba(26,46,59,0.92) 0%, rgba(26,46,59,0.5) 50%, rgba(26,46,59,0.15) 100%)",
          }}
        />
      </div>

      {/* コンテンツ */}
      <div className="relative z-10 container pb-20 pt-32">
        <div className="max-w-2xl">
          {/* イベントタグ */}
          <div className="flex flex-wrap gap-2 mb-6">
            <span
              className="sticker-badge"
              style={{ background: "#E8A04A", color: "#1A2E3B" }}
            >
              📅 2024.7.7
            </span>
            <span
              className="sticker-badge"
              style={{ background: "rgba(255,255,255,0.15)", color: "#FBF8F3" }}
            >
              📍 鎌倉 材木座海岸
            </span>
            <span
              className="sticker-badge"
              style={{ background: "rgba(91,155,173,0.3)", color: "#FBF8F3" }}
            >
              by NAMIMATI
            </span>
          </div>

          {/* タイトル */}
          <h1
            className="text-5xl md:text-7xl font-black mb-4 leading-tight"
            style={{
              fontFamily: "'Noto Serif JP', serif",
              color: "#FBF8F3",
              textShadow: "0 2px 20px rgba(0,0,0,0.4)",
            }}
          >
            La-Vita
            <span style={{ color: "#E8A04A" }}>!!!</span>
          </h1>

          {/* サブタイトル */}
          <p
            className="text-lg md:text-xl mb-2 font-light italic"
            style={{
              fontFamily: "'Playfair Display', serif",
              color: "#E8A04A",
            }}
          >
            NAMIMATI BEACH CLEAN w/ mammababy & HiLife Beach House
          </p>

          <p
            className="text-base md:text-lg leading-relaxed mb-8"
            style={{ color: "rgba(251,248,243,0.85)" }}
          >
            忙しい大学生に、リフレッシュとビタミンチャージを。
            <br />
            このページは、La-Vita!!!の企画意図・実施内容・苦労した点・協賛情報を
            <br className="hidden md:block" />
            仲間に伝えるためのまとめです。次の企画に活かしてください。
          </p>

          <p
            className="text-sm"
            style={{ color: "rgba(251,248,243,0.6)" }}
          >
            Written by <strong style={{ color: "#E8A04A" }}>Haruka Goto</strong>（NAMIMATI 2年）
          </p>
        </div>
      </div>

      {/* スクロールインジケーター */}
      <div
        className="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-1 animate-bounce"
        style={{ color: "rgba(251,248,243,0.5)" }}
      >
        <span className="text-xs tracking-widest">SCROLL</span>
        <svg width="16" height="24" viewBox="0 0 16 24" fill="none">
          <path d="M8 0v20M1 13l7 7 7-7" stroke="currentColor" strokeWidth="1.5" strokeLinecap="round" />
        </svg>
      </div>
    </section>
  );
}

// ─── セクションヘッダー共通コンポーネント ─────────────────────────────────
function SectionHeader({
  en,
  ja,
  light = false,
}: {
  en: string;
  ja: string;
  light?: boolean;
}) {
  return (
    <div className="mb-10">
      <p
        className="text-xs tracking-[0.3em] uppercase mb-2 font-medium"
        style={{
          fontFamily: "'Playfair Display', serif",
          color: light ? "rgba(251,248,243,0.5)" : "#5B9BAD",
        }}
      >
        {en}
      </p>
      <span className="gold-line" />
      <h2
        className="text-3xl md:text-4xl font-bold"
        style={{
          fontFamily: "'Noto Serif JP', serif",
          color: light ? "#FBF8F3" : "#1A2E3B",
        }}
      >
        {ja}
      </h2>
    </div>
  );
}

// ─── コンセプトセクション ─────────────────────────────────────────────────
function ConceptSection() {
  const ref = useFadeInUp();
  return (
    <section
      id="concept"
      className="py-20 md:py-28"
      style={{ background: "#FBF8F3" }}
    >
      <div className="container">
        <div
          ref={ref}
          className="fade-in-up grid md:grid-cols-2 gap-12 items-center"
        >
          {/* テキスト */}
          <div>
            <SectionHeader en="Concept" ja="La-Vita!!!とは" />
            <p
              className="text-base leading-relaxed mb-4"
              style={{ color: "#2C2C2C" }}
            >
              「La-Vita」はイタリア語で、ビタミンの語源となった言葉です。このイベントを通して
              <strong style={{ color: "#E8A04A" }}>気分もリフレッシュ、ビタミンもチャージ</strong>
              してもらいたいという想いが込められています。
            </p>
            <p
              className="text-base leading-relaxed mb-4"
              style={{ color: "#2C2C2C" }}
            >
              イタリア発祥の<strong>mammababy</strong>さんの日焼け止めを使って
              肌も大事にして欲しいという想い、そして学校・バイト・サークル・課題と
              多岐に渡って活動する忙しい大学生に、
              <strong style={{ color: "#E8A04A" }}>少しでも息抜きできる空間</strong>を
              提供したいという願いから企画されました。
            </p>
            <div
              className="mt-6 p-4 rounded-lg border-l-4"
              style={{
                borderColor: "#E8A04A",
                background: "rgba(232,160,74,0.08)",
              }}
            >
              <p
                className="text-sm italic font-medium"
                style={{
                  fontFamily: "'Playfair Display', serif",
                  color: "#1A2E3B",
                }}
              >
                "Enjoy La-Vita!!! Have fun!!!"
              </p>
            </div>
          </div>

          {/* 集合写真 */}
          <div className="relative">
            <img
              src={IMAGES.heroGroup}
              alt="La-Vita!!!参加者の集合写真"
              className="w-full rounded-2xl object-cover photo-card"
              style={{
                aspectRatio: "4/3",
                boxShadow: "0 20px 60px rgba(26,46,59,0.25)",
              }}
            />
            <div
              className="absolute -bottom-4 -right-4 px-4 py-2 rounded-xl text-sm font-bold"
              style={{
                background: "#1A2E3B",
                color: "#E8A04A",
                fontFamily: "'Noto Serif JP', serif",
              }}
            >
              50名以上が参加
            </div>
          </div>
        </div>
      </div>
    </section>
  );
}

// ─── コンテンツカード ─────────────────────────────────────────────────────
interface ContentCardProps {
  icon: string;
  title: string;
  description: string;
  images: string[];
  imageAlts: string[];
  reverse?: boolean;
  delay?: number;
}

function ContentCard({
  icon,
  title,
  description,
  images,
  imageAlts,
  reverse = false,
  delay = 0,
}: ContentCardProps) {
  const ref = useRef<HTMLDivElement>(null);
  useEffect(() => {
    const el = ref.current;
    if (!el) return;
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setTimeout(() => el.classList.add("visible"), delay);
          observer.disconnect();
        }
      },
      { threshold: 0.1 }
    );
    observer.observe(el);
    return () => observer.disconnect();
  }, [delay]);

  return (
    <div
      ref={ref}
      className={`fade-in-up grid md:grid-cols-2 gap-8 md:gap-12 items-center ${
        reverse ? "md:[&>*:first-child]:order-2" : ""
      }`}
    >
      {/* テキスト */}
      <div>
        <div className="flex items-center gap-3 mb-4">
          <span className="text-3xl">{icon}</span>
          <h3
            className="text-2xl font-bold"
            style={{
              fontFamily: "'Noto Serif JP', serif",
              color: "#1A2E3B",
            }}
          >
            {title}
          </h3>
        </div>
        <span className="gold-line" />
        <p
          className="text-base leading-relaxed"
          style={{ color: "#2C2C2C" }}
          dangerouslySetInnerHTML={{ __html: description }}
        />
      </div>

      {/* 写真グリッド */}
      <div
        className={`grid gap-3 ${images.length === 1 ? "grid-cols-1" : images.length === 2 ? "grid-cols-2" : "grid-cols-2"}`}
      >
        {images.map((src, i) => (
          <img
            key={i}
            src={src}
            alt={imageAlts[i]}
            className={`w-full rounded-xl object-cover photo-card ${
              images.length === 3 && i === 2 ? "col-span-2" : ""
            }`}
            style={{
              aspectRatio: images.length === 1 ? "4/3" : "1/1",
              boxShadow: "0 8px 30px rgba(26,46,59,0.15)",
            }}
          />
        ))}
      </div>
    </div>
  );
}

// ─── コンテンツセクション ─────────────────────────────────────────────────
function ContentsSection() {
  const headerRef = useFadeInUp();

  const contents = [
    {
      icon: "🌊",
      title: "ビーチクリーン",
      description:
        "環境と浜辺に優しい行動をすることで、自身の心もリフレッシュ＆マインドリセット！<br/><br/>" +
        "mammababyさんの<strong>可愛いクリアボトル</strong>に海洋プラスチック・マイクロプラスチックのゴミを入れることで、浜辺のマイプラを<strong style='color:#E8A04A'>「見える化」</strong>。SNSで発信しやすくなる仕掛けにもなりました。<br/><br/>" +
        "チル空間を楽しむ前にエコ活動をすることで、マインドをリフレッシュし、その後の宴をより心から楽しめる設計です。",
      images: [IMAGES.clean1, IMAGES.clean2, IMAGES.clean3],
      imageAlts: ["ビーチクリーンの様子1", "クリアボトルにゴミを集める様子", "砂浜でビーチクリーンをする参加者"],
      reverse: false,
    },
    {
      icon: "🏐",
      title: "ビーチバレー",
      description:
        "クリーンの時に集めた材木座海岸の<strong>流木を使ってコートを造った</strong>のがポイント。身体を動かすことで自然と笑顔に。<br/><br/>" +
        "クリーンのチームごとに試合をすることで仲良くなれる設計にし、パスをする時に名前を呼ぶことで<strong style='color:#E8A04A'>なみまちの新メンバーが名前を覚えるチャンス</strong>を増やしました。<br/><br/>" +
        "スポーツを通したハッピーな声掛けで、メンバーの距離感を縮めることができました！（スポーツの力はすごい！！！）",
      images: [IMAGES.volley1, IMAGES.volley2, IMAGES.volley3],
      imageAlts: ["ビーチバレーでスパイクする様子", "夕暮れの中でチームが集まる様子", "砂浜でビーチバレーをする様子"],
      reverse: true,
    },
    {
      icon: "🥤",
      title: "ドリンク",
      description:
        "<strong>HiLife Beach House</strong>さんのドリンクでビタミンチャージ。<br/><br/>" +
        "ウェルカムドリンクでビタミンチャージ＆リフレッシュ、現実から非日常世界へ入り込む瞬間を演出。ビーチクリーンとバレーで体を動かした後に2度目のドリンクサービスをし、エネルギーチャージ。<br/><br/>" +
        "フレーバーは<strong style='color:#E8A04A'>マンゴー・パイン・グレープフルーツ・オレンジ</strong>の4種類。皆んなで乾杯（Saluti）することで、仲良くなれる瞬間を作りました。",
      images: [IMAGES.drinks1, IMAGES.drinks2],
      imageAlts: ["フルーツの準備の様子", "海辺でドリンクを乾杯する様子"],
      reverse: false,
    },
    {
      icon: "🎺",
      title: "音楽 & キャンドル",
      description:
        "吹奏楽の<strong>生演奏</strong>で癒される特別な時間。トロンボーン＆トランペット奏者は知り合いの高校生＆NAMIMATIメンバーのご協力によるもの。<br/><br/>" +
        "七夕にちなんだ曲「<strong style='color:#E8A04A'>Twinkle Twinkle Little Star ✨</strong>」の生演奏で、特別感を演出。参加者のリクエストに応えた洋楽も流し、チルいムードを作りました。<br/><br/>" +
        "キャンドルは「<strong>1/fゆらぎ</strong>」と呼ばれる炎の癒し効果を活かし、エモーショナルな空間を確立。",
      images: [IMAGES.music, IMAGES.candle],
      imageAlts: ["海辺での金管楽器の生演奏", "砂浜に置かれたキャンドル"],
      reverse: true,
    },
    {
      icon: "🎁",
      title: "サプライズ & 参加者への感謝",
      description:
        "イベントに込めた想い全てをデザイン化した<strong>ステッカーのプレゼント（全4種類）</strong>。<br/><br/>" +
        "モノをすぐに捨てないで大事にしてもらいたいという想いを込めて、ステッカーにある仕掛けを付け、次回のイベント時などにネタバラシする計画も。<br/><br/>" +
        "Instagramのストーリー機能で「<strong style='color:#E8A04A'>La-Vita!/@namimati</strong>」と書き込み、イベントの写真を投稿していただくお願いをすることで、NAMIMATIという学生団体の活動を広める仕掛けにしました。",
      images: [IMAGES.sticker1, IMAGES.sticker2, IMAGES.stickerDesigns],
      imageAlts: ["ステッカーを手に持つ様子", "ノベルティとイベントビジュアル", "全4種類のステッカーデザイン"],
      reverse: false,
    },
  ];

  return (
    <section
      id="contents"
      className="py-20 md:py-28"
      style={{ background: "#FBF8F3" }}
    >
      <div className="container">
        <div ref={headerRef} className="fade-in-up mb-16">
          <SectionHeader en="Contents" ja="イベントのコンテンツ" />
          <p style={{ color: "#555" }}>
            La-Vita!!!は「チル空間の創造」をテーマに、複数のコンテンツを有機的に組み合わせた企画です。
          </p>
        </div>

        <div className="flex flex-col gap-20">
          {contents.map((c, i) => (
            <ContentCard key={c.title} {...c} delay={i * 100} />
          ))}
        </div>
      </div>
    </section>
  );
}

// ─── 協賛セクション ───────────────────────────────────────────────────────
function SponsorsSection() {
  const ref = useFadeInUp();

  return (
    <section
      id="sponsors"
      className="py-20 md:py-28"
      style={{ background: "#1A2E3B" }}
    >
      <div className="container">
        <div ref={ref} className="fade-in-up">
          <SectionHeader en="Sponsors" ja="ご協賛企業" light />
          <p className="mb-12" style={{ color: "rgba(251,248,243,0.7)" }}>
            今回のLa-Vita!!!は、2社の企業様のご協賛により実現しました。
            協賛をつけることでイベントのボリュームが増し、集客率の向上にも繋がりました。
          </p>

          <div className="grid md:grid-cols-2 gap-8">
            {/* mammababy */}
            <div
              className="rounded-2xl p-8 photo-card"
              style={{
                background: "rgba(255,255,255,0.05)",
                border: "1px solid rgba(232,160,74,0.3)",
              }}
            >
              <div className="flex items-start gap-4 mb-6">
                <div
                  className="w-12 h-12 rounded-full flex items-center justify-center text-2xl flex-shrink-0"
                  style={{ background: "rgba(232,160,74,0.2)" }}
                >
                  ☀️
                </div>
                <div>
                  <h3
                    className="text-xl font-bold mb-1"
                    style={{
                      fontFamily: "'Noto Serif JP', serif",
                      color: "#E8A04A",
                    }}
                  >
                    mammababy
                  </h3>
                  <p
                    className="text-xs tracking-widest uppercase"
                    style={{ color: "rgba(251,248,243,0.4)" }}
                  >
                    イタリア発祥のスキンケアブランド
                  </p>
                </div>
              </div>

              <div className="grid grid-cols-2 gap-4 mb-6">
                <img
                  src={IMAGES.mammababyProduct}
                  alt="mammababy UV MILK製品"
                  className="w-full rounded-xl object-cover"
                  style={{ aspectRatio: "4/3" }}
                />
                <img
                  src={IMAGES.sponsorUv}
                  alt="mammababy UV MILKの配布の様子"
                  className="w-full rounded-xl object-cover"
                  style={{ aspectRatio: "4/3" }}
                />
              </div>

              <div
                className="rounded-xl p-4"
                style={{ background: "rgba(255,255,255,0.05)" }}
              >
                <p
                  className="text-xs uppercase tracking-widest mb-2"
                  style={{ color: "#5B9BAD" }}
                >
                  協賛内容（PDF記載）
                </p>
                <ul className="space-y-1">
                  <li className="flex items-center gap-2 text-sm" style={{ color: "#FBF8F3" }}>
                    <span style={{ color: "#E8A04A" }}>✦</span>
                    NON-CHEMICAL UV MILK SPF50+ / PA++++ × <strong>50個</strong>
                  </li>
                  <li className="flex items-center gap-2 text-sm" style={{ color: "#FBF8F3" }}>
                    <span style={{ color: "#E8A04A" }}>✦</span>
                    オリジナルステッカー
                  </li>
                </ul>
              </div>

              <p
                className="mt-4 text-sm leading-relaxed"
                style={{ color: "rgba(251,248,243,0.65)" }}
              >
                高価な商品でもあるため、mammababyさんに信頼していただけたからこそご協賛いただけました。
                今後も良い繋がりを持ち続けられるように努めたいと感じています。
              </p>
            </div>

            {/* HiLife Beach House */}
            <div
              className="rounded-2xl p-8 photo-card"
              style={{
                background: "rgba(255,255,255,0.05)",
                border: "1px solid rgba(91,155,173,0.3)",
              }}
            >
              <div className="flex items-start gap-4 mb-6">
                <div
                  className="w-12 h-12 rounded-full flex items-center justify-center text-2xl flex-shrink-0"
                  style={{ background: "rgba(91,155,173,0.2)" }}
                >
                  🌴
                </div>
                <div>
                  <h3
                    className="text-xl font-bold mb-1"
                    style={{
                      fontFamily: "'Noto Serif JP', serif",
                      color: "#5B9BAD",
                    }}
                  >
                    HiLife Beach House
                  </h3>
                  <p
                    className="text-xs tracking-widest uppercase"
                    style={{ color: "rgba(251,248,243,0.4)" }}
                  >
                    鎌倉のビーチハウス
                  </p>
                </div>
              </div>

              <div className="grid grid-cols-1 gap-4 mb-6">
                <img
                  src={IMAGES.sponsorDrinks}
                  alt="HiLife Beach Houseのドリンク"
                  className="w-full rounded-xl object-cover"
                  style={{ aspectRatio: "16/7" }}
                />
              </div>

              <div
                className="rounded-xl p-4"
                style={{ background: "rgba(255,255,255,0.05)" }}
              >
                <p
                  className="text-xs uppercase tracking-widest mb-2"
                  style={{ color: "#5B9BAD" }}
                >
                  協賛内容（PDF記載）
                </p>
                <ul className="space-y-1">
                  <li className="flex items-center gap-2 text-sm" style={{ color: "#FBF8F3" }}>
                    <span style={{ color: "#5B9BAD" }}>✦</span>
                    ドリンク協賛（マンゴー・パイン・グレープフルーツ・オレンジ）
                  </li>
                </ul>
              </div>

              <p
                className="mt-4 text-sm leading-relaxed"
                style={{ color: "rgba(251,248,243,0.65)" }}
              >
                HiLifeさんからも「NAMIMATIの印象が良い」とお褒めの言葉をいただきました。
                ドリンクの片付けや配布なども積極的に協力してくださる姿勢が素晴らしかったです。
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  );
}

// ─── 振り返りセクション ───────────────────────────────────────────────────
function ReviewSection() {
  const ref = useFadeInUp();
  const [activeTab, setActiveTab] = useState<"good" | "issue">("good");

  const goodPoints = [
    {
      icon: "🎉",
      title: "全員が楽しめた",
      body: "参加者・企画者含め、みんなが楽しんでくれた。最後まで妥協せず細部までこだわり抜いた。",
    },
    {
      icon: "📸",
      title: "SNS投稿率が高かった",
      body: "ストーリーを投稿した人にはステッカープレゼントのシステムにしたため、普段より多くの参加者に投稿していただけた。その場で投稿してもらう工夫が奏功。",
    },
    {
      icon: "👥",
      title: "新歓効果もあった",
      body: "新入生にもなみまちをメンションしたストーリーを投稿してもらうことで、学生団体の新歓という側面でも良い効果があった。",
    },
    {
      icon: "📈",
      title: "集客が想定以上",
      body: "協賛をつけてボリュームのある企画にできたため、集客率も上がった。想定人数を上回る50名以上が参加。",
    },
    {
      icon: "🤝",
      title: "相互扶助が機能した",
      body: "メンバー1人1人が一所懸命その場に必要なことを考えて動いていた。全体最適より部分最適に努めた点が結果として全体の成功につながった。",
    },
    {
      icon: "🌅",
      title: "夕陽が最高だった",
      body: "夕陽が最高に綺麗で、バレーボールをしているシルエットが映えていた。参加者も肩の荷を下ろして心から楽しめている様子が伺えた。",
    },
  ];

  const issuePoints = [
    {
      icon: "📋",
      title: "役割分担に苦戦",
      body: "短期間かつイベント創設メンバー全員での顔合わせができなかったため、最初の段階では役割分担に苦戦した。",
      lesson: "→ 少なくとも1〜2ヶ月前からミーティング日を固定で決めておく！",
    },
    {
      icon: "💬",
      title: "情報が分散した",
      body: "LINEグループが複数に派生していて、情報が散在していた。イベント当日までバタバタで情報の離散・重複が発生。",
      lesson: "→ Zoom or 対面でのミーティングは必須！LINEだけだと情報共有の漏れが出る。",
    },
    {
      icon: "⏱️",
      title: "タイムテーブルが曖昧",
      body: "当日の段取りが少し雑になってしまった。イベント中の待ち時間など、間延びしている場面が多かった。",
      lesson: "→ タイムテーブルをボードなどに書いておく。声を出せる企画メンバーの必要性 or マイクなど。",
    },
    {
      icon: "🥤",
      title: "ドリンク配布のオペレーション",
      body: "マイグラスを回収してドリンクを渡すまでの時間がかかりすぎた。渡した人数集計が不透明になってしまった。",
      lesson: "→ 整列させてある程度秩序のある空気感を作ることも大切。半セルフサービスも検討。",
    },
    {
      icon: "⚖️",
      title: "緩さと秩序のバランス",
      body: "チル空間を創るためには大きな声掛けや秩序のある雰囲気をなくして、ある程度の緩さを出すことも必要。しかし運営する以上、限度が必要。",
      lesson: "→ 緩和性と厳粛性のバランス感がとても大事！！！",
    },
    {
      icon: "🎯",
      title: "当日の流れ想定に時間を割く",
      body: "参加者はイベントを終えた後は各々のことに興味がいってしまうため、その場でやってもらうようにする（LINE登録・ストーリー更新など）。",
      lesson: "→ 当日の流れ想定にもっと時間を割く。フライヤーは動画も活用して視覚的な集客を。",
    },
  ];

  return (
    <section
      id="review"
      className="py-20 md:py-28"
      style={{ background: "#FBF8F3" }}
    >
      <div className="container">
        <div ref={ref} className="fade-in-up">
          <SectionHeader en="Review" ja="振り返り" />
          <p className="mb-10" style={{ color: "#555" }}>
            La-Vita!!!を通して得た学びを、次の企画に活かしてください。
            成功した点も、苦労した点も、すべてが財産です。
          </p>

          {/* タブ切り替え */}
          <div className="flex gap-2 mb-8">
            <button
              onClick={() => setActiveTab("good")}
              className="px-6 py-2.5 rounded-full text-sm font-bold transition-all duration-200"
              style={{
                background: activeTab === "good" ? "#E8A04A" : "transparent",
                color: activeTab === "good" ? "#1A2E3B" : "#888",
                border: `2px solid ${activeTab === "good" ? "#E8A04A" : "#ddd"}`,
              }}
            >
              ✅ 良かったこと
            </button>
            <button
              onClick={() => setActiveTab("issue")}
              className="px-6 py-2.5 rounded-full text-sm font-bold transition-all duration-200"
              style={{
                background: activeTab === "issue" ? "#1A2E3B" : "transparent",
                color: activeTab === "issue" ? "#FBF8F3" : "#888",
                border: `2px solid ${activeTab === "issue" ? "#1A2E3B" : "#ddd"}`,
              }}
            >
              ⚠️ 課題・改善点
            </button>
          </div>

          {/* 良かったこと */}
          {activeTab === "good" && (
            <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-5">
              {goodPoints.map((p, i) => (
                <div
                  key={i}
                  className="rounded-2xl p-6 photo-card"
                  style={{
                    background: "#fff",
                    border: "1px solid rgba(232,160,74,0.2)",
                    boxShadow: "0 4px 20px rgba(26,46,59,0.06)",
                  }}
                >
                  <span className="text-3xl mb-3 block">{p.icon}</span>
                  <h4
                    className="font-bold text-base mb-2"
                    style={{
                      fontFamily: "'Noto Serif JP', serif",
                      color: "#1A2E3B",
                    }}
                  >
                    {p.title}
                  </h4>
                  <p className="text-sm leading-relaxed" style={{ color: "#555" }}>
                    {p.body}
                  </p>
                </div>
              ))}
            </div>
          )}

          {/* 課題・改善点 */}
          {activeTab === "issue" && (
            <div className="flex flex-col gap-4">
              {issuePoints.map((p, i) => (
                <div
                  key={i}
                  className="rounded-2xl p-6 photo-card"
                  style={{
                    background: "#fff",
                    border: "1px solid rgba(26,46,59,0.1)",
                    boxShadow: "0 4px 20px rgba(26,46,59,0.06)",
                  }}
                >
                  <div className="flex items-start gap-4">
                    <span className="text-2xl flex-shrink-0">{p.icon}</span>
                    <div className="flex-1">
                      <h4
                        className="font-bold text-base mb-1"
                        style={{
                          fontFamily: "'Noto Serif JP', serif",
                          color: "#1A2E3B",
                        }}
                      >
                        {p.title}
                      </h4>
                      <p className="text-sm leading-relaxed mb-3" style={{ color: "#555" }}>
                        {p.body}
                      </p>
                      <div
                        className="text-sm font-medium px-3 py-2 rounded-lg"
                        style={{
                          background: "rgba(232,160,74,0.1)",
                          color: "#1A2E3B",
                          borderLeft: "3px solid #E8A04A",
                        }}
                      >
                        {p.lesson}
                      </div>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          )}

          {/* 重要メッセージ */}
          <div
            className="mt-12 rounded-2xl p-8 text-center"
            style={{
              background: "linear-gradient(135deg, #1A2E3B 0%, #2a4a5e 100%)",
            }}
          >
            <p
              className="text-2xl font-bold mb-3"
              style={{
                fontFamily: "'Noto Serif JP', serif",
                color: "#E8A04A",
              }}
            >
              ！！！緩和性と厳粛性のバランス感がとても大事！！！
            </p>
            <p className="text-sm" style={{ color: "rgba(251,248,243,0.7)" }}>
              チル空間を創るためには、大きな声掛けや秩序のある雰囲気をなくして、ある程度の緩さを出すことも必要。
              しかし、イベントを運営する以上、限度が必要になってくる。
            </p>
          </div>
        </div>
      </div>
    </section>
  );
}

// ─── メンバーの声セクション ───────────────────────────────────────────────
function VoicesSection() {
  const ref = useFadeInUp();

  const voices = [
    "バタバタしてしまって反省する点はたくさんあるけど、この最高なメンバーの企画に携われて本当によかったです。みんなの積極的に動いてくれるところに本当に救われてばかりでした。もっと企画してみたい！という意欲にもなりました！！感謝しかないし、このメンバーでよかったです。",
    "不安要素たくさんでどうなるかと思ったし、本当に反省しました。でもアルバム写真の量の多さとかから見ても本当にみんな楽しんでくれていたと思うし、私自身も楽しすぎたからこのイベント参加できてよかった！！最高でした！！",
    "実際使ってみたいと思う商品を協賛にイベントができてすごく嬉しかった！先方の意図・意向を汲みとってその中で企画を考えようとしていたが、今回40本の現品協賛を実現できたように、自分たちが実現させたいことも言ってみて擦り合わせすることが大事で、より良いイベントにしていく重要なプロセスだと感じた。",
    "約1ヶ月間でしたが、本当にありがとうございました！！初めてのイベントをこんなに素敵なメンバーの皆さんと企画させていただけて、嬉しかったです！これからもよろしくお願いします！！",
  ];

  return (
    <section
      id="voices"
      className="py-20 md:py-28"
      style={{
        background: "linear-gradient(135deg, #1A2E3B 0%, #0f1e28 100%)",
      }}
    >
      <div className="container">
        <div ref={ref} className="fade-in-up">
          <SectionHeader en="Member Voices" ja="企画者たちの声" light />
          <p className="mb-12" style={{ color: "rgba(251,248,243,0.6)" }}>
            ♡ 企画者たちの感想まとめ ♡
          </p>

          <div className="grid md:grid-cols-2 gap-6">
            {voices.map((v, i) => (
              <div
                key={i}
                className="rounded-2xl p-6 photo-card"
                style={{
                  background: "rgba(255,255,255,0.05)",
                  border: "1px solid rgba(232,160,74,0.15)",
                }}
              >
                <div
                  className="text-4xl mb-4 font-serif leading-none"
                  style={{ color: "#E8A04A", opacity: 0.4 }}
                >
                  "
                </div>
                <p
                  className="text-sm leading-relaxed"
                  style={{ color: "rgba(251,248,243,0.85)" }}
                >
                  {v}
                </p>
                <div
                  className="mt-4 text-xs"
                  style={{ color: "rgba(251,248,243,0.35)" }}
                >
                  — NAMIMATI メンバー
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </section>
  );
}

// ─── 次回企画者へのメッセージ ─────────────────────────────────────────────
function MessageSection() {
  const ref = useFadeInUp();
  return (
    <section
      className="py-20 md:py-24"
      style={{ background: "#FBF8F3" }}
    >
      <div className="container">
        <div ref={ref} className="fade-in-up max-w-2xl mx-auto text-center">
          <span className="text-4xl block mb-6">ᐢ⸝⸝•⩊•⸝⸝ᐡ</span>
          <h2
            className="text-2xl md:text-3xl font-bold mb-6"
            style={{
              fontFamily: "'Noto Serif JP', serif",
              color: "#1A2E3B",
            }}
          >
            次の企画者へ
          </h2>
          <p
            className="text-base leading-relaxed mb-4"
            style={{ color: "#2C2C2C" }}
          >
            この反省点を生かすことを視野に入れてイベント企画をすると、
            完成度の高い企画ができると思います！
            これを読んでみるとイベントの成功に対する不安も増えてしまうかもしれませんが、
            失敗することでさらに良いイベントを作るモチベーションを上げることもできます！
          </p>
          <p
            className="text-base leading-relaxed mb-6"
            style={{ color: "#2C2C2C" }}
          >
            実際にLa-Vita!の創設メンバーもこのイベントを通してたくさん学ぶことができました！
            そのため、気楽に自分らしい素敵なイベントを作ってみてください！！
          </p>
          <div
            className="rounded-2xl p-6"
            style={{
              background: "rgba(232,160,74,0.1)",
              border: "1px solid rgba(232,160,74,0.3)",
            }}
          >
            <p
              className="text-base font-medium"
              style={{
                fontFamily: "'Noto Serif JP', serif",
                color: "#1A2E3B",
              }}
            >
              うまくいくと信じて企画すれば多分いい企画になると思います！
              <br />
              <span style={{ color: "#E8A04A" }}>Good luck!! (๑•᎑&lt;๑)ｰ☆</span>
            </p>
          </div>
          <p
            className="mt-8 text-sm"
            style={{ color: "#888" }}
          >
            — La-Vita!!!創設者一同より
            <br />
            そして、来てくれたみんな本当にありがとう！感謝すぎる〜！！
          </p>
        </div>
      </div>
    </section>
  );
}

// ─── フッター ─────────────────────────────────────────────────────────────
function Footer() {
  return (
    <footer
      className="py-10"
      style={{ background: "#0f1e28" }}
    >
      <div className="container flex flex-col md:flex-row items-center justify-between gap-4">
        <div className="flex items-center gap-3">
          <img src={IMAGES.logo} alt="La-Vita logo" className="w-8 h-8 opacity-80" />
          <div>
            <p
              className="font-bold text-sm"
              style={{ color: "#E8A04A", fontFamily: "'Noto Serif JP', serif" }}
            >
              La-Vita!!!
            </p>
            <p className="text-xs" style={{ color: "rgba(251,248,243,0.4)" }}>
              2024.7.7 @ 鎌倉 材木座海岸
            </p>
          </div>
        </div>

        <div className="text-center md:text-right">
          <p className="text-xs" style={{ color: "rgba(251,248,243,0.4)" }}>
            
          </p>
          <p className="text-xs mt-1" style={{ color: "rgba(251,248,243,0.3)" }}>
            © 2024 NAMIMATI. All rights reserved.
          </p>
        </div>
      </div>
    </footer>
  );
}

// ─── メインエクスポート ────────────────────────────────────────────────────
export default function Home() {
  return (
    <div className="min-h-screen" style={{ background: "#FBF8F3" }}>
      <Nav />
      <Hero />
      <ConceptSection />
      <ContentsSection />
      <SponsorsSection />
      <ReviewSection />
      <VoicesSection />
      <MessageSection />
      <Footer />
    </div>
  );
}

