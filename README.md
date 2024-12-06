
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fixed Legend Chart</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        #chart-container {
            width: 100%;
            max-width: 800px;
            margin: auto;
        }
        .chart-legend {
            text-align: center;
            margin-bottom: 20px;
        }
    </style>
</head>
<body>
    <div id="chart-container">
        <div class="chart-legend">
            <strong>Categories: </strong>
            <span style="color: #4a90e2;">Fantasy & Sci-Fi</span>,
            <span style="color: #e94e77;">Romance</span>,
            <span style="color: #f5a623;">Mystery/Crime</span>,
            <span style="color: #7ed321;">General</span>,
            <span style="color: #bd10e0;">Western</span>,
            <span style="color: #50e3c2;">Literature</span>
        </div>
        <canvas id="myChart"></canvas>
    </div>

    <script>
        const ctx = document.getElementById('myChart').getContext('2d');
        const myChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['2010', '2020', '2030'], // X-axis years
                datasets: [
                    {
                        label: 'Fantasy & Sci-Fi',
                        data: [12, 19, 3],
                        backgroundColor: '#4a90e2'
                    },
                    {
                        label: 'Romance',
                        data: [5, 15, 10],
                        backgroundColor: '#e94e77'
                    },
                    {
                        label: 'Mystery/Crime',
                        data: [8, 10, 12],
                        backgroundColor: '#f5a623'
                    },
                    {
                        label: 'General',
                        data: [6, 7, 8],
                        backgroundColor: '#7ed321'
                    },
                    {
                        label: 'Western',
                        data: [3, 5, 7],
                        backgroundColor: '#bd10e0'
                    },
                    {
                        label: 'Literature',
                        data: [9, 8, 11],
                        backgroundColor: '#50e3c2'
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: false // Hide the legend inside the chart
                    },
                    tooltip: {
                        enabled: true
                    }
                },
                scales: {
                    x: {
                        stacked: true
                    },
                    y: {
                        stacked: true
                    }
                }
            }
        });
    </script>
</body>
</html>



![image](https://github.com/user-attachments/assets/a67cb035-c242-4f95-b562-dbd3daec8f3d)

I want to fixed display (Fantasy & Sci Fi
Romance
Mystery/Crime
General
Western
Literature)
not scrolling 
