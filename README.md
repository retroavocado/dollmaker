<!-- DollzMaker - A Modern Static HTML Doll Maker Site with Drag-and-Drop -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DollzMaker</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css">
    <style>
        body { font-family: Arial, sans-serif; }
        .draggable { cursor: grab; }
        .dropzone { width: 300px; height: 500px; border: 2px dashed #ddd; position: relative; }
        .item { position: absolute; }
    </style>
</head>
<body class="bg-gray-100 p-6">

    <div class="max-w-4xl mx-auto">
        <div class="bg-white p-4 rounded-xl shadow-md mb-6">
            <h1 class="text-3xl font-bold mb-4">DollzMaker</h1>
            <div class="flex gap-4 mb-6">
                <div class="dropzone bg-white rounded-xl shadow p-4">
                    <h2 class="font-bold mb-2">Your Doll</h2>
                    <div id="doll-area" class="dropzone"></div>
                </div>
                <div>
                    <h2 class="font-bold">Drag & Drop Items</h2>
                    <img src="1.png" class="draggable" id="item-top" width="100" draggable="true" />
                </div>
            </div>
        </div>
    </div>

    <script>
        const dollArea = document.getElementById('doll-area');

        document.querySelectorAll('.draggable').forEach(item => {
            item.addEventListener('dragstart', dragStart);
        });

        dollArea.addEventListener('dragover', dragOver);
        dollArea.addEventListener('drop', drop);

        function dragStart(event) {
            event.dataTransfer.setData('text/plain', event.target.id);
        }

        function dragOver(event) {
            event.preventDefault();
        }

        function drop(event) {
            event.preventDefault();
            const id = event.dataTransfer.getData('text');
            const item = document.getElementById(id);
            const clone = item.cloneNode(true);
            clone.style.position = 'absolute';
            clone.style.left = `${event.offsetX - (clone.width / 2)}px`;
            clone.style.top = `${event.offsetY - (clone.height / 2)}px`;
            dollArea.appendChild(clone);
        }
    </script>

</body>
</html>
