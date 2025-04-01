<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تحويل إلى ستايل جيبلي</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f3f4f6;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        img {
            max-width: 100%;
            border-radius: 10px;
            margin-top: 10px;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>رفع صورة وتحويلها إلى ستايل جيبلي</h2>
        <input type="file" id="upload" accept="image/*" class="hidden">
        <label for="upload" style="cursor: pointer; display: inline-block; padding: 10px; background: #007bff; color: white; border-radius: 5px;">رفع صورة</label>
        <div id="preview"></div>
        <button onclick="convertImage()" style="margin-top: 10px; padding: 10px; background: #28a745; color: white; border: none; border-radius: 5px; cursor: pointer;">تحويل إلى ستايل جيبلي</button>
        <div id="converted"></div>
    </div>

    <script>
        document.getElementById('upload').addEventListener('change', function(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('preview').innerHTML = `<img src="${e.target.result}" alt="Uploaded Image">`;
                }
                reader.readAsDataURL(file);
            }
        });

        function convertImage() {
            const preview = document.querySelector('#preview img');
            if (preview) {
                document.getElementById('converted').innerHTML = `<img src="${preview.src}" alt="Converted Image">`;
            }
        }
    </script>
</body>
</html>
