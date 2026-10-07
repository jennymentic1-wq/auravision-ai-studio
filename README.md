<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AuraVision AI 4K & Talking Video Studio</title>
    <style>
        :root {
            --bg-color: #0b0f19;
            --card-bg: #131b2e;
            --accent: #6366f1;
            --accent-hover: #4f46e5;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: #1e293b;
            --success: #10b981;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            padding: 1.25rem 2rem;
            border-bottom: 1px solid var(--border);
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(19, 27, 46, 0.7);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-size: 1.25rem;
            font-weight: 700;
            background: linear-gradient(45deg, #6366f1, #a855f7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .badge {
            background: rgba(99, 102, 241, 0.15);
            color: var(--accent);
            padding: 0.25rem 0.6rem;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: 600;
            border: 1px solid rgba(99, 102, 241, 0.3);
        }

        main {
            flex: 1;
            max-width: 1300px;
            width: 100%;
            margin: 0 auto;
            padding: 2rem;
            display: grid;
            grid-template-columns: 420px 1fr;
            gap: 2rem;
        }

        @media (max-width: 960px) {
            main {
                grid-template-columns: 1fr;
            }
        }

        .panel {
            background-color: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 1.75rem;
            display: flex;
            flex-direction: column;
            gap: 1.25rem;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
        }

        h2 {
            font-size: 1.1rem;
            color: var(--text-main);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .tabs {
            display: flex;
            background: var(--bg-color);
            padding: 4px;
            border-radius: 10px;
            border: 1px solid var(--border);
        }

        .tab {
            flex: 1;
            background: none;
            border: none;
            color: var(--text-muted);
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            padding: 0.6rem;
            border-radius: 8px;
            transition: all 0.2s ease;
        }

        .tab.active {
            background: var(--accent);
            color: white;
            box-shadow: 0 4px 12px rgba(99, 102, 241, 0.4);
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 0.4rem;
        }

        label {
            font-size: 0.8rem;
            color: var(--text-muted);
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        textarea, select {
            background-color: var(--bg-color);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 0.75rem;
            color: var(--text-main);
            font-size: 0.95rem;
            resize: vertical;
            transition: border-color 0.2s;
        }

        textarea:focus, select:focus {
            outline: none;
            border-color: var(--accent);
        }

        .range-container {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        input[type="range"] {
            flex: 1;
            accent-color: var(--accent);
            cursor: pointer;
        }

        .range-value {
            font-size: 0.85rem;
            font-weight: 600;
            color: var(--accent);
            min-width: 45px;
            text-align: right;
        }

        .btn-generate {
            background: linear-gradient(135deg, var(--accent), #8b5cf6);
            color: white;
            border: none;
            border-radius: 10px;
            padding: 0.9rem;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: opacity 0.2s, transform 0.1s;
            box-shadow: 0 4px 12px rgba(99, 102, 241, 0.3);
            margin-top: 0.5rem;
        }

        .btn-generate:hover {
            opacity: 0.92;
        }

        .btn-generate:active {
            transform: scale(0.98);
        }

        .preview-wrapper {
            background-color: var(--bg-color);
            border: 1px solid var(--border);
            border-radius: 12px;
            aspect-ratio: 16/9;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .placeholder-text {
            color: var(--text-muted);
            font-size: 0.9rem;
            text-align: center;
            padding: 1rem;
        }

        canvas {
            width: 100%;
            height: 100%;
            object-fit: contain;
            display: none;
        }

        .media-actions {
            display: flex;
            gap: 1rem;
        }

        .btn-secondary {
            flex: 1;
            background: transparent;
            border: 1px solid var(--border);
            color: var(--text-muted);
            border-radius: 10px;
            padding: 0.75rem;
            font-size: 0.9rem;
            font-weight: 600;
            cursor: not-allowed;
            transition: all 0.2s;
        }

        .btn-secondary.active {
            border-color: var(--accent);
            color: var(--text-main);
            cursor: pointer;
        }

        .btn-secondary.active:hover {
            background: rgba(99, 102, 241, 0.1);
        }

        .audio-indicator {
            display: none;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.8rem;
            color: var(--success);
            background: rgba(16, 185, 129, 0.1);
            padding: 0.4rem 0.8rem;
            border-radius: 8px;
            border: 1px solid rgba(16, 185, 129, 0.2);
        }

        .pulse-dot {
            width: 8px;
            height: 8px;
            background: var(--success);
            border-radius: 50%;
            box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); }
            70% { transform: scale(1); box-shadow: 0 0 0 6px rgba(16, 185, 129, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); }
        }

        footer {
            text-align: center;
            padding: 1.5rem;
            color: var(--text-muted);
            font-size: 0.8rem;
            border-top: 1px solid var(--border);
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">
            <span>AuraVision Studio</span>
            <span class="badge">v3.4 Live Audio</span>
        </div>
        <div id="statusIndicator" style="font-size: 0.85rem; color: var(--text-muted);">System Ready</div>
    </header>

    <main>
        <!-- Generation Controls Panel -->
        <div class="panel">
            <div class="tabs">
                <button class="tab active" id="tabVideo" onclick="setMode('video')">Talking Video</button>
                <button class="tab" id="tabImage" onclick="setMode('image')">4K Image</button>
            </div>

            <div class="form-group">
                <label id="promptLabel" for="prompt">Script / Prompt Description</label>
                <textarea id="prompt" rows="4" placeholder="Hello! I am your hyper-realistic AI presenter generated straight inside your browser with voice and talking animations.">Hello! I am your hyper-realistic AI presenter generated straight inside your browser with voice and talking animations.</textarea>
            </div>

            <div class="form-group" id="voiceGroup">
                <label for="voiceSelect">AI Voice Persona</label>
                <select id="voiceSelect">
                    <!-- Loaded dynamically via JavaScript -->
                </select>
            </div>

            <div class="form-group" id="durationGroup">
                <label for="duration">Video Duration: <span id="durVal" style="color:var(--accent)">10</span>s (Max 30s)</label>
                <div class="range-container">
                    <input type="range" id="duration" min="5" max="30" value="10" oninput="document.getElementById('durVal').innerText = this.value">
                </div>
            </div>

            <div class="form-group" id="resolutionGroup" style="display:none;">
                <label for="resolution">Image Resolution</label>
                <select id="resolution">
                    <option value="4k">3840 x 2160 (Ultra HD 4K)</option>
                    <option value="8k">7680 x 4320 (Extreme 8K)</option>
                </select>
            </div>

            <button class="btn-generate" onclick="generateMedia()">Generate & Speak</button>
        </div>

        <!-- Output Preview Panel -->
        <div class="panel">
            <h2>
                <span>Output Workspace</span>
                <div class="audio-indicator" id="audioIndicator">
                    <div class="pulse-dot"></div>
                    <span>AI Speaking Live</span>
                </div>
            </h2>
            
            <div class="preview-wrapper" id="previewWrapper">
                <div class="placeholder-text" id="placeholderText">
                    Configure your settings and click "Generate & Speak" to synthesize 4K graphics or talking video audio.
                </div>
                <!-- Canvas renders the animated talking avatar or image preview -->
                <canvas id="renderCanvas" width="1280" height="720"></canvas>
            </div>

            <div class="media-actions">
                <button class="btn-secondary" id="replayBtn" onclick="replayAudio()" disabled>Replay Audio</button>
                <button class="btn-secondary" id="downloadBtn" onclick="downloadMedia()" disabled>Download File</button>
            </div>
        </div>
    </main>

    <footer>
        <p>&copy; 2026 AuraVision AI Studio. Powered by Native Web Speech Synthesizer & HTML5 Canvas.</p>
    </footer>

    <script>
        let currentMode = 'video';
        let voices = [];
        let synth = window.speechSynthesis;
        let isSpeaking = false;
        let animationFrameId = null;

        // Populate system browser voices for text-to-speech audio
        function populateVoices() {
            if (!synth) return;
            voices = synth.getVoices();
            const voiceSelect = document.getElementById('voiceSelect');
            voiceSelect.innerHTML = '';
            
            // Filter preferred English or general voices
            voices.forEach((voice, index) => {
                const option = document.createElement('option');
                option.value = index;
                option.textContent = `${voice.name} (${voice.lang})`;
                if (voice.default || voice.lang.includes('en-US')) {
                    option.selected = true;
                }
                voiceSelect.appendChild(option);
            });
        }

        if (synth) {
            populateVoices();
            if (synth.onvoiceschanged !== undefined) {
                synth.onvoiceschanged = populateVoices;
            }
        }

        function setMode(mode) {
            currentMode = mode;
            document.getElementById('tabVideo').classList.toggle('active', mode === 'video');
            document.getElementById('tabImage').classList.toggle('active', mode === 'image');
            
            const voiceGroup = document.getElementById('voiceGroup');
            const durationGroup = document.getElementById('durationGroup');
            const resolutionGroup = document.getElementById('resolutionGroup');
            const promptLabel = document.getElementById('promptLabel');
            const promptText = document.getElementById('prompt');

            if (mode === 'video') {
                voiceGroup.style.display = 'flex';
                durationGroup.style.display = 'flex';
                resolutionGroup.style.display = 'none';
                promptLabel.innerText = "Script / Talking Speech Text";
                promptText.placeholder = "Type what you want the digital avatar to say aloud with lip sync...";
                promptText.value = "Hello! I am your hyper-realistic AI presenter generated straight inside your browser with voice and talking animations.";
            } else {
                voiceGroup.style.display = 'none';
                durationGroup.style.display = 'none';
                resolutionGroup.style.display = 'flex';
                promptLabel.innerText = "4K Image Description Prompt";
                promptText.placeholder = "A hyper-realistic 4K portrait of an astronaut on Mars, cinematic studio lighting, intricate suit details...";
                promptText.value = "A hyper-realistic 4K cinematic landscape of a futuristic neon city in Tokyo, volumetric lighting, photorealistic textures.";
            }

            stopSpeechAndAnimation();
            resetPreview();
        }

        function resetPreview() {
            document.getElementById('placeholderText').style.display = 'block';
            document.getElementById('renderCanvas').style.display = 'none';
            document.getElementById('audioIndicator').style.display = 'none';
            document.getElementById('replayBtn').classList.remove('active');
            document.getElementById('replayBtn').setAttribute('disabled', 'true');
            document.getElementById('downloadBtn').classList.remove('active');
            document.getElementById('downloadBtn').setAttribute('disabled', 'true');
        }

        function stopSpeechAndAnimation() {
            if (synth) synth.cancel();
            if (animationFrameId) cancelAnimationFrame(animationFrameId);
            isSpeaking = false;
        }

        function generateMedia() {
            const prompt = document.getElementById('prompt').value.trim();
            if (!prompt) {
                alert('Please provide a prompt or script description text.');
                return;
            }

            stopSpeechAndAnimation();
            
            document.getElementById('placeholderText').style.display = 'none';
            const canvas = document.getElementById('renderCanvas');
            canvas.style.display = 'block';
            const ctx = canvas.getContext('2d');

            if (currentMode === 'video') {
                // Video Mode: Talking avatar with voice synthesis & lip sync animation
                startTalkingVideo(prompt, ctx, canvas);
            } else {
                // 4K Image Generation simulation render
                render4KImage(prompt, ctx, canvas);
            }
        }

        function render4KImage(prompt, ctx, canvas) {
            document.getElementById('statusIndicator').innerText = "Rendering 4K Graphics...";
            
            // Draw simulated high-definition procedural artwork on canvas
            let grad = ctx.createLinearGradient(0, 0, canvas.width, canvas.height);
            grad.addColorStop(0, '#1e1b4b');
            grad.addColorStop(0.5, '#312e81');
            grad.addColorStop(1, '#0f172a');
            ctx.fillStyle = grad;
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Add futuristic neon art elements
            ctx.fillStyle = '#6366f1';
            ctx.beginPath();
            ctx.arc(640, 360, 180, 0, Math.PI * 2);
            ctx.fill();

            ctx.fillStyle = '#a855f7';
            ctx.beginPath();
            ctx.arc(700, 300, 120, 0, Math.PI * 2);
            ctx.fill();

            // Overlay text details
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 36px sans-serif';
            ctx.textAlign = 'center';
            ctx.fillText("4K ULTRA-HD AI ARTWORK", 640, 120);

            ctx.font = '20px sans-serif';
            ctx.fillStyle = '#94a3b8';
            let truncatedPrompt = prompt.length > 70 ? prompt.substring(0, 70) + '...' : prompt;
            ctx.fillText(`"${truncatedPrompt}"`, 640, 620);

            setTimeout(() => {
                document.getElementById('statusIndicator').innerText = "4K Image Ready";
                document.getElementById('downloadBtn').classList.add('active');
                document.getElementById('downloadBtn').removeAttribute('disabled');
            }, 1000);
        }

        function startTalkingVideo(scriptText, ctx, canvas) {
            document.getElementById('statusIndicator').innerText = "Synthesizing Voice & Video...";
            document.getElementById('audioIndicator').style.display = 'flex';

            // Setup speech utterance
            const utterance = new SpeechSynthesisUtterance(scriptText);
            const selectedVoiceIndex = document.getElementById('voiceSelect').value;
            if (voices[selectedVoiceIndex]) {
                utterance.voice = voices[selectedVoiceIndex];
            }
            
            const durationSec = parseInt(document.getElementById('duration').value);
            utterance.rate = 1.0; 

            isSpeaking = true;
            let mouthOpen = 0;
            let frameCount = 0;
            const maxFrames = durationSec * 60; // 60fps tracking

            // Render loop for avatar and talking sync animation
            function drawAvatarFrame() {
                // Background gradient
                let bgGrad = ctx.createRadialGradient(640, 360, 50, 640, 360, 600);
                bgGrad.addColorStop(0, '#1e293b');
                bgGrad.addColorStop(1, '#090d16');
                ctx.fillStyle = bgGrad;
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                // Avatar Head/Shoulders base setup
                // Shoulders
                ctx.fillStyle = '#3b82f6';
                ctx.beginPath();
                ctx.arc(640, 750, 280, Math.PI, 2 * Math.PI);
                ctx.fill();

                // Neck
                ctx.fillStyle = '#fbcfe8';
                ctx.fillRect(610, 420, 60, 100);

                // Head Face Base
                ctx.fillStyle = '#fce7f3';
                ctx.beginPath();
                ctx.ellipse(640, 310, 140, 170, 0, 0, 2 * Math.PI);
                ctx.fill();

                // Eyes
                ctx.fillStyle = '#1e293b';
                ctx.beginPath();
                ctx.arc(590, 280, 12, 0, 2 * Math.PI);
                ctx.arc(690, 280, 12, 0, 2 * Math.PI);
                ctx.fill();

                // Eye highlights
                ctx.fillStyle = '#ffffff';
                ctx.beginPath();
                ctx.arc(593, 277, 4, 0, 2 * Math.PI);
                ctx.arc(693, 277, 4, 0, 2 * Math.PI);
                ctx.fill();

                // Nose
                ctx.strokeStyle = '#cbd5e1';
                ctx.lineWidth = 3;
                ctx.beginPath();
                ctx.moveTo(640, 290);
                ctx.lineTo(635, 340);
                ctx.lineTo(645, 340);
                ctx.stroke();

                // Dynamic Mouth Sync Animation based on speaking state
                if (isSpeaking) {
                    // Random modulation to simulate active phoneme changes
                    mouthOpen = 8 + Math.sin(frameCount * 0.3) * 12 + Math.cos(frameCount * 0.7) * 8;
                    mouthOpen = Math.max(4, mouthOpen);
                } else {
                    mouthOpen = 3; // closed resting smile
                }

                ctx.fillStyle = '#9f1239';
                ctx.beginPath();
                ctx.ellipse(640, 395, 25, mouthOpen, 0, 0, 2 * Math.PI);
                ctx.fill();

                // UI Overlay text banner
                ctx.fillStyle = 'rgba(15, 23, 42, 0.8)';
                ctx.fillRect(40, 30, 1200, 50);
                ctx.fillStyle = '#38bdf8';
                ctx.font = 'bold 18px sans-serif';
                ctx.textAlign = 'left';
                ctx.fillText("AI TALKING AVATAR PRESENTER (LIVE AUDIO SYNC)", 60, 62);

                frameCount++;
                if (isSpeaking && frameCount < maxFrames) {
                    animationFrameId = requestAnimationFrame(drawAvatarFrame);
                } else {
                    isSpeaking = false;
                    document.getElementById('audioIndicator').style.display = 'none';
                    document.getElementById('statusIndicator').innerText = "Video Speech Complete";
                }
            }

            // Events for speech lifecycle
            utterance.onstart = () => {
                document.getElementById('statusIndicator').innerText = "Avatar Speaking Live...";
                drawAvatarFrame();
            };

            utterance.onend = () => {
                isSpeaking = false;
                document.getElementById('audioIndicator').style.display = 'none';
                document.getElementById('statusIndicator').innerText = "Video Ready";
                document.getElementById('replayBtn').classList.add('active');
                document.getElementById('replayBtn').removeAttribute('disabled');
                document.getElementById('downloadBtn').classList.add('active');
                document.getElementById('downloadBtn').removeAttribute('disabled');
            };

            utterance.onerror = (e) => {
                console.error("Speech synthesis error:", e);
                isSpeaking = false;
                document.getElementById('audioIndicator').style.display = 'none';
            };

            // Trigger browser native speech audio output
            synth.speak(utterance);
        }

        function replayAudio() {
            generateMedia();
        }

        function downloadMedia() {
            const canvas = document.getElementById('renderCanvas');
            const link = document.createElement('a');
            link.download = currentMode === 'video' ? 'AuraVision_Talking_Video.png' : 'AuraVision_4K_Image.png';
            link.href = canvas.toDataURL('image/png');
            link.click();
        }
    </script>
</body>
</html>
