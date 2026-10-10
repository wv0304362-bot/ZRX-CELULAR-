<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel de Rastreamento - Find My Device</title>
    <style>
        :root {
            background-color: #121212;
            color: #e0e0e0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
        }
        .container {
            width: 100%;
            max-width: 400px;
            background: #1e1e1e;
            padding: 25px;
            border-radius: 16px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            text-align: center;
        }
        h2 {
            color: #4285F4;
            margin-bottom: 10px;
        }
        p {
            font-size: 14px;
            color: #aaa;
            margin-bottom: 25px;
        }
        .btn {
            display: block;
            width: 100%;
            padding: 14px;
            margin: 12px 0;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            box-sizing: border-box;
            transition: background 0.3s;
        }
        .btn-google {
            background-color: #4285F4;
            color: white;
        }
        .btn-google:hover {
            background-color: #3367D6;
        }
        .btn-local {
            background-color: #34A853;
            color: white;
        }
        .btn-local:hover {
            background-color: #2e8b57;
        }
        #info-localizacao {
            margin-top: 20px;
            font-size: 13px;
            background: #2a2a2a;
            padding: 10px;
            border-radius: 6px;
            display: none;
            text-align: left;
            word-break: break-all;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Localizador Android</h2>
        <p>Gerencie seus dispositivos conectados ou obtenha a posição atual deste aparelho.</p>

        <!-- Botão que redireciona para o Google Find My Device oficial -->
        <a href="https://www.google.com/android/find/" target="_blank" class="btn btn-google">
            Abrir Google Find My Device
        </a>

        <!-- Botão para capturar coordenadas locais via API do navegador -->
        <button class="btn btn-local" onclick="pegarLocalizacaoAtual()">
            Ver Coordenadas Deste Aparelho
        </button>

        <div id="info-localizacao"></div>
    </div>

    <script>
        function pegarLocalizacaoAtual() {
            const box = document.getElementById("info-localizacao");
            box.style.display = "block";
            box.innerHTML = "Buscando localização via GPS...";

            if (!navigator.geolocation) {
                box.innerHTML = "Erro: Geolocalização não é suportada pelo seu navegador.";
                return;
            }

            navigator.geolocation.getCurrentPosition(
                (pos) => {
                    const lat = pos.coords.latitude;
                    const lon = pos.coords.longitude;
                    box.innerHTML = `<b>Latitude:</b> ${lat}<br>` +
                                    `<b>Longitude:</b> ${lon}<br>` +
                                    `<a href="https://maps.google.com/?q=${lat},${lon}" target="_blank" style="color: #8ab4f8; display:inline-block; margin-top:8px;">Abrir no Google Maps</a>`;
                },
                (err) => {
                    box.innerHTML = "Erro ao obter localização. Verifique as permissões de GPS do navegador.";
                },
                { enableHighAccuracy: true, timeout: 10000 }
            );
        }
    </script>

</body>
</html>
