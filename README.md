<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dependent Filters</title>
</head>
<body>
    <h2>Dynamic Dependent Filters</h2>

    <!-- Filters -->
    <label for="filter1">ID:</label>
    <input type="text" id="filter1" onkeyup="updateFilters(1)" placeholder="Enter ID"><br><br>

    <label for="filter2">Name:</label>
    <input type="text" id="filter2" onkeyup="updateFilters(2)" placeholder="Enter Name"><br><br>

    <label for="filter3">Category:</label>
    <input type="text" id="filter3" onkeyup="updateFilters(3)" placeholder="Enter Category"><br><br>

    <label for="filter4">Location:</label>
    <input type="text" id="filter4" onkeyup="updateFilters(4)" placeholder="Enter Location"><br><br>

    <label for="filter5">Status:</label>
    <input type="text" id="filter5" onkeyup="updateFilters(5)" placeholder="Enter Status"><br><br>

    <!-- Results -->
    <h3>Results:</h3>
    <div id="results"></div>

    <script>
        // Fetches options for other filters based on current filter values
        async function fetchOptions(filterValues) {
            try {
                // Replace with actual API endpoint
                const response = await fetch(`https://yourapi.com/filters?${new URLSearchParams(filterValues)}`);
                const data = await response.json();

                return data;  // assuming the API response has options for each filter
            } catch (error) {
                console.error('Error fetching options:', error);
                return {};
            }
        }

        async function updateFilters(changedFilter) {
            // Gather current values from all filters
            const filterValues = {
                filter1: document.getElementById('filter1').value,
                filter2: document.getElementById('filter2').value,
                filter3: document.getElementById('filter3').value,
                filter4: document.getElementById('filter4').value,
                filter5: document.getElementById('filter5').value
            };

            // Fetch updated options for other filters based on current filter values
            const options = await fetchOptions(filterValues);

            // Update each filter's placeholder with new options based on the response
            if (changedFilter !== 1) {
                updateFilterPlaceholder('filter1', options.filter1);
            }
            if (changedFilter !== 2) {
                updateFilterPlaceholder('filter2', options.filter2);
            }
            if (changedFilter !== 3) {
                updateFilterPlaceholder('filter3', options.filter3);
            }
            if (changedFilter !== 4) {
                updateFilterPlaceholder('filter4', options.filter4);
            }
            if (changedFilter !== 5) {
                updateFilterPlaceholder('filter5', options.filter5);
            }

            // Update the results section
            updateResults(filterValues);
        }

        // Update the placeholder with available options
        function updateFilterPlaceholder(filterId, options) {
            const filter = document.getElementById(filterId);
            filter.placeholder = options && options.length > 0 ? `Available options: ${options.join(', ')}` : 'No options available';
        }

        // Fetches and displays filtered results based on current filter values
        async function updateResults(filterValues) {
            try {
                // Replace with actual API endpoint
                const response = await fetch(`https://yourapi.com/results?${new URLSearchParams(filterValues)}`);
                const data = await response.json();

                // Display results
                const resultsDiv = document.getElementById('results');
                resultsDiv.innerHTML = JSON.stringify(data.results, null, 2);  // assuming API response has `results` array
            } catch (error) {
                console.error('Error fetching results:', error);
            }
        }
    </script>
</body>
</html>

<!---
winngwephyo9/winngwephyo9 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
