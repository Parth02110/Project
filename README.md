
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Registration Portal - Single Submission System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .hero-bg {
            background: linear-gradient(135deg, #0f0c29 0%, #302b63 50%, #24243e 100%);
        }
        .form-container {
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }
        .event-card {
            transition: all 0.3s ease;
        }
        .event-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
        }
        .success-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        .modal-content {
            background: white;
            border-radius: 10px;
            padding: 30px;
            text-align: center;
        }
        .admin-toggle {
            font-size: 14px;
            color: #666;
            cursor: pointer;
        }
        .admin-section {
            display: none;
            margin-top: 50px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 20px;
        }
    </style>
</head>
<body class="hero-bg min-h-screen text-gray-800">
    <div id="successModal" class="success-modal">
        <div class="modal-content">
            <h2 class="text-2xl font-bold text-green-600 mb-4">Registration Successful!</h2>
            <p class="mb-4">Your form has been submitted successfully for the selected event. Data recorded in system.</p>
          
            <button onclick="closeModal()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Close</button>
        </div>
    </div>

    <div class="container mx-auto px-4 py-10">
        <header class="text-center mb-10">
            <h1 class="text-5xl font-extrabold text-white mb-4">Event Registration Portal</h1>
            <p class="text-xl text-gray-300">Choose one event to register. Secure system ensures data privacy.</p>
        </header>

        <main class="max-w-4xl mx-auto">
            <div class="form-container bg-white rounded-lg p-8 event-card">
                <h2 class="text-2xl font-semibold mb-6 text-center">Register for the Events</h2>
                <form id="registrationForm" class="space-y-6">
                    <div class="grid md:grid-cols-2 gap-6">
                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-700 mb-2">Full Name</label>
                            <input type="text" id="name" name="name" required 
                                   class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
                                   placeholder="Enter your full name">
                        </div>
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-700 mb-2">Email Address</label>
                            <input type="email" id="email" name="email" required 
                                   class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
                                   placeholder="your.email@example.com">
                        </div>
                    </div>
                    
                    <div>
                        <label for="event" class="block text-sm font-medium text-gray-700 mb-2">Select Event (One at a time)</label>
                        <select id="event" name="event" required 
                                class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
                            <option value="" disabled selected>Choose an event to attend</option>
                            <option value="Event 1: Tech Conference">Event 1: Tech Conference - Immersive innovation talks</option>
                            <option value="Event 2: Art Workshop">Event 2: Art Workshop - Creative hands-on sessions</option>
                            <option value="Event 3: Music Festival">Event 3: Music Festival - Live performances and networking</option>
                            <option value="Event 4: Cooking Class">Event 4: Cooking Class - Gourmet tasting experience</option>
                            <option value="Event 5: Yoga Retreat">Event 5: Yoga Retreat - Wellness and relaxation journey</option>
                            <option value="Event 6: Coding Bootcamp">Event 6: Coding Bootcamp - Intensive learning program</option>
                            <option value="Event 7: Business Networking">Event 7: Business Networking - Professional connections event</option>
                        </select>
                    </div>
                    
                    <button type="submit" 
                            class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-md transition duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
                        Submit Registration
                    </button>
                </form>
            </div>

            <div class="mt-4 text-center">
                <p id="adminToggle" class="admin-toggle" onclick="toggleAdmin()">Owner/Admin Access</p>
            </div>

            <div id="adminSection" class="admin-section">
                <h3 class="text-xl font-semibold mb-4">Admin: Registration Database (Simulated Excel View)</h3>
                <div class="overflow-x-auto">
                    <table class="min-w-full bg-white border border-gray-300">
                        <thead class="bg-gray-100">
                            <tr>
                                <th class="px-4 py-2 border-b text-left">Name</th>
                                <th class="px-4 py-2 border-b text-left">Email</th>
                                <th class="px-4 py-2 border-b text-center">Event 1</th>
                                <th class="px-4 py-2 border-b text-center">Event 2</th>
                                <th class="px-4 py-2 border-b text-center">Event 3</th>
                                <th class="px-4 py-2 border-b text-center">Event 4</th>
                                <th class="px-4 py-2 border-b text-center">Event 5</th>
                                <th class="px-4 py-2 border-b text-center">Event 6</th>
                                <th class="px-4 py-2 border-b text-center">Event 7</th>
                            </tr>
                        </thead>
                        <tbody id="registrationTableBody">
                            <!-- Data will be loaded here -->
                        </tbody>
                    </table>
                </div>
                <p class="text-sm text-gray-600 mt-4">Data is stored locally. Refresh to update view.</p>
            </div>
        </main>
    </div>

    <script>
        // List of events for dynamic handling
        const events = [
            "Event 1: Tech Conference",
            "Event 2: Art Workshop",
            "Event 3: Music Festival",
            "Event 4: Cooking Class",
            "Event 5: Yoga Retreat",
            "Event 6: Coding Bootcamp",
            "Event 7: Business Networking"
        ];

        // Load registrations from localStorage (simulating database/Excel)
        let registrations = JSON.parse(localStorage.getItem('eventRegistrations')) || [];

        // Function to render the admin table
        function renderAdminTable() {
            const tbody = document.getElementById('registrationTableBody');
            tbody.innerHTML = '';

            registrations.forEach((reg) => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td class="px-4 py-2 border-b">${reg.name}</td>
                    <td class="px-4 py-2 border-b">${reg.email}</td>
                    ${events.map(ev => `<td class="px-4 py-2 border-b text-center">${reg.event === ev ? 'Registered' : ''}</td>`).join('')}
                `;
                tbody.appendChild(row);
            });
        }

        // Toggle admin section with password prompt (simple simulation)
        function toggleAdmin() {
            const password = prompt('Enter admin password to view registrations:');
            if (password === 'adminpassword') {  // Change this password as needed
                renderAdminTable();
                document.getElementById('adminSection').style.display = 'block';
                document.getElementById('adminToggle').style.display = 'none';
            } else {
                alert('Incorrect password. Access denied.');
            }
        }

        // Handle form submission
        document.getElementById('registrationForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const name = document.getElementById('name').value.trim();
            const email = document.getElementById('email').value.trim();
            const selectedEvent = document.getElementById('event').value;

            if (!name || !email || !selectedEvent) {
                alert('Please fill in all fields.');
                return;
            }

            // Create registration object
            const registration = {
                name: name,
                email: email,
                event: selectedEvent,
                timestamp: new Date().toISOString()
            };

            // Add to registrations array
            registrations.push(registration);
            
            // Save to localStorage (simulating Excel file storage)
            localStorage.setItem('eventRegistrations', JSON.stringify(registrations));

            // Show success modal
            document.getElementById('successModal').style.display = 'flex';
            
            // Log to console for debugging (simulating console output like Flask)
            console.log('New Registration:\n', registration);

            // Reset form
            this.reset();
        });

        // Close modal function
        function closeModal() {
            document.getElementById('successModal').style.display = 'none';
        }

        // Update admin table on load if admin was previously opened
        window.addEventListener('load', function() {
            if (document.getElementById('adminSection').style.display === 'block') {
                renderAdminTable();
            }
        });
    </script>
</body>
</html>
</content>
</create_file>
