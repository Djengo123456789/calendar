# calendar
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Календарь</title>
  <style>
    body {
      font-family: sans-serif;
      background-color: #000;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
    }

    h1 {
      margin: 10px;
    }

    .calendar {
      width: 350px;
    }

    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .days, .dates {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      text-align: center;
      margin-top: 10px;
    }

    .days div {
      font-weight: bold;
      padding: 8px 0;
    }

    .dates div {
      padding: 10px 0;
    }

    .today {
      background: #ff3b30;
      border-radius: 50%;
      color: white;
      font-weight: bold;
    }

    button {
      background: none;
      border: none;
      color: #ff453a;
      font-size: 24px;
      cursor: pointer;
    }

  </style>
</head>
<body>
  <div class="calendar">
    <div class="header">
      <button onclick="changeMonth(-1)">←</button>
      <h1 id="monthYear">Май 2025</h1>
      <button onclick="changeMonth(1)">→</button>
    </div>
    <div class="days">
      <div>П</div><div>В</div><div>С</div><div>Ч</div><div>П</div><div>С</div><div>В</div>
    </div>
    <div class="dates" id="dates"></div>
  </div>

  <script>
    const monthNames = [
      "Январь", "Февраль", "Март", "Апрель", "Май", "Июнь",
      "Июль", "Август", "Сентябрь", "Октябрь", "Ноябрь", "Декабрь"
    ];

    let currentDate = new Date();

    function renderCalendar() {
      const year = currentDate.getFullYear();
      const month = currentDate.getMonth();
      const today = new Date();
      const monthYear = document.getElementById("monthYear");
      const dates = document.getElementById("dates");

      monthYear.textContent = `${monthNames[month]} ${year}`;
      dates.innerHTML = "";

      const firstDay = new Date(year, month, 1).getDay();
      const offset = (firstDay + 6) % 7;
      const lastDate = new Date(year, month + 1, 0).getDate();

      for (let i = 0; i < offset; i++) {
        dates.innerHTML += `<div></div>`;
      }

      for (let d = 1; d <= lastDate; d++) {
        const isToday = d === today.getDate() && month === today.getMonth() && year === today.getFullYear();
        dates.innerHTML += `<div class="${isToday ? 'today' : ''}">${d}</div>`;
      }
    }

    function changeMonth(delta) {
      currentDate.setMonth(currentDate.getMonth() + delta);
      renderCalendar();
    }

    renderCalendar();
  </script>
</body>
</html>
