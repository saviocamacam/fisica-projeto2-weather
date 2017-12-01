<!doctype html>
<html>
    <head>
        <script type='text/javascript' src='https://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js'></script>
        <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
        <script type="text/javascript">
// set your channel's read api key here if necessary
var api_key = '39YJM4SS4Q8ZCZT0';
// set your channel id here
var channel_id = 369399;
// global variables
var data;

google.charts.load('current', {'packages':['gauge']});
google.charts.setOnLoadCallback(drawChart);

function drawChart() {
    $.getJSON('https://api.thingspeak.com/channels/'+channel_id+'/feed/last.json?api_key='+api_key, function(data) {
        data = google.visualization.arrayToDataTable([
            ['Label', 'Value'],
            ['Field1', parseFloat(data.field1)],
            ['Field2', parseFloat(data.field2)],
            ['Field3', parseFloat(data.field3)],
            ['Field4', parseFloat(data.field3)],
            ['Field5', parseFloat(data.field3)]
        ]);

        var options = {
            width: 400, height: 120,
            redFrom: 90, redTo: 100,
            yellowFrom:75, yellowTo: 90,
            minorTicks: 5
        };

        var chart = new google.visualization.Gauge(document.getElementById('chart_div'));

        chart.draw(data, options);

        setInterval(function() {
            $.getJSON('https://api.thingspeak.com/channels/'+channel_id+'/feed/last.json?api_key='+api_key, function(json) {
                console.log(json)
                data.setValue(0, 1, parseFloat(json.field1));
                data.setValue(1, 1, parseFloat(json.field2));
                data.setValue(2, 1, parseFloat(json.field3));
                data.setValue(3, 1, parseFloat(json.field3));
                data.setValue(4, 1, parseFloat(json.field3));
                chart.draw(data, options);
            })
        }, 100);
    })
}
        </script>
    </head>
    <body>
        <div id="chart_div" style="width: 400px; height: 120px;"></div>
        #Teste
    </body>
</html>