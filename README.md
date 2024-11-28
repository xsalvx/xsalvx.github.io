<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Notepad</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f9f9f9;
            color: #333;
        }
        textarea {
            width: 100%;
            height: 300px;
            margin-bottom: 20px;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
            resize: vertical;
        }
        .image-preview {
            margin-top: 20px;
        }
        .image-preview img {
            max-width: 100%;
            max-height: 300px;
            margin-top: 10px;
            display: block;
        }
        input[type="file"] {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <h1>Simple Notepad with Image Upload</h1>
    <textarea id="notepad" placeholder="Type your notes here..."></textarea>
    <br>
    <label for="imageUpload">Upload an image:</label>
    <input type="file" id="imageUpload" accept="image/*">
    <div class="image-preview" id="imagePreview"></div>

    <script>
        // Save and restore text from local storage
        const notepad = document.getElementById('notepad');
        const savedText = localStorage.getItem('notepadText');
        if (savedText) {
            notepad.value = savedText;
        }
        notepad.addEventListener('input', () => {
            localStorage.setItem('notepadText', notepad.value);
        });

        // Handle image uploads
        const imageUpload = document.getElementById('imageUpload');
        const imagePreview = document.getElementById('imagePreview');

        imageUpload.addEventListener('change', () => {
            const file = imageUpload.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = () => {
                    const img = document.createElement('img');
                    img.src = reader.result;
                    imagePreview.innerHTML = ''; // Clear previous images
                    imagePreview.appendChild(img);
                };
                reader.readAsDataURL(file);
            }
        });
    </script>
</body>
</html>
