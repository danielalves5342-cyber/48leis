import zipfile
import os

# Código HTML atualizado com o vídeo
html_code = '''<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>As 48 Leis do Poder - Robert Greene | Manual Definitivo do Poder</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --gold: #D4AF37;
            --gold-light: #F4E4BC;
            --dark: #0a0a0a;
            --darker: #050505;
            --red-dark: #8B0000;
            --text: #e0e0e0;
            --text-muted: #888;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--darker);
            color: var(--text);
            line-height: 1.6;
            overflow-x: hidden;
        }

        .bg-pattern {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                radial-gradient(circle at 20% 50%, rgba(212, 175, 55, 0.03) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(139, 0, 0, 0.03) 0%, transparent 50%);
            pointer-events: none;
            z-index: 0;
        }

        header {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 20px 5%;
            background: rgba(5, 5, 5, 0.95);
            backdrop-filter: blur(10px);
            z-index: 1000;
            border-bottom: 1px solid rgba(212, 175, 55, 0.1);
            transition: all 0.3s ease;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1400px;
            margin: 0 auto;
        }

        .logo {
            font-family: 'Cinzel', serif;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--gold);
            text-decoration: none;
            letter-spacing: 2px;
        }

        .nav-cta {
            background: linear-gradient(135deg, var(--gold) 0%, #B8941F 100%);
            color: var(--dark);
            padding: 12px 28px;
            border-radius: 30px;
            text-decoration: none;
            font-weight: 600;
            font-size: 0.9rem;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
        }

        .nav-cta:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.4);
        }

        /* Hero Section com Vídeo */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 120px 5% 80px;
            position: relative;
            overflow: hidden;
        }

        .video-background {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            overflow: hidden;
        }

        .video-background video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.4;
        }

        .video-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, rgba(5,5,5,0.7) 0%, rgba(5,5,5,0.9) 100%);
            z-index: 1;
        }

        .hero-container {
            max-width: 1400px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 60px;
            align-items: center;
            position: relative;
            z-index: 2;
        }

        .hero-content h1 {
            font-family: 'Cinzel', serif;
            font-size: 3.5rem;
            font-weight: 700;
            line-height: 1.2;
            margin-bottom: 20px;
            background: linear-gradient(135deg, var(--gold-light) 0%, var(--gold) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero-content .subtitle {
            font-size: 1.3rem;
            color: var(--text-muted);
            margin-bottom: 30px;
            font-weight: 300;
        }

        .hero-content .description {
            font-size: 1.1rem;
            color: var(--text);
            margin-bottom: 40px;
            line-height: 1.8;
        }

        .highlight {
            color: var(--gold);
            font-weight: 600;
        }

        .book-showcase {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .book-container {
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.5s ease;
        }

        .book-container:hover {
            transform: rotateY(-5deg) rotateX(5deg);
        }

        .book-cover {
            width: 320px;
            height: 480px;
            object-fit: cover;
            border-radius: 8px;
            box-shadow: 
                0 20px 60px rgba(0,0,0,0.8),
                0 0 0 1px rgba(212, 175, 55, 0.2);
            position: relative;
            z-index: 2;
        }

        .book-shadow {
            position: absolute;
            bottom: -30px;
            left: 50%;
            transform: translateX(-50%);
            width: 280px;
            height: 40px;
            background: radial-gradient(ellipse, rgba(0,0,0,0.6) 0%, transparent 70%);
            filter: blur(10px);
        }

        .floating-badge {
            position: absolute;
            top: -20px;
            right: -20px;
            background: linear-gradient(135deg, var(--red-dark) 0%, #600000 100%);
            color: white;
            padding: 15px 25px;
            border-radius: 50%;
            font-weight: 700;
            font-size: 0.9rem;
            box-shadow: 0 10px 30px rgba(139, 0, 0, 0.4);
            animation: float 3s ease-in-out infinite;
            z-index: 3;
            border: 2px solid rgba(255,255,255,0.1);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .cta-button {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            background: linear-gradient(135deg, #00C851 0%, #007E33 100%);
            color: white;
            padding: 20px 50px;
            border-radius: 50px;
            text-decoration: none;
            font-size: 1.2rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(0, 200, 81, 0.3);
            position: relative;
            overflow: hidden;
            border: none;
            cursor: pointer;
        }

        .cta-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }

        .cta-button:hover::before {
            left: 100%;
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(0, 200, 81, 0.4);
        }

        .cta-button.pulse {
            animation: pulse-green 2s infinite;
        }

        @keyframes pulse-green {
            0% { box-shadow: 0 0 0 0 rgba(0, 200, 81, 0.4); }
            70% { box-shadow: 0 0 0 20px rgba(0, 200, 81, 0); }
            100% { box-shadow: 0 0 0 0 rgba(0, 200, 81, 0); }
        }

        .price-tag {
            margin-top: 20px;
            font-size: 1.1rem;
            color: var(--text-muted);
        }

        .price {
            font-size: 2.5rem;
            color: var(--gold);
            font-weight: 700;
            display: block;
            margin-top: 5px;
        }

        .price span {
            font-size: 1rem;
            color: var(--text-muted);
            text-decoration: line-through;
            margin-left: 10px;
        }

        /* Seção do Vídeo Destaque */
        .video-section {
            padding: 100px 5%;
            background: linear-gradient(to bottom, var(--dark), var(--darker));
            position: relative;
            overflow: hidden;
        }

        .video-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 50% 50%, rgba(212, 175, 55, 0.05) 0%, transparent 70%);
        }

        .video-container {
            max-width: 800px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
        }

        .video-wrapper {
            position: relative;
            padding-bottom: 177.78%; /* Proporção 9:16 para vídeo vertical */
            height: 0;
            overflow: hidden;
            border-radius: 20px;
            box-shadow: 0 30px 60px rgba(0,0,0,0.8);
            border: 2px solid rgba(212, 175, 55, 0.2);
        }

        .video-wrapper video {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .video-caption {
            text-align: center;
            margin-top: 30px;
            font-family: 'Cinzel', serif;
            font-size: 1.5rem;
            color: var(--gold-light);
        }

        .video-subcaption {
            text-align: center;
            margin-top: 10px;
            color: var(--text-muted);
            font-size: 1rem;
        }

        .features {
            padding: 100px 5%;
            background: linear-gradient(to bottom, var(--darker), var(--dark));
            position: relative;
        }

        .section-title {
            text-align: center;
            font-family: 'Cinzel', serif;
            font-size: 2.5rem;
            color: var(--gold-light);
            margin-bottom: 60px;
            position: relative;
        }

        .section-title::after {
            content: '';
            display: block;
            width: 100px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
            margin: 20px auto 0;
        }

        .features-grid {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(212, 175, 55, 0.1);
            border-radius: 15px;
            padding: 40px 30px;
            text-align: center;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .feature-card:hover::before {
            transform: scaleX(1);
        }

        .feature-card:hover {
            transform: translateY(-10px);
            border-color: rgba(212, 175, 55, 0.3);
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
        }

        .feature-icon {
            font-size: 3rem;
            margin-bottom: 20px;
            display: block;
        }

        .feature-card h3 {
            font-family: 'Cinzel', serif;
            font-size: 1.3rem;
            color: var(--gold);
            margin-bottom: 15px;
        }

        .feature-card p {
            color: var(--text-muted);
            line-height: 1.6;
        }

        .social-proof {
            padding: 100px 5%;
            background: var(--dark);
            position: relative;
        }

        .testimonials {
            max-width: 1000px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .testimonial {
            background: rgba(255, 255, 255, 0.02);
            border-left: 3px solid var(--gold);
            padding: 30px;
            border-radius: 0 10px 10px 0;
            position: relative;
        }

        .testimonial::before {
            content: '"';
            font-family: 'Cinzel', serif;
            font-size: 4rem;
            color: var(--gold);
            opacity: 0.3;
            position: absolute;
            top: -10px;
            left: 20px;
        }

        .testimonial-text {
            font-style: italic;
            margin-bottom: 20px;
            color: var(--text);
            line-height: 1.8;
            position: relative;
            z-index: 1;
        }

        .testimonial-author {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .author-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--gold), var(--red-dark));
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            color: white;
        }

        .author-info h4 {
            color: var(--gold-light);
            font-size: 1rem;
        }

        .author-info p {
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .stars {
            color: var(--gold);
            margin-bottom: 10px;
            font-size: 1.2rem;
        }

        .urgency {
            padding: 80px 5%;
            background: linear-gradient(135deg, rgba(139, 0, 0, 0.1) 0%, rgba(212, 175, 55, 0.05) 100%);
            text-align: center;
            border-top: 1px solid rgba(212, 175, 55, 0.1);
            border-bottom: 1px solid rgba(212, 175, 55, 0.1);
        }

        .urgency-content {
            max-width: 800px;
            margin: 0 auto;
        }

        .urgency h2 {
            font-family: 'Cinzel', serif;
            font-size: 2rem;
            color: var(--gold-light);
            margin-bottom: 20px;
        }

        .countdown {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 40px 0;
            flex-wrap: wrap;
        }

        .time-unit {
            background: rgba(0,0,0,0.5);
            border: 1px solid rgba(212, 175, 55, 0.3);
            border-radius: 10px;
            padding: 20px;
            min-width: 80px;
        }

        .time-value {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--gold);
            display: block;
            line-height: 1;
        }

        .time-label {
            font-size: 0.9rem;
            color: var(--text-muted);
            text-transform: uppercase;
            margin-top: 5px;
        }

        .stock-warning {
            background: rgba(139, 0, 0, 0.2);
            border: 1px solid var(--red-dark);
            color: #ff6b6b;
            padding: 15px 30px;
            border-radius: 30px;
            display: inline-block;
            margin-top: 20px;
            font-weight: 600;
            animation: blink 2s infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .faq {
            padding: 100px 5%;
            max-width: 800px;
            margin: 0 auto;
        }

        .faq-item {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid rgba(212, 175, 55, 0.1);
            border-radius: 10px;
            margin-bottom: 20px;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .faq-item:hover {
            border-color: rgba(212, 175, 55, 0.3);
        }

        .faq-question {
            padding: 25px 30px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: 600;
            color: var(--gold-light);
            transition: all 0.3s ease;
        }

        .faq-question:hover {
            background: rgba(212, 175, 55, 0.05);
        }

        .faq-icon {
            font-size: 1.5rem;
            transition: transform 0.3s ease;
        }

        .faq-item.active .faq-icon {
            transform: rotate(45deg);
        }

        .faq-answer {
            padding: 0 30px;
            max-height: 0;
            overflow: hidden;
            transition: all 0.3s ease;
            color: var(--text-muted);
            line-height: 1.8;
        }

        .faq-item.active .faq-answer {
            padding: 0 30px 25px;
            max-height: 200px;
        }

        .final-cta {
            padding: 100px 5%;
            text-align: center;
            background: radial-gradient(ellipse at center, rgba(212, 175, 55, 0.05) 0%, transparent 70%);
            position: relative;
        }

        .final-cta h2 {
            font-family: 'Cinzel', serif;
            font-size: 2.5rem;
            color: var(--gold-light);
            margin-bottom: 20px;
        }

        .final-cta p {
            color: var(--text-muted);
            font-size: 1.2rem;
            margin-bottom: 40px;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        .guarantee {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            margin-top: 40px;
            padding: 30px;
            background: rgba(0, 200, 81, 0.05);
            border: 1px solid rgba(0, 200, 81, 0.2);
            border-radius: 15px;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        .guarantee-icon {
            font-size: 3rem;
        }

        .guarantee-text h4 {
            color: #00C851;
            margin-bottom: 5px;
        }

        .guarantee-text p {
            color: var(--text-muted);
            font-size: 0.95rem;
            margin: 0;
        }

        footer {
            background: var(--darker);
            padding: 60px 5% 30px;
            border-top: 1px solid rgba(212, 175, 55, 0.1);
            text-align: center;
        }

        .footer-content {
            max-width: 1200px;
            margin: 0 auto;
        }

        .footer-logo {
            font-family: 'Cinzel', serif;
            font-size: 2rem;
            color: var(--gold);
            margin-bottom: 20px;
            display: inline-block;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .footer-links a {
            color: var(--text-muted);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-links a:hover {
            color: var(--gold);
        }

        .copyright {
            color: var(--text-muted);
            font-size: 0.9rem;
            padding-top: 30px;
            border-top: 1px solid rgba(255,255,255,0.05);
        }

        @media (max-width: 968px) {
            .hero-container {
                grid-template-columns: 1fr;
                text-align: center;
            }

            .hero-content h1 {
                font-size: 2.5rem;
            }

            .book-cover {
                width: 260px;
                height: 390px;
            }

            .features-grid {
                grid-template-columns: 1fr;
            }

            .countdown {
                gap: 15px;
            }

            .time-unit {
                padding: 15px;
                min-width: 70px;
            }

            .time-value {
                font-size: 2rem;
            }

            .video-wrapper {
                padding-bottom: 177.78%; /* Mantém proporção vertical no mobile */
            }
        }

        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: var(--gold);
            border-radius: 50%;
            opacity: 0.3;
            animation: float-particle 10s infinite linear;
        }

        @keyframes float-particle {
            0% { transform: translateY(100vh) translateX(0); opacity: 0; }
            10% { opacity: 0.3; }
            90% { opacity: 0.3; }
            100% { transform: translateY(-100vh) translateX(100px); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="bg-pattern"></div>
    <div class="particles" id="particles"></div>

    <header>
        <nav>
            <a href="#" class="logo">48 LEIS</a>
            <a href="https://pay.cakto.com.br/7jcf5gr_764139" class="nav-cta">Comprar Agora</a>
        </nav>
    </header>

    <!-- Hero Section com Vídeo de Fundo -->
    <section class="hero">
        <div class="video-background">
            <video autoplay muted loop playsinline>
                <source src="https://kimi-web-img.moonshot.cn/img/1000049878.mp4" type="video/mp4">
            </video>
            <div class="video-overlay"></div>
        </div>

        <div class="hero-container">
            <div class="hero-content fade-in">
                <h1>As 48 Leis do Poder</h1>
                <p class="subtitle">O Manual Definitivo para Quem Quer Entender o Jogo do Poder</p>
                <p class="description">
                    Descubra as <span class="highlight">estratégias milenares</span> usadas pelos maiores líderes da história. 
                    De Maquiavel a Sun Tzu, Robert Greene compilou <span class="highlight">48 leis fundamentais</span> 
                    para você navegar no mundo complexo das relações de poder, influência e liderança.
                </p>
                
                <a href="https://pay.cakto.com.br/7jcf5gr_764139" class="cta-button pulse">
                    <span>Quero o Livro Agora</span>
                    <span>→</span>
                </a>
                
                <div class="price-tag">
                    Oferta Especial de Lançamento
                    <span class="price">R$ 47,90 <span>R$ 97,00</span></span>
                </div>
            </div>

            <div class="book-showcase fade-in">
                <div class="book-container">
                    <div class="floating-badge">-50% OFF</div>
                    <img src="https://kimi-web-img.moonshot.cn/img/rocco.com.br/f3243ee02bc2982605ce897fd3638dfc89bb8d9d.png" alt="As 48 Leis do Poder - Capa do Livro" class="book-cover">
                    <div class="book-shadow"></div>
                </div>
            </div>
        </div>
    </section>

    <!-- Seção do Vídeo em Destaque -->
    <section class="video-section">
        <h2 class="section-title fade-in">A Verdade sobre o Poder</h2>
        <div class="video-container fade-in">
            <div class="video-wrapper">
                <video controls poster="https://kimi-web-img.moonshot.cn/img/1000049878.mp4">
                    <source src="https://kimi-web-img.moonshot.cn/img/1000049878.mp4" type="video/mp4">
                    Seu navegador não suporta vídeos.
                </video>
            </div>
            <p class="video-caption">"O mundo é um lugar perigoso para os ingênuos"</p>
            <p class="video-subcaption">Assista e descubra por que você precisa conhecer as 48 Leis do Poder</p>
        </div>
    </section>

    <section class="features">
        <h2 class="section-title fade-in">O Que Você Vai Descobrir</h2>
        
        <div class="features-grid">
            <div class="feature-card fade-in">
                <span class="feature-icon">👑</span>
                <h3>Lei 1: Não Ofusque o Mestre</h3>
                <p>Aprenda a fazer com que seus superiores se sintam superiores, garantindo sua posição sem ameaçar quem está acima.</p>
            </div>

            <div class="feature-card fade-in">
                <span class="feature-icon">🎭</span>
                <h3>Lei 3: Oculte suas Intenções</h3>
                <p>Mantenha as pessoas fora de equilíbrio. Ninguém pode se preparar para o que não conhece. A arte da dissimulação.</p>
            </div>

            <div class="feature-card fade-in">
                <span class="feature-icon">⚔️</span>
                <h3>Lei 15: Aniquile o Inimigo</h3>
                <p>Quando estiver em vantagem, não pare no meio do caminho. Esmague totalmente seus adversários.</p>
            </div>

            <div class="feature-card fade-in">
                <span class="feature-icon">🌟</span>
                <h3>Lei 6: Chame Atenção</h3>
                <p>Todas as pessoas são julgadas pela aparência. O que é invisível não serve para nada. Destaque-se a qualquer custo.</p>
            </div>

            <div class="feature-card fade-in">
                <span class="feature-icon">🤝</span>
                <h3>Lei 12: Use a Honestidade Seletiva</h3>
                <p>Um único ato sincero é capaz de cobrir dúzias de desonestidades. A arte de desarmar suas vítimas.</p>
            </div>

            <div class="feature-card fade-in">
                <span class="feature-icon">🎯</span>
                <h3>Lei 29: Planeje até o Fim</h3>
                <p>O resultado é tudo o que importa. Leve em consideração o contexto geral e pense muito à frente dos demais.</p>
            </div>
        </div>
    </section>

    <section class="social-proof">
        <h2 class="section-title fade-in">O Que os Leitores Dizem</h2>
        
        <div class="testimonials">
            <div class="testimonial fade-in">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">
                    "Simplesmente magnífico! Comecei a me encantar nos primeiros 15 minutos de leitura. 
                    Mudou completamente minha visão sobre dinâmicas de poder no trabalho."
                </p>
                <div class="testimonial-author">
                    <div class="author-avatar">PC</div>
                    <div class="author-info">
                        <h4>Pedro Correia</h4>
                        <p>Empresário, São Paulo</p>
                    </div>
                </div>
            </div>

            <div class="testimonial fade-in">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">
                    "Leitura fácil, com exemplos históricos que ajudam a entender cada lei. 
                    Essencial para quem trabalha em ambientes corporativos competitivos."
                </p>
                <div class="testimonial-author">
                    <div class="author-avatar">MK</div>
                    <div class="author-info">
                        <h4>Marina K.</h4>
                        <p>Executiva de RH, Rio de Janeiro</p>
                    </div>
                </div>
            </div>

            <div class="testimonial fade-in">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">
                    "Vale a pena, especialmente para a vida profissional. 
                    As 48 leis me ajudaram a identificar manipulações e me proteger de jogos de poder."
                </p>
                <div class="testimonial-author">
                    <div class="author-avatar">RL</div>
                    <div class="author-info">
                        <h4>Ricardo Lima</h4>
                        <p>Advogado, Brasília</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="urgency">
        <div class="urgency-content fade-in">
            <h2>⚡ Oferta por Tempo Limitado</h2>
            <p>Esta promoção encerra em breve. Garanta seu exemplar agora!</p>
            
            <div class="countdown" id="countdown">
                <div class="time-unit">
                    <span class="time-value" id="hours">04</span>
                    <span class="time-label">Horas</span>
                </div>
                <div class="time-unit">
                    <span class="time-value" id="minutes">32</span>
                    <span class="time-label">Minutos</span>
                </div>
                <div class="time-unit">
                    <span class="time-value" id="seconds">15</span>
                    <span class="time-label">Segundos</span>
                </div>
            </div>

            <div class="stock-warning">
                🔥 Apenas 17 exemplares restantes neste valor!
            </div>

            <div style="margin-top: 40px;">
                <a href="https://pay.cakto.com.br/7jcf5gr_764139" class="cta-button pulse">
                    Garantir Meu Livro Agora →
                </a>
            </div>
        </div>
    </section>

    <section class="faq">
        <h2 class="section-title fade-in">Perguntas Frequentes</h2>
        
        <div class="faq-item fade-in">
            <div class="faq-question" onclick="toggleFaq(this)">
                <span>O livro é físico ou digital?</span>
                <span class="faq-icon">+</span>
            </div>
            <div class="faq-answer">
                Você receberá a versão digital (PDF + ePub) imediatamente após a confirmação do pagamento, 
                podendo começar a ler em minutos. A versão física pode ser adquirida separadamente.
            </div>
        </div>

        <div class="faq-item fade-in">
            <div class="faq-question" onclick="toggleFaq(this)">
                <span>Como recebo o material?</span>
                <span class="faq-icon">+</span>
            </div>
            <div class="faq-answer">
                Após a compra, você receberá um e-mail com o link para download imediato. 
                O acesso é vitalício e você pode baixar quantas vezes quiser.
            </div>
        </div>

        <div class="faq-item fade-in">
            <div class="faq-question" onclick="toggleFaq(this)">
                <span>Tem garantia de satisfação?</span>
                <span class="faq-icon">+</span>
            </div>
            <div class="faq-answer">
                Sim! Você tem 7 dias de garantia incondicional. Se não gostar do conteúdo, 
                devolvemos 100% do seu dinheiro, sem perguntas.
            </div>
        </div>

        <div class="faq-item fade-in">
            <div class="faq-question" onclick="toggleFaq(this)">
                <span>Posso ler no Kindle?</span>
                <span class="faq-icon">+</span>
            </div>
            <div class="faq-answer">
                Sim! O arquivo ePub é compatível com Kindle, além de todos os outros 
                dispositivos de leitura digital (tablet, celular, computador).
            </div>
        </div>
    </section>

    <section class="final-cta">
        <div class="fade-in">
            <h2>Domine o Jogo do Poder</h2>
            <p>
                Milhares de pessoas já transformaram suas vidas com essas estratégias milenares. 
                Agora é sua vez de entender as regras do jogo.
            </p>
            
            <a href="https://pay.cakto.com.br/7jcf5gr_764139" class="cta-button pulse" style="font-size: 1.4rem; padding: 25px 60px;">
                Quero Acessar Agora →
            </a>

            <div class="guarantee">
                <span class="guarantee-icon">🛡️</span>
                <div class="guarantee-text">
                    <h4>Garantia de 7 Dias</h4>
                    <p>Risco zero para você. Satisfação garantida ou seu dinheiro de volta.</p>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <div class="footer-content">
            <div class="footer-logo">48 LEIS DO PODER</div>
            <div class="footer-links">
                <a href="#">Termos de Uso</a>
                <a href="#">Política de Privacidade</a>
                <a href="#">Contato</a>
                <a href="https://pay.cakto.com.br/7jcf5gr_764139">Comprar</a>
            </div>
            <div class="copyright">
                <p>© 2024 - As 48 Leis do Poder. Todos os direitos reservados.</p>
                <p style="margin-top: 10px; font-size: 0.8rem;">Este site não é afiliado à Editora Rocco. O livro é de autoria de Robert Greene.</p>
            </div>
        </div>
    </footer>

    <script>
        function updateCountdown() {
            const now = new Date();
            const endOfDay = new Date();
            endOfDay.setHours(23, 59, 59, 999);
            
            const diff = endOfDay - now;
            
            const hours = Math.floor(diff / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((diff % (1000 * 60)) / 1000);
            
            document.getElementById('hours').textContent = hours.toString().padStart(2, '0');
            document.getElementById('minutes').textContent = minutes.toString().padStart(2, '0');
            document.getElementById('seconds').textContent = seconds.toString().padStart(2, '0');
        }

        setInterval(updateCountdown, 1000);
        updateCountdown();

        function toggleFaq(element) {
            const item = element.parentElement;
            const isActive = item.classList.contains('active');
            
            document.querySelectorAll('.faq-item').forEach(faq => {
                faq.classList.remove('active');
            });
            
            if (!isActive) {
                item.classList.add('active');
            }
        }

        const observerOptions = {
            threshold: 0.1,
            rootMargin: "0px 0px -50px 0px"
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));

        function createParticles() {
            const container = document.getElementById('particles');
            const particleCount = 30;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 10 + 's';
                particle.style.animationDuration = (Math.random() * 10 + 10) + 's';
                container.appendChild(particle);
            }
        }

        createParticles();

        window.addEventListener('scroll', () => {
            const header = document.querySelector('header');
            if (window.scrollY > 100) {
                header.style.background = 'rgba(5, 5, 5, 0.98)';
                header.style.boxShadow = '0 5px 30px rgba(0,0,0,0.5)';
            } else {
                header.style.background = 'rgba(5, 5, 5, 0.95)';
                header.style.boxShadow = 'none';
            }
        });

        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                }
            });
        });
    </script>
</body>
</html>'''

# Criar pasta temporária e salvar index.html na raiz
temp_dir = '/mnt/kimi/output/temp_site_video'
os.makedirs(temp_dir, exist_ok=True)

# Salvar o arquivo index.html
with open(os.path.join(temp_dir, 'index.html'), 'w', encoding='utf-8') as f:
    f.write(html_code)

# Criar ZIP com o arquivo na raiz
zip_path = '/mnt/kimi/output/site-48-leis-com-video.zip'
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zipf:
    zipf.write(os.path.join(temp_dir, 'index.html'), 'index.html')

print("✅ Site atualizado com vídeo!")
print(f"📦 Arquivo: {zip_path}")
print("\n🎬 O vídeo foi adicionado em 2 lugares:")
print("   1. Background da Hero Section (efeito dramático)")
print("   2. Seção dedicada 'A Verdade sobre o Poder'")
