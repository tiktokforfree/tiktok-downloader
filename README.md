
<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>TikTok Video Downloader</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet"/>
</head>
<body class="bg-gray-100">
  <div class="max-w-xl mx-auto mt-20 p-6 bg-white rounded-2xl shadow-lg text-center">
    <h1 class="text-3xl font-bold mb-4">TikTok Video Downloader</h1>
    <p class="mb-6 text-gray-600">Paste a TikTok link below to download the video.</p>
    <input id="videoUrl" type="text" placeholder="https://www.tiktok.com/..." class="w-full p-3 border rounded mb-4" />
    <button onclick="downloadVideo()" class="bg-blue-600 text-white px-6 py-3 rounded hover:bg-blue-700">Download</button>
    <div id="result" class="mt-6"></div>
  </div>  <script>
    async function downloadVideo() {
      const url = document.getElementById('videoUrl').value;
      const result = document.getElementById('result');
      result.innerHTML = "Fetching video...";

      try {
        const response = await fetch('https://api.tiktokdownloader.live/api/download', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ url })
        });

        const data = await response.json();

        if (data && data.downloadUrl) {
          result.innerHTML = `<a href="${data.downloadUrl}" class="text-blue-600 underline" target="_blank">Click here to download</a>`;
        } else {
          result.innerHTML = "Failed to fetch video. Try another link.";
        }
      } catch (error) {
        console.error(error);
        result.innerHTML = "Error fetching video.";
      }
    }
  </script></body>
</html>
