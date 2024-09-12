<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplicativo de Pânico</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #FFC0CB;
            text-align: center;
            padding-top: 50px;
        }
        #panicButton {
            background-color: #FF0000;
            color: white;
            font-size: 20px;
            padding: 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        #panicButton:hover {
            background-color: #cc0000;
        }
        #confirmationPopup, #emergencyPopup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border: 2px solid #000;
            z-index: 10;
        }
        #overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: none;
            z-index: 5;
        }
    </style>
</head>
<body>

    <h1>Olá!</h1>
    <button id="panicButton">Botão de Pânico</button>

    <div id="confirmationPopup">
        <p>Tem certeza da ação?</p>
        <button onclick="confirmAction()">Confirmar</button>
        <button onclick="cancelAction()">Cancelar</button>
    </div>

    <div id="emergencyPopup">
        <p>Chamada de emergência iniciada.</p>
        <button onclick="closeEmergencyPopup()">Fechar</button>
    </div>

    <div id="overlay"></div>

    <script>
        const panicButton = document.getElementById('panicButton');
        const confirmationPopup = document.getElementById('confirmationPopup');
        const emergencyPopup = document.getElementById('emergencyPopup');
        const overlay = document.getElementById('overlay');
        let emergencyTimeout;

        panicButton.addEventListener('click', () => {
            overlay.style.display = 'block';
            confirmationPopup.style.display = 'block';
            emergencyTimeout = setTimeout(performEmergencyAction, 5000); // 5 segundos para acionar
        });

        function confirmAction() {
            clearTimeout(emergencyTimeout);
            performEmergencyAction();
        }

        function cancelAction() {
            clearTimeout(emergencyTimeout);
            confirmationPopup.style.display = 'none';
            overlay.style.display = 'none';
        }

        function performEmergencyAction() {
            confirmationPopup.style.display = 'none';
            emergencyPopup.style.display = 'block';
            overlay.style.display = 'block';
            window.open('tel:+55190'); // Disca o número de emergência
        }

        function closeEmergencyPopup() {
            emergencyPopup.style.display = 'none';
            overlay.style.display = 'none';
        }
    </script>

</body>
</html>
