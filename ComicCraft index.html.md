```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>ComicCraft - AI Comic Story Creator</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            background: #f4f1ff;
            color: #222;
        }

        header {
            background: linear-gradient(135deg, #6c2bd9, #9b59ff);
            color: white;
            padding: 30px;
            text-align: center;
        }

        header h1 {
            font-size: 38px;
            margin-bottom: 8px;
        }

        header p {
            font-size: 17px;
        }

        .container {
            width: 90%;
            max-width: 1100px;
            margin: 30px auto;
        }

        .card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
        }

        .card h2 {
            color: #6c2bd9;
            margin-bottom: 20px;
        }

        label {
            display: block;
            font-weight: bold;
            margin: 15px 0 7px;
        }

        input,
        textarea,
        select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 15px;
        }

        textarea {
            height: 120px;
            resize: vertical;
        }

        .row {
            display: flex;
            gap: 20px;
        }

        .row div {
            flex: 1;
        }

        button {
            margin-top: 20px;
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 8px;
            background: #6c2bd9;
            color: white;
            font-size: 17px;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            background: #5420ae;
        }

        #loading {
            display: none;
            text-align: center;
            padding: 20px;
            color: #6c2bd9;
            font-weight: bold;
        }

        .comic-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }

        .panel {
            border: 3px solid #222;
            border-radius: 10px;
            overflow: hidden;
            background: white;
        }

        .panel-image {
            height: 200px;
            background: linear-gradient(135deg, #ddd, #eee);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 55px;
        }

        .panel-content {
            padding: 15px;
        }

        .panel-content h3 {
            color: #6c2bd9;
            margin-bottom: 8px;
        }

        .speech {
            background: #fff;
            border: 2px solid #222;
            border-radius: 15px;
            padding: 10px;
            margin-top: 10px;
            font-style: italic;
        }

        footer {
            text-align: center;
            padding: 20px;
            background: #222;
            color: white;
            margin-top: 40px;
        }

        @media (max-width: 700px) {
            .row,
            .comic-grid {
                display: block;
            }

            .panel {
                margin-bottom: 20px;
            }

            header h1 {
                font-size: 30px;
            }
        }
    </style>
</head>

<body>

<header>
    <h1>🎨 ComicCraft</h1>
    <p>AI Comic Story Creator using Gemini Models</p>
</header>

<div class="container">

    <div class="card">

        <h2>✨ Create Your Comic</h2>

        <label for="title">Comic Title</label>

        <input
            type="text"
            id="title"
            placeholder="Enter your comic title"
        >

        <label for="story">Story Idea</label>

        <textarea
            id="story"
            placeholder="Example: A young superhero discovers a mysterious power..."
        ></textarea>

        <div class="row">

            <div>
                <label for="genre">Genre</label>

                <select id="genre">
                    <option>Adventure</option>
                    <option>Fantasy</option>
                    <option>Science Fiction</option>
                    <option>Comedy</option>
                    <option>Horror</option>
                    <option>Superhero</option>
                    <option>Romance</option>
                </select>
            </div>

            <div>
                <label for="panels">Number of Panels</label>

                <select id="panels">
                    <option value="4">4 Panels</option>
                    <option value="6">6 Panels</option>
                    <option value="8">8 Panels</option>
                </select>
            </div>

        </div>

        <label for="character">Main Character</label>

        <input
            type="text"
            id="character"
            placeholder="Example: Arjun - a brave college student"
        >

        <button onclick="generateComic()">
            🚀 Generate Comic
        </button>

        <div id="loading">
            🤖 Creating your comic...
        </div>

    </div>


    <div class="card" id="comicSection" style="display:none;">

        <h2 id="comicTitle">Your AI Comic</h2>

        <div class="comic-grid" id="comicGrid"></div>

    </div>

</div>


<footer>
    <p>© 2026 ComicCraft | AI Comic Story Creator</p>
</footer>


<script>

function generateComic() {

    const title =
        document.getElementById("title").value ||
        "My AI Comic";

    const story =
        document.getElementById("story").value ||
        "An exciting adventure begins.";

    const genre =
        document.getElementById("genre").value;

    const character =
        document.getElementById("character").value ||
        "A brave hero";

    const panelCount =
        parseInt(document.getElementById("panels").value);

    const loading =
        document.getElementById("loading");

    const comicSection =
        document.getElementById("comicSection");

    const comicGrid =
        document.getElementById("comicGrid");

    const comicTitle =
        document.getElementById("comicTitle");


    loading.style.display = "block";

    comicSection.style.display = "none";

    comicGrid.innerHTML = "";


    setTimeout(() => {

        loading.style.display = "none";

        comicSection.style.display = "block";

        comicTitle.innerHTML =
            "📖 " + title;


        const scenes = [
            "The adventure begins...",
            "A mysterious event changes everything...",
            "The hero discovers a hidden secret...",
            "A powerful enemy appears...",
            "The hero faces a difficult challenge...",
            "The final battle begins...",
            "The hero discovers their true power...",
            "The story reaches an exciting ending..."
        ];


        for (let i = 0; i < panelCount; i++) {

            const panel =
                document.createElement("div");

            panel.className = "panel";

            panel.innerHTML = `

                <div class="panel-image">
                    🖼️
                </div>

                <div class="panel-content">

                    <h3>Panel ${i + 1}</h3>

                    <p>
                        <strong>${character}</strong>
                        - ${scenes[i % scenes.length]}
                    </p>

                    <div class="speech">
                        "${i === 0
                            ? story
                            : "What happens next?"}"
                    </div>

                </div>

            `;

            comicGrid.appendChild(panel);
        }

    }, 1500);
}

</script>

</body>
</html>
```