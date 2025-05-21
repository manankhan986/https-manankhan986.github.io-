<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Convert JPG images to PDF online instantly. 100% free, fast, and secure tool. No signup needed. Works on mobile and desktop." />
  <title>Smart JPG to PDF Converter - Free Online Image to PDF Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f8f9fa;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    header {
      background-color: #dc3545;
      color: white;
      padding: 1rem 2rem;
      width: 100%;
      text-align: center;
    }
    main {
      max-width: 600px;
      margin: 2rem;
      text-align: center;
      background: white;
      padding: 2rem;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
    }
    input[type="file"] {
      margin: 1rem 0;
    }
    button {
      background-color: #28a745;
      color: white;
      padding: 0.75rem 1.5rem;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    footer {
      margin-top: 2rem;
      text-align: center;
      color: #888;
    }
  </style>
</head>
<body>
  <header>
    <h1>Smart JPG to PDF Converter</h1>
  </header>
  <main>
    <h2>Convert JPG to PDF Instantly</h2>
    <p>Select JPG images to convert into a single PDF file.</p>
    <input type="file" id="jpgInput" multiple accept="image/jpeg">
    <br />
    <button onclick="convertToPDF()">Convert to PDF</button>
    <p id="status"></p>
  </main>
  <footer>
    <p>&copy; 2025 Smart JPG to PDF Converter. All rights reserved.</p>
  </footer>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script>
    async function convertToPDF() {
      const input = document.getElementById('jpgInput');
      const status = document.getElementById('status');
      const { jsPDF } = window.jspdf;
      if (input.files.length === 0) {
        alert('Please select JPG images.');
        return;
      }
      const pdf = new jsPDF();
      status.innerText = 'Converting...';
      for (let i = 0; i < input.files.length; i++) {
        const file = input.files[i];
        const imgData = await readFileAsDataURL(file);
        if (i > 0) pdf.addPage();
        pdf.addImage(imgData, 'JPEG', 10, 10, 190, 270);
      }
      pdf.save('converted-images.pdf');
      status.innerText = 'Done! Your PDF has been downloaded.';
    }

    function readFileAsDataURL(file) {
      return new Promise((resolve) => {
        const reader = new FileReader();
        reader.onload = (e) => resolve(e.target.result);
        reader.readAsDataURL(file);
      });
    }
  </script>
</body>
</html>
