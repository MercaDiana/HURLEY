<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galería de Imágenes</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .gallery {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }
        .gallery img {
            width: 200px;
            height: 150px;
            object-fit: cover;
            margin: 10px;
            border-radius: 10px;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.2);
            cursor: pointer;
            transition: transform 0.3s ease-in-out;
        }
        .gallery img:hover {
            transform: scale(1.1);
        }
        .hidden { display: none; }
    </style>
</head>
<body>
    <h2>Sube tus imágenes</h2>
    <input type="file" id="fileInput" multiple accept="image/*">
    <button onclick="uploadImages()">Subir</button>
    <p id="message" class="hidden">No se ha seleccionado ninguna imagen.</p>
    <h3>Galería</h3>
    <div class="gallery" id="gallery"></div>

    <script>
        function uploadImages() {
            const input = document.getElementById('fileInput');
            const gallery = document.getElementById('gallery');
            const message = document.getElementById('message');

            if (input.files.length === 0) {
                message.classList.remove('hidden');
                return;
            } else {
                message.classList.add('hidden');
            }

            for (let file of input.files) {
                if (!file.type.startsWith('image/')) {
                    alert("Solo se permiten archivos de imagen.");
                    continue;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    img.onclick = function() {
                        if (confirm("¿Eliminar esta imagen?")) {
                            img.remove();
                        }
                    };
                    gallery.appendChild(img);
                };
                reader.readAsDataURL(file);
            }
        }
    </script>
</body>
</html>
