<!DOCTYPE html>
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

        /* Background Pattern */
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

        /* Header */
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

        /* Hero Section */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 120px 5% 80px;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -20%;
            width: 800px;
            height: 800px;
            background: radial-gradient(circle, rgba(212, 175, 55, 0.1) 0%, transparent 70%);
            animation: pulse 4s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; }
        }

        .hero-container {
            max-width: 1400px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 60px;
            align-items: center;
            position: relative;
            z-index: 1;
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

        /* Book Cover */
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

        /* CTA Button */
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

        /* Features Section */
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

        /* Social Proof */
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

        /* Urgency Section */
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

        /* FAQ Section */
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

        /* Final CTA */
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

        /* Footer */
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

        /* Mobile Responsive */
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
        }

        /* Scroll Animation */
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* Particle Effect */
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
            0% { 
