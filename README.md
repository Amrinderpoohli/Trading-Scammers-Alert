# Trading-Scammers-Alert
“A repository to raise awareness and report scams in trading communities.”
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta content="width=device-width, initial-scale=1" name="viewport"/>
  <title>Trading Scam Alerts</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" rel="stylesheet"/>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet"/>
  <style>
    body {
      font-family: 'Inter', sans-serif;
    }
    #reportsList {
      scrollbar-width: thin;
      scrollbar-color: #a0aec0 transparent;
    }
    #reportsList::-webkit-scrollbar {
      width: 8px;
    }
    #reportsList::-webkit-scrollbar-track {
      background: transparent;
    }
    #reportsList::-webkit-scrollbar-thumb {
      background-color: #a0aec0;
      border-radius: 4px;
      border: 2px solid transparent;
    }
  </style>
</head>
<body class="bg-gray-50 text-gray-900 min-h-screen flex flex-col">
  <header class="bg-white shadow-md">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col sm:flex-row sm:items-center sm:justify-between">
      <div>
        <h1 class="text-3xl font-semibold tracking-tight">Trading Scam Alerts</h1>
        <p class="mt-1 text-gray-600 max-w-xl">Share and read reports to protect the trading community.</p>
        <p class="mt-2 text-sm text-gray-500">Disclaimer: Reports are user-submitted and pending moderation. We don’t guarantee accuracy.</p>
      </div>
      <img alt="Shield icon symbolizing protection for traders" class="mt-4 sm:mt-0" height="80" src="https://storage.googleapis.com/a1aa/image/a34b3fcb-d6f4-4ad8-7c30-1ab829b11548.jpg" width="80"/>
    </div>
  </header>
  <main class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 grid grid-cols-1 lg:grid-cols-3 gap-10">
    <!-- Submission Form -->
    <section class="lg:col-span-1 bg-white rounded-lg shadow-md p-6">
      <h2 class="text-xl font-semibold mb-4 border-b border-gray-200 pb-2">Report a Scam</h2>
      <form class="space-y-5" id="scamForm" novalidate>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1" for="scamType">Scam Type</label>
          <select class="block w-full rounded-md border border-gray-300 shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" id="scamType" name="scamType" required>
            <option disabled selected value="">Select scam type</option>
            <option value="Telegram Group">Telegram Group</option>
            <option value="Funded Account">Funded Account</option>
            <option value="Investment Scheme">Investment Scheme</option>
          </select>
          <p class="mt-1 text-xs text-red-600 hidden" id="scamTypeError">Please select a scam type.</p>
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1" for="scamName">Group/Person/Company Name</label>
          <input class="block w-full rounded-md border border-gray-300 shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" id="scamName" name="scamName" placeholder="Enter name" required type="text"/>
          <p class="mt-1 text-xs text-red-600 hidden" id="scamNameError">Please enter a name.</p>
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1" for="scamDetails">Scam Details</label>
          <textarea class="block w-full rounded-md border border-gray-300 shadow-sm py-2 px-3 resize-y focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" id="scamDetails" name="scamDetails" placeholder="Describe the scam in detail" required rows="4"></textarea>
          <p class="mt-1 text-xs text-red-600 hidden" id="scamDetailsError">Please provide scam details.</p>
        </div>
        <div class="flex items-center space-x-2">
          <input class="h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500" id="postAnonymous" name="postAnonymous" type="checkbox"/>
          <label class="text-sm text-gray-700 select-none" for="postAnonymous">Post Anonymously</label>
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1" for="evidenceLink">Evidence (Google Drive link)</label>
          <input class="block w-full rounded-md border border-gray-300 shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" id="evidenceLink" name="evidenceLink" placeholder="Paste Google Drive link here" type="url"/>
          <p class="mt-1 text-xs text-gray-500">Upload evidence to Google Drive and share the link. Reports are moderated before display.</p>
        </div>
        <button class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-2 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-1" type="submit">Submit Report</button>
      </form>
      <p class="mt-3 text-green-600 font-medium hidden" id="formSuccess">Report submitted! Awaiting moderation.</p>
    </section>
    <!-- Reported Scams and Tips -->
    <section class="lg:col-span-2 flex flex-col space-y-8">
      <!-- Reported Scams -->
      <div class="bg-white rounded-lg shadow-md p-6 flex flex-col">
        <h2 class="text-xl font-semibold mb-4 border-b border-gray-200 pb-2">Reported Scams</h2>
        <div class="mb-4">
          <label class="sr-only" for="searchReports">Search Reports</label>
          <div class="relative text-gray-600 focus-within:text-gray-400">
            <input autocomplete="off" class="block w-full rounded-md border border-gray-300 py-2 pl-10 pr-3 shadow-sm placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" id="searchReports" placeholder="Search by scam type, name, or details..." type="search"/>
            <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
              <i class="fas fa-search text-gray-400"></i>
            </div>
          </div>
        </div>
        <div aria-label="List of reported scams" class="overflow-y-auto max-h-[480px] divide-y divide-gray-200 border border-gray-200 rounded-md" id="reportsList" tabindex="0">
          <!-- Scam reports will be dynamically inserted here -->
        </div>
        <p class="mt-4 text-center text-gray-500 hidden" id="noReportsMsg">No reports found. Submit one to start!</p>
      </div>
      <!-- Tips Section -->
      <div class="bg-white rounded-lg shadow-md p-6">
        <h2 class="text-xl font-semibold mb-3 border-b border-gray-200 pb-2">Tips</h2>
        <p class="text-gray-700 leading-relaxed">Tips: Always check for FCA regulation (e.g., brokers like Pepperstone) and avoid groups promising guaranteed profits.</p>
      </div>
    </section>
  </main>
  <footer class="bg-white border-t border-gray-200 py-6 mt-12">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center text-gray-500 text-sm">
      © 2025 Trading Scam Alerts. All rights reserved.
    </div>
  </footer>
  <script>
    (() => {
      const form = document.getElementById('scamForm');
      const scamType = document.getElementById('scamType');
      const scamName = document.getElementById('scamName');
      const scamDetails = document.getElementById('scamDetails');
      const postAnonymous = document.getElementById('postAnonymous');
      const evidenceLink = document.getElementById('evidenceLink');
      const reportsList = document.getElementById('reportsList');
      const searchInput = document.getElementById('searchReports');
      const formSuccess = document.getElementById('formSuccess');
      const noReportsMsg = document.getElementById('noReportsMsg');

      // Error message elements
      const scamTypeError = document.getElementById('scamTypeError');
      const scamNameError = document.getElementById('scamNameError');
      const scamDetailsError = document.getElementById('scamDetailsError');

      // Storage keys for localStorage
      const PENDING_KEY = 'tradingScamReportsPending';
      const APPROVED_KEY = 'tradingScamReportsApproved';

      // Load reports from localStorage
      function loadReports(key) {
        const data = localStorage.getItem(key);
        if (!data) return [];
        try {
          return JSON.parse(data);
        } catch {
          return [];
        }
      }

      // Save reports to localStorage
      function saveReports(key, reports) {
        localStorage.setItem(key, JSON.stringify(reports));
      }

      // Sanitize input to prevent XSS
      function sanitizeInput(input) {
        const div = document.createElement('div');
        div.textContent = input;
        return div.innerHTML;
      }

      // Format date to readable string
      function formatDate(dateStr) {
        const d = new Date(dateStr);
        if (isNaN(d)) return '';
        return d.toLocaleDateString(undefined, {
          year: 'numeric',
          month: 'short',
          day: 'numeric',
          hour: '2-digit',
          minute: '2-digit',
        });
      }

      // Create a DOM element for a single report
      function createReportElement(report) {
        const container = document.createElement('article');
        container.className = 'p-4 hover:bg-gray-50 focus-within:bg-gray-50 outline-none';

        // Scam type and name
        const header = document.createElement('div');
        header.className = 'flex flex-wrap justify-between items-center mb-2';

        const scamTypeEl = document.createElement('span');
        scamTypeEl.className = 'inline-block bg-indigo-100 text-indigo-800 text-xs font-semibold px-2 py-0.5 rounded';
        scamTypeEl.textContent = sanitizeInput(report.scamType);

        const nameEl = document.createElement('h3');
        nameEl.className = 'text-lg font-semibold text-gray-900 truncate max-w-[70%]';
        nameEl.textContent = report.postAnonymous ? 'Anonymous' : sanitizeInput(report.scamName);

        header.appendChild(nameEl);
        header.appendChild(scamTypeEl);

        // Details
        const detailsEl = document.createElement('p');
        detailsEl.className = 'text-gray-700 mb-2 whitespace-pre-wrap';
        detailsEl.textContent = sanitizeInput(report.scamDetails);

        // Evidence link
        const evidenceEl = document.createElement('div');
        evidenceEl.className = 'mb-2';
        if (report.evidenceLink) {
          const link = document.createElement('a');
          link.href = sanitizeInput(report.evidenceLink);
          link.target = '_blank';
          link.rel = 'noopener noreferrer';
          link.className = 'text-indigo-600 hover:underline flex items-center space-x-2';
          link.innerHTML = '<i class="fas fa-link"></i><span>View Evidence Link</span>';
          evidenceEl.appendChild(link);
        }

        // Posted date
        const dateEl = document.createElement('time');
        dateEl.className = 'text-xs text-gray-500';
        dateEl.dateTime = report.postedDate;
        dateEl.textContent = `Posted: ${formatDate(report.postedDate)}`;

        container.appendChild(header);
        container.appendChild(detailsEl);
        if (evidenceEl.children.length) container.appendChild(evidenceEl);
        container.appendChild(dateEl);

        container.tabIndex = 0;

        return container;
      }

      // Render approved reports filtered by search term
      function renderReports(filter = '') {
        const reports = loadReports(APPROVED_KEY);
        const filtered = reports.filter((r) => {
          const search = filter.toLowerCase();
          return (
            r.scamType.toLowerCase().includes(search) ||
            r.scamName.toLowerCase().includes(search) ||
            r.scamDetails.toLowerCase().includes(search)
          );
        });

        reportsList.innerHTML = '';
        if (filtered.length === 0) {
          noReportsMsg.classList.remove('hidden');
          return;
        } else {
          noReportsMsg.classList.add('hidden');
        }

        filtered
          .sort((a, b) => new Date(b.postedDate) - new Date(a.postedDate))
          .forEach((report) => {
            const el = createReportElement(report);
            reportsList.appendChild(el);
          });
      }

      // Validate form fields and show/hide error messages
      function validateForm() {
        let valid = true;

        ifSRP (!scamType.value) {
          scamTypeError.classList.remove('hidden');
          valid = false;
        } else {
          scamTypeError.classList.add('hidden');
        }

        if (!scamName.value.trim()) {
          scamNameError.classList.remove('hidden');
          valid = false;
        } else {
          scamNameError.classList.add('hidden');
        }

        if (!scamDetails.value.trim()) {
          scamDetailsError.classList.remove('hidden');
          valid = false;
        } else {
          scamDetailsError.classList.add('hidden');
        }

        return valid;
      }

      // Clear form inputs
      function clearForm() {
        form.reset();
        evidenceLink.value = '';
      }

      // On form submit
      form.addEventListener('submit', (e) => {
        e.preventDefault();
        formSuccess.classList.add('hidden');

        if (!validateForm()) {
          return;
        }

        // Prepare report object
        const report = {
          scamType: sanitizeInput(scamType.value),
          scamName: sanitizeInput(scamName.value.trim()),
          scamDetails: sanitizeInput(scamDetails.value.trim()),
          postAnonymous: postAnonymous.checked,
          evidenceLink: evidenceLink.value.trim() ? sanitizeInput(evidenceLink.value.trim()) : null,
          postedDate: new Date().toISOString(),
        };

        // Basic URL validation for evidence link
        if (report.evidenceLink) {
          try {
            new URL(report.evidenceLink);
          } catch {
            alert('Please enter a valid URL for the evidence link.');
            return;
          }
        }

        // Save to pending reports in localStorage
        const pendingReports = loadReports(PENDING_KEY);
        pendingReports.push(report);
        saveReports(PENDING_KEY, pendingReports);

        // Update UI
        clearForm();
        formSuccess.classList.remove('hidden');

        // Scroll to reports section on mobile after submit
        if (window.innerWidth < 1024) {
          reportsList.scrollIntoView({ behavior: 'smooth' });
        }

        // Note: For a live site, pending reports need manual moderation
        alert('Report submitted! Awaiting moderation. For now, manually add to approved list.');
      });

      // Search input event
      searchInput.addEventListener('input', (e) => {
        renderReports(e.target.value.trim());
      });

      // Initial render
      renderReports();
    })();
  </script>
</body>
</html>