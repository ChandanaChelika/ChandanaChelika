Here's the Markdown Notes App with everything combined into a single index.html file:


---

index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Markdown Notes App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        textarea {
            width: 80%;
            height: 100px;
            margin-bottom: 10px;
        }
        button {
            padding: 5px 10px;
            margin-bottom: 20px;
        }
        #preview {
            border: 1px solid #ccc;
            padding: 10px;
            width: 80%;
            margin: auto;
            text-align: left;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            background: #f4f4f4;
            padding: 5px;
            margin: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Markdown Notes</h1>
    <textarea id="noteInput" placeholder="Write your markdown here..."></textarea>
    <button onclick="saveNote()">Save</button>
    <h2>Preview</h2>
    <div id="preview"></div>
    <h2>Saved Notes</h2>
    <ul id="notesList"></ul>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/marked/4.3.0/marked.min.js"></script>
    <script>
        document.getElementById('noteInput').addEventListener('input', updatePreview);

        function updatePreview() {
            let inputText = document.getElementById('noteInput').value;
            document.getElementById('preview').innerHTML = marked.parse(inputText);
        }

        function saveNote() {
            let notes = JSON.parse(localStorage.getItem('notes')) || [];
            let inputText = document.getElementById('noteInput').value;
            if (inputText.trim()) {
                notes.push(inputText);
                localStorage.setItem('notes', JSON.stringify(notes));
                document.getElementById('noteInput').value = '';
                updatePreview();
                loadNotes();
            }
        }

        function loadNotes() {
            let notes = JSON.parse(localStorage.getItem('notes')) || [];
            let notesList = document.getElementById('notesList');
            notesList.innerHTML = '';
            notes.forEach((note, index) => {
                let li = document.createElement('li');
                li.innerHTML = marked.parse(note);
                li.onclick = () => loadNoteToEdit(index);
                notesList.appendChild(li);
            });
        }

        function loadNoteToEdit(index) {
            let notes = JSON.parse(localStorage.getItem('notes'));
            document.getElementById('noteInput').value = notes[index];
            updatePreview();
        }

        window.onload = loadNotes;
    </script>
</body>


