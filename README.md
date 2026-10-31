
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>AI Avatar Call</title>
<style>
body {
  background: #101522;
  color: white;
  font-family: Arial;
  text-align: center;
  padding: 25px;
}
main {
  max-width: 550px;
  margin: auto;
}
img, video {
  width: 100%;
  max-height: 350px;
  object-fit: cover;
  border-radius: 15px;
  background: #252a38;
}
button {
  padding: 12px 20px;
  margin: 8px;
  border: 0;
  border-radius: 8px;
  background: #526dff;
  color: white;
}
</style>
</head>
<body>
<main>
<h2>AI Avatar Call Demo</h2>
<p>AI Avatar Preview</p>

<input type="file" id="photo" accept="image/*">
<br><br>
<img id="avatar" alt="AI Avatar Preview" hidden>

<h3>Camera Preview</h3>
<video id="camera" autoplay muted playsinline></video>
<br>
<button onclick="startCamera()">Start Camera</button>
<button onclick="stopCamera()">Stop Camera</button>
<p id="status">Camera is off</p>
</main>

<script>
let stream;

document.getElementById("photo").onchange = function(e) {
  const file = e.target.files[0];
  if (!file) return;
  const img = document.getElementById("avatar");
  img.src = URL.createObjectURL(file);
  img.hidden = false;
};

async function startCamera() {
  try {
    stream = await navigator.mediaDevices.getUserMedia({
      video: true,
      audio: true
    });
    document.getElementById("camera").srcObject = stream;
    document.getElementById("status").textContent = "Camera is running";
  } catch (e) {
    alert(e.message);
  }
}

function stopCamera() {
  if (stream) {
    stream.getTracks().forEach(t => t.stop());
    stream = null;
  }
  document.getElementById("camera").srcObject = null;
  document.getElementById("status").textContent = "Camera is off";
}
</script>
</body>
</html>
