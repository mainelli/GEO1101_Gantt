<html>
<head>

  <h1> Team 5 Gantt Chart </h1>
  <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
  <script type="text/javascript">
    google.charts.load('current', {'packages':['gantt']});
    google.charts.setOnLoadCallback(drawChart);

    var today = new Date();
    var yyyy = today.getFullYear();
    var mm = String(today.getMonth()).padStart(2, '0');
    var dd = String(today.getDate()).padStart(2, '0');
    var mm_forshow = String(today.getMonth() +1).padStart(2, '0');

    today = new Date(yyyy, mm, dd);
    showdate = yyyy + '/' + (mm_forshow) + '/' + dd;
    document.write("Today's date: "+ showdate);


    function millisecondsToDays(milliseconds) {
      return milliseconds / 1000 / 60 / 60 / 24;
    }

    function percent (startdate, duration) {
      var now = today; //"now"
      var start = startdate;  // some date
      var diff = (now-start);  // difference in milliseconds
      days = millisecondsToDays(diff);
      progress = ((days/duration) * 100);
      return progress;
    }

    function drawChart() {

      var otherData = new google.visualization.DataTable();
      otherData.addColumn('string', 'Task ID');
      otherData.addColumn('string', 'Task Name');
      otherData.addColumn('string', 'Category');
      otherData.addColumn('date', 'Start Date');
      otherData.addColumn('date', 'End Date');
      otherData.addColumn('number', 'Duration');
      otherData.addColumn('number', 'Percent Complete');
      otherData.addColumn('string', 'Dependencies');

      otherData.addRows([
        ['summary', 'Write 150 word summary', 'writing', new Date(2021, 3, 19), new Date(2021, 3, 23), , percent(new Date(2021, 3, 19), 4), null],
        ['pid', 'Project Initiation Document', 'writing', new Date(2021, 3, 21), new Date(2021, 3, 30), , percent(new Date(2021, 3, 21), 9), null],
        ['litrev', 'Literature Review', 'research', new Date(2021, 3, 21), new Date(2021, 4, 14), , percent(new Date(2021, 3, 21), 23), null],
        ['designphase', 'Exploring Point Cloud & Designing Visualisations', 'designing', new Date(2021, 4, 3), new Date(2021, 4, 14), , percent(new Date(2021, 4, 3), 11), 'pid'],
        ['engines', 'Exploring Game Engines', 'software', new Date(2021, 4, 10), new Date(2021, 4, 18), , percent(new Date(2021, 4, 10), 8), null],
        ['midterm', 'Preparing Mid-term Presentation', 'presenting', new Date(2021, 4, 17), new Date(2021, 4, 19), , percent(new Date(2021, 4, 3), 2), 'designphase'],
        ['startviz', 'Building the Chosen Visualisations', 'coding', new Date(2021, 4, 20), new Date(2021, 5, 2), , percent(new Date(2021, 4, 20), 13), 'designphase, engines'],
        ['usertest', 'User Testing', 'research', new Date(2021, 5, 3), new Date(2021, 5, 8), , percent(new Date(2021, 5, 3), 5), 'startviz'],
        ['finalviz', 'Finetuning Final Visualisations', 'coding', new Date(2021, 5, 7), new Date(2021, 5, 11), , percent(new Date(2021, 5, 7), 4), 'usertest'],
        ['report', 'Writing Final Report', 'writing', new Date(2021, 5, 5), new Date(2021, 5, 18), , percent(new Date(2021, 5, 5), 13), null],
        ['video', 'Recording & Editing Video', 'presenting', new Date(2021, 5, 19), new Date(2021, 5, 24), , percent(new Date(2021, 5, 21), 5), 'finalviz'],
        ['presentation', 'Preparing Final Presentation', 'presenting', new Date(2021, 5, 21), new Date(2021, 5, 25), , percent(new Date(2021, 5, 21), 4), 'finalviz, report'],
        ['tasks', 'Completing Task Distribution Form', 'admin', new Date(2021, 5, 28), new Date(2021, 6, 01), , percent(new Date(2021, 5, 28), 3), 'presentation'],

      ]);

      var options = {
        height: 800,
        gantt: {
          defaultStartDate: new Date(2021, 3, 19),
          criticalPathEnabled: true,
          // criticalPathStyle: {
          //   stroke: '#890e08',
          //   strokeWidth: 6
          // }
          innerGridHorizLine: {
            stroke: '#acb4b7',
            strokeWidth: 1
          },
          innerGridTrack: {fill: '#fff'},
          innerGridDarkTrack: {fill: '#dce9ef'},
          barCornerRadius: 1,
          barHeight: 25,
          shadowOffset: 2,
          sortTasks: true,
          arrow: {
            angle: 50,
            width: 2,
            color: '#890842',
            radius: 5
          }
        }
      };


      var chart = new google.visualization.Gantt(document.getElementById('chart_div'));

      chart.draw(otherData, options);
    }
  </script>
</head>
<body>
  <div id="chart_div"></div>
</body>
</html>
