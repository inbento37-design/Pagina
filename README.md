<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tarea Tecnología 9-2 - I.E. Barrio Santa Margaritas</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        body {
            background-color: #1a1a1a;
            color: #ffffff;
            padding: 30px 15px;
            text-align: center;
        }

        .encabezado {
            background-color: #ffb700;
            color: #111111;
            padding: 20px;
            border-radius: 16px;
            margin-bottom: 30px;
        }

        .contenedor {
            max-width: 750px;
            margin: 0 auto;
        }

        .caja {
            background-color: #2d2d2d;
            border-radius: 16px;
            padding: 25px;
            margin-bottom: 25px;
        }

        h2 {
            color: #ffcc00;
            margin-bottom: 15px;
        }

        p {
            font-size: 18px;
            line-height: 1.6;
        }

        .imagen {
            width: 280px;
            height: 280px;
            border-radius: 14px;
            margin: 15px 0;
            object-fit: cover;
        }

        .ruleta-contenedor{
            position:relative;
            width:320px;
            height:320px;
            margin:20px auto;
        }
        #ruleta{
            width:100%;
            height:100%;
            border-radius:50%;
            border:6px solid white;
            transition: transform 4s cubic-bezier(0.2, 0.9, 0.2, 1);
        }
        .indicador{
            position:absolute;
            top:0;
            left:50%;
            transform:translateX(-50%);
            font-size:50px;
            z-index:10;
        }
        button{
            padding:14px 28px;
            font-size:20px;
            background:#ffb700;
            color:#111;
            border:none;
            border-radius:12px;
            cursor:pointer;
            font-weight:bold;
            margin-top:15px;
        }
        #resultado{
            font-size:28px;
            color:#ffcc00;
            margin-top:15px;
            font-weight:bold;
        }
    </style>
</head>
<body>
    <div class="contenedor">
        <div class="encabezado">
            <h1>📚 Tarea de Tecnología</h1>
            <h2>I.E. Barrio Santa Margaritas</h2>
            <h3>Grado 9 - 2</h3>
            <h4>Profesor Julián Arenas</h4>
        </div>

        <div class="caja">
            <h2>🎡 Ruleta Giratoria del 1 al 10</h2>
            <div class="ruleta-contenedor">
                <div class="indicador">▼</div>
                <svg id="ruleta" viewBox="0 0 100 100">
                    <path d="M50,50 L50,0 A50,50 0 0,1 80.90,9.55 Z" fill="#e74c3c"/>
                    <path d="M50,50 L80.90,9.55 A50,50 0 0,1 96.18,30.90 Z" fill="#3498db"/>
                    <path d="M50,50 L96.18,30.90 A50,50 0 0,1 96.18,69.10 Z" fill="#2ecc71"/>
                    <path d="M50,50 L96.18,69.10 A50,50 0 0,1 80.90,90.45 Z" fill="#f39c12"/>
                    <path d="M50,50 L80.90,90.45 A50,50 0 0,1 50,100 Z" fill="#9b59b6"/>
                    <path d="M50,50 L50,100 A50,50 0 0,1 19.10,90.45 Z" fill="#1abc9c"/>
                    <path d="M50,50 L19.10,90.45 A50,50 0 0,1 3.82,69.10 Z" fill="#e67e22"/>
                    <path d="M50,50 L3.82,69.10 A50,50 0 0,1 3.82,30.90 Z" fill="#34495e"/>
                    <path d="M50,50 L3.82,30.90 A50,50 0 0,1 19.10,9.55 Z" fill="#c0392b"/>
                    <path d="M50,50 L19.10,9.55 A50,50 0 0,1 50,0 Z" fill="#16a085"/>
                    <text x="62" y="12" fill="white" font-size="4">1</text>
                    <text x="84" y="26" fill="white" font-size="4">2</text>
                    <text x="86" y="54" fill="white" font-size="4">3</text>
                    <text x="78" y="80" fill="white" font-size="4">4</text>
                    <text x="54" y="88" fill="white" font-size="4">5</text>
                    <text x="26" y="82" fill="white" font-size="4">6</text>
                    <text x="12" y="56" fill="white" font-size="4">7</text>
                    <text x="14" y="30" fill="white" font-size="4">8</text>
                    <text x="28" y="12" fill="white" font-size="4">9</text>
                    <text x="46" y="10" fill="white" font-size="4">10</text>
                </svg>
            </div>
            <button onclick="girarRuleta()">🎯 GIRAR LA RULETA</button>
            <div id="resultado"></div>
        </div>

        <div class="caja">
            <h2>🟡 Monstruo de Plastilina 3D</h2>
            <img class="imagen" src="https://i.imgur.com/9FkL7sD.png" alt="Monstruo plastilina 3D">
            <p>Los modelos en plastilina 3D nos permiten dar volumen y forma física a nuestras ideas, desarrollando nuestra creatividad, la coordinación manual y la percepción de las tres dimensiones. Podemos crear cualquier monstruo o criatura que imaginemos.</p>
        </div>

        <div class="caja">
            <h2>📌 ¿Para qué se utiliza la ruleta?</h2>
            <p>La ruleta es un objeto circular giratorio que se usa para seleccionar opciones al azar, realizar sorteos, asignar turnos, tomar decisiones y crear juegos didácticos de forma divertida e imparcial.</p>
        </div>
    </div>

    <script>
        const ruleta = document.getElementById('ruleta');
        const resultado = document.getElementById('resultado');
        let rotacionTotal = 0;
        const gradosPorNumero = 36;

        function girarRuleta(){
            resultado.textContent = "";
            document.querySelector("button").disabled = true;

            const numeroElegido = Math.floor(Math.random() * 10) + 1;
            const vueltasCompletas = 6 + Math.random() * 5;
            rotacionTotal = vueltasCompletas * 360 + ((numeroElegido - 1) * gradosPorNumero);
            ruleta.style.transform = `rotate(${rotacionTotal}deg)`;

            setTimeout(()=>{
                resultado.textContent = "🎉 ¡Salió el número: " + numeroElegido + "!";
                document.querySelector("button").disabled = false;
            }, 4200);
        }
    </script>
</body>
</html>
