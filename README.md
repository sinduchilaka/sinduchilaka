<!Doctype html>

<head>
    <title>
        Alarm Clock
      </title>
</head>

<body>
    <input type="datetime-local" id="alarmTime"/>
    <button onclick="setAlarm(this);" id="alarmButton">Set Alarm</button>
    <div id="alarmOptions" style="display: none;">
      <button onclick="snooze();">Snooze 5 minutes</button>
      <button onclick="stopAlarm();">Stop Alarm</button>
    </div>


  <script>
          
          var alarmSound = new Audio();
          alarmSound.src='alarm.mp3';
          var alarmTimer ;

      function setAlarm(button)
      {
          var ms=document.getElementById('alarmTime').valueAsNumber;
          if(isNaN(ms)){
              alert('Invalid Date');
              return ;
          }

          var alarm= new Date(ms);
          var alarmTime = new Date(alarm.getUTCFullYear(),alarm.getUTCMonth(),alarm.getUTCDate(),alarm.getUTCHours(),alarm.getUTCMinutes(),alarm.getSeconds());
          var differenceInMs = alarmTime.getTime()-(new Date()).getTime();

          if(differenceInMs <0)
          {
              alert ('Specified time is passed');
              return;
          }

          alarmTimer = setTimeout(initAlarm,differenceInMs);

          button.innerText='cancel alarm';
         button.setAttribute('onclick','cancelAlarm(this);');
         clearTimeout(alarmTimer);
    };


    function cancelAlarm(button)
    {
           button.innerText='Set Alarm';
           button.setAttribute('onclick','setAlarm(this);');
    };

    function initAlarm()
    {
       alarmSound.play();
       document.getElementById('alarmOptions').style.display='';
    };

      function stopAlarm()
      {
            alarmSound.pause();
            alarmSound.currentTime = 0;
            document.getElementById('alarmOptions').style.display='none';
            cancelAlarm(document.getElementById('alarmButton'));
      };

      function snooze()
      {
            stopAlarm();
            setTimeout(initAlarm,36000);
      };

  </script>

</body>
</html>
