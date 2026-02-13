import zipfile
import os

# Código HTML completo e otimizado
html_code = '''<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>As 48 Leis do Poder - Robert Greene</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #050505;
            color: #fff;
            line-height: 1.6;
        }

        /* Header */
        header {
            background: rgba(0,0,0,0.95);
            padding: 15px 20px;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 2px solid #D4AF37;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            color: #D4AF37;
            font-size: 1.5rem;
            font-weight: bold;
            text-decoration: none;
        }

        .nav-cta {
            background: #D4AF37;
            color: #000;
            padding: 10px 20px;
            border-radius: 25px;
            text-decoration: none;
            font-weight: bold;
            font-size: 0.9rem;
        }

        /* Hero Section */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 100px 20px 50px;
            background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 100%);
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -20%;
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(212,175,55,0.1) 0%, transparent 70%);
            animation: pulse 4s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; }
        }

        .hero-container {
            max-width: 1200px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 50px;
            align-items: center;
            position: relative;
            z-index: 1;
        }

        .hero-content h1 {
            font-size: 3rem;
            color: #D4AF37;
            margin-bottom: 20px;
            line-height: 1.2;
        }

        .hero-content .subtitle {
            font-size: 1.2rem;
            color: #aaa;
            margin-bottom: 20px;
        }

        .hero-content .description {
            font-size: 1rem;
            color: #ddd;
            margin-bottom: 30px;
        }

        .highlight {
            color: #D4AF37;
            font-weight: bold;
        }

        .cta-button {
            display: inline-block;
            background: linear-gradient(135deg, #00C851 0%, #007E33 100%);
            color: white;
            padding: 18px 40px;
            border-radius: 50px;
            text-decoration: none;
            font-size: 1.1rem;
            font-weight: bold;
            text-transform: uppercase;
            box-shadow: 0 10px 30px rgba(0,200,81,0.3);
            animation: pulse-green 2s infinite;
            margin-bottom: 20px;
        }

        @keyframes pulse-green {
            0% { box-shadow: 0 0 0 0 rgba(0,200,81,0.4); }
            70% { box-shadow: 0 0 0 15px rgba(0,200,81,0); }
            100% { box-shadow: 0 0 0 0 rgba(0,200,81,0); }
        }

        .price-tag {
            font-size: 1rem;
            color: #aaa;
        }

        .price {
            font-size: 2.2rem;
            color: #D4AF37;
            font-weight: bold;
        }

        .price span {
            font-size: 1rem;
            color: #666;
            text-decoration: line-through;
            margin-left: 10px;
        }

        /* Book Showcase */
        .book-showcase {
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .book-container {
            position: relative;
        }

        .book-cover {
            width: 280px;
            height: 420px;
            border-radius: 10px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.8);
            border: 2px solid rgba(212,175,55,0.3);
        }

        .floating-badge {
            position: absolute;
            top: -15px;
            right: -15px;
            background: #8B0000;
            color: white;
            padding: 12px 20px;
            border-radius: 50%;
            font-weight: bold;
            font-size: 0.9rem;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        /* Features */
        .features {
            padding: 80px 20px;
            background: #0a0a0a;
        }

        .section-title {
            text-align: center;
            font-size: 2.2rem;
            color: #D4AF37;
            margin-bottom: 50px;
        }

        .features-grid {
            max-width: 1000px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }

        .feature-card {
            background: #111;
            border: 1px solid #333;
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-10px);
            border-color: #D4AF37;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
        }

        .feature-icon {
            font-size: 2.5rem;
            margin-bottom: 15px;
        }

        .feature-card h3 {
            color: #D4AF37;
            margin-bottom: 10px;
            font-size: 1.2rem;
        }

        .feature-card p {
            color: #aaa;
            font-size: 0.95rem;
        }

        /* Testimonials */
        .testimonials {
            padding: 80px 20px;
            background: #050505;
        }

        .testimonials-grid {
            max-width: 1000px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .testimonial {
            background: #111;
            border-left: 3px solid #D4AF37;
            padding: 25px;
            border-radius: 0 10px 10px 0;
        }

        .stars {
            color: #D4AF37;
            margin-bottom: 10px;
        }

        .testimonial-text {
            color: #ddd;
            font-style: italic;
            margin-bottom: 15px;
        }

        .testimonial-author {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .author-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, #D4AF37, #8B0000);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .author-info h4 {
            color: #D4AF37;
            font-size: 0.95rem;
        }

        .author-info p {
            color: #666;
            font-size: 0.85rem;
        }

        /* Urgency */
        .urgency {
            padding: 60px 20px;
            background: linear-gradient(135deg, rgba(139,0,0,0.1) 0%, rgba(212,175,55,0.05) 100%);
            text-align: center;
        }

        .urgency h2 {
            color: #D4AF37;
            font-size: 1.8rem;
            margin-bottom: 20px;
        }

        .countdown {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
            flex-wrap: wrap;
        }

        .time-unit {
            background: #111;
            border: 1px solid #333;
            border-radius: 10px;
            padding: 15px;
            min-width: 70px;
        }

        .time-value {
            font-size: 2rem;
            font-weight: bold;
            color: #D4AF37;
        }

        .time-label {
            font-size: 0.8rem;
            color: #666;
            text-transform: uppercase;
        }

        .stock-warning {
            background: rgba(139,0,0,0.2);
            border: 1px solid #8B0000;
            color: #ff6b6b;
            padding: 12px 25px;
            border-radius: 25px;
            display: inline-block;
            margin: 20px 0;
            font-weight: bold;
            animation: blink 2s infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        /* FAQ */
        .faq {
            padding: 80px 20px;
            max-width: 800px;
            margin: 0 auto;
        }

        .faq-item {
            background: #111;
            border: 1px solid #333;
            border-radius: 10px;
            margin-bottom: 15px;
            overflow: hidden;
        }

        .faq-question {
            padding: 20px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: bold;
            color: #D4AF37;
        }

        .faq-answer {
            padding: 0 20px;
            max-height: 0;
            overflow: hidden;
            transition: all 0.3s ease;
            color: #aaa;
        }

        .faq-item.active .faq-answer {
            padding: 0 20px 20px;
            max-height: 200px;
        }

        /* Final CTA */
        .final-cta {
            padding: 80px 20px;
            text-align: center;
            background: radial-gradient(ellipse at center, rgba(212,175,55,0.05) 0%, transparent 70%);
        }

        .final-cta h2 {
            color: #D4AF37;
            font-size: 2rem;
            margin-bottom: 20px;
        }

        .final-cta p {
            color: #aaa;
            margin-bottom: 30px;
        }

        .guarantee {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
            padding: 20px;
            background: rgba(0,200,81,0.05);
            border: 1px solid rgba(0,200,81,0.2);
            border-radius: 10px;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
        }

        .guarantee-text h4 {
            color: #00C851;
        }

        .guarantee-text p {
            color: #aaa;
            margin: 0;
            font-size: 0.9rem;
        }

        /* Footer */
        footer {
            background: #000;
            padding: 40px 20px;
            text-align: center;
            border-top: 1px solid #333;
        }

        .footer-logo {
            color: #D4AF37;
            font-size: 1.5rem;
            margin-bottom: 20px;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .footer-links a {
            color: #666;
            text-decoration: none;
        }

        .footer-links a:hover {
            color: #D4AF37;
        }

        /* Mobile */
        @media (max-width: 768px) {
            .hero-container {
                grid-template-columns: 1fr;
                text-align: center;
            }

            .hero-content h1 {
                font-size: 2.2rem;
            }

            .book-cover {
                width: 220px;
                height: 330px;
            }

            .features-grid,
            .testimonials-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <header>
        <a href="#" class="logo">48 LEIS</a>
        <a href="https://pay.cakto.com.br/7jcf5gr_764753" class="nav-cta">COMPRAR AGORA</a>
    </header>

    <section class="hero">
        <div class="hero-container">
            <div class="hero-content">
                <h1>As 48 Leis do Poder</h1>
                <p class="subtitle">O Manual Definitivo para Quem Quer Entender o Jogo do Poder</p>
                <p class="description">
                    Descubra as <span class="highlight">estratégias milenares</span> usadas pelos maiores líderes da história. 
                    De Maquiavel a Sun Tzu, Robert Greene compilou <span class="highlight">48 leis fundamentais</span> 
                    para você navegar no mundo complexo das relações de poder.
                </p>
                
                <a href="https://pay.cakto.com.br/7jcf5gr_764753" class="cta-button">
                    QUERO O LIVRO AGORA →
                </a>
                
                <div class="price-tag">
                    Oferta Especial<br>
                    <span class="price">R$ 47,90 <span>R$ 97,00</span></span>
                </div>
            </div>

            <div class="book-showcase">
                <div class="book-container">
                    <div class="floating-badge">-50%</div>
                    <img src="https://m.media-amazon.com/images/I/71f+9T4-+jL._AC_UF1000,1000_QL80_.jpg" alt="As 48 Leis do Poder" class="book-cover">
                </div>
            </div>
        </div>
    </section>

    <section class="features">
        <h2 class="section-title">O Que Você Vai Descobrir</h2>
        
        <div class="features-grid">
            <div class="feature-card">
                <div class="feature-icon">👑</div>
                <h3>Lei 1: Não Ofusque o Mestre</h3>
                <p>Faça seus superiores se sentirem superiores. Nunca mostre que é mais capaz que eles.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🎭</div>
                <h3>Lei 3: Oculte suas Intenções</h3>
                <p>Mantenha as pessoas fora de equilíbrio. Ninguém pode se defender do que não vê.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">⚔️</div>
                <h3>Lei 15: Aniquile o Inimigo</h3>
                <p>Quando atacar, não pare no meio. Esmague totalmente seus adversários.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🌟</div>
                <h3>Lei 6: Chame Atenção</h3>
                <p>Todas as pessoas são julgadas pela aparência. Destaque-se a qualquer custo.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🤝</div>
                <h3>Lei 12: Honestidade Seletiva</h3>
                <p>Um ato sincero cobre dúzias de desonestidades. A arte de desarmar suas vítimas.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🎯</div>
                <h3>Lei 29: Planeje até o Fim</h3>
                <p>O resultado é tudo. Pense muito à frente dos demais.</p>
            </div>
        </div>
    </section>

    <section class="testimonials">
        <h2 class="section-title">O Que os Leitores Dizem</h2>
        
        <div class="testimonials-grid">
            <div class="testimonial">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">"Mudou completamente minha visão sobre dinâmicas de poder no trabalho. Simplesmente magnífico!"</p>
                <div class="testimonial-author">
                    <div class="author-avatar">PC</div>
                    <div class="author-info">
                        <h4>Pedro Correia</h4>
                        <p>Empresário, SP</p>
                    </div>
                </div>
            </div>

            <div class="testimonial">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">"Essencial para quem trabalha em ambientes corporativos competitivos. Leitura transformadora."</p>
                <div class="testimonial-author">
                    <div class="author-avatar">MK</div>
                    <div class="author-info">
                        <h4>Marina K.</h4>
                        <p>Executiva de RH, RJ</p>
                    </div>
                </div>
            </div>

            <div class="testimonial">
                <div class="stars">★★★★★</div>
                <p class="testimonial-text">"Me ajudou a identificar manipulações e me proteger de jogos de poder. Vale cada centavo!"</p>
                <div class="testimonial-author">
                    <div class="author-avatar">RL</div>
                    <div class="author-info">
                        <h4>Ricardo Lima</h4>
                        <p>Advogado, DF</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="urgency">
        <h2>⚡ Oferta por Tempo Limitado</h2>
        <p style="color: #aaa;">Esta promoção encerra em breve!</p>
        
        <div class="countdown">
            <div class="time-unit">
                <div class="time-value" id="hours">04</div>
                <div class="time-label">Horas</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="minutes">32</div>
                <div class="time-label">Minutos</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="seconds">15</div>
                <div class="time-label">Segundos</div>
            </div>
        </div>

        <div class="stock-warning">
            🔥 Apenas 17 exemplares restantes!
        </div>

        <br><br>

        <a href="https://pay.cakto.com.br/7jcf5gr_764753" class="cta-button">
            GARANTIR MEU LIVRO →
        </a>
    </section>

    <section class="faq">
        <h2 class="section-title">Perguntas Frequentes</h2>
        
        <div class="faq-item" onclick="this.classList.toggle('active')">
            <div class="faq-question">
                <span>O livro é físico ou digital?</span>
                <span>+</span>
            </div>
            <div class="faq-answer">
                Você receberá a versão digital (PDF + ePub) imediatamente após a confirmação do pagamento.
            </div>
        </div>

        <div class="faq-item" onclick="this.classList.toggle('active')">
            <div class="faq-question">
                <span>Como recebo o material?</span>
                <span>+</span>
            </div>
            <div class="faq-answer">
                Após a compra, você receberá um e-mail com o link para download imediato. Acesso vitalício!
            </div>
        </div>

        <div class="faq-item" onclick="this.classList.toggle('active')">
            <div class="faq-question">
                <span>Tem garantia?</span>
                <span>+</span>
            </div>
            <div class="faq-answer">
                Sim! 7 dias de garantia incondicional. Não gostou? Devolvemos 100% do seu dinheiro.
            </div>
        </div>

        <div class="faq-item" onclick="this.classList.toggle('active')">
            <div class="faq-question">
                <span>Posso ler no Kindle?</span>
                <span>+</span>
            </div>
            <div class="faq-answer">
                Sim! O arquivo é compatível com Kindle, tablet, celular e computador.
            </div>
        </div>
    </section>

    <section class="final-cta">
        <h2>Domine o Jogo do Poder</h2>
        <p>Milhares de pessoas já transformaram suas vidas. Agora é sua vez!</p>
        
  
