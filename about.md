---
layout: single
title: "About"
permalink: /about/
author_profile: true
classes: wide
---

About me, CV

<head>
  <meta charset="UTF-8">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.14.305/pdf.min.js"></script>
  <style>
    body {
      margin: 0;
      background: #fff;
      display: flex;
      min-height: 100vh;
    }
    canvas {
      display: block;
      width: auto;
      max-width: 100%;
      height: auto;
      border: none;
    }
  </style>
</head>
<body>
  <canvas id="pdf-canvas"></canvas>
  <script>
    const url = '/assets/pdfs/cv.pdf';
    pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.14.305/pdf.worker.min.js';
    pdfjsLib.getDocument(url).promise.then(pdf => {
      return pdf.getPage(1);
    }).then(page => {
      const scale = 3;
      const viewport = page.getViewport({ scale });
      const canvas = document.getElementById('pdf-canvas');
      const context = canvas.getContext('2d');
      const crop = {
        x: 165,
        y: 100,
        width: viewport.width - 100,
        height: viewport.height - 100
      };
      canvas.width = crop.width;
      canvas.height = crop.height;
      context.translate(-crop.x, -crop.y);
      page.render({
        canvasContext: context,
        viewport: viewport
      });
    });
  </script>
</body>