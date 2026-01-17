<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NextWeb - Développement Web Moderne</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0a0a;
            color: #fff;
            overflow-x: hidden;
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 20px 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            background: rgba(10, 10, 10, 0.8);
            backdrop-filter: blur(10px);
            transition: all 0.3s;
        }

        nav.scrolled {
            padding: 15px 50px;
            background: rgba(10, 10, 10, 0.95);
        }

        .logo {
            font-size: 28px;
            font-weight: bold;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo-icon {
            width: 40px;
            height: 40px;
            position: relative;
        }

        .logo-icon svg {
            width: 100%;
            height: 100%;
            filter: drop-shadow(0 0 10px rgba(102, 126, 234, 0.3));
        }

        .nav-links {
            display: flex;
            gap: 40px;
            list-style: none;
        }

        .nav-links a {
            color: #fff;
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s;
            position: relative;
        }

        .nav-links a:hover {
            color: #667eea;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            transition: width 0.3s;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        /* Menu Hamburger */
        .hamburger {
            display: none;
            flex-direction: column;
            gap: 5px;
            cursor: pointer;
            z-index: 1001;
        }

        .hamburger span {
            width: 30px;
            height: 3px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 3px;
            transition: all 0.3s;
        }

        .hamburger.active span:nth-child(1) {
            transform: rotate(45deg) translate(8px, 8px);
        }

        .hamburger.active span:nth-child(2) {
            opacity: 0;
        }

        .hamburger.active span:nth-child(3) {
            transform: rotate(-45deg) translate(8px, -8px);
        }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
            padding: 0 20px;
        }

        .hero-bg {
            position: absolute;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            opacity: 0.1;
        }

        .hero-content {
            text-align: center;
            z-index: 1;
            animation: fadeInUp 1s ease;
        }

        .hero h1 {
            font-size: 72px;
            margin-bottom: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero p {
            font-size: 24px;
            color: #aaa;
            margin-bottom: 40px;
        }

        .cta-button {
            padding: 15px 40px;
            font-size: 18px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #fff;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(102, 126, 234, 0.5);
        }

        /* Floating shapes */
        .shape {
            position: absolute;
            border-radius: 50%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            opacity: 0.1;
            animation: float 6s ease-in-out infinite;
        }

        .shape1 { width: 300px; height: 300px; top: 10%; left: 10%; animation-delay: 0s; }
        .shape2 { width: 200px; height: 200px; bottom: 20%; right: 15%; animation-delay: 2s; }
        .shape3 { width: 150px; height: 150px; top: 50%; right: 30%; animation-delay: 4s; }

        /* Services Section */
        .services {
            padding: 100px 50px;
            background: #0f0f0f;
        }

        .section-title {
            text-align: center;
            font-size: 48px;
            margin-bottom: 60px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .service-card {
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
            padding: 40px;
            border-radius: 20px;
            transition: all 0.3s;
            border: 1px solid rgba(102, 126, 234, 0.2);
            cursor: pointer;
        }

        .service-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 50px rgba(102, 126, 234, 0.3);
            border-color: rgba(102, 126, 234, 0.5);
        }

        .service-icon {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .service-card h3 {
            font-size: 24px;
            margin-bottom: 15px;
            color: #667eea;
        }

        .service-card p {
            color: #aaa;
            line-height: 1.6;
        }

        /* Steps Section */
        .steps {
            padding: 100px 50px;
            background: #0a0a0a;
        }

        .steps-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 30px;
        }

        .step-card {
            text-align: center;
            padding: 30px 20px;
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
            border-radius: 20px;
            border: 1px solid rgba(102, 126, 234, 0.2);
            transition: all 0.3s;
            position: relative;
            display: flex;
            flex-direction: column;
            min-height: 280px;
        }

        .step-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 50px rgba(102, 126, 234, 0.3);
            border-color: rgba(102, 126, 234, 0.5);
        }

        .step-number {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            font-weight: bold;
            margin: 0 auto 20px;
            color: #fff;
        }

        .step-card h3 {
            font-size: 22px;
            color: #667eea;
            margin-bottom: 15px;
        }

        .step-card p {
            color: #aaa;
            line-height: 1.6;
            font-size: 16px;
        }

        /* FAQ Section */
        .faq {
            padding: 100px 50px;
            background: #0f0f0f;
        }

        .faq-container {
            max-width: 900px;
            margin: 0 auto;
        }

        .faq-item {
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
            border: 1px solid rgba(102, 126, 234, 0.2);
            border-radius: 15px;
            margin-bottom: 20px;
            overflow: hidden;
            transition: all 0.3s;
        }

        .faq-item:hover {
            border-color: rgba(102, 126, 234, 0.4);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.2);
        }

        .faq-question {
            padding: 25px 30px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            user-select: none;
        }

        .faq-question h3 {
            font-size: 20px;
            color: #667eea;
            margin: 0;
        }

        .faq-icon {
            font-size: 28px;
            color: #667eea;
            font-weight: 300;
            transition: transform 0.3s;
        }

        .faq-item.active .faq-icon {
            transform: rotate(45deg);
        }

        .faq-answer {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease, padding 0.3s ease;
            padding: 0 30px;
        }

        .faq-item.active .faq-answer {
            max-height: 800px;
            padding: 0 30px 25px 30px;
        }

        .faq-answer p {
            color: #aaa;
            line-height: 1.8;
            margin: 0;
        }

        .faq-answer ul {
            list-style: none;
            padding: 0;
        }

        .faq-answer ul li {
            color: #aaa;
            padding: 5px 0;
        }

        /* Contact Section */
        .contact {
            padding: 100px 50px;
            background: #0a0a0a;
            text-align: center;
        }

        .contact-content {
            max-width: 600px;
            margin: 0 auto;
        }

        .contact-content a:hover {
            transform: scale(1.05);
            text-shadow: 0 0 20px rgba(102, 126, 234, 0.5);
        }

        /* Formulaire de contact */
        .contact-form {
            max-width: 600px;
            margin: 40px auto 0;
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
            padding: 40px;
            border-radius: 20px;
            border: 1px solid rgba(102, 126, 234, 0.2);
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #667eea;
            font-weight: 500;
            font-size: 16px;
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 12px 18px;
            background: rgba(10, 10, 10, 0.5);
            border: 2px solid rgba(102, 126, 234, 0.3);
            border-radius: 10px;
            color: #fff;
            font-size: 16px;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: all 0.3s;
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 15px rgba(102, 126, 234, 0.3);
        }

        .form-group textarea {
            resize: vertical;
            min-height: 120px;
        }

        .submit-button {
            width: 100%;
            padding: 15px 40px;
            font-size: 18px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #fff;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
            font-weight: 600;
        }

        .submit-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(102, 126, 234, 0.5);
        }

        .divider {
            display: flex;
            align-items: center;
            text-align: center;
            margin: 40px 0;
            color: #666;
        }

        .divider::before,
        .divider::after {
            content: '';
            flex: 1;
            border-bottom: 1px solid rgba(102, 126, 234, 0.2);
        }

        .divider span {
            padding: 0 15px;
            font-size: 14px;
        }

        /* Footer */
        footer {
            padding: 40px;
            text-align: center;
            background: #0f0f0f;
            color: #666;
        }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(10deg); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.6s;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* RESPONSIVE MOBILE */
        @media (max-width: 768px) {
            nav {
                padding: 15px 20px;
            }

            nav.scrolled {
                padding: 12px 20px;
            }

            .logo {
                font-size: 22px;
            }

            .logo-icon {
                width: 32px;
                height: 32px;
            }

            .hamburger {
                display: flex;
            }

            .nav-links {
                position: fixed;
                top: 0;
                right: -100%;
                height: 100vh;
                width: 70%;
                max-width: 300px;
                background: rgba(10, 10, 10, 0.98);
                backdrop-filter: blur(20px);
                flex-direction: column;
                justify-content: center;
                align-items: center;
                gap: 30px;
                transition: right 0.3s ease;
                padding: 40px;
            }

            .nav-links.active {
                right: 0;
            }

            .nav-links a {
                font-size: 24px;
            }

            .hero h1 {
                font-size: 42px;
            }

            .hero p {
                font-size: 18px;
            }

            .hero p:last-of-type {
                font-size: 16px !important;
            }

            .cta-button {
                padding: 12px 30px;
                font-size: 16px;
            }

            .shape1 { width: 200px; height: 200px; }
            .shape2 { width: 150px; height: 150px; }
            .shape3 { width: 100px; height: 100px; }

            .services, .steps, .faq, .contact {
                padding: 60px 20px;
            }

            .section-title {
                font-size: 36px;
                margin-bottom: 40px;
            }

            .services-grid {
                grid-template-columns: 1fr;
                gap: 30px;
            }

            .service-card {
                padding: 30px;
            }

            .steps-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }

            .step-card {
                min-height: auto;
                padding: 25px 20px;
            }

            .faq-question {
                padding: 20px;
            }

            .faq-question h3 {
                font-size: 18px;
            }

            .faq-answer {
                padding: 0 20px;
            }

            .faq-item.active .faq-answer {
                padding: 0 20px 20px 20px;
            }

            .contact-content a {
                font-size: 20px !important;
            }

            footer {
                padding: 30px 20px;
                font-size: 14px;
            }
        }

        @media (max-width: 480px) {
            .hero h1 {
                font-size: 32px;
            }

            .hero p {
                font-size: 16px;
            }

            .section-title {
                font-size: 28px;
            }

            .service-card h3, .step-card h3 {
                font-size: 20px;
            }

            .service-card p, .step-card p {
                font-size: 15px;
            }
        }

        @media (min-width: 769px) and (max-width: 1024px) {
            .steps-container {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <nav id="navbar">
        <div class="logo">
            <div class="logo-icon">
                <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                        <linearGradient id="logoGradient" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" style="stop-color:#667eea;stop-opacity:1" />
                            <stop offset="100%" style="stop-color:#764ba2;stop-opacity:1" />
                        </linearGradient>
                    </defs>
                    <path d="M 35 20 L 20 20 L 20 80 L 35 80" 
                          stroke="url(#logoGradient)" 
                          stroke-width="6" 
                          fill="none" 
                          stroke-linecap="round" 
                          stroke-linejoin="round"/>
                    <path d="M 65 20 L 80 20 L 80 80 L 65 80" 
                          stroke="url(#logoGradient)" 
                          stroke-width="6" 
                          fill="none" 
                          stroke-linecap="round" 
                          stroke-linejoin="round"/>
                    <path d="M 42 40 L 42 60 M 42 40 L 58 60 M 58 40 L 58 60" 
                          stroke="url(#logoGradient)" 
                          stroke-width="5" 
                          fill="none" 
                          stroke-linecap="round" 
                          stroke-linejoin="round"/>
                    <circle cx="72" cy="28" r="3" fill="url(#logoGradient)"/>
                </svg>
            </div>
            NextWeb
        </div>
        
        <div class="hamburger" id="hamburger">
            <span></span>
            <span></span>
            <span></span>
        </div>

        <ul class="nav-links" id="navLinks">
            <li><a href="#accueil">Accueil</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#etapes">Étapes</a></li>
            <li><a href="#faq">FAQ</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>

    <section class="hero" id="accueil">
        <div class="hero-bg"></div>
        <div class="shape shape1"></div>
        <div class="shape shape2"></div>
        <div class="shape shape3"></div>
        <div class="hero-content">
            <h1>NextWeb</h1>
            <p>Des sites internet de <strong>qualité</strong>, un service <strong>personnalisé</strong></p>
            <p style="font-size: 18px; color: #888; margin-top: 10px;">Développeur indépendant passionné, je crée chaque projet de <strong>A à Z</strong> avec attention et professionnalisme</p>
            <button class="cta-button" onclick="scrollToContact()">Démarrer un projet</button>
        </div>
    </section>

    <section class="services" id="services">
        <h2 class="section-title fade-in">Mes Services</h2>
        <div style="max-width: 800px; margin: 0 auto 60px; text-align: center; color: #aaa; font-size: 18px; line-height: 1.8;">
            <p>Passionné par le développement web, je réalise <strong>personnellement</strong> chaque projet du design initial jusqu'à la mise en ligne. Mon approche artisanale me permet de créer des sites internet <strong>sur-mesure</strong>, parfaitement adaptés à vos besoins et à votre identité.</p>
            <p style="margin-top: 20px;">Ce site que vous visitez actuellement ? Je l'ai <strong>entièrement conçu et développé moi-même</strong>, il reflète ma vision d'un web <strong>moderne, élégant et performant</strong>.</p>
        </div>
        <div class="services-grid">
            <div class="service-card fade-in">
                <div class="service-icon">🏢</div>
                <h3>Grandes Entreprises</h3>
                <p>Sites web professionnels et plateformes robustes pour accompagner la croissance des grandes entreprises avec des solutions évolutives et sécurisées.</p>
            </div>
            <div class="service-card fade-in">
                <div class="service-icon">💼</div>
                <h3>Indépendants</h3>
                <p>Sites vitrine élégants et portfolios sur-mesure pour les freelances et entrepreneurs qui veulent se démarquer et attirer leurs clients idéaux.</p>
            </div>
            <div class="service-card fade-in">
                <div class="service-icon">🎉</div>
                <h3>Événements</h3>
                <p>Sites dédiés pour vos événements : conférences, festivals, mariages ou lancements de produits. Design unique et gestion des inscriptions.</p>
            </div>
        </div>
    </section>

    <section class="steps" id="etapes">
        <h2 class="section-title fade-in">Comment ça marche ?</h2>
        <div class="steps-container">
            <div class="step-card fade-in">
                <div class="step-number">1</div>
                <h3>Contactez-moi</h3>
                <p>Prenez contact avec moi par téléphone ou via les réseaux sociaux pour discuter de votre projet.</p>
            </div>
            <div class="step-card fade-in">
                <div class="step-number">2</div>
                <h3>Explication concrète</h3>
                <p>Vous m'expliquez votre projet en détail : vos besoins, vos objectifs et votre vision.</p>
            </div>
            <div class="step-card fade-in">
                <div class="step-number">3</div>
                <h3>Je réalise</h3>
                <p>Je conçois et développe votre site web personnalisé de A à Z avec soin et professionnalisme.</p>
            </div>
            <div class="step-card fade-in">
                <div class="step-number">4</div>
                <h3>Le site est à vous</h3>
                <p>Votre site est mis en ligne et livré clé en main. Vous êtes maintenant prêt à conquérir le web !</p>
            </div>
        </div>
    </section>

    <section class="faq" id="faq">
        <h2 class="section-title fade-in">Questions Fréquentes</h2>
        <div class="faq-container">
            <div class="faq-item fade-in">
                <div class="faq-question">
                    <h3>👨‍💻 Qui suis-je ?</h3>
                    <span class="faq-icon">+</span>
                </div>
                <div class="faq-answer">
                    <p>Je m'appelle Alexis, j'ai <strong>17 ans</strong> et je suis basé en <strong>Belgique</strong>. Passionné par le développement web depuis plusieurs années, je crée des sites internet modernes et professionnels. Je réalise <strong>tous mes projets entièrement moi-même</strong>, du design initial jusqu'à la mise en ligne, ce qui me permet de garantir une qualité constante et un suivi personnalisé.</p>
                </div>
            </div>

            <div class="faq-item fade-in">
                <div class="faq-question">
                    <h3>💰 Comment se passe le paiement ?</h3>
                    <span class="faq-icon">+</span>
                </div>
                <div class="faq-answer">
                    <p>Le paiement s'effectue via <strong>PayPal</strong> en toute sécurité. Je demande un <strong>acompte minimum de 30%</strong> au démarrage du projet pour confirmer votre commande. Le solde est à régler à la livraison du site finalisé. Cette méthode de paiement protège à la fois vous et moi, et permet de travailler sereinement.</p>
                </div>
            </div>

            <div class="faq-item fade-in">
                <div class="faq-question">
                    <h3>💵 Quels sont vos tarifs ?</h3>
                    <span class="faq-icon">+</span>
                </div>
                <div class="faq-answer">
                    <p>Les tarifs <strong>varient en fonction du type de projet</strong> et de vos besoins spécifiques :</p>
                    <ul style="margin-top: 15px; text-align: left; line-height: 1.8;">
                        <li><strong>Site vitrine</strong> : pour présenter votre activité, vos services ou votre portfolio</li>
                        <li><strong>Site e-commerce</strong> : boutique en ligne avec système de paiement intégré</li>
                        <li><strong>Site événementiel</strong> : pour un mariage, festival, conférence ou lancement</li>
                        <li><strong>Site sur-mesure</strong> : fonctionnalités personnalisées selon vos besoins</li>
                    </ul>
                    <p style="margin-top: 15px;">Chaque projet est unique ! Contactez-moi pour obtenir un <strong>devis gratuit et personnalisé</strong> adapté à votre budget et vos objectifs.</p>
                </div>
            </div>

            <div class="faq-item fade-in">
                <div class="faq-question">
                    <h3>⏱️ Quels sont les délais de réalisation ?</h3>
                    <span class="faq-icon">+</span>
                </div>
                <div class="faq-answer">
                    <p>Les délais dépendent de la complexité du projet. En moyenne :</p>
                    <ul style="margin-top: 15px; text-align: left; line-height: 1.8;">
                        <li><strong>Site vitrine simple</strong> : 2 à 3 jours</li>
                        <li><strong>Site vitrine avancé</strong> : 3 à 5 jours</li>
                        <li><strong>Site e-commerce</strong> : 1 à 2 semaines</li>
                        <li><strong>Projet sur-mesure</strong> : selon les fonctionnalités demandées</li>
                    </ul>
                    <p style="margin-top: 15px;">Je vous tiendrai informé de l'avancement tout au long du projet !</p>
                </div>
            </div>

            <div class="faq-item fade-in">
                <div class="faq-question">
                    <h3>🛠️ Quels services sont inclus ?</h3>
                    <span class="faq-icon">+</span>
                </div>
                <div class="faq-answer">
                    <p>Chaque projet inclut :</p>
                    <ul style="margin-top: 15px; text-align: left; line-height: 1.8;">
                        <li>✅ Design moderne et responsive (adapté mobile/tablette/PC)</li>
                        <li>✅ Développement entièrement personnalisé</li>
                        <li>✅ Optimisation des performances et du référencement (SEO)</li>
                        <li>✅ Mise en ligne du site</li>
                        <li>✅ Formation pour gérer votre contenu</li>
                        <li>✅ Support après livraison</li>
                    </ul>
                    <p style="margin-top: 15px;">L'hébergement et le nom de domaine peuvent être inclus selon la formule choisie.</p>
                </div>
            </div>

            <div class="faq-item fade-in">
                <div class="faq-question">
                    <h3>🔄 Puis-je modifier mon site après livraison ?</h3>
                    <span class="faq-icon">+</span>
                </div>
                <div class="faq-answer">
                    <p>Absolument ! Je vous forme pour que vous puissiez <strong>modifier facilement vos textes, images et contenus</strong>. Pour des modifications plus complexes (design, fonctionnalités), je reste disponible pour vous accompagner. Des formules de maintenance peuvent être proposées selon vos besoins.</p>
                </div>
            </div>
        </div>
    </section>

    <section class="contact" id="contact">
        <h2 class="section-title fade-in">Contactez-moi</h2>
        <div class="contact-content fade-in">
            
            <!-- Formulaire de contact -->
            <div class="contact-form">
                <div class="form-group">
                    <label for="name">Votre nom</label>
                    <input type="text" id="name" required>
                </div>
                <div class="form-group">
                    <label for="email">Votre email</label>
                    <input type="email" id="email" required>
                </div>
                <div class="form-group">
                    <label for="subject">Sujet</label>
                    <input type="text" id="subject" required>
                </div>
                <div class="form-group">
                    <label for="message">Votre message</label>
                    <textarea id="message" required></textarea>
                </div>
                <button class="submit-button" onclick="sendEmail()">Envoyer le message</button>
            </div>

            <div class="divider">
                <span>OU CONTACTEZ-MOI DIRECTEMENT</span>
            </div>

            <div style="display: flex; flex-direction: column; gap: 20px; align-items: center;">
                <a href="tel:0495543815" style="font-size: 24px; color: #667eea; font-weight: bold; text-decoration: none; transition: all 0.3s;">
                    📞 0495 54 38 15
                </a>
                <a href="https://www.instagram.com/next.web" target="_blank" style="font-size: 24px; color: #667eea; font-weight: bold; display: flex; align-items: center; gap: 10px; text-decoration: none; transition: all 0.3s;">
                    <svg width="32" height="32" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect x="2" y="2" width="20" height="20" rx="5" stroke="currentColor" stroke-width="2"/>
                        <circle cx="12" cy="12" r="4" stroke="currentColor" stroke-width="2"/>
                        <circle cx="18" cy="6" r="1.5" fill="currentColor"/>
                    </svg>
                    next.web
                </a>
                <div style="display: flex; flex-direction: column; align-items: center; gap: 5px;">
                    <a href="https://www.tiktok.com/@next.web0" target="_blank" style="font-size: 24px; color: #667eea; font-weight: bold; display: flex; align-items: center; gap: 10px; text-decoration: none; transition: all 0.3s;">
                        <svg width="32" height="32" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path d="M19.59 6.69a4.83 4.83 0 0 1-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 0 1-5.2 1.74 2.89 2.89 0 0 1 2.31-4.64 2.93 2.93 0 0 1 .88.13V9.4a6.84 6.84 0 0 0-1-.05A6.33 6.33 0 0 0 5 20.1a6.34 6.34 0 0 0 10.86-4.43v-7a8.16 8.16 0 0 0 4.77 1.52v-3.4a4.85 4.85 0 0 1-1-.1z" stroke="currentColor" stroke-width="1.5" fill="currentColor"/>
                        </svg>
                        next.web0
                    </a>
                    <span style="font-size: 12px; color: #888; font-style: italic;">Cliquer pour voir</span>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <p>&copy; 2026 NextWeb. Tous droits réservés.</p>
    </footer>

    <script>
        // Fonction d'envoi email
        function sendEmail() {
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const subject = document.getElementById('subject').value;
            const message = document.getElementById('message').value;

            // Vérification des champs
            if (!name || !email || !subject || !message) {
                alert('Veuillez remplir tous les champs du formulaire');
                return;
            }

            // Création du corps de l'email
            const body = `Nom: ${name}%0D%0AEmail: ${email}%0D%0A%0D%0AMessage:%0D%0A${message}`;
            
            // Ouverture du client email
            window.location.href = `mailto:graindorgealexis8@gmail.com?subject=${encodeURIComponent(subject)}&body=${body}`;
        }

        // Menu Hamburger Toggle
        const hamburger = document.getElementById('hamburger');
        const navLinks = document.getElementById('navLinks');

        hamburger.addEventListener('click', () => {
            hamburger.classList.toggle('active');
            navLinks.classList.toggle('active');
        });

        // Fermer le menu quand on clique sur un lien
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', () => {
                hamburger.classList.remove('active');
                navLinks.classList.remove('active');
            });
        });

        // Fermer le menu si on clique en dehors
        document.addEventListener('click', (e) => {
            if (!hamburger.contains(e.target) && !navLinks.contains(e.target)) {
                hamburger.classList.remove('active');
                navLinks.classList.remove('active');
            }
        });

        // Function to scroll to contact
        function scrollToContact() {
            const contactSection = document.getElementById('contact');
            contactSection.scrollIntoView({ behavior: 'smooth', block: 'start' });
            
            const contactContent = document.querySelector('.contact-content');
            contactContent.style.animation = 'pulse 0.5s ease';
            setTimeout(() => {
                contactContent.style.animation = '';
            }, 500);
        }

        // Scroll animation navbar
        const navbar = document.getElementById('navbar');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
        });

        // Fade in on scroll
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));

        // FAQ Toggle
        document.querySelectorAll('.faq-question').forEach(question => {
            question.addEventListener('click', () => {
                const faqItem = question.parentElement;
                const isActive = faqItem.classList.contains('active');
                
                // Fermer toutes les autres FAQ
                document.querySelectorAll('.faq-item').forEach(item => {
                    item.classList.remove('active');
                });
                
                // Ouvrir celle cliquée si elle n'était pas déjà ouverte
                if (!isActive) {
                    faqItem.classList.add('active');
                }
            });
        });

        // Smooth scroll
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
</html>
