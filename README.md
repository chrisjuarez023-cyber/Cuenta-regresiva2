<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cuenta Regresiva Estelar</title>
    <style>
        body {
            background-color: #000; /* Fondo Negro Profundo */
            color: #fff;
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden; /* Evita que las estrellas creen barras de scroll */
        }

        h1 {
            font-size: 2.5rem;
            text-shadow: 0 0 15px #fff, 0 0 30px #4e54c8;
            z-index: 10;
        }

        .countdown-container {
            display: flex;
            gap: 15px;
            z-index: 10;
        }

        .segment {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.3);
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            min-width: 90px;
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
        }

        .number { font-size: 3.5rem; font-weight: bold; display: block; color: #f0f0f0; }
        .label { font-size: 0.8rem; text-transform: uppercase; letter-spacing: 2px; }

        /* Estilo de las estrellas */
        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            box-shadow: 0 0 10px white, 0 0 20px white;
            animation: twinkle 2s infinite ease-in-out;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.3; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.2); }
        }
    </style>
</head>
<body>

    <h1 id="title">Destino Estelar: 25 de Marzo</h1>

    <div class="countdown-container">
        <div class="segment">
            <span class="number" id="days">00</span>
            <span class="label">Días</span>
        </div>
        <div class="segment">
            <span class="number" id="hours">00</span>
            <span class="label">Hrs</span>
        </div>
        <div class="segment">
            <span class="number" id="minutes">00</span>
            <span class="label">Min</span>
        </div>
        <div class="segment">
            <span class="number" id="seconds">00</span>
            <span class="label">Seg</span>
        </div>
    </div>

    <script>
        // CONFIGURACIÓN DE FECHA
        const targetDate = new Date("March 25, 2026 00:00:00").getTime();

        function update() {
            const now = new Date().getTime();
            const diff = targetDate - now;

            const d = Math.floor(diff / (1000 * 60 * 60 * 24));
            const h = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const s = Math.floor((diff % (1000 * 60)) / 1000);

            document.getElementById("days").innerText = d;
            document.getElementById("hours").innerText = h;
            document.getElementById("minutes").innerText = m;
            document.getElementById("seconds").innerText = s;

            if (diff < 0) {
                document.querySelector(".countdown-container").innerHTML = "<h2>¡El cielo brilla hoy!</h2>";
            }
        }

        // LÓGICA DE LAS ESTRELLAS
        function createStars() {
            const now = new Date().getTime();
            const diff = targetDate - now;
            const daysLeft = Math.floor(diff / (1000 * 60 * 60 * 24));

            // Si faltan 25 días o menos
            if (daysLeft <= 25 && daysLeft >= 0) {
                // El número de estrellas será (25 - días restantes) + 1
                // Ejemplo: Si faltan 25 días, hay 1 estrella. Si faltan 24, hay 2...
                const starCount = (25 - daysLeft) + 1;

                for (let i = 0; i < starCount; i++) {
                    const star = document.createElement("div");
                    star.className = "star";
                    
                    // Posición aleatoria
                    const x = Math.random() * window.innerWidth;
                    const y = Math.random() * window.innerHeight;
                    const size = Math.random() * 3 + 1;

                    star.style.left = `${x}px`;
                    star.style.top = `${y}px`;
                    star.style.width = `${size}px`;
                    star.style.height = `${size}px`;
                    star.style.animationDelay = `${Math.random() * 2}s`;

                    document.body.appendChild(star);
                }
            }
        }

        setInterval(update, 1000);
        update();
        createStars(); // Se ejecuta al cargar para mostrar las estrellas ganadas
    </script>
</body>
</html>
