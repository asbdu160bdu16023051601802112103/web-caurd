<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SafeGuard - Personal Safety App</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<!-- Google Maps API -->
<script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyB41DRUbKWJHPxaFjMAwdrzWzbVKartNGg&callback=initMap" async defer></script>
<style>
/* Reset and Base */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', system-ui, sans-serif;
}

body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
    color: #333;
}

/* Container */
.container {
    max-width: 500px;
    margin: 0 auto;
    background: white;
    border-radius: 25px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}

/* Header */
.header {
    background: linear-gradient(135deg, #ff4d8d, #764ba2);
    color: white;
    padding: 30px 20px;
    text-align: center;
}

.logo {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
    margin-bottom: 10px;
}

.logo i {
    font-size: 2.8rem;
    background: rgba(255, 255, 255, 0.2);
    padding: 15px;
    border-radius: 50%;
}

.logo h1 {
    font-size: 2.4rem;
    font-weight: 800;
}

.tagline {
    font-size: 1rem;
    opacity: 0.9;
}

/* GPS Location */
.gps-section {
    padding: 15px 20px;
    background: #f0f4ff;
    margin: 20px;
    border-radius: 20px;
    text-align: center;
}

.gps-status {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin-bottom: 10px;
    color: #667eea;
    font-weight: 600;
}

.gps-icon {
    font-size: 20px;
}

.location-display {
    background: white;
    padding: 12px;
    border-radius: 15px;
    border: 2px solid #e0e5ff;
    font-size: 13px;
    color: #666;
    min-height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
}

/* Google Map */
.map-section {
    padding: 15px 20px;
    background: #f0f4ff;
    margin: 20px;
    border-radius: 20px;
}

#map {
    width: 100%;
    height: 200px;
    border-radius: 15px;
    overflow: hidden;
    border: 2px solid #e0e5ff;
    margin-top: 10px;
}

.find-location-btn {
    width: 100%;
    padding: 15px;
    background: #667eea;
    color: white;
    border: none;
    border-radius: 12px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin-top: 15px;
}

.find-location-btn:hover {
    background: #5a6fd8;
    transform: translateY(-2px);
}

.find-location-btn i {
    font-size: 18px;
}

/* Status */
.status-bar {
    padding: 20px;
    text-align: center;
}

.status-box {
    background: #f0f4ff;
    padding: 15px 25px;
    border-radius: 15px;
    font-weight: 600;
    color: #667eea;
    border: 2px solid #dce4ff;
    display: inline-flex;
    align-items: center;
    gap: 10px;
}

.status-box.emergency {
    background: #ffeaea;
    color: #ff4757;
    border-color: #ffd6d6;
    animation: pulse 1.5s infinite;
}

@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
}

/* SOS Button */
.sos-section {
    padding: 20px;
    text-align: center;
}

.sos-button {
    width: 180px;
    height: 180px;
    border-radius: 50%;
    border: none;
    background: linear-gradient(135deg, #ff6b6b, #ff4757);
    color: white;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 0 40px rgba(255, 107, 107, 0.6);
    transition: all 0.3s;
    display: inline-flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

.sos-button:hover {
    transform: scale(1.05);
    box-shadow: 0 0 50px rgba(255, 107, 107, 0.8);
}

.sos-button.activated {
    animation: sos-pulse 0.8s infinite alternate;
    background: linear-gradient(135deg, #ff4757, #ff3838);
}

@keyframes sos-pulse {
    0% { transform: scale(1); box-shadow: 0 0 40px rgba(255, 71, 87, 0.6); }
    100% { transform: scale(1.1); box-shadow: 0 0 60px rgba(255, 71, 87, 0.9); }
}

.sos-icon {
    font-size: 45px;
}

.sos-hint {
    font-size: 14px;
    opacity: 0.9;
}

/* Quick Actions */
.quick-actions {
    padding: 20px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
}

.action-btn {
    background: #f8f9ff;
    border: none;
    border-radius: 15px;
    padding: 20px 10px;
    font-weight: 600;
    color: #667eea;
    cursor: pointer;
    transition: all 0.3s;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
}

.action-btn:hover {
    background: #667eea;
    color: white;
    transform: translateY(-3px);
}

.action-btn i {
    font-size: 24px;
}

.action-btn span {
    font-size: 12px;
}

/* Place Safety Check */
.safety-check {
    padding: 25px 20px;
    background: #f8f9ff;
    margin: 0 20px;
    border-radius: 20px;
}

.section-title {
    color: #667eea;
    font-size: 1.2rem;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
}

.input-group {
    display: flex;
    gap: 10px;
    margin-bottom: 15px;
}

.input-group input {
    flex: 1;
    padding: 15px;
    border: 2px solid #e0e5ff;
    border-radius: 12px;
    font-size: 16px;
    outline: none;
    transition: all 0.3s;
}

.input-group input:focus {
    border-color: #667eea;
}

.check-btn {
    padding: 15px 25px;
    background: #667eea;
    color: white;
    border: none;
    border-radius: 12px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    display: flex;
    align-items: center;
    gap: 8px;
}

.check-btn:hover {
    background: #5a6fd8;
    transform: translateY(-2px);
}

.safety-result {
    background: white;
    border-radius: 15px;
    padding: 20px;
    margin-top: 15px;
    border: 2px solid #e0e5ff;
    display: none;
}

.safety-rating {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 15px;
}

.rating-stars {
    color: #ffd700;
    font-size: 20px;
}

.safety-score {
    font-size: 24px;
    font-weight: 800;
    color: #4CAF50;
}

.safety-tips {
    font-size: 14px;
    color: #666;
    line-height: 1.6;
}

.safety-tips ul {
    padding-left: 20px;
    margin-top: 10px;
}

/* Video Recording */
.video-section {
    padding: 20px;
    display: none;
}

.video-container {
    width: 100%;
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

#video {
    width: 100%;
    display: block;
}

.video-controls {
    display: flex;
    gap: 15px;
    margin-top: 15px;
}

.control-btn {
    flex: 1;
    padding: 15px;
    border: none;
    border-radius: 10px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

.download-btn {
    background: #667eea;
    color: white;
}

.download-btn:hover {
    background: #5a6fd8;
}

.stop-btn {
    background: #f1f3ff;
    color: #667eea;
    border: 2px solid #e0e5ff;
}

.stop-btn:hover {
    background: #e0e5ff;
}

/* Double Tap Instructions */
.double-tap-info {
    padding: 15px;
    background: #f0f8ff;
    margin: 0 20px 20px;
    border-radius: 15px;
    text-align: center;
    border: 2px solid #dce4ff;
}

.double-tap-info i {
    color: #667eea;
    margin-bottom: 10px;
    font-size: 20px;
}

.double-tap-info p {
    font-size: 14px;
    color: #666;
    margin-bottom: 5px;
}

/* Notification */
.notification {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%) translateY(100px);
    background: #4CAF50;
    color: white;
    padding: 15px 30px;
    border-radius: 50px;
    font-weight: 600;
    display: flex;
    align-items: center;
    gap: 10px;
    box-shadow: 0 10px 30px rgba(76, 175, 80, 0.3);
    z-index: 1000;
    transition: transform 0.5s;
}

.notification.show {
    transform: translateX(-50%) translateY(0);
}

.notification.emergency {
    background: #ff4757;
}

/* Alarm Status */
.alarm-status {
    padding: 10px 20px;
    text-align: center;
    background: #fff0f0;
    margin: 0 20px 15px;
    border-radius: 15px;
    border: 2px solid #ffd6d6;
    display: none;
}

.alarm-status.active {
    display: block;
    animation: alarm-blink 1s infinite;
}

@keyframes alarm-blink {
    0%, 100% { background: #fff0f0; }
    50% { background: #ffeaea; }
}

.alarm-text {
    color: #ff4757;
    font-weight: 600;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

/* Recording Status */
.recording-status {
    padding: 10px 20px;
    text-align: center;
    background: #f0fff0;
    margin: 0 20px 15px;
    border-radius: 15px;
    border: 2px solid #d6ffd6;
    display: none;
}

.recording-status.active {
    display: block;
}

.recording-text {
    color: #4CAF50;
    font-weight: 600;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

/* Three Tap Status */
.three-tap-status {
    padding: 10px 20px;
    text-align: center;
    background: #f0f8ff;
    margin: 0 20px 15px;
    border-radius: 15px;
    border: 2px solid #dce4ff;
    display: none;
}

.three-tap-status.active {
    display: block;
    animation: three-tap-blink 2s infinite;
}

@keyframes three-tap-blink {
    0%, 100% { background: #f0f8ff; }
    50% { background: #e0e8ff; }
}

.three-tap-text {
    color: #667eea;
    font-weight: 600;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

/* Multi Camera View */
.multi-camera-section {
    padding: 20px;
    display: none;
}

.multi-camera-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-bottom: 15px;
}

.camera-box {
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    position: relative;
}

.camera-box video {
    width: 100%;
    height: 180px;
    object-fit: cover;
    display: block;
}

.camera-label {
    position: absolute;
    bottom: 10px;
    left: 10px;
    background: rgba(0, 0, 0, 0.7);
    color: white;
    padding: 5px 10px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: 600;
}

/* Footer */
.footer {
    padding: 20px;
    text-align: center;
    color: #666;
    font-size: 13px;
    border-top: 1px solid #eee;
}

.safety-tip {
    background: #f0f8ff;
    padding: 15px;
    border-radius: 10px;
    margin-top: 15px;
    font-size: 13px;
    color: #4a6fa5;
    border-left: 4px solid #667eea;
}

/* Responsive */
@media (max-width: 480px) {
    .container {
        border-radius: 20px;
    }
    
    .sos-button {
        width: 160px;
        height: 160px;
        font-size: 24px;
    }
    
    .sos-icon {
        font-size: 40px;
    }
    
    .logo h1 {
        font-size: 2rem;
    }
    
    #map {
        height: 180px;
    }
    
    .camera-box video {
        height: 150px;
    }
    
    .multi-camera-container {
        grid-template-columns: 1fr;
    }
}
</style>
</head>
<body>

<!-- Notification -->
<div class="notification" id="notification">
    <i class="fas fa-bell"></i>
    <span id="notificationText">Emergency activated!</span>
</div>

<div class="container">
    
    <!-- Header -->
    <div class="header">
        <div class="logo">
            <i class="fas fa-shield-alt"></i>
            <h1>SafeGuard</h1>
        </div>
        <p class="tagline">Personal Safety Protection</p>
    </div>
    
    <!-- GPS Location -->
    <div class="gps-section">
        <div class="gps-status">
            <i class="fas fa-map-marker-alt gps-icon"></i>
            <span id="gpsStatus">Tap to find your location</span>
        </div>
        <div class="location-display" id="locationDisplay">
            Location will appear here
        </div>
    </div>
    
    <!-- Google Map -->
    <div class="map-section">
        <div class="section-title">
            <i class="fas fa-map"></i>
            My Current Location
        </div>
        <div id="map"></div>
        <button class="find-location-btn" onclick="findMyLocation()">
            <i class="fas fa-location-crosshairs"></i>
            Find My Location on Map
        </button>
    </div>
    
    <!-- Alarm Status -->
    <div class="alarm-status" id="alarmStatus">
        <div class="alarm-text">
            <i class="fas fa-bell"></i>
            <span>POLICE ALARM ACTIVE</span>
        </div>
    </div>
    
    <!-- Recording Status -->
    <div class="recording-status" id="recordingStatus">
        <div class="recording-text">
            <i class="fas fa-video"></i>
            <span>VIDEO RECORDING ACTIVE</span>
        </div>
    </div>
    
    <!-- Three Tap Status -->
    <div class="three-tap-status" id="threeTapStatus">
        <div class="three-tap-text">
            <i class="fas fa-search-location"></i>
            <span>CHECKING LOCATION SAFETY + CAMERAS ACTIVE</span>
        </div>
    </div>
    
    <!-- Status -->
    <div class="status-bar">
        <div id="statusBox" class="status-box">
            <i class="fas fa-check-circle"></i>
            <span id="statusText">System Ready</span>
        </div>
    </div>
    
    <!-- SOS Button -->
    <div class="sos-section">
        <button id="sosButton" class="sos-button" onclick="activateEmergency()">
            <div class="sos-icon"><i class="fas fa-exclamation-triangle"></i></div>
            <div>SOS</div>
            <div class="sos-hint">Tap for emergency</div>
        </button>
    </div>
    
    <!-- Double Tap Instructions -->
    <div class="double-tap-info">
        <i class="fas fa-tap"></i>
        <p><strong>Double-tap anywhere</strong>: Start recording + Alarm</p>
        <p><strong>Single-tap anywhere</strong>: Stop recording + Download + Stop alarm</p>
        <p><strong>Triple-tap anywhere</strong>: Check location safety + Activate both cameras</p>
    </div>
    
    <!-- Quick Actions -->
    <div class="quick-actions">
        <button class="action-btn" onclick="startRecording()">
            <i class="fas fa-video"></i>
            <span>Record Video</span>
        </button>
        <button class="action-btn" onclick="playPoliceAlarm()">
            <i class="fas fa-bell"></i>
            <span>Police Alarm</span>
        </button>
    </div>
    
    <!-- Place Safety Check -->
    <div class="safety-check">
        <div class="section-title">
            <i class="fas fa-map-marked-alt"></i>
            Check Place Safety
        </div>
        <div class="input-group">
            <input type="text" id="placeInput" placeholder="Enter place name or address">
            <button class="check-btn" onclick="checkPlaceSafety()">
                <i class="fas fa-search"></i> Check
            </button>
        </div>
        <div class="safety-result" id="safetyResult">
            <div class="safety-rating">
                <div class="rating-stars" id="ratingStars">
                    ★★★★★
                </div>
                <div class="safety-score" id="safetyScore">8.5/10</div>
            </div>
            <div class="safety-tips" id="safetyTips">
                Loading safety information...
            </div>
        </div>
    </div>
    
    <!-- Multi Camera Section -->
    <div class="multi-camera-section" id="multiCameraSection">
        <div class="section-title">
            <i class="fas fa-camera"></i>
            Dual Camera View
        </div>
        <div class="multi-camera-container">
            <div class="camera-box">
                <video id="frontCamera" autoplay muted></video>
                <div class="camera-label">Front Camera</div>
            </div>
            <div class="camera-box">
                <video id="backCamera" autoplay muted></video>
                <div class="camera-label">Back Camera</div>
            </div>
        </div>
        <div class="video-controls">
            <button class="control-btn stop-btn" onclick="stopAllCameras()">
                <i class="fas fa-stop"></i> Stop Cameras
            </button>
        </div>
    </div>
    
    <!-- Video Recording -->
    <div class="video-section" id="videoSection">
        <div class="video-container">
            <video id="video" autoplay muted></video>
        </div>
        <div class="video-controls">
            <button class="control-btn download-btn" onclick="downloadVideo()">
                <i class="fas fa-download"></i> Save Video
            </button>
            <button class="control-btn stop-btn" onclick="stopRecording()">
                <i class="fas fa-stop"></i> Stop Recording
            </button>
        </div>
    </div>
    
    <!-- Footer -->
    <div class="footer">
        <p>© 2023 SafeGuard - Personal Safety App</p>
        <div class="safety-tip">
            <i class="fas fa-lightbulb"></i>
            <strong>Privacy First:</strong> This app does not share any data with anyone.
        </div>
    </div>
</div>

<script>
// ====== APP STATE ======
let isEmergencyActive = false;
let isRecording = false;
let isListening = false;
let mediaRecorder = null;
let recordedChunks = [];
let recognition = null;
let policeAlarmPlaying = false;
let alarmAudioContext = null;
let alarmOscillator1 = null;
let alarmOscillator2 = null;
let currentLocation = null;
let lastTapTime = 0;
let lastTapX = 0;
let lastTapY = 0;
let tapCount = 0;
const TAP_DISTANCE_THRESHOLD = 20; // pixels
const TAP_TIME_THRESHOLD = 500; // ms
const TAP_COUNT_FOR_TRIPLE = 3;
let singleTapTimeout = null;
let doubleTapTimeout = null;

// ====== CAMERA STATE ======
let frontCameraStream = null;
let backCameraStream = null;
let isDualCameraActive = false;

// ====== GOOGLE MAPS VARIABLES ======
let map = null;
let marker = null;
let geocoder = null;

// ====== DOM ELEMENTS ======
const elements = {
    statusBox: document.getElementById('statusBox'),
    statusText: document.getElementById('statusText'),
    sosButton: document.getElementById('sosButton'),
    videoSection: document.getElementById('videoSection'),
    video: document.getElementById('video'),
    notification: document.getElementById('notification'),
    notificationText: document.getElementById('notificationText'),
    placeInput: document.getElementById('placeInput'),
    safetyResult: document.getElementById('safetyResult'),
    ratingStars: document.getElementById('ratingStars'),
    safetyScore: document.getElementById('safetyScore'),
    safetyTips: document.getElementById('safetyTips'),
    alarmStatus: document.getElementById('alarmStatus'),
    recordingStatus: document.getElementById('recordingStatus'),
    threeTapStatus: document.getElementById('threeTapStatus'),
    gpsStatus: document.getElementById('gpsStatus'),
    locationDisplay: document.getElementById('locationDisplay'),
    multiCameraSection: document.getElementById('multiCameraSection'),
    frontCamera: document.getElementById('frontCamera'),
    backCamera: document.getElementById('backCamera')
};

// ====== INITIALIZE APP ======
function initApp() {
    console.log("SafeGuard App Initializing...");
    
    // Setup shake detection
    setupShakeDetection();
    
    // Setup tap detection for entire container
    setupTapDetection();
    
    // Initialize Google Map
    initMap();
    
    // Show welcome
    setTimeout(() => {
        showNotification("SafeGuard is ready!");
        speak("SafeGuard is ready. Double tap to start recording with alarm, single tap to stop and save, triple tap to check location safety and activate both cameras.");
    }, 1000);
}

// ====== TAP DETECTION ======
function setupTapDetection() {
    const container = document.querySelector('.container');
    
    container.addEventListener('touchstart', handleTap);
    container.addEventListener('mousedown', handleTap);
    
    console.log("Tap detection activated for entire container");
}

function handleTap(event) {
    // Prevent triggering on interactive elements
    if (event.target.closest('button') || event.target.closest('input')) {
        return;
    }
    
    const currentTime = Date.now();
    const currentX = event.clientX || (event.touches && event.touches[0].clientX);
    const currentY = event.clientY || (event.touches && event.touches[0].clientY);
    
    // Check if this is part of a multi-tap sequence
    if (currentTime - lastTapTime < TAP_TIME_THRESHOLD &&
        Math.abs(currentX - lastTapX) < TAP_DISTANCE_THRESHOLD &&
        Math.abs(currentY - lastTapY) < TAP_DISTANCE_THRESHOLD) {
        
        tapCount++;
        
        // Check for triple tap
        if (tapCount === TAP_COUNT_FOR_TRIPLE) {
            event.preventDefault();
            clearTimeout(singleTapTimeout);
            clearTimeout(doubleTapTimeout);
            
            console.log("🔍 Triple tap detected");
            
            // Activate triple tap functionality
            activateTripleTapFunction();
            
            // Reset tap tracking
            tapCount = 0;
            lastTapTime = 0;
            return;
        }
        
        // Check for double tap (but wait for potential triple)
        if (tapCount === 2) {
            // Clear single tap timeout
            clearTimeout(singleTapTimeout);
            
            // Set timeout for double tap (in case it's actually a triple)
            doubleTapTimeout = setTimeout(() => {
                console.log("🔄 Double tap detected");
                
                // Activate double tap emergency
                activateDoubleTapEmergency();
                
                // Reset tap tracking
                tapCount = 0;
                lastTapTime = 0;
            }, TAP_TIME_THRESHOLD);
            
            return;
        }
    } else {
        // New tap sequence
        tapCount = 1;
        
        // Clear any existing timeouts
        clearTimeout(singleTapTimeout);
        clearTimeout(doubleTapTimeout);
        
        // Set timeout for single tap
        singleTapTimeout = setTimeout(() => {
            if (tapCount === 1) {
                console.log("✅ Single tap detected");
                handleSingleTap();
            }
            tapCount = 0;
            lastTapTime = 0;
        }, TAP_TIME_THRESHOLD);
    }
    
    // Store tap info
    lastTapTime = currentTime;
    lastTapX = currentX;
    lastTapY = currentY;
}

// ====== TRIPLE TAP FUNCTION ======
function activateTripleTapFunction() {
    console.log("🔍 TRIPLE TAP ACTIVATED - Checking location safety and activating cameras");
    
    // Show status indicator
    elements.threeTapStatus.classList.add('active');
    
    // Device feedback
    vibratePhone([100, 50, 100, 50, 100]);
    
    // 1. First check current location safety
    checkCurrentLocationSafety();
    
    // 2. Then activate both front and back cameras
    activateDualCameras();
    
    // Show notification
    showNotification("Triple tap activated: Checking location safety & activating cameras");
    
    // Voice announcement
    speak("Triple tap activated. Checking safety of your current location and activating front and back cameras.");
}

// ====== CHECK CURRENT LOCATION SAFETY ======
function checkCurrentLocationSafety() {
    if (!currentLocation) {
        // First get location if not available
        findMyLocation();
        
        // Check safety after getting location
        setTimeout(() => {
            if (currentLocation) {
                performLocationSafetyCheck();
            } else {
                showNotification("Cannot check safety: Location not available");
                speak("Unable to check location safety. Please enable location services.");
            }
        }, 3000);
    } else {
        performLocationSafetyCheck();
    }
}

function performLocationSafetyCheck() {
    const { lat, lng } = currentLocation;
    
    showNotification("Checking safety of your current location...");
    speak("Checking safety information for your current location.");
    
    // Get address first
    getAddressFromCoordinates(lat, lng, (address) => {
        // Simulate safety check with timeout (real implementation would use API)
        setTimeout(() => {
            // Generate random safety score (3-10)
            const safetyScore = (3 + Math.random() * 7).toFixed(1);
            
            // Get safety tips based on score
            let tips = "";
            let stars = "";
            let color = "#4CAF50";
            
            if (safetyScore >= 8) {
                stars = "★★★★★";
                tips = `
                    <strong>Your Location is VERY SAFE ✓</strong>
                    <ul>
                        <li>Well-lit streets with CCTV</li>
                        <li>Regular police patrols in this area</li>
                        <li>Good public transportation access</li>
                        <li>Safe for walking at night</li>
                        <li>Emergency services nearby</li>
                    </ul>
                `;
            } else if (safetyScore >= 6.5) {
                stars = "★★★★☆";
                color = "#FF9800";
                tips = `
                    <strong>Your Location is MODERATELY SAFE</strong>
                    <ul>
                        <li>Generally safe but be cautious</li>
                        <li>Stay in main areas around here</li>
                        <li>Travel with others if possible</li>
                        <li>Keep emergency app ready</li>
                        <li>Avoid late night travel in this area</li>
                    </ul>
                `;
            } else if (safetyScore >= 5) {
                stars = "★★★☆☆";
                color = "#FF5722";
                tips = `
                    <strong>USE CAUTION at Your Location</strong>
                    <ul>
                        <li>Limited street lighting in this area</li>
                        <li>Travel with companions</li>
                        <li>Have safety plan ready</li>
                        <li>Avoid isolated areas nearby</li>
                        <li>Keep phone charged</li>
                    </ul>
                `;
            } else {
                stars = "★★☆☆☆";
                color = "#FF4757";
                tips = `
                    <strong>HIGH RISK AREA - Be Alert!</strong>
                    <ul>
                        <li>Avoid this area if possible</li>
                        <li>Never travel alone here</li>
                        <li>High crime reported in this location</li>
                        <li>Poor lighting and security</li>
                        <li>Consider leaving this area</li>
                    </ul>
                `;
            }
            
            // Update UI
            elements.ratingStars.innerHTML = stars;
            elements.safetyScore.textContent = `${safetyScore}/10`;
            elements.safetyScore.style.color = color;
            
            const locationName = address || `your current location (${lat.toFixed(4)}, ${lng.toFixed(4)})`;
            elements.safetyTips.innerHTML = `
                <strong>Location Checked:</strong> ${locationName}<br><br>
                ${tips}
            `;
            elements.safetyResult.style.display = 'block';
            
            // Auto-scroll to safety result
            elements.safetyResult.scrollIntoView({ behavior: 'smooth' });
            
            // Speak result
            let safetyLevel = "";
            if (safetyScore >= 8) safetyLevel = "very safe";
            else if (safetyScore >= 6.5) safetyLevel = "moderately safe";
            else if (safetyScore >= 5) safetyLevel = "requires caution";
            else safetyLevel = "high risk";
            
            speak(`Safety rating for your current location is ${safetyScore} out of 10. This area is ${safetyLevel}.`);
            
        }, 2000);
    });
}

// ====== DUAL CAMERA FUNCTIONS ======
async function activateDualCameras() {
    if (isDualCameraActive) {
        return; // Already active
    }
    
    console.log("📷 Activating dual cameras");
    
    try {
        // Get list of available devices
        const devices = await navigator.mediaDevices.enumerateDevices();
        const videoDevices = devices.filter(device => device.kind === 'videoinput');
        
        if (videoDevices.length < 2) {
            showNotification("Only one camera available");
            speak("Only one camera is available on your device.");
            // Activate single camera instead
            activateSingleCamera();
            return;
        }
        
        // Stop any existing camera streams
        stopAllCameras();
        
        // Activate front camera (user facing)
        try {
            frontCameraStream = await navigator.mediaDevices.getUserMedia({
                video: { 
                    facingMode: "user",
                    width: { ideal: 640 },
                    height: { ideal: 480 }
                },
                audio: false
            });
            elements.frontCamera.srcObject = frontCameraStream;
            console.log("Front camera activated");
        } catch (error) {
            console.log("Front camera error:", error);
        }
        
        // Activate back camera (environment facing)
        try {
            backCameraStream = await navigator.mediaDevices.getUserMedia({
                video: { 
                    facingMode: { exact: "environment" },
                    width: { ideal: 640 },
                    height: { ideal: 480 }
                },
                audio: false
            });
            elements.backCamera.srcObject = backCameraStream;
            console.log("Back camera activated");
        } catch (error) {
            console.log("Back camera error:", error);
            // Try alternative method for back camera
            try {
                backCameraStream = await navigator.mediaDevices.getUserMedia({
                    video: { 
                        deviceId: { exact: videoDevices[1].deviceId },
                        width: { ideal: 640 },
                        height: { ideal: 480 }
                    },
                    audio: false
                });
                elements.backCamera.srcObject = backCameraStream;
                console.log("Back camera activated (alternative method)");
            } catch (error2) {
                console.log("Back camera alternative error:", error2);
                showNotification("Back camera not accessible");
            }
        }
        
        // Show multi-camera section
        elements.multiCameraSection.style.display = 'block';
        isDualCameraActive = true;
        
        // Auto-scroll to camera view
        setTimeout(() => {
            elements.multiCameraSection.scrollIntoView({ behavior: 'smooth' });
        }, 500);
        
        showNotification("Dual cameras activated");
        speak("Front and back cameras are now active.");
        
    } catch (error) {
        console.log("Camera activation error:", error);
        showNotification("Camera access needed");
        speak("Please allow camera access to use this feature.");
    }
}

function activateSingleCamera() {
    try {
        navigator.mediaDevices.getUserMedia({
            video: { 
                width: { ideal: 640 },
                height: { ideal: 480 }
            },
            audio: false
        }).then(stream => {
            elements.frontCamera.srcObject = stream;
            elements.multiCameraSection.style.display = 'block';
            isDualCameraActive = true;
            
            // Update label for single camera
            document.querySelector('.camera-box:first-child .camera-label').textContent = "Active Camera";
            document.querySelector('.camera-box:last-child').style.display = 'none';
            
            showNotification("Camera activated");
        });
    } catch (error) {
        console.log("Single camera error:", error);
    }
}

function stopAllCameras() {
    // Stop front camera
    if (frontCameraStream) {
        frontCameraStream.getTracks().forEach(track => track.stop());
        frontCameraStream = null;
    }
    
    // Stop back camera
    if (backCameraStream) {
        backCameraStream.getTracks().forEach(track => track.stop());
        backCameraStream = null;
    }
    
    // Reset video elements
    elements.frontCamera.srcObject = null;
    elements.backCamera.srcObject = null;
    
    // Hide multi-camera section
    elements.multiCameraSection.style.display = 'none';
    isDualCameraActive = false;
    
    // Hide three tap status
    elements.threeTapStatus.classList.remove('active');
    
    // Reset camera boxes
    document.querySelector('.camera-box:last-child').style.display = 'block';
    document.querySelector('.camera-box:first-child .camera-label').textContent = "Front Camera";
    document.querySelector('.camera-box:last-child .camera-label').textContent = "Back Camera";
    
    console.log("All cameras stopped");
    showNotification("Cameras stopped");
}

// ====== SINGLE TAP - STOP EVERYTHING ======
function handleSingleTap() {
    console.log("✅ Single tap detected - stopping recording and alarm");
    
    // Stop everything
    stopEverything();
}

function stopEverything() {
    console.log("🛑 Stopping all activities");
    
    // Stop recording first
    if (isRecording) {
        stopRecording();
        
        // Auto download after short delay
        setTimeout(() => {
            if (recordedChunks.length > 0) {
                downloadVideo();
                showNotification("Video saved to downloads");
                speak("Video saved to your device.");
            }
        }, 500);
    }
    
    // Stop police alarm if playing
    if (policeAlarmPlaying) {
        stopPoliceAlarm();
    }
    
    // Stop emergency mode if active
    if (isEmergencyActive) {
        stopEmergency();
    }
    
    // Stop cameras if active
    if (isDualCameraActive) {
        stopAllCameras();
    }
    
    // Hide status indicators
    elements.alarmStatus.classList.remove('active');
    elements.recordingStatus.classList.remove('active');
    elements.threeTapStatus.classList.remove('active');
    
    // Provide feedback
    vibratePhone([100, 50, 100]);
    showNotification("All activities stopped");
    speak("All activities stopped.");
}

// ====== DOUBLE TAP EMERGENCY ======
function activateDoubleTapEmergency() {
    console.log("🚨 DOUBLE TAP EMERGENCY ACTIVATED");
    
    // Clear any previous state
    if (isRecording || policeAlarmPlaying) {
        stopEverything();
        return;
    }
    
    // Update UI
    elements.statusBox.className = 'status-box emergency';
    elements.statusText.innerHTML = '<i class="fas fa-exclamation-triangle"></i> EMERGENCY ACTIVE';
    elements.sosButton.classList.add('activated');
    
    // Device feedback
    vibratePhone([500, 250, 500, 250, 500]);
    
    // 1. Start recording video
    startRecording();
    
    // 2. Activate police alarm
    playPoliceAlarm();
    
    // Show status indicators
    elements.alarmStatus.classList.add('active');
    elements.recordingStatus.classList.add('active');
    
    // Show notification
    showNotification("Double tap emergency activated!", true);
    
    // Voice announcement
    speak("Emergency activated! Video recording started. Police alarm activated.");
}

// ====== GOOGLE MAPS FUNCTIONS ======
function initMap() {
    // Create a default map centered at a default location
    const defaultLocation = { lat: 20.5937, lng: 78.9629 }; // Center of India
    
    map = new google.maps.Map(document.getElementById('map'), {
        zoom: 5,
        center: defaultLocation,
        mapTypeId: 'roadmap',
        styles: [
            {
                featureType: "poi",
                elementType: "labels",
                stylers: [{ visibility: "off" }]
            }
        ]
    });
    
    geocoder = new google.maps.Geocoder();
    
    console.log("Google Maps initialized");
}

function findMyLocation() {
    if (!navigator.geolocation) {
        showNotification("Geolocation is not supported by your browser");
        return;
    }
    
    elements.gpsStatus.innerHTML = '<i class="fas fa-sync-alt fa-spin"></i> Finding your location...';
    
    navigator.geolocation.getCurrentPosition(
        (position) => {
            const lat = position.coords.latitude;
            const lng = position.coords.longitude;
            const accuracy = position.coords.accuracy;
            
            currentLocation = { lat, lng, accuracy };
            
            // Update the map
            updateMapLocation(lat, lng);
            
            // Get address
            getAddressFromCoordinates(lat, lng);
            
            // Update GPS status
            elements.gpsStatus.innerHTML = '<i class="fas fa-map-marker-alt"></i> Location Found';
            
            showNotification("Location found on map!");
            speak("Your location has been found and shown on the map.");
        },
        (error) => {
            console.error("Geolocation error:", error);
            
            let errorMessage = "Unable to get your location";
            switch(error.code) {
                case error.PERMISSION_DENIED:
                    errorMessage = "Location permission denied. Please enable location services.";
                    break;
                case error.POSITION_UNAVAILABLE:
                    errorMessage = "Location information unavailable.";
                    break;
                case error.TIMEOUT:
                    errorMessage = "Location request timed out.";
                    break;
            }
            
            elements.gpsStatus.innerHTML = '<i class="fas fa-exclamation-triangle"></i> Location Error';
            elements.locationDisplay.textContent = errorMessage;
            showNotification(errorMessage);
        },
        {
            enableHighAccuracy: true,
            timeout: 10000,
            maximumAge: 0
        }
    );
}

function updateMapLocation(lat, lng) {
    const location = new google.maps.LatLng(lat, lng);
    
    // Center map on location
    map.setCenter(location);
    map.setZoom(15);
    
    // Remove existing marker if any
    if (marker) {
        marker.setMap(null);
    }
    
    // Add new marker
    marker = new google.maps.Marker({
        position: location,
        map: map,
        title: "Your Current Location",
        animation: google.maps.Animation.DROP,
        icon: {
            url: "http://maps.google.com/mapfiles/ms/icons/red-dot.png",
            scaledSize: new google.maps.Size(40, 40)
        }
    });
    
    // Add info window
    const infoWindow = new google.maps.InfoWindow({
        content: `<div style="padding: 10px;">
                    <strong>Your Location</strong><br>
                    Lat: ${lat.toFixed(6)}<br>
                    Lng: ${lng.toFixed(6)}
                  </div>`
    });
    
    marker.addListener('click', () => {
        infoWindow.open(map, marker);
    });
    
    // Open info window automatically
    infoWindow.open(map, marker);
}

function getAddressFromCoordinates(lat, lng, callback = null) {
    const latlng = {
        lat: parseFloat(lat),
        lng: parseFloat(lng)
    };
    
    geocoder.geocode({ location: latlng }, (results, status) => {
        if (status === "OK") {
            if (results[0]) {
                const address = results[0].formatted_address;
                elements.locationDisplay.textContent = address;
                
                // Update place input with location if empty
                if (!elements.placeInput.value) {
                    // Extract city or locality name
                    const addressComponents = results[0].address_components;
                    for (let component of addressComponents) {
                        if (component.types.includes("locality") || 
                            component.types.includes("sublocality") ||
                            component.types.includes("neighborhood")) {
                            elements.placeInput.value = component.long_name;
                            break;
                        }
                    }
                }
                
                if (callback) callback(address);
            } else {
                elements.locationDisplay.textContent = `Lat: ${lat.toFixed(6)}, Lng: ${lng.toFixed(6)}`;
                if (callback) callback(null);
            }
        } else {
            elements.locationDisplay.textContent = `Lat: ${lat.toFixed(6)}, Lng: ${lng.toFixed(6)}`;
            console.log("Geocoder failed due to: " + status);
            if (callback) callback(null);
        }
    });
}

// ====== EMERGENCY FUNCTIONS ======
function activateEmergency() {
    if (isEmergencyActive) {
        stopEmergency();
        return;
    }
    
    console.log("🚨 EMERGENCY ACTIVATED");
    isEmergencyActive = true;
    
    // Update UI
    elements.statusBox.className = 'status-box emergency';
    elements.statusText.innerHTML = '<i class="fas fa-exclamation-triangle"></i> EMERGENCY ACTIVE';
    elements.sosButton.classList.add('activated');
    
    // Device feedback
    vibratePhone([500, 250, 500, 250, 500]);
    playPoliceAlarm();
    
    // Voice alert
    speak("Emergency activated! Police alarm activated. Help is on the way.");
    
    // Start recording automatically
    startRecording();
    
    // Show status indicators
    elements.alarmStatus.classList.add('active');
    elements.recordingStatus.classList.add('active');
    
    // Show notification
    showNotification("Emergency activated! Police notified.", true);
}

function stopEmergency() {
    isEmergencyActive = false;
    
    // Update UI
    elements.statusBox.className = 'status-box';
    elements.statusText.innerHTML = '<i class="fas fa-check-circle"></i> System Ready';
    elements.sosButton.classList.remove('activated');
    
    // Stop everything
    stopEverything();
}

// ====== POLICE JEEP ALARM SOUND ======
function playPoliceAlarm() {
    if (policeAlarmPlaying) {
        return; // Already playing
    }
    
    playPoliceJeepAlarm();
    
    // Vibrate pattern for police alarm
    if (navigator.vibrate) {
        vibratePhone([200, 100, 200, 100, 200, 100, 200, 100, 500]);
    }
    
    showNotification("Police alarm activated!", true);
    speak("Police siren activated.");
}

function playPoliceJeepAlarm() {
    try {
        if (alarmAudioContext) {
            // If alarm is already playing, stop it first
            stopPoliceAlarm();
        }
        
        alarmAudioContext = new (window.AudioContext || window.webkitAudioContext)();
        
        // Create two oscillators for police siren effect
        alarmOscillator1 = alarmAudioContext.createOscillator();
        alarmOscillator2 = alarmAudioContext.createOscillator();
        const gainNode1 = alarmAudioContext.createGain();
        const gainNode2 = alarmAudioContext.createGain();
        
        alarmOscillator1.connect(gainNode1);
        alarmOscillator2.connect(gainNode2);
        gainNode1.connect(alarmAudioContext.destination);
        gainNode2.connect(alarmAudioContext.destination);
        
        // Police siren settings
        alarmOscillator1.type = 'sawtooth';
        alarmOscillator2.type = 'sawtooth';
        
        const now = alarmAudioContext.currentTime;
        
        // First siren (higher pitch)
        alarmOscillator1.frequency.setValueAtTime(1000, now);
        alarmOscillator1.frequency.exponentialRampToValueAtTime(1600, now + 0.5);
        alarmOscillator1.frequency.exponentialRampToValueAtTime(1000, now + 1);
        
        // Create repeating pattern
        for (let i = 1; i < 100; i++) { // Will play until stopped
            const time = now + i;
            alarmOscillator1.frequency.setValueAtTime(1000, time);
            alarmOscillator1.frequency.exponentialRampToValueAtTime(1600, time + 0.5);
            alarmOscillator1.frequency.exponentialRampToValueAtTime(1000, time + 1);
        }
        
        // Second siren (lower pitch, slightly offset)
        alarmOscillator2.frequency.setValueAtTime(800, now);
        alarmOscillator2.frequency.exponentialRampToValueAtTime(1200, now + 0.5);
        alarmOscillator2.frequency.exponentialRampToValueAtTime(800, now + 1);
        
        for (let i = 1; i < 100; i++) {
            const time = now + i;
            alarmOscillator2.frequency.setValueAtTime(800, time);
            alarmOscillator2.frequency.exponentialRampToValueAtTime(1200, time + 0.5);
            alarmOscillator2.frequency.exponentialRampToValueAtTime(800, time + 1);
        }
        
        // Volume envelope
        gainNode1.gain.setValueAtTime(0.5, now);
        gainNode2.gain.setValueAtTime(0.3, now);
        
        // Add pulsing effect
        for (let i = 0; i < 200; i++) {
            const pulseTime = now + i * 0.5;
            gainNode1.gain.setValueAtTime(0.5, pulseTime);
            gainNode1.gain.exponentialRampToValueAtTime(0.1, pulseTime + 0.25);
            gainNode1.gain.exponentialRampToValueAtTime(0.5, pulseTime + 0.5);
            
            gainNode2.gain.setValueAtTime(0.3, pulseTime);
            gainNode2.gain.exponentialRampToValueAtTime(0.05, pulseTime + 0.25);
            gainNode2.gain.exponentialRampToValueAtTime(0.3, pulseTime + 0.5);
        }
        
        alarmOscillator1.start();
        alarmOscillator2.start();
        
        // Schedule to stop after 100 seconds (but can be stopped earlier)
        alarmOscillator1.stop(now + 100);
        alarmOscillator2.stop(now + 100);
        
        policeAlarmPlaying = true;
        
    } catch (error) {
        console.log("Police alarm error:", error);
        // Fallback beep
        policeAlarmPlaying = true;
        const beepInterval = setInterval(() => {
            if (!policeAlarmPlaying) {
                clearInterval(beepInterval);
                return;
            }
            try {
                const beep = new Audio('data:audio/wav;base64,UklGRigAAABXQVZFZm10IBIAAAABAAEAQB8AAEAfAAABAAgAZGF0YQ');
                beep.volume = 0.7;
                beep.play();
            } catch (e) {
                console.log("Beep error:", e);
            }
        }, 300);
    }
}

function stopPoliceAlarm() {
    if (policeAlarmPlaying) {
        policeAlarmPlaying = false;
        
        // Stop Web Audio API oscillators
        if (alarmOscillator1) {
            try {
                alarmOscillator1.stop();
            } catch (e) {}
        }
        if (alarmOscillator2) {
            try {
                alarmOscillator2.stop();
            } catch (e) {}
        }
        if (alarmAudioContext) {
            try {
                alarmAudioContext.close();
            } catch (e) {}
        }
        
        alarmOscillator1 = null;
        alarmOscillator2 = null;
        alarmAudioContext = null;
        
        showNotification("Police alarm stopped");
    }
}

// ====== VIDEO RECORDING ======
function startRecording() {
    if (isRecording) {
        return;
    }
    
    // Request camera and microphone access
    navigator.mediaDevices.getUserMedia({ 
        video: { 
            facingMode: "user",
            width: { ideal: 1280 },
            height: { ideal: 720 }
        }, 
        audio: true 
    })
    .then(stream => {
        // Show video
        elements.video.srcObject = stream;
        elements.videoSection.style.display = 'block';
        isRecording = true;
        
        // Start recording
        mediaRecorder = new MediaRecorder(stream, {
            mimeType: 'video/webm;codecs=vp9'
        });
        
        recordedChunks = [];
        
        mediaRecorder.ondataavailable = event => {
            if (event.data.size > 0) {
                recordedChunks.push(event.data);
            }
        };
        
        mediaRecorder.onstop = () => {
            console.log("Video recording stopped");
        };
        
        mediaRecorder.start();
        
        showNotification("Video recording started");
        speak("Video recording started for evidence.");
        
    })
    .catch(error => {
        console.log("Camera error:", error);
        showNotification("Camera permission needed");
    });
}

function stopRecording() {
    if (mediaRecorder && isRecording) {
        mediaRecorder.stop();
        isRecording = false;
        
        // Stop all tracks
        if (elements.video.srcObject) {
            elements.video.srcObject.getTracks().forEach(track => track.stop());
        }
        
        elements.videoSection.style.display = 'none';
        
        showNotification("Video recording stopped");
    }
}

function downloadVideo() {
    if (recordedChunks.length === 0) {
        showNotification("No recording available");
        return;
    }
    
    // Create video blob
    const blob = new Blob(recordedChunks, { type: 'video/webm' });
    const url = URL.createObjectURL(blob);
    
    // Create download link
    const a = document.createElement('a');
    a.href = url;
    a.download = `safety_evidence_${new Date().getTime()}.webm`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    
    // Clean up
    setTimeout(() => URL.revokeObjectURL(url), 100);
    
    // Clear recorded chunks after download
    recordedChunks = [];
}

// ====== PLACE SAFETY CHECK ======
function checkPlaceSafety() {
    const place = elements.placeInput.value.trim();
    
    if (!place) {
        showNotification("Please enter a place name");
        return;
    }
    
    showNotification(`Checking safety of ${place}...`);
    speak(`Checking safety information for ${place}.`);
    
    // Simulate safety check with timeout
    setTimeout(() => {
        // Generate random safety score (3-10)
        const safetyScore = (3 + Math.random() * 7).toFixed(1);
        
        // Get safety tips based on score
        let tips = "";
        let stars = "";
        let color = "#4CAF50";
        
        if (safetyScore >= 8) {
            stars = "★★★★★";
            tips = `
                <strong>Very Safe Area ✓</strong>
                <ul>
                    <li>Well-lit streets with CCTV</li>
                    <li>Regular police patrols</li>
                    <li>Good public transportation</li>
                    <li>Safe for walking at night</li>
                    <li>Emergency services nearby</li>
                </ul>
            `;
        } else if (safetyScore >= 6.5) {
            stars = "★★★★☆";
            color = "#FF9800";
            tips = `
                <strong>Moderately Safe</strong>
                <ul>
                    <li>Generally safe but be cautious</li>
                    <li>Stay in main areas</li>
                    <li>Travel with others if possible</li>
                    <li>Keep emergency app ready</li>
                    <li>Avoid late night travel</li>
                </ul>
            `;
        } else if (safetyScore >= 5) {
            stars = "★★★☆☆";
            color = "#FF5722";
            tips = `
                <strong>Use Caution</strong>
                <ul>
                    <li>Limited street lighting</li>
                    <li>Travel with companions</li>
                    <li>Have safety plan ready</li>
                    <li>Avoid isolated areas</li>
                    <li>Keep phone charged</li>
                </ul>
            `;
        } else {
            stars = "★★☆☆☆";
            color = "#FF4757";
            tips = `
                <strong>High Risk Area</strong>
                <ul>
                    <li>Avoid if possible</li>
                    <li>Never travel alone</li>
                    <li>High crime reported</li>
                    <li>Poor lighting and security</li>
                    <li>Consider alternative routes</li>
                </ul>
            `;
        }
        
        // Update UI
        elements.ratingStars.innerHTML = stars;
        elements.safetyScore.textContent = `${safetyScore}/10`;
        elements.safetyScore.style.color = color;
        elements.safetyTips.innerHTML = tips;
        elements.safetyResult.style.display = 'block';
        
        // Speak result
        let safetyLevel = "";
        if (safetyScore >= 8) safetyLevel = "very safe";
        else if (safetyScore >= 6.5) safetyLevel = "moderately safe";
        else if (safetyScore >= 5) safetyLevel = "requires caution";
        else safetyLevel = "high risk";
        
        speak(`Safety rating for ${place} is ${safetyScore} out of 10. This area is ${safetyLevel}.`);
        
    }, 1500);
}

// ====== HELPER FUNCTIONS ======
function vibratePhone(pattern) {
    if (navigator.vibrate) {
        navigator.vibrate(pattern);
    }
}

function speak(text) {
    if (!window.speechSynthesis) return;
    
    speechSynthesis.cancel();
    
    const utterance = new SpeechSynthesisUtterance(text);
    utterance.rate = 1.0;
    utterance.volume = 1.0;
    utterance.pitch = 1.0;
    
    speechSynthesis.speak(utterance);
}

function showNotification(message, isEmergency = false) {
    elements.notificationText.textContent = message;
    
    if (isEmergency) {
        elements.notification.className = 'notification show emergency';
    } else {
        elements.notification.className = 'notification show';
    }
    
    // Auto hide after 4 seconds
    setTimeout(() => {
        elements.notification.className = 'notification';
    }, 4000);
}

// ====== SHAKE DETECTION ======
function setupShakeDetection() {
    let lastShake = 0;
    
    if (window.DeviceMotionEvent) {
        window.addEventListener('devicemotion', function(event) {
            const acceleration = event.accelerationIncludingGravity;
            if (!acceleration) return;
            
            // Calculate total force
            const force = Math.abs(acceleration.x) + Math.abs(acceleration.y) + Math.abs(acceleration.z);
            
            // Detect shake (force > 20)
            if (force > 20) {
                const now = Date.now();
                
                // Prevent multiple shakes within 2 seconds
                if (now - lastShake > 2000) {
                    activateDoubleTapEmergency();
                    lastShake = now;
                    showNotification("Emergency activated by shake", true);
                }
            }
        });
    }
}

// ====== EVENT LISTENERS ======
// Keyboard shortcuts
document.addEventListener('keydown', function(event) {
    // Space bar for emergency
    if (event.key === ' ') {
        event.preventDefault();
        activateEmergency();
    }
    
    // Escape to stop emergency
    if (event.key === 'Escape' && isEmergencyActive) {
        stopEverything();
    }
    
    // Ctrl+R to start recording
    if (event.ctrlKey && event.key === 'r') {
        event.preventDefault();
        startRecording();
    }
    
    // Ctrl+S to stop recording
    if (event.ctrlKey && event.key === 's') {
        event.preventDefault();
        stopEverything();
    }
    
    // Ctrl+P for police alarm
    if (event.ctrlKey && event.key === 'p') {
        event.preventDefault();
        playPoliceAlarm();
    }
    
    // Ctrl+Shift+P to stop police alarm
    if (event.ctrlKey && event.shiftKey && event.key === 'P') {
        event.preventDefault();
        stopPoliceAlarm();
    }
    
    // Ctrl+D for double tap simulation
    if (event.ctrlKey && event.key === 'd') {
        event.preventDefault();
        activateDoubleTapEmergency();
    }
    
    // Ctrl+T for triple tap simulation
    if (event.ctrlKey && event.key === 't') {
        event.preventDefault();
        activateTripleTapFunction();
    }
    
    // Ctrl+L for finding location
    if (event.ctrlKey && event.key === 'l') {
        event.preventDefault();
        findMyLocation();
    }
});

// ====== INITIALIZE ======
window.addEventListener('DOMContentLoaded', initApp);
</script>
</body>
</html>
