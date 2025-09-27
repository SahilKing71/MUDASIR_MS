<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic GitHub README Preview</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles for a dark, stylish look and Inter font */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #1a202c; /* Dark background */
            color: #e2e8f0; /* Light text */
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: flex-start; /* Start content from the top */
            padding: 20px;
        }
        .container {
            width: 100%;
            max-width: 900px;
        }
        /* Custom Heroku-like magenta color */
        .heroku-bg {
            background-color: #430098;
        }
        .heroku-icon {
            color: #fff;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- HEADER WITH DYNAMIC WIDGETS (CLOCK & BATTERY) -->
        <header class="flex justify-between items-center p-4 bg-gray-800 rounded-xl shadow-lg mb-8 flex-wrap">
            
            <!-- Live Digital Clock (Top-Left) -->
            <div id="live-clock" class="text-2xl font-extrabold text-teal-400 p-2 sm:p-0 w-full sm:w-auto text-center sm:text-left">
                <!-- Clock will be injected here -->
            </div>

            <h1 class="text-3xl sm:text-4xl font-black text-center text-white my-4 sm:my-0 w-full sm:w-auto">
                Mera Dynamic README
            </h1>

            <!-- Live Battery Status (Top-Right) -->
            <div id="battery-status" class="text-lg font-medium text-amber-400 p-2 sm:p-0 w-full sm:w-auto text-center sm:text-right">
                <!-- Battery info will be injected here -->
                Battery Loading...
            </div>

        </header>

        <!-- MAIN CONTENT AREA -->
        <main class="space-y-6">
            
            <!-- Project Introduction Card -->
            <section class="p-6 bg-gray-700 rounded-xl shadow-2xl transition duration-300 hover:shadow-teal-500/50">
                <h2 class="text-2xl font-bold text-teal-400 mb-3">📋 Project Ka Naam: Awesome App</h2>
                <p class="text-gray-300 leading-relaxed">
                    Yeh project ek naye tareeqe se data manage karne ka hal (solution) pesh karta hai. Ismein modern web technologies aur user-centric design ka istemaal kiya gaya hai. Aap is project ko deploy karke dekhein!
                </p>
            </section>

            <!-- Heroku-themed Link Box -->
            <section class="p-6 heroku-bg rounded-xl shadow-2xl border-4 border-purple-400">
                <div class="flex items-center justify-between flex-wrap">
                    
                    <!-- Heroku Icon (Custom SVG) -->
                    <div class="flex items-center space-x-3">
                        <svg class="heroku-icon w-8 h-8" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm-5-9h10a1 1 0 011 1v2a1 1 0 01-1 1H5a1 1 0 01-1-1v-2a1 1 0 011-1zM5 7h10a1 1 0 011 1v.5a1 1 0 01-1 1H5a1 1 0 01-1-1V8a1 1 0 011-1zm0 8h10a1 1 0 011 1v.5a1 1 0 01-1 1H5a1 1 0 01-1-1V16a1 1 0 011-1z" clip-rule="evenodd"></path>
                        </svg>
                        <h3 class="text-xl font-semibold text-white">🚀 Live Deployment / Heroku Link</h3>
                    </div>

                    <!-- GitHub/Deployed Link Button -->
                    <a id="project-link" href="https://github.com/your-github-username/your-repo-name" target="_blank" class="mt-4 sm:mt-0 px-6 py-3 bg-white text-gray-900 font-bold rounded-full shadow-lg hover:bg-gray-200 transition duration-300 transform hover:scale-105">
                        GitHub Par Dekhein
                    </a>
                </div>
            </section>
        </main>
    </div>

    <script>
        // --- JAVASCRIPT FOR DYNAMIC FEATURES ---

        // 1. Live Digital Clock
        function updateClock() {
            const now = new Date();
            // Options for time formatting (e.g., 10:45:30 AM)
            const options = { hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: true };
            const timeString = now.toLocaleTimeString('en-US', options);
            document.getElementById('live-clock').textContent = timeString;
        }

        // Update clock every second
        setInterval(updateClock, 1000);
        updateClock(); // Initial call to display immediately

        // 2. Live Battery Status
        function updateBattery(battery) {
            const statusElement = document.getElementById('battery-status');
            
            // Calculate percentage
            const level = (battery.level * 100).toFixed(0);
            const charging = battery.charging ? '⚡ Charging' : '🔋 Discharging';
            
            // Display status
            statusElement.innerHTML = `${level}% | ${charging}`;
        }

        function handleBatteryStatus() {
            // Check if the Battery Status API is supported
            if ('getBattery' in navigator) {
                navigator.getBattery().then(battery => {
                    // Initial status display
                    updateBattery(battery);

                    // Listen for changes in level and charging status
                    battery.addEventListener('levelchange', () => updateBattery(battery));
                    battery.addEventListener('chargingchange', () => updateBattery(battery));
                }).catch(error => {
                    console.error("Battery API access denied:", error);
                    document.getElementById('battery-status').textContent = '⚠️ Battery Status (Access Denied)';
                });
            } else {
                // Fallback message if the API is not supported by the browser
                document.getElementById('battery-status').textContent = '❌ Battery API Not Supported';
            }
        }
        
        // Run the battery handler when the window loads
        window.onload = handleBatteryStatus;

        // You can change the GitHub link here:
        document.getElementById('project-link').href = 'YOUR_ACTUAL_GITHUB_REPOSITORY_URL'; // Replace this URL
    </script>
</body>
</html>
