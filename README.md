<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Telegram Бот | Социальные сети</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #ff0000;
            --secondary: #000;
            --accent: #fff;
            --dark-bg: #111;
            --card-bg: #1a1a1a;
        }
        
        body {
            background-color: var(--secondary);
            color: var(--accent);
            line-height: 1.6;
            min-height: 100vh;
            background: linear-gradient(135deg, #000000 0%, #1a0000 100%);
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            padding: 40px 0;
            position: relative;
        }
        
        h1 {
            font-size: 3rem;
            color: var(--accent);
            text-shadow: 0 0 15px rgba(255, 0, 0, 0.7);
            margin-bottom: 10px;
            letter-spacing: 2px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: #ccc;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .tabs {
            display: flex;
            justify-content: center;
            margin: 30px 0;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .tab-button {
            background-color: transparent;
            color: var(--accent);
            border: 2px solid var(--primary);
            padding: 12px 25px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            border-radius: 30px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .tab-button:hover {
            background-color: var(--primary);
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(255, 0, 0, 0.4);
        }
        
        .tab-button.active {
            background-color: var(--primary);
            color: var(--secondary);
        }
        
        .tab-content {
            display: none;
            padding: 30px;
            background-color: var(--dark-bg);
            border: 1px solid #333;
            border-radius: 10px;
            min-height: 400px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        }
        
        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        h2 {
            color: var(--primary);
            margin-bottom: 25px;
            text-align: center;
            font-size: 2rem;
            position: relative;
            padding-bottom: 10px;
        }
        
        h2:after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 3px;
            background: var(--primary);
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .info-card {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: 10px;
            border-left: 4px solid var(--primary);
            transition: transform 0.3s ease;
        }
        
        .info-card:hover {
            transform: translateY(-5px);
        }
        
        .info-card h3 {
            color: var(--primary);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .info-card p {
            color: #ddd;
            line-height: 1.7;
        }
        
        .social-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .social-card {
            background: linear-gradient(145deg, #1a1a1a, #222);
            border-radius: 10px;
            padding: 25px 20px;
            text-align: center;
            transition: all 0.3s ease;
            border: 1px solid #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .social-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 20px rgba(255, 0, 0, 0.2);
            border-color: var(--primary);
        }
        
        .social-icon {
            font-size: 3rem;
            margin-bottom: 15px;
            height: 80px;
            width: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            background-color: rgba(255, 0, 0, 0.1);
        }
        
        .telegram { color: #0088cc; }
        .discord { color: #5865F2; }
        
        .social-card h3 {
            font-size: 1.3rem;
            margin-bottom: 10px;
            color: var(--accent);
        }
        
        .social-card p {
            color: #aaa;
            margin-bottom: 20px;
            font-size: 0.9rem;
        }
        
        .btn {
            display: inline-block;
            background-color: var(--primary);
            color: var(--secondary);
            padding: 10px 20px;
            border-radius: 30px;
            text-decoration: none;
            font-weight: 600;
            transition: all 0.3s ease;
            border: 2px solid var(--primary);
        }
        
        .btn:hover {
            background-color: transparent;
            color: var(--primary);
        }
        
        .btn-outline {
            background-color: transparent;
            color: var(--primary);
            border: 2px solid var(--primary);
        }
        
        .btn-outline:hover {
            background-color: var(--primary);
            color: var(--secondary);
        }
        
        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            border-top: 1px solid #333;
            color: #888;
            font-size: 0.9rem;
        }
        
        .highlight {
            color: var(--primary);
            font-weight: bold;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .tab-button {
                width: 100%;
                justify-content: center;
            }
            
            .info-grid, .social-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>МОЙ TELEGRAM БОТ</h1>
            <p class="subtitle">Многофункциональный бот для решения ваших задач с интеграцией в популярные платформы</p>
        </header>
        
        <div class="tabs">
            <button class="tab-button active" data-tab="info">
                <i class="fas fa-info-circle"></i> ИНФО О БОТЕ
            </button>
            <button class="tab-button" data-tab="social">
                <i class="fas fa-share-alt"></i> СОЦ. СЕТИ
            </button>
        </div>
        
        <div class="tab-content active" id="info-tab">
            <h2>ИНФОРМАЦИЯ О БОТЕ</h2>
            <div class="info-grid">
                <div class="info-card">
                    <h3><i class="fas fa-robot"></i> ОСНОВНЫЕ ФУНКЦИИ</h3>
                    <p>Мой бот предоставляет широкий спектр функций: автоматизация задач, уведомления, интеграция с API, мультимедийные возможности и многое другое.</p>
                </div>
                
                <div class="info-card">
                    <h3><i class="fas fa-cogs"></i> ТЕХНОЛОГИИ</h3>
                    <p>Бот разработан на современном стеке технологий с использованием Node.js, Python и специализированных библиотек для Telegram Bot API.</p>
                </div>
                
                <div class="info-card">
                    <h3><i class="fas fa-history"></i> ИСТОРИЯ ОБНОВЛЕНИЙ</h3>
                    <p>Постоянно работаю над улучшением функционала. Последнее обновление добавило интеграцию с Discord и новые команды для администраторов.</p>
                </div>
                
                <div class="info-card">
                    <h3><i class="fas fa-question-circle"></i> ПОДДЕРЖКА</h3>
                    <p>Если у вас возникли проблемы с ботом или есть предложения по улучшению, напишите мне в Telegram или присоединяйтесь к нашему Discord серверу.</p>
                </div>
            </div>
            
            <div style="text-align: center; margin-top: 30px;">
                <a href="#" class="btn"><i class="fas fa-rocket"></i> НАЧАТЬ ИСПОЛЬЗОВАТЬ БОТА</a>
            </div>
        </div>
        
        <div class="tab-content" id="social-tab">
            <h2>СОЦИАЛЬНЫЕ СЕТИ И КОНТАКТЫ</h2>
            
            <div class="social-grid">
                <div class="social-card">
                    <div class="social-icon telegram">
                        <i class="fab fa-telegram-plane"></i>
                    </div>
                    <h3>TELEGRAM БОТ</h3>
                    <p>Основной бот с полным функционалом</p>
                    <a href="https://t.me/your_bot" class="btn" target="_blank">Перейти</a>
                </div>
                
                <div class="social-card">
                    <div class="social-icon telegram">
                        <i class="fas fa-broadcast-tower"></i>
                    </div>
                    <h3>TELEGRAM КАНАЛ</h3>
                    <p>Новости, обновления и анонсы</p>
                    <a href="https://t.me/your_channel" class="btn" target="_blank">Подписаться</a>
                </div>
                
                <div class="social-card">
                    <div class="social-icon telegram">
                        <i class="fas fa-user"></i>
                    </div>
                    <h3>TELEGRAM АККАУНТ</h3>
                    <p>Связь с разработчиком</p>
                    <a href="https://t.me/your_account" class="btn" target="_blank">Написать</a>
                </div>
                
                <div class="social-card">
                    <div class="social-icon discord">
                        <i class="fab fa-discord"></i>
                    </div>
                    <h3>DISCORD СЕРВЕР</h3>
                    <p>Сообщество и поддержка</p>
                    <a href="https://discord.gg/your_invite" class="btn btn-outline" target="_blank">Присоединиться</a>
                </div>
            </div>
            
            <div style="margin-top: 40px; background: var(--card-bg); padding: 20px; border-radius: 10px;">
                <h3 style="color: var(--primary); margin-bottom: 15px; text-align: left;"><i class="fas fa-link"></i> КАК ИСПОЛЬЗОВАТЬ ССЫЛКИ</h3>
                <p>Замените ссылки выше на актуальные для вашего проекта. Для этого найдите в коде атрибуты <span class="highlight">href</span> и замените значения на свои.</p>
            </div>
        </div>
        
        <footer>
            <p>© 2023 Мой Telegram Бот. Все права защищены.</p>
            <p style="margin-top: 10px;">Сайт разработан специально для GitHub Pages</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const tabButtons = document.querySelectorAll('.tab-button');
            const tabContents = document.querySelectorAll('.tab-content');
            
            tabButtons.forEach(button => {
                button.addEventListener('click', () => {
                    // Убираем активный класс у всех кнопок и контента
                    tabButtons.forEach(btn => btn.classList.remove('active'));
                    tabContents.forEach(content => content.classList.remove('active'));
                    
                    // Добавляем активный класс к нажатой кнопке
                    button.classList.add('active');
                    
                    // Показываем соответствующий контент
                    const tabId = button.getAttribute('data-tab') + '-tab';
                    document.getElementById(tabId).classList.add('active');
                });
            });
        });
    </script>
</body>
</html>
