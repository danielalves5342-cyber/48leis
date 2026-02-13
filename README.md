import zipfile
import os

# Código HTML simplificado e funcional
html_code = '''<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>As 48 Leis do Poder</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            font-family: Arial, sans-serif; 
            background: #0a0a0a; 
            color: #fff; 
            line-height: 1.6;
        }
        .container { max-width: 1200px; margin: 0 auto; padding: 20px; }
        
        /* Header */
        header { 
            background: #000; 
            padding: 20px; 
            text-align: center; 
            border-bottom: 2px solid #D4AF37;
        }
        .logo { 
            color: #D4AF37; 
            font-size: 2rem; 
            font-weight: bold;
            text-decoration: none;
        }
        
        /* Hero com Vídeo */
        .hero {
            position: relative;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        .video-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
        }
        .video-bg video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.3;
        }
        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 1;
        }
        .hero-content {
            position: relative;
            z-index: 2;
            text-align: center;
            padding: 20px;
        }
        h1 {
            font-size: 3rem;
            color: #D4AF37;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
        }
        .subtitle {
            font-size: 1.3rem;
            color: #ccc;
            margin-bottom: 30px;
        }
        .cta-button {
            display: inline-block;
            background: #00C851;
            color: white;
            padding: 20px 50px;
            border-radius: 50px;
            text-decoration: none;
            font-size: 1.2rem;
            font-weight: bold;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,200,81,0.3);
        }
        .price {
            font-size: 2.5rem;
            color: #D4AF37;
            margin-top: 20px;
        }
        .price span {
            text-decoration: line-through;
            color: #666;
            font-size: 1.5rem;
        }
        
        /* Seção Vídeo */
        .video-section {
            padding: 80px 20px;
            background: #050505;
            text-align: center;
        }
        .video-section h2 {
            color: #D4AF37;
            font-size: 2rem;
            margin-bottom: 30px;
        }
        .video-container {
            max-width: 400px;
            margin: 0 auto;
            border-radius: 20px;
            overflow: hidden;
            border: 2px solid #D4AF37;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
        }
        .video-container video {
            width: 100%;
            display: block;
        }
        
        /* Features */
        .features {
            padding: 80px 20px;
            background: #0a0a0a;
        }
        .features h2 {
            color: #D4AF37;
            text-align: center;
            font-size: 2rem;
            margin-bottom: 40px;
        }
        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }
        .feature-card {
            background: #111;
            border: 1px solid #333;
            border-radius: 15px;
            padding: 30px;
            text-align: center;
        }
        .feature-card h3 {
            color: #D4AF37;
            margin-bottom: 15px;
        }
        .feature-card p {
            color: #aaa;
        }
        
        /* Footer CTA */
        .final-cta {
            padding: 80px 20px;
            text-align: center;
            background: linear-gradient(to bottom, #0a0a0a, #000);
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
        
        /* Footer */
        footer {
            background: #000;
            padding: 40px 20px;
            text-align: center;
            border-top: 1px solid #333;
        }
        footer a {
            color: #D4AF37;
            text-decoration: none;
        }
    </style>
</head>
<body>
    <header>
        <a href="#" class="logo">48 LEIS DO PODER</a>
    </header>

    <section class="hero">
        <div class="video-bg">
            <video autoplay muted loop playsinline>
                <source src="https://files.catbox.moe/abc123.mp4" type="video/mp4">
            </video>
            <div class="overlay"></div>
        </div>
        <div class="hero-content">
            <h1>As 48 Leis do Poder</h1>
            <p class="subtitle">O Manual Definitivo para Quem Quer Entender o Jogo do Poder</p>
            <a href="https://pay.cakto.com.br/7jcf5gr_764139" class="cta-button">
                QUERO O LIVRO AGORA →
            </a>
            <div class="price">
                R$ 47,90 <span>R$ 97,00</span>
            </div>
        </div>
    </section>

    <section class="video-section">
        <h2>A Verdade sobre o Poder</h2>
        <div class="video-container">
            <video controls poster="">
                <source src="https://files.catbox.moe/abc123.mp4" type="video/mp4">
                Seu navegador não suporta vídeos.
            </video>
        </div>
        <p style="color: #aaa; margin-top: 20px;">"O mundo é um lugar perigoso para os ingênuos"</p>
    </section>

    <section class="features">
        <h2>O Que Você Vai Descobrir</h2>
        <div class="feature-grid">
            <div class="feature-card">
                <h3> Lei 1: Não Ofusque o Mestre</h3>
                <p>Faça seus superiores se sentirem superiores. Nunca mostre que é mais capaz que eles.</p>
            </div>
            <div class="feature-card">
                <h3> Lei 3: Oculte suas Intenções</h3>
                <p>Mantenha as pessoas fora de equilíbrio. Ninguém pode se defender do que não vê.</p>
            </div>
            <div class="feature-card">
                <h3>⚔️ Lei 15: Aniquile o Inimigo</h3>
                <p>Quando atacar, não pare no meio. Esmague totalmente seus adversários.</p>
            </div>
        </div>
    </section>

    <section class="final-cta">
        <h2>Domine o Jogo do Poder</h2>
        <p>Transforme sua vida com as estratégias milenares dos grandes líderes</p>
        <a href="https://pay.cakto.com.br/7jcf5gr_764139" class="cta-button">
            GARANTIR MEU LIVRO →
        </a>
    </section>

    <footer>
        <p style="color: #666;">© 2024 - As 48 Leis do Poder</p>
        <p style="margin-top: 10px;"><a href="https://pay.cakto.com.br/7jcf5gr_764139">Comprar Agora</a></p>
    </footer>
</body>
</html>'''

# Criar o arquivo diretamente na raiz do ZIP
zip_path = '/mnt/kimi/output/site-48-leis-v3.zip'

with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zipf:
    zipf.writestr('index.html', html_
