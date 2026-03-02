// DOM Elements
const page1 = document.getElementById('page1');
const page2 = document.getElementById('page2');
const page3 = document.getElementById('page3');
const video = document.getElementById('video');
const canvas = document.getElementById('canvas');
const overlayImg = document.getElementById('overlay-img');

// Navigation
document.getElementById('startBtn').addEventListener('click', () => {
    page1.classList.remove('active');
    page2.classList.add('active');
    startCamera();
});

document.getElementById('nextBtn').addEventListener('click', () => {
    page2.classList.remove('active');
    page3.classList.add('active');
});

// Camera Logic
function startCamera() {
    navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } })
        .then(stream => {
            video.srcObject = stream;
        })
        .catch(err => {
            console.error("Camera error:", err);
            alert("Please allow camera access to take a selfie!");
        });
}

// Capture & Save Logic
document.getElementById('captureBtn').addEventListener('click', () => {
    const context = canvas.getContext('2d');
    
    // Set canvas to match video dimensions
    canvas.width = video.videoWidth;
    canvas.height = video.videoHeight;

    // 1. Draw the Video Feed
    // We add the filter effect here too so it saves in the picture
    context.filter = 'saturate(1.5) contrast(1.1) hue-rotate(-10deg)';
    context.drawImage(video, 0, 0, canvas.width, canvas.height);
    context.filter = 'none'; // Reset filter for the image overlay

    // 2. Draw the Couple Overlay
    // We need to calculate the position relative to the video size
    // Let's put the couple in the bottom right corner, scaled appropriately
    const imgWidth = canvas.width * 0.45; // 45% of screen width
    const imgHeight = (overlayImg.naturalHeight / overlayImg.naturalWidth) * imgWidth;
    const x = canvas.width - imgWidth - 20; // 20px padding from right
    const y = canvas.height - imgHeight; // Align to bottom

    context.drawImage(overlayImg, x, y, imgWidth, imgHeight);

    // 3. Save the image
    const link = document.createElement('a');
    link.download = 'holi-with-us.png';
    link.href = canvas.toDataURL('image/png');
    link.click();
});
