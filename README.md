# Fres-bol-tiro-br
 O pior jogo do momento 😈<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black">
    <title>Battle Royale 3D - Profissional</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            overflow: hidden;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #000;
            color: #fff;
            user-select: none;
        }

        #app {
            width: 100vw;
            height: 100vh;
        }

        /* ===== MIRA ===== */
        .mira {
            position: fixed;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            transform: translate(-50%, -50%);
            pointer-events: none;
            z-index: 100;
        }

        .mira-dot {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #00ff00;
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            box-shadow: 0 0 10px #00ff00;
        }

        .mira-line {
            position: absolute;
            background: #00ff00;
            top: 50%;
            left: 50%;
        }

        .mira-h {
            width: 8px;
            height: 1px;
            margin-left: -4px;
            margin-top: -0.5px;
        }

        .mira-v {
            width: 1px;
            height: 8px;
            margin-left: -0.5px;
            margin-top: -4px;
        }

        /* ===== HUD ===== */
        #hud {
            position: fixed;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 50;
        }

        .hud-top {
            position: fixed;
            top: 10px;
            left: 10px;
            display: flex;
            gap: 20px;
            z-index: 50;
        }

        .hud-info {
            background: rgba(0, 0, 0, 0.85);
            padding: 15px 20px;
            border-radius: 8px;
            border: 2px solid #00ff00;
            backdrop-filter: blur(10px);
        }

        .hud-label {
            font-size: 11px;
            color: #00ff00;
            margin-bottom: 5px;
            text-transform: uppercase;
            font-weight: bold;
        }

        .hud-value {
            font-size: 18px;
            font-weight: bold;
            color: #fff;
        }

        /* ===== SAÚDE ===== */
        .health-container {
            position: fixed;
            bottom: 30px;
            left: 30px;
            width: 280px;
            z-index: 50;
        }

        .health-bar, .armor-bar {
            width: 100%;
            height: 22px;
            background: rgba(0, 0, 0, 0.85);
            border: 2px solid #00ff00;
            border-radius: 5px;
            overflow: hidden;
            position: relative;
            margin-top: 8px;
            backdrop-filter: blur(10px);
        }

        .armor-bar {
            border-color: #0099ff;
            height: 18px;
        }

        .health-fill, .armor-fill {
            height: 100%;
            background: linear-gradient(90deg, #00ff00, #00aa00);
            transition: width 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 11px;
            box-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
        }

        .armor-fill {
            background: linear-gradient(90deg, #0099ff, #0066aa);
            box-shadow: 0 0 10px rgba(0, 153, 255, 0.5);
        }

        /* ===== MUNIÇÃO ===== */
        .ammo-container {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: rgba(0, 0, 0, 0.85);
            padding: 15px 25px;
            border-radius: 8px;
            border: 2px solid #ff6600;
            z-index: 50;
            backdrop-filter: blur(10px);
        }

        .ammo-label {
            font-size: 11px;
            color: #ff6600;
            text-transform: uppercase;
            margin-bottom: 5px;
            font-weight: bold;
        }

        .ammo-value {
            font-size: 24px;
            font-weight: bold;
            color: #ff6600;
            text-align: center;
        }

        /* ===== KILLS ===== */
        .kills-container {
            position: fixed;
            top: 50%;
            right: 30px;
            background: rgba(0, 0, 0, 0.85);
            padding: 15px 25px;
            border-radius: 8px;
            border: 2px solid #ff3333;
            z-index: 50;
            transform: translateY(-50%);
            backdrop-filter: blur(10px);
        }

        .kills-label {
            font-size: 11px;
            color: #ff3333;
            text-transform: uppercase;
            margin-bottom: 5px;
            font-weight: bold;
        }

        .kills-value {
            font-size: 22px;
            font-weight: bold;
            color: #ff3333;
            text-align: center;
        }

        /* ===== MINIMAP ===== */
        .minimap-canvas {
            position: fixed;
            bottom: 30px;
            left: 330px;
            border: 2px solid #00ff00;
            border-radius: 8px;
            display: block;
            z-index: 50;
            background: rgba(0, 0, 0, 0.9);
            box-shadow: 0 0 15px rgba(0, 255, 0, 0.3);
        }

        /* ===== LOADING ===== */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            z-index: 300;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: #00ff00;
        }

        .loading-content {
            text-align: center;
        }

        .loading-text {
            font-size: 24px;
            margin-bottom: 20px;
            text-transform: uppercase;
            font-weight: bold;
        }

        .loading-bar {
            width: 300px;
            height: 10px;
            background: rgba(0, 255, 0, 0.2);
            border: 2px solid #00ff00;
            border-radius: 5px;
            overflow: hidden;
        }

        .loading-fill {
            height: 100%;
            background: #00ff00;
            animation: loading 3s ease-in-out forwards;
            box-shadow: 0 0 10px #00ff00;
        }

        @keyframes loading {
            0% { width: 0%; }
            100% { width: 100%; }
        }

        /* ===== GAME OVER ===== */
        .game-over-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            z-index: 200;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(10px);
        }

        .game-over-screen.show {
            display: flex;
        }

        .game-over-content {
            text-align: center;
            animation: popIn 0.5s ease-out;
        }

        .game-over-content h1 {
            font-size: 48px;
            color: #ff3333;
            margin-bottom: 30px;
            text-transform: uppercase;
            text-shadow: 0 0 20px #ff3333;
        }

        .game-over-stats {
            font-size: 20px;
            margin: 15px 0;
            color: #00ff00;
        }

        .restart-btn {
            margin-top: 30px;
            padding: 15px 40px;
            font-size: 18px;
            background: linear-gradient(135deg, #ff3333, #ff5555);
            color: white;
            border: 2px solid #ff3333;
            border-radius: 5px;
            cursor: pointer;
            text-transform: uppercase;
            font-weight: bold;
            transition: all 0.3s;
            box-shadow: 0 0 20px rgba(255, 51, 51, 0.5);
        }

        .restart-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px rgba(255, 51, 51, 0.8);
        }

        @keyframes popIn {
            0% {
                opacity: 0;
                transform: scale(0.5);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }

        /* ===== FPS COUNTER ===== */
        .fps-counter {
            position: fixed;
            top: 10px;
            right: 10px;
            background: rgba(0, 0, 0, 0.85);
            padding: 10px 15px;
            border-radius: 5px;
            border: 1px solid #00ff00;
            color: #00ff00;
            font-size: 12px;
            font-weight: bold;
            z-index: 50;
        }

        /* ===== ANTICHEAT WARNING ===== */
        .anticheat-warning {
            position: fixed;
            top: 100px;
            right: 30px;
            background: rgba(255, 50, 50, 0.95);
            border: 2px solid #ff3333;
            padding: 15px 20px;
            border-radius: 8px;
            color: white;
            font-weight: bold;
            z-index: 100;
            animation: slideIn 0.5s ease-out;
            box-shadow: 0 0 20px rgba(255, 51, 51, 0.7);
        }

        @keyframes slideIn {
            from {
                transform: translateX(400px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        /* ===== RESPONSIVIDADE ===== */
        @media (max-width: 768px) {
            .health-container {
                width: 250px;
                bottom: 120px;
                left: 10px;
            }

            .ammo-container, .kills-container {
                padding: 10px 15px;
            }

            .minimap-canvas {
                display: none;
            }

            .hud-top {
                flex-direction: column;
                gap: 10px;
            }

            .kills-container {
                top: 20px;
                right: 10px;
                transform: none;
            }
        }
    </style>
</head>
<body>
    <div id="app"></div>
    
    <!-- HUD -->
    <div id="hud">
        <div class="mira">
            <div class="mira-dot"></div>
            <div class="mira-line mira-h"></div>
            <div class="mira-line mira-v"></div>
        </div>

        <div class="hud-top">
            <div class="hud-info">
                <div class="hud-label">Jogadores</div>
                <div class="hud-value" id="players-alive">50</div>
            </div>
            <div class="hud-info">
                <div class="hud-label">Zona</div>
                <div class="hud-value" id="safe-zone-radius">150m</div>
            </div>
        </div>

        <div class="health-container">
            <div class="hud-label">Saúde</div>
            <div class="health-bar">
                <div class="health-fill" id="health-fill" style="width: 100%;">100</div>
            </div>
            <div class="armor-bar">
                <div class="armor-fill" id="armor-fill" style="width: 100%;">100</div>
            </div>
        </div>

        <div class="ammo-container">
            <div class="ammo-label">Munição</div>
            <div class="ammo-value" id="ammo-value">30/150</div>
        </div>

        <div class="kills-container">
            <div class="kills-label">Abatidos</div>
            <div class="kills-value" id="kills-value">0</div>
        </div>

        <canvas id="minimap-canvas" class="minimap-canvas" width="180" height="180"></canvas>
        <div class="fps-counter" id="fps-counter">60 FPS</div>
    </div>

    <!-- Loading -->
    <div id="loading-screen" class="loading-screen">
        <div class="loading-content">
            <div class="loading-text">🎮 Preparando o mapa...</div>
            <div class="loading-bar">
                <div class="loading-fill"></div>
            </div>
        </div>
    </div>

    <!-- Game Over -->
    <div id="game-over-screen" class="game-over-screen">
        <div class="game-over-content">
            <h1>💀 DERROTADO</h1>
            <div class="game-over-stats">
                <p>Duração: <span id="game-over-time">0:00</span></p>
                <p>Inimigos: <span id="game-over-kills">0</span></p>
                <p>Posição: <span id="game-over-rank">50º</span></p>
            </div>
            <button class="restart-btn" onclick="location.reload()">Reiniciar</button>
        </div>
    </div>

    <!-- Scripts -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/cannon-es@0.20.0/dist/cannon-es.js"></script>

    <script>
        // ====== CONFIG DO DEVICE ======
        const isWebGL2 = !!document.createElement('canvas').getContext('webgl2');
        const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry/i.test(navigator.userAgent);
        const isLowEndDevice = navigator.deviceMemory < 4 || navigator.hardwareConcurrency < 4;

        window.DEVICE_CONFIG = {
            isWebGL2,
            isMobile,
            isLowEndDevice,
            maxDrawCalls: isMobile ? 500 : 2000
        };

        console.log(`%c🎮 Device: Mobile=${isMobile}, LowEnd=${isLowEndDevice}`, 'color: #00ff00; font-weight: bold;');

        // ====== CONFIG CENTRALIZADA ======
        const GAME_CONFIG = {
            map: { size: 200, fogNear: 300, fogFar: 500 },
            player: { maxHealth: 100, maxArmor: 100, maxAmmo: 150 },
            armor: { damageReduction: 0.5 },
            safeZone: { initialSize: 150, shrinkInterval: 30000, shrinkAmount: 0.85, damagePerSecond: 2 },
            enemies: { initialCount: 50, maxCount: isMobile ? 15 : 30, spawnRate: 3000 },
            antiCheat: {
                enabled: true,
                maxSpeed: 0.3,
                maxAccuracy: 0.95,
                maxHeadshotRate: 0.8,
                positionCheckInterval: 500,
                banThreshold: 100,
                suspiciousThreshold: 50,
                allowLocalBan: true
            },
            performance: {
                enableShadows: !isMobile,
                shadowMapSize: isMobile ? 1024 : 2048,
                enableFog: true,
                targetFPS: isLowEndDevice ? 30 : 60
            }
        };

        // ====== LOGGER ======
        class Logger {
            constructor(namespace = 'App') {
                this.namespace = namespace;
            }
            info(msg, data) {
                console.log(`%c[${this.namespace}] ${msg}`, 'color: #00ff00; font-weight: bold;', data || '');
            }
            warn(msg, data) {
                console.warn(`%c[${this.namespace}] ${msg}`, 'color: #ffaa00; font-weight: bold;', data || '');
            }
            error(msg, data) {
                console.error(`%c[${this.namespace}] ${msg}`, 'color: #ff3333; font-weight: bold;', data || '');
            }
        }

        // ====== EVENT MANAGER ======
        class EventManager {
            constructor() {
                this.events = {};
            }
            on(event, callback) {
                if (!this.events[event]) this.events[event] = [];
                this.events[event].push(callback);
            }
            emit(event, data) {
                if (this.events[event]) {
                    this.events[event].forEach(cb => {
                        try { cb(data); } catch (e) { console.error(`Erro em ${event}:`, e); }
                    });
                }
            }
        }

        // ====== ANTI-CHEAT SYSTEM 🔒 ======
        class AntiCheatSystem {
            constructor(config, eventManager, gameManager) {
                this.logger = new Logger('AntiCheat');
                this.config = config.antiCheat;
                this.eventManager = eventManager;
                this.gameManager = gameManager;

                this.playerStats = {
                    totalShots: 0,
                    totalHits: 0,
                    accuracy: 0,
                    suspicionScore: 0,
                    flags: [],
                    banned: false,
                    warnings: 0
                };

                this.checks = {
                    lastPositionCheck: Date.now(),
                    positionHistory: []
                };

                this.bannedPlayers = this.loadBannedPlayers();
            }

            update(deltaTime, player) {
                if (!this.config.enabled || !player) return;

                const now = Date.now();
                if (now - this.checks.lastPositionCheck > this.config.positionCheckInterval) {
                    this.checkPosition(player);
                    this.checks.lastPositionCheck = now;
                }

                this.updateSuspicionScore();

                if (this.playerStats.suspicionScore >= this.config.banThreshold) {
                    this.banPlayer('Limite de suspeição excedido');
                } else if (this.playerStats.suspicionScore >= this.config.suspiciousThreshold) {
                    this.warnPlayer();
                }
            }

            checkPosition(player) {
                const pos = player.position;

                // Fora do mapa
                if (Math.abs(pos.x) > this.gameManager.config.map.size / 2 || Math.abs(pos.z) > this.gameManager.config.map.size / 2) {
                    this.flag('POSITION_OUT_OF_BOUNDS', 50);
                }

                // Teleporte
                if (this.checks.positionHistory.length > 0) {
                    const lastPos = this.checks.positionHistory[this.checks.positionHistory.length - 1];
                    const distance = pos.distanceTo(lastPos);
                    if (distance > 5) {
                        this.flag('IMPOSSIBLE_TELEPORT', 75);
                    }
                }

                this.checks.positionHistory.push(pos.clone());
                if (this.checks.positionHistory.length > 10) {
                    this.checks.positionHistory.shift();
                }
            }

            recordShot(accuracy) {
                this.playerStats.totalShots++;
                if (accuracy > 0.5) this.playerStats.totalHits++;
                this.playerStats.accuracy = this.playerStats.totalHits / this.playerStats.totalShots;

                if (this.playerStats.accuracy > this.config.maxAccuracy) {
                    this.flag('IMPOSSIBLE_ACCURACY', 40);
                }
            }

            flag*

