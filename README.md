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

        async function convertImage() {
            const preview = document.querySelector('#preview img');
            if (!preview) return alert("الرجاء رفع صورة أولًا!");

            const formData = new FormData();
            formData.append("image", preview.src); // تأكد من طريقة إضافة الصورة بشكل صحيح

            try {
                const response = await fetch("https://api.deepai.org/api/deepdream", {
                    method: "POST",
                    headers: {
                        "Api-Key": "417e5ef1-0cfc-4960-9785-b24f4b61e577" // استبدل هذا بمفتاحك
                    },
                    body: formData
                });

                if (!response.ok) {
                    throw new Error('هناك خطأ في الاتصال بـ API');
                }

                const data = await response.json();
                if (data && data.output_url) {
                    document.getElementById('converted').innerHTML = `<img src="${data.output_url}" alt="Converted Image">`;
                } else {
                    throw new Error('لم يتم العثور على الصورة المحولة');
                }
            } catch (error) {
                console.error("Error:", error);
                alert("حدث خطأ أثناء المعالجة: " + error.message);
            }
        }
    </script>
</body>
</html>
