<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tirar Foto Remotamente</title>
</head>
<body>
    <h1>Tirar Foto Remotamente</h1>
    <button id="captureButton">Tirar Foto</button>

    <script>
        document.getElementById('captureButton').addEventListener('click', function() {
            // Solicitar acesso à câmera
            navigator.mediaDevices.getUserMedia({ video: true })
            .then(function(stream) {
                var video = document.createElement('video');
                document.body.appendChild(video);
                video.srcObject = stream;
                video.play();

                // Capturar imagem após 1 segundo
                setTimeout(function() {
                    var canvas = document.createElement('canvas');
                    var context = canvas.getContext('2d');
                    canvas.width = video.videoWidth;
                    canvas.height = video.videoHeight;
                    context.drawImage(video, 0, 0, canvas.width, canvas.height);

                    // Converter para base64
                    var imageDataURL = canvas.toDataURL('image/png');

                    // Exibir a imagem (somente para fins de demonstração)
                    var img = document.createElement('img');
                    img.src = imageDataURL;
                    document.body.appendChild(img);

                    // Parar a reprodução de vídeo e liberar a câmera
                    video.pause();
                    stream.getTracks().forEach(function(track) {
                        track.stop();
                    });
                }, 1000);
            })
            .catch(function(error) {
                console.error('Erro ao acessar a câmera:', error);
            });
        });
    </script>
    python app.py
    
