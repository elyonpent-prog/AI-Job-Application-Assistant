# AI-Job-Application-Assistant
Automate your job applications with intelligent CV distribution

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Job Application Assistant</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        
        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }
        
        .content {
            padding: 40px;
        }
        
        .section {
            margin-bottom: 40px;
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            border-left: 5px solid #4facfe;
        }
        
        .section h2 {
            color: #333;
            margin-bottom: 20px;
            font-size: 1.8em;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #555;
        }
        
        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: #4facfe;
        }
        
        .form-group textarea {
            height: 120px;
            resize: vertical;
        }
        
        .btn {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            margin-right: 10px;
            margin-bottom: 10px;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.4);
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        
        .job-list {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
        }
        
        .job-item {
            background: white;
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 10px;
            border-left: 4px solid #4facfe;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
        }
        
        .job-item h3 {
            color: #333;
            margin-bottom: 10px;
        }
        
        .job-item p {
            color: #666;
            margin-bottom: 5px;
        }
        
        .status {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
        }
        
        .status.pending { background: #fff3cd; color: #856404; }
        .status.sent { background: #d4edda; color: #155724; }
        .status.failed { background: #f8d7da; color: #721c24; }
        
        .tabs {
            display: flex;
            border-bottom: 2px solid #e0e0e0;
            margin-bottom: 30px;
        }
        
        .tab {
            padding: 15px 25px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
            font-weight: 600;
        }
        
        .tab.active {
            border-bottom-color: #4facfe;
            color: #4facfe;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .progress-bar {
            background: #e0e0e0;
            height: 8px;
            border-radius: 4px;
            margin: 10px 0;
            overflow: hidden;
        }
        
        .progress-fill {
            background: linear-gradient(90deg, #4facfe, #00f2fe);
            height: 100%;
            width: 0%;
            transition: width 0.3s;
        }
        
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        
        .alert-info {
            background: #e7f3ff;
            border-left: 4px solid #4facfe;
            color: #0c5460;
        }
        
        .alert-success {
            background: #d4edda;
            border-left: 4px solid #28a745;
            color: #155724;
        }
        
        @media (max-width: 768px) {
            .header h1 { font-size: 2em; }
            .content { padding: 20px; }
            .section { padding: 20px; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🤖 AI Job Application Assistant</h1>
            <p>Automate your job applications with intelligent CV distribution</p>
        </div>
        
        <div class="content">
            <div class="tabs">
                <div class="tab active" onclick="switchTab('setup')">Setup</div>
                <div class="tab" onclick="switchTab('jobs')">Job Search</div>
                <div class="tab" onclick="switchTab('applications')">Applications</div>
                <div class="tab" onclick="switchTab('analytics')">Analytics</div>
            </div>
            
            <!-- Setup Tab -->
            <div id="setup" class="tab-content active">
                <div class="section">
                    <h2>📋 Profile Setup</h2>
                    <div class="form-group">
                        <label>Upload Your CV</label>
                        <input type="file" id="cvFile" accept=".pdf,.doc,.docx" onchange="handleCVUpload(event)">
                    </div>
                    
                    <div class="form-group">
                        <label>Full Name</label>
                        <input type="text" id="fullName" placeholder="Enter your full name">
                    </div>
                    
                    <div class="form-group">
                        <label>Email Address</label>
                        <input type="email" id="email" placeholder="your.email@example.com">
                    </div>
                    
                    <div class="form-group">
                        <label>Phone Number</label>
                        <input type="tel" id="phone" placeholder="+1 (555) 123-4567">
                    </div>
                    
                    <div class="form-group">
                        <label>Target Job Titles</label>
                        <textarea id="jobTitles" placeholder="e.g., Software Engineer, Full Stack Developer, Frontend Developer"></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label>Skills & Keywords</label>
                        <textarea id="skills" placeholder="e.g., JavaScript, React, Python, Machine Learning, etc."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label>Cover Letter Template</label>
                        <textarea id="coverLetter" placeholder="Dear Hiring Manager, I am writing to express my interest in the [POSITION] role at [COMPANY]..."></textarea>
                    </div>
                    
                    <button class="btn" onclick="saveProfile()">Save Profile</button>
                </div>
            </div>
            
            <!-- Jobs Tab -->
            <div id="jobs" class="tab-content">
                <div class="section">
                    <h2>🔍 Job Search Configuration</h2>
                    
                    <div class="form-group">
                        <label>Job Boards to Monitor</label>
                        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px; margin-top: 10px;">
                            <label><input type="checkbox" checked> LinkedIn Jobs</label>
                            <label><input type="checkbox" checked> Indeed</label>
                            <label><input type="checkbox" checked> Glassdoor</label>
                            <label><input type="checkbox"> AngelList</label>
                            <label><input type="checkbox"> Stack Overflow Jobs</label>
                            <label><input type="checkbox"> Remote.co</label>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>Location</label>
                        <input type="text" id="location" placeholder="e.g., New York, NY or Remote">
                    </div>
                    
                    <div class="form-group">
                        <label>Salary Range (Annual)</label>
                        <div style="display: flex; gap: 10px;">
                            <input type="number" placeholder="Min (e.g., 80000)" style="width: 50%;">
                            <input type="number" placeholder="Max (e.g., 120000)" style="width: 50%;">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>Experience Level</label>
                        <select>
                            <option>Entry Level (0-2 years)</option>
                            <option>Mid Level (3-5 years)</option>
                            <option>Senior Level (5-10 years)</option>
                            <option>Lead/Principal (10+ years)</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label>Company Size Preference</label>
                        <select>
                            <option>Any Size</option>
                            <option>Startup (1-50 employees)</option>
                            <option>Small (51-200 employees)</option>
                            <option>Medium (201-1000 employees)</option>
                            <option>Large (1000+ employees)</option>
                        </select>
                    </div>
                    
                    <button class="btn" onclick="startJobSearch()">🚀 Start Automated Job Search</button>
                    <button class="btn btn-secondary" onclick="pauseSearch()">⏸️ Pause Search</button>
                </div>
                
                <div class="alert alert-info">
                    <strong>🔄 Search Status:</strong> <span id="searchStatus">Ready to start</span>
                    <div class="progress-bar">
                        <div class="progress-fill" id="searchProgress"></div>
                    </div>
                </div>
            </div>
            
            <!-- Applications Tab -->
            <div id="applications" class="tab-content">
                <div class="section">
                    <h2>📊 Application Management</h2>
                    
                    <div style="display: flex; gap: 20px; margin-bottom: 20px;">
                        <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #4facfe, #00f2fe); color: white; border-radius: 10px; flex: 1;">
                            <h3 id="totalApps">0</h3>
                            <p>Total Applications</p>
                        </div>
                        <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #43e97b, #38f9d7); color: white; border-radius: 10px; flex: 1;">
                            <h3 id="successRate">0%</h3>
                            <p>Success Rate</p>
                        </div>
                        <div style="text-align: center; padding: 20px; background: linear-gradient(135deg, #fa709a, #fee140); color: white; border-radius: 10px; flex: 1;">
                            <h3 id="pendingApps">0</h3>
                            <p>Pending</p>
                        </div>
                    </div>
                    
                    <div class="job-list" id="applicationsList">
                        <!-- Applications will be populated here -->
                    </div>
                    
                    <button class="btn" onclick="exportApplications()">📥 Export to CSV</button>
                    <button class="btn btn-secondary" onclick="generateReport()">📈 Generate Report</button>
                </div>
            </div>
            
            <!-- Analytics Tab -->
            <div id="analytics" class="tab-content">
                <div class="section">
                    <h2>📈 Application Analytics</h2>
                    
                    <div class="alert alert-success">
                        <strong>🎯 AI Insights:</strong> Based on your application data, you have a higher success rate with remote positions and companies in the tech sector. Consider focusing more applications on these types of opportunities.
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px;">
                        <div style="background: white; padding: 20px; border-radius: 10px; border-left: 4px solid #4facfe;">
                            <h3>Top Performing Keywords</h3>
                            <ul style="list-style: none; padding: 0;">
                                <li style="padding: 8px 0; border-bottom: 1px solid #eee;">React - 85% response rate</li>
                                <li style="padding: 8px 0; border-bottom: 1px solid #eee;">JavaScript - 78% response rate</li>
                                <li style="padding: 8px 0; border-bottom: 1px solid #eee;">Full Stack - 72% response rate</li>
                                <li style="padding: 8px 0;">Python - 68% response rate</li>
                            </ul>
                        </div>
                        
                        <div style="background: white; padding: 20px; border-radius: 10px; border-left: 4px solid #43e97b;">
                            <h3>Best Application Times</h3>
                            <ul style="list-style: none; padding: 0;">
                                <li style="padding: 8px 0; border-bottom: 1px solid #eee;">Tuesday 10 AM - Highest open rate</li>
                                <li style="padding: 8px 0; border-bottom: 1px solid #eee;">Wednesday 2 PM - Best response time</li>
                                <li style="padding: 8px 0; border-bottom: 1px solid #eee;">Thursday 11 AM - Most interviews</li>
                                <li style="padding: 8px 0;">Friday 3 PM - Avoid (low response)</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let jobApplications = [];
        let searchInterval;
        let isSearching = false;

        function switchTab(tabName) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // Remove active class from all tabs
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Show selected tab content
            document.getElementById(tabName).classList.add('active');
            
            // Add active class to clicked tab
            event.target.classList.add('active');
        }

        function handleCVUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    // In a real implementation, you'd parse the CV content here
                    console.log('CV uploaded:', file.name);
                    alert(`CV "${file.name}" uploaded successfully! 📄`);
                };
                reader.readAsText(file);
            }
        }

        function saveProfile() {
            const profile = {
                fullName: document.getElementById('fullName').value,
                email: document.getElementById('email').value,
                phone: document.getElementById('phone').value,
                jobTitles: document.getElementById('jobTitles').value,
                skills: document.getElementById('skills').value,
                coverLetter: document.getElementById('coverLetter').value
            };
            
            // Store profile (in real app, this would go to a backend)
            console.log('Profile saved:', profile);
            alert('Profile saved successfully! ✅');
        }

        function startJobSearch() {
            if (isSearching) return;
            
            isSearching = true;
            document.getElementById('searchStatus').textContent = 'Searching for jobs...';
            
            // Simulate job search progress
            let progress = 0;
            const progressBar = document.getElementById('searchProgress');
            
            searchInterval = setInterval(() => {
                progress += Math.random() * 20;
                if (progress > 100) progress = 100;
                
                progressBar.style.width = progress + '%';
                
                if (progress >= 100) {
                    clearInterval(searchInterval);
                    document.getElementById('searchStatus').textContent = 'Search completed! Found new opportunities.';
                    generateSampleApplications();
                    isSearching = false;
                }
            }, 500);
        }

        function pauseSearch() {
            if (searchInterval) {
                clearInterval(searchInterval);
                isSearching = false;
                document.getElementById('searchStatus').textContent = 'Search paused';
            }
        }

        function generateSampleApplications() {
            const sampleJobs = [
                {
                    title: 'Senior Frontend Developer',
                    company: 'TechCorp Inc.',
                    location: 'San Francisco, CA',
                    salary: '$95,000 - $125,000',
                    status: 'sent',
                    appliedDate: new Date().toLocaleDateString()
                },
                {
                    title: 'Full Stack Engineer',
                    company: 'StartupXYZ',
                    location: 'Remote',
                    salary: '$80,000 - $110,000',
                    status: 'pending',
                    appliedDate: new Date().toLocaleDateString()
                },
                {
                    title: 'React Developer',
                    company: 'Digital Solutions Ltd',
                    location: 'New York, NY',
                    salary: '$90,000 - $120,000',
                    status: 'sent',
                    appliedDate: new Date().toLocaleDateString()
                }
            ];
            
            jobApplications = [...jobApplications, ...sampleJobs];
            updateApplicationsDisplay();
            updateStats();
        }

        function updateApplicationsDisplay() {
            const applicationsList = document.getElementById('applicationsList');
            applicationsList.innerHTML = '';
            
            jobApplications.forEach((app, index) => {
                const jobItem = document.createElement('div');
                jobItem.className = 'job-item';
                jobItem.innerHTML = `
                    <h3>${app.title}</h3>
                    <p><strong>Company:</strong> ${app.company}</p>
                    <p><strong>Location:</strong> ${app.location}</p>
                    <p><strong>Salary:</strong> ${app.salary}</p>
                    <p><strong>Applied:</strong> ${app.appliedDate}</p>
                    <span class="status ${app.status}">${app.status}</span>
                `;
                applicationsList.appendChild(jobItem);
            });
        }

        function updateStats() {
            const totalApps = jobApplications.length;
            const sentApps = jobApplications.filter(app => app.status === 'sent').length;
            const pendingApps = jobApplications.filter(app => app.status === 'pending').length;
            const successRate = totalApps > 0 ? Math.round((sentApps / totalApps) * 100) : 0;
            
            document.getElementById('totalApps').textContent = totalApps;
            document.getElementById('successRate').textContent = successRate + '%';
            document.getElementById('pendingApps').textContent = pendingApps;
        }

        function exportApplications() {
            if (jobApplications.length === 0) {
                alert('No applications to export yet!');
                return;
            }
            
            const csvContent = "data:text/csv;charset=utf-8," + 
                "Title,Company,Location,Salary,Status,Applied Date\n" +
                jobApplications.map(app => 
                    `"${app.title}","${app.company}","${app.location}","${app.salary}","${app.status}","${app.appliedDate}"`
                ).join('\n');
            
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "job_applications.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function generateReport() {
            alert('📊 Detailed analytics report generated! Check your email for the full report.');
        }

        // Initialize the app
        updateStats();
    </script>
</body>
</html>
