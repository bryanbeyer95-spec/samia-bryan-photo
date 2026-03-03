# samia-bryan-photo<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bryan Photographie | Samia</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Inter:wght@200;300;400;500&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --noir: #050505;
            --noir-soft: #0a0a0a;
            --blanc: #f8f8f6;
            --blanc-casse: #e0e0dc;
            --or: #c9a962;
            --or-pale: #d4b978;
        }
        
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--noir);
            color: var(--blanc);
            overflow-x: hidden;
        }
        
        .font-serif { font-family: 'Cormorant Garamond', serif; }
        
        /* Grain animé */
        .grain {
            position: fixed;
            top: -50%; left: -50%;
            width: 200%; height: 200%;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
            opacity: 0.03;
            pointer-events: none;
            z-index: 9999;
            animation: grain 8s steps(10) infinite;
        }
        
        @keyframes grain {
            0%, 100% { transform: translate(0, 0); }
            10% { transform: translate(-5%, -10%); }
            20% { transform: translate(-15%, 5%); }
            30% { transform: translate(7%, -25%); }
            40% { transform: translate(-5%, 25%); }
            50% { transform: translate(-15%, 10%); }
            60% { transform: translate(15%, 0%); }
            70% { transform: translate(0%, 15%); }
            80% { transform: translate(3%, 35%); }
            90% { transform: translate(-10%, 10%); }
        }
        
        /* Cursor */
        .cursor {
            position: fixed;
            width: 15px; height: 15px;
            border: 1px solid var(--or);
            border-radius: 50%;
            pointer-events: none;
            z-index: 10000;
            transition: transform 0.15s, background 0.15s;
            mix-blend-mode: difference;
        }
        .cursor.hover {
            transform: scale(2);
            background: var(--or);
            opacity: 0.2;
        }
        .cursor-dot {
            position: fixed;
            width: 3px; height: 3px;
            background: var(--or);
            border-radius: 50%;
            pointer-events: none;
            z-index: 10001;
        }
        
        /* Loader */
        .loader {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: var(--noir);
            z-index: 9998;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 2rem;
        }
        .loader-text {
            font-family: 'Cormorant Garamond', serif;
            font-size: 0.9rem;
            letter-spacing: 0.8em;
            text-transform: uppercase;
            color: var(--or);
        }
        .loader-line {
            width: 0; height: 1px;
            background: var(--or);
        }
        
        /* Navigation */
        .nav {
            position: fixed;
            top: 0; left: 0;
            width: 100%;
            padding: 1.5rem 3rem;
            z-index: 100;
            display: flex;
            justify-content: space-between;
            align-items: center;
            opacity: 0;
            transform: translateY(-20px);
            transition: all 0.6s ease;
            background: linear-gradient(to bottom, rgba(5,5,5,0.8), transparent);
        }
        .nav.visible { opacity: 1; transform: translateY(0); }
        .nav-logo {
            font-size: 0.7rem;
            letter-spacing: 0.4em;
            text-transform: uppercase;
            color: var(--blanc-casse);
        }
        .nav-menu {
            display: flex;
            gap: 2rem;
            font-size: 0.65rem;
            letter-spacing: 0.2em;
            text-transform: uppercase;
        }
        .nav-menu span {
            cursor: pointer;
            opacity: 0.6;
            transition: opacity 0.3s;
        }
        .nav-menu span:hover { opacity: 1; color: var(--or); }
        
        /* Chapitres */
        .chapter {
            min-height: 100vh;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            padding: 3rem 2rem;
        }
        
        /* Chapitre 1 */
        .chapter-1 {
            background: linear-gradient(135deg, var(--noir) 0%, #0f0f0f 50%, var(--noir) 100%);
        }
        .chapter-1 .chapter-image {
            position: absolute;
            width: 45%;
            max-width: 700px;
            height: auto;
            max-height: 80vh;
            object-fit: contain;
            opacity: 0;
            filter: brightness(0.4);
            transform: scale(1.05);
            cursor: pointer;
        }
        .chapter-1 .chapter-content {
            position: relative;
            z-index: 10;
            text-align: center;
            max-width: 700px;
        }
        
        .chapter-number {
            font-size: 0.65rem;
            letter-spacing: 0.8em;
            text-transform: uppercase;
            color: var(--or);
            margin-bottom: 1.5rem;
            opacity: 0;
        }
        .chapter-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: clamp(2.5rem, 6vw, 5rem);
            font-weight: 300;
            line-height: 1;
            margin-bottom: 2rem;
            opacity: 0;
            transform: translateY(30px);
        }
        .chapter-quote {
            font-family: 'Cormorant Garamond', serif;
            font-size: clamp(1rem, 2vw, 1.4rem);
            font-style: italic;
            line-height: 1.8;
            color: var(--blanc-casse);
            opacity: 0;
        }
        
        /* Chapitre 2 - Élégance */
        .chapter-2 {
            background: var(--noir-soft);
            flex-direction: column;
            padding-top: 6rem;
        }
        .chapter-2 .gallery-reveal {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1.5rem;
            width: 100%;
            max-width: 1100px;
            margin-top: 3rem;
        }
        .reveal-item {
            position: relative;
            overflow: hidden;
            opacity: 0;
            transform: translateY(50px);
            aspect-ratio: 3/4;
            cursor: pointer;
        }
        .reveal-item img {
            width: 100%; height: 100%;
            object-fit: cover;
            filter: grayscale(100%) brightness(0.7);
            transform: scale(1.1);
            transition: all 1.2s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-item.revealed img {
            filter: grayscale(0%) brightness(1);
            transform: scale(1);
        }
        
        /* Chapitre 3 - Intimité */
        .chapter-3 {
            background: linear-gradient(to bottom, var(--noir-soft), var(--noir));
            flex-direction: column;
            padding-top: 6rem;
        }
        .chapter-3 .veil-gallery {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 2rem;
            max-width: 900px;
            width: 100%;
            margin-top: 3rem;
        }
        .veil-item {
            position: relative;
            overflow: hidden;
            opacity: 0;
            aspect-ratio: 4/5;
            cursor: pointer;
        }
        .veil-item img {
            width: 100%; height: 100%;
            object-fit: cover;
            filter: brightness(0.5) contrast(1.1);
            transition: all 0.8s ease;
        }
        .veil-item:hover img {
            filter: brightness(0.9) contrast(1);
            transform: scale(1.03);
        }
        
        /* Chapitre 4 - La Muse (50 photos) */
        .chapter-4 {
            background: var(--noir);
            flex-direction: column;
            padding: 6rem 2rem;
            min-height: auto;
        }
        .chapter-4 .muse-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 1rem;
            max-width: 1400px;
            width: 100%;
            margin-top: 3rem;
        }
        .muse-item {
            position: relative;
            overflow: hidden;
            opacity: 0;
            transform: scale(0.9);
            aspect-ratio: 1;
            cursor: pointer;
        }
        .muse-item img {
            width: 100%; height: 100%;
            object-fit: cover;
            filter: grayscale(50%) brightness(0.85);
            transition: all 0.5s ease;
        }
        .muse-item:hover img {
            filter: grayscale(0%) brightness(1);
            transform: scale(1.08);
        }
        .muse-item:nth-child(6n+1) { grid-column: span 2; grid-row: span 2; }
        .muse-item:nth-child(9n+3) { grid-column: span 2; }
        
        /* Final */
        .final {
            min-height: 80vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 4rem 2rem;
            background: radial-gradient(ellipse at center, #0f0f0f 0%, var(--noir) 70%);
        }
        .final-text {
            font-family: 'Cormorant Garamond', serif;
            font-size: clamp(1.5rem, 4vw, 2.5rem);
            font-style: italic;
            font-weight: 300;
            max-width: 700px;
            line-height: 1.6;
            margin-bottom: 3rem;
        }
        .final-text .line {
            display: block;
            opacity: 0;
            transform: translateY(20px);
        }
        .final-signature {
            font-size: 0.7rem;
            letter-spacing: 0.6em;
            text-transform: uppercase;
            color: var(--or);
            opacity: 0;
        }
        .final-line {
            width: 1px; height: 60px;
            background: linear-gradient(to bottom, var(--or), transparent);
            margin: 2rem 0;
            opacity: 0;
        }
        
        /* Lightbox */
        .lightbox {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(5,5,5,0.98);
            z-index: 9997;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            visibility: hidden;
            transition: all 0.4s ease;
            padding: 2rem;
        }
        .lightbox.active {
            opacity: 1;
            visibility: visible;
        }
        .lightbox img {
            max-width: 90%;
            max-height: 90%;
            object-fit: contain;
            transform: scale(0.95);
            transition: transform 0.4s ease;
        }
        .lightbox.active img { transform: scale(1); }
        .lightbox-close {
            position: absolute;
            top: 2rem; right: 2rem;
            width: 40px; height: 40px;
            border: 1px solid var(--or);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            color: var(--blanc);
            font-size: 1.2rem;
            transition: all 0.3s ease;
            background: transparent;
        }
        .lightbox-close:hover {
            background: var(--or);
            color: var(--noir);
            transform: rotate(90deg);
        }
        
        /* Responsive */
        @media (max-width: 1200px) {
            .chapter-4 .muse-grid { grid-template-columns: repeat(4, 1fr); }
        }
        @media (max-width: 968px) {
            .chapter-2 .gallery-reveal { grid-template-columns: repeat(2, 1fr); }
            .chapter-3 .veil-gallery { grid-template-columns: 1fr; max-width: 400px; }
            .chapter-4 .muse-grid { grid-template-columns: repeat(3, 1fr); }
            .chapter-1 .chapter-image { width: 60%; }
            .nav { padding: 1rem; }
            .nav-menu { display: none; }
        }
        @media (max-width: 640px) {
            .chapter { padding: 2rem 1rem; }
            .chapter-2 .gallery-reveal { grid-template-columns: 1fr; max-width: 300px; }
            .chapter-4 .muse-grid { grid-template-columns: repeat(2, 1fr); }
            .muse-item:nth-child(6n+1) { grid-column: span 1; grid-row: span 1; }
            .muse-item:nth-child(9n+3) { grid-column: span 1; }
            .chapter-1 .chapter-image { width: 80%; }
        }
        
        /* Hide cursor on touch */
        @media (pointer: coarse) {
            body { cursor: auto; }
            .cursor, .cursor-dot { display: none; }
        }
    </style>
</head>
<body>
    <!-- Grain overlay -->
    <div class="grain"></div>
    
    <!-- Custom cursor -->
    <div class="cursor"></div>
    <div class="cursor-dot"></div>
    
    <!-- Loader -->
    <div class="loader">
        <div class="loader-text">Bryan Photographie</div>
        <div class="loader-line"></div>
    </div>
    
    <!-- Navigation -->
    <nav class="nav" id="nav">
        <div class="nav-logo">Bryan Photographie</div>
        <div class="nav-menu">
            <span onclick="scrollToChapter(1)">L'Ombre</span>
            <span onclick="scrollToChapter(2)">L'Élégance</span>
            <span onclick="scrollToChapter(3)">L'Intimité</span>
            <span onclick="scrollToChapter(4)">La Muse</span>
        </div>
    </nav>
    
    <!-- Chapitre 1: L'Ombre et la Lumière -->
    <section class="chapter chapter-1" id="chapter-1">
        <img src="https://i.ibb.co/qLspGz3T/152192-B4-B01-E-4554-AD20-A39-B12823170.jpg" alt="Samia" class="chapter-image" id="ch1-img" onclick="openLightbox(this.src)">
        <div class="chapter-content">
            <div class="chapter-number">Chapitre I</div>
            <h1 class="chapter-title font-serif">L'Ombre et<br>la Lumière</h1>
            <p class="chapter-quote font-serif">Le regard du photographe capture ce que l'âme refuse d'oublier.</p>
        </div>
    </section>
    
    <!-- Chapitre 2: L'Élégance (6 photos) -->
    <section class="chapter chapter-2" id="chapter-2">
        <div class="chapter-content" style="text-align: center;">
            <div class="chapter-number">Chapitre II</div>
            <h2 class="chapter-title font-serif">L'Élégance</h2>
            <p class="chapter-quote font-serif" style="max-width: 500px; margin: 0 auto;">La beauté n'est pas dans le visage, mais dans la lumière qui l'habite.</p>
        </div>
        <div class="gallery-reveal">
            <div class="reveal-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/93TPZtZ3/5972057-E-854-B-402-F-BEC5-E799-B4493646.jpg" alt="Samia">
            </div>
            <div class="reveal-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/zWZS88x9/6606-BE3-C-7-A6-C-47-A0-B1-E1-1-A2785372-AA4.jpg" alt="Samia">
            </div>
            <div class="reveal-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/609gKDk8/F183-D34-C-B805-40-C4-A708-A64-E1-F4-D59-AD.jpg" alt="Samia">
            </div>
            <div class="reveal-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/JFHNML10/316-E4805-BC17-496-B-BDC5-06187-F8-FFED3.jpg" alt="Samia">
            </div>
            <div class="reveal-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/XZ5tZhBm/375-AE8-CF-60-A5-4-DD0-951-D-3102-C73-C3911.jpg" alt="Samia">
            </div>
            <div class="reveal-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/1JPn1QHF/3071-F064-2480-42-CF-8-D7-B-8-AF1098-EF14-F.jpg" alt="Samia">
            </div>
        </div>
    </section>
    
    <!-- Chapitre 3: L'Intimité (4 photos) -->
    <section class="chapter chapter-3" id="chapter-3">
        <div class="chapter-content" style="text-align: center;">
            <div class="chapter-number">Chapitre III</div>
            <h2 class="chapter-title font-serif">L'Intimité</h2>
            <p class="chapter-quote font-serif" style="max-width: 500px; margin: 0 auto;">La sensualité est l'art de suggérer sans montrer.</p>
        </div>
        <div class="veil-gallery">
            <div class="veil-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/vCk79CVT/C2-E64638-8-BF5-4030-9-CB8-E8-E09-D4-F60-E5.jpg" alt="Samia">
            </div>
            <div class="veil-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/TBhnMWx3/D256-D116-AAE9-4-CBD-85-E3-8-AD099-C1782-A.jpg" alt="Samia">
            </div>
            <div class="veil-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/Sw55HbYH/DSC01234.jpg" alt="Samia">
            </div>
            <div class="veil-item" onclick="openLightbox(this.querySelector('img').src)">
                <img src="https://i.ibb.co/wZN0mMVz/DSC02423.jpg" alt="Samia">
            </div>
        </div>
    </section>
    
    <!-- Chapitre 4: La Muse (50 photos) -->
    <section class="chapter chapter-4" id="chapter-4">
        <div class="chapter-content" style="text-align: center;">
            <div class="chapter-number">Chapitre IV</div>
            <h2 class="chapter-title font-serif">La Muse</h2>
            <p class="chapter-quote font-serif" style="max-width: 500px; margin: 0 auto;">Chaque muse porte en elle l'éternité d'un instant.</p>
        </div>
        <div class="muse-grid">
            <!-- Photos 1-10 -->
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/NdrRVqt5/DSC02423-1.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/N28zhTp2/DSC02435.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/G3PR2dK8/DSC02438.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/B5H6DSzw/DSC02823.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/Wq3Wyy5/DSC03426.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/KpByM1QZ/IMG-0093.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/tTqkvwQL/IMG-0095-1.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/DDLGhhcy/IMG-0098.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/4nwbMF6H/IMG-0105.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/Gv0L2fP8/IMG-0108.jpg" alt="Samia"></div>
            
            <!-- Photos 11-20 -->
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/fdgxbFHv/IMG-0115-1.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/5WqkG4fb/IMG-0377.png" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/219CdV9c/IMG-0378.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/gbBxyHZy/IMG-0834.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/9k9Ynk8V/IMG-1113.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/QF0MSmcC/IMG-1115.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/KpLKJsj7/IMG-1117.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/HfGpkS3w/IMG-1133.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/fYmjm1GC/IMG-1138.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/mVxx7150/IMG-1163.png" alt="Samia"></div>
            
            <!-- Photos 21-30 -->
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/qMVh3V6j/IMG-1196.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/N2gZK64v/IMG-1202.png" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/PGzsw3gZ/IMG-1210.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/TBKJq8cS/IMG-1236.png" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/R4sBhKHN/IMG-1296.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/YFXybwtQ/IMG-1408.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/9kCM9mYW/IMG-1416.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/KxXQ87BW/IMG-6789.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/fdVfwsxt/IMG-6795.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/23XFF4yc/IMG-6797.jpg" alt="Samia"></div>
            
            <!-- Photos 31-40 -->
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/wh4ct8m0/IMG-6799.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/chNZ7493/IMG-6811.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/RT9KBBBZ/IMG-6835.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/k25W7ZK9/IMG-6837.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/TfF9C3g/IMG-6842.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/3Y94hSnR/IMG-6850.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/m1qz3Cn/IMG-6852.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/sng11M9/IMG-6862.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/Cs9LPrXQ/IMG-6865.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/rGrLzgFg/IMG-6868.jpg" alt="Samia"></div>
            
            <!-- Photos 41-50 -->
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/1wkQfmZ/IMG-6897.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/1YR6dbrh/IMG-6901.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/6jZ2ZtG/IMG-6903.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/1Ymtx76K/IMG-6916.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/mF076B5Z/IMG-6918.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/0yJjJPFL/IMG-9435.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/6c0BDQPT/IMG-9438.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/bgnyxkDf/6-D90-CA19-4-A00-412-B-91-FF-AADCA573-ACEA.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/VWKKNgXx/Ajoute-un-lampadaire-avec-une-Nano-Banana-Pro-65879.jpg" alt="Samia"></div>
            <div class="muse-item" onclick="openLightbox(this.querySelector('img').src)"><img src="https://i.ibb.co/fYbbWkPY/Fait-moi-une-retouche-sans-tou-Nano-Banana-Pro-82932.jpg" alt="Samia"></div>
        </div>
    </section>
    
    <!-- Final -->
    <section class="final" id="final">
        <p class="final-text font-serif">
            <span class="line">L'art de capturer l'âme d'un instant,</span>
            <span class="line">la beauté d'un regard,</span>
            <span class="line">l'éternité d'une émotion.</span>
        </p>
        <div class="final-line"></div>
        <div class="final-signature">Bryan Photographie — Pour Samia, ma muse</div>
    </section>
    
    <!-- Lightbox -->
    <div class="lightbox" id="lightbox" onclick="closeLightbox(event)">
        <button class="lightbox-close" onclick="closeLightbox(event)">×</button>
        <img src="" alt="Samia" id="lightboxImage">
    </div>
    
    <script>
        // Register GSAP
        gsap.registerPlugin(ScrollTrigger);
        
        // Custom cursor
        const cursor = document.querySelector('.cursor');
        const cursorDot = document.querySelector('.cursor-dot');
        
        if (window.matchMedia('(pointer: fine)').matches) {
            document.addEventListener('mousemove', (e) => {
                cursor.style.left = e.clientX + 'px';
                cursor.style.top = e.clientY + 'px';
                cursorDot.style.left = e.clientX + 'px';
                cursorDot.style.top = e.clientY + 'px';
            });
            
            document.querySelectorAll('.reveal-item, .veil-item, .muse-item, .chapter-image').forEach(el => {
                el.addEventListener('mouseenter', () => cursor.classList.add('hover'));
                el.addEventListener('mouseleave', () => cursor.classList.remove('hover'));
            });
        }
        
        // Loader animation
        window.addEventListener('load', () => {
            const tl = gsap.timeline();
            
            tl.to('.loader-text', { opacity: 1, duration: 0.8 })
            .to('.loader-line', { width: '200px', duration: 1.2, ease: 'power2.inOut' }, '-=0.4')
            .to('.loader', { opacity: 0, duration: 0.8, ease: 'power2.inOut', 
                onComplete: () => {
                    document.querySelector('.loader').style.display = 'none';
                    initAnimations();
                }
            });
        });
        
        function initAnimations() {
            gsap.to('.nav', { opacity: 1, y: 0, duration: 0.8, delay: 0.3 });
            
            // Chapter 1
            gsap.to('#ch1-img', { opacity: 1, scale: 1, filter: 'brightness(0.6)', duration: 2, ease: 'power2.out' });
            gsap.to('#chapter-1 .chapter-number', { opacity: 1, duration: 0.8, delay: 0.5 });
            gsap.to('#chapter-1 .chapter-title', { opacity: 1, y: 0, duration: 1.2, delay: 0.7, ease: 'power3.out' });
            gsap.to('#chapter-1 .chapter-quote', { opacity: 1, duration: 1, delay: 1.2 });
            
            // Parallax ch1
            gsap.to('#ch1-img', {
                yPercent: 15,
                ease: 'none',
                scrollTrigger: { trigger: '#chapter-1', start: 'top top', end: 'bottom top', scrub: true }
            });
        }
        
        // Chapter 2
        gsap.utils.toArray('.reveal-item').forEach((item, i) => {
            ScrollTrigger.create({
                trigger: item,
                start: 'top 85%',
                onEnter: () => {
                    gsap.to(item, { opacity: 1, y: 0, duration: 0.8, delay: i * 0.1, ease: 'power3.out' });
                    setTimeout(() => item.classList.add('revealed'), 300);
                }
            });
        });
        
        gsap.to('#chapter-2 .chapter-number, #chapter-2 .chapter-title, #chapter-2 .chapter-quote', {
            opacity: 1, y: 0, duration: 1, stagger: 0.2,
            scrollTrigger: { trigger: '#chapter-2', start: 'top 70%' }
        });
        
        // Chapter 3
        gsap.utils.toArray('.veil-item').forEach((item, i) => {
            gsap.to(item, {
                opacity: 1, duration: 1, delay: i * 0.15,
                scrollTrigger: { trigger: item, start: 'top 85%' }
            });
        });
        
        gsap.to('#chapter-3 .chapter-number, #chapter-3 .chapter-title, #chapter-3 .chapter-quote', {
            opacity: 1, y: 0, duration: 1, stagger: 0.2,
            scrollTrigger: { trigger: '#chapter-3', start: 'top 70%' }
        });
        
        // Chapter 4 - 50 photos
        gsap.utils.toArray('.muse-item').forEach((item, i) => {
            gsap.to(item, {
                opacity: 1, scale: 1, duration: 0.6, delay: (i % 10) * 0.05,
                ease: 'back.out(1.4)',
                scrollTrigger: { trigger: item, start: 'top 90%' }
            });
        });
        
        gsap.to('#chapter-4 .chapter-number, #chapter-4 .chapter-title, #chapter-4 .chapter-quote', {
            opacity: 1, y: 0, duration: 1, stagger: 0.2,
            scrollTrigger: { trigger: '#chapter-4', start: 'top 70%' }
        });
        
        // Final
        gsap.to('.final-text .line', { opacity: 1, y: 0, duration: 0.8, stagger: 0.2,
            scrollTrigger: { trigger: '.final', start: 'top 70%' }
        });
        gsap.to('.final-line', { opacity: 1, duration: 0.6, delay: 0.6,
            scrollTrigger: { trigger: '.final', start: 'top 70%' }
        });
        gsap.to('.final-signature', { opacity: 1, duration: 0.8, delay: 0.8,
            scrollTrigger: { trigger: '.final', start: 'top 70%' }
        });
        
        // Navigation
        function scrollToChapter(n) {
            const chapter = document.getElementById(`chapter-${n}`);
            if (chapter) {
                gsap.to(window, { duration: 1.2, scrollTo: { y: chapter, offsetY: 0 }, ease: 'power3.inOut' });
            }
        }
        
        // Show/hide nav
        ScrollTrigger.create({
            trigger: '#chapter-2',
            start: 'top 80%',
            onEnter: () => document.getElementById('nav').classList.add('visible'),
            onLeaveBack: () => document.getElementById('nav').classList.remove('visible')
        });
        
        // Lightbox
        function openLightbox(src) {
            document.getElementById('lightboxImage').src = src;
            document.getElementById('lightbox').classList.add('active');
            document.body.style.overflow = 'hidden';
        }
        
        function closeLightbox(e) {
            if (e.target.id === 'lightbox' || e.target.classList.contains('lightbox-close')) {
                document.getElementById('lightbox').classList.remove('active');
                document.body.style.overflow = '';
            }
        }
        
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') closeLightbox({ target: { id: 'lightbox' } });
        });
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollToPlugin.min.js"></script>
</body>
</html>

