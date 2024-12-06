![image](https://github.com/user-attachments/assets/c46393db-3353-4eec-9174-eb5080425d6e)


上の凡例と、下の人数の数値は固定し、棒グラフだけがスクロールできるようにして欲しい。<br>                       .bar-chart {
    height: auto;
    max-height: 48vh;
    overflow: auto;
}<br><br>function createTotalPeopleBarChart(data) {
    const formattedData = [
        ['Company', '60歳以上', '40～59歳', '40歳未満', '不明']
    ];
    // Sort data by company_name in ascending order
    data.sort((a, b) => a.company_name.localeCompare(b.company_name));

    data.forEach(function (row) {
        // const totalPeople = Number(row.number_of_people);
        const totalPeople = Number(row.number_of_people_1_2_3);
        const over60 = row.number_of_people_over_60_year_old ? Number(row.number_of_people_over_60_year_old) : 0;
        const between40_59 = row.number_of_people_between_40_59_year_old ? Number(row.number_of_people_between_40_59_year_old) : 0;
        const under40 = row.number_of_people_under_40_year_old ? Number(row.number_of_people_under_40_year_old) : 0;

        const definedPeople = over60 + between40_59 + under40;
        const undefinedPeople = totalPeople - definedPeople;
        formattedData.push([
            row.company_name,
            over60 || 0,
            between40_59 || 0,
            under40 || 0,
            undefinedPeople > 0 ? undefinedPeople : 0
        ]);
    });
    return formattedData;
}<br><br>const dataTable = google.visualization.arrayToDataTable(formattedData);
    const numDataPoints = dataTable.getNumberOfRows();
    const numColumns = dataTable.getNumberOfColumns();

    let maxTotalPeople = 0;
    for (let rowIndex = 0; rowIndex < numDataPoints; rowIndex++) {
        let columnTotal = 0;
        for (let colIndex = 1; colIndex < numColumns; colIndex++) { // Start from 1 to skip the first column (company name)
            columnTotal += dataTable.getValue(rowIndex, colIndex);
        }
        if (columnTotal > maxTotalPeople) {
            maxTotalPeople = columnTotal;
        }
    }
    // Generate ticks for the hAxis
    const step = Math.max(1, Math.floor(maxTotalPeople / 10));
    const length = Math.floor(maxTotalPeople / step);
    const ticks = Array.from({ length }, (_, i) => (i + 1) * step);
    var options = {
        title: titleName,
        width: 1200,
        height: numDataPoints >= 20 ? 1800 : 200 + numDataPoints * 50,
        isStacked: true,
        legend: { position: 'top', maxLines: 4 },
        bar: { groupWidth: numDataPoints >= 20 ? '95%' : '50%' },
        chartArea: {
            left: 280,
            top: 80,
            bottom: 50,
            width: '90%',
            height: '80%'
        },
        vAxis: {
            title: '会社名',
            textStyle: {
                fontSize: numDataPoints >= 20 ? 10 : 14
            }
        },
        hAxis: {
            title: '人数',
            viewWindow: {
                min: 0,
                max: maxTotalPeople // Set this to the maximum value you expect
            },
            ticks: ticks, // Use generated ticks
            textStyle: {
                fontSize: 12
            }
        }
    };
    var chart = new google.visualization.BarChart(document.getElementById("chart_div"));
    chart.draw(dataTable, options);<br><br> <div id="chart_div" class="bar-chart"></div>

reference design from image
and add annotation that number of people
上の凡例 is not defined constant cause of this value is change depend on other event
