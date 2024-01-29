# Odmh31
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Thumbnail Fetcher</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        h1 {
            text-align: center;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input, button {
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
            margin-bottom: 10px;
        }
        button {
            background-color: #3498db;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        #thumbnailContainer {
            margin-top: 20px;
        }
        img {
            max-width: 100%;
            height: auto;
            display: block;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <h1>YouTube Thumbnail Fetcher</h1>
    <label for="videoId">Enter YouTube Video ID:</label>
    <input type="text" id="videoId" placeholder="Video ID">
    <button onclick="getThumbnail('default')">Get Default Thumbnail</button>
    <button onclick="getThumbnail('high')">Get High Quality Thumbnail</button>
    <button onclick="getThumbnail('maxres')">Get Maximum Resolution Thumbnail</button>
    <div id="thumbnailContainer"></div>

    <script>
        function getThumbnail(quality) {
            const videoId = document.getElementById('videoId').value;
            const apiKey =  yk m'YOUR_API_KEY'; // Replace with your actual API key

            const thumbnailContainer = document.getElementById('thumbnailContainer');
            thumbnailContainer.innerHTML = '';

            const img = document.createElement('img');
            img.alt = 'YouTube Thumbnail';

            const apiUrl = `https://www.googleapis.com/youtube/v3/videos?part=snippet&id=${videoId}&key=${apiKey}`;
            
            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    let thumbnailUrl;
                    switch (quality) {
                        case 'high':
                            thumbnailUrl = data.items[0].snippet.thumbnails.high.url;
                            break;
                        case 'maxres':
                            thumbnailUrl = data.items[0].snippet.thumbnails.maxres.url;
                            break;
                        default:
                            thumbnailUrl = data.items[0].snippet.thumbnails.default.url;
                            break;
                    }
                    img.src = thumbnailUrl;
                    thumbnailContainer.appendChild(img);
                })
                .catch(error => console.error('Error fetching thumbnail:', error));
        }
    </script>
</body>
</html>
