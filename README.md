# tainiy-santa
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Тайный Санта</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-image: url('https://img.freepik.com/premium-vector/christmas-santa-claus-vector-design-merry-christmas-greeting-text-with-santa-claus-character_572293-2788.jpg?w=2000'); /* Замените 'your-image-url.jpg' на URL вашего изображения */
      background-size: cover;
    }

    .container {
      width: 80%;
      margin: 0 auto;
      text-align: center;
      background-color: rgba(104, 9, 128, 0.959); /* Чтобы текст был виден на фоне */
      padding: 20px;
    }

    button {
      padding: 10px 20px;
      font-size: 16px;
      background-color: #954caf;
      color: white;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Игра Тайный Санта
        Лимит от 3000 до 5000тг 
    </h1>
    <label for="participantName">Введите ваше имя:</label>
    <input type="text" id="participantName">
    <button onclick="findGiftee()">Узнать для кого вы будете тайной сантой</button>
    <p id="result"></p>

    <script>
      function shuffleArray(array) {
        for (let i = array.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [array[i], array[j]] = [array[j], array[i]];
        }
        return array;
      }

      function secretSanta(participants) {
        const shuffledParticipants = shuffleArray(participants.slice());
        const pairs = [];

        for (let i = 0; i < shuffledParticipants.length; i++) {
          let gifteeIndex = (i + 1) % shuffledParticipants.length;
          pairs.push({ Santa: shuffledParticipants[i], Giftee: shuffledParticipants[gifteeIndex] });
        }

        return pairs;
      }

      function findGiftee() {
        const inputName = document.getElementById('participantName');
        const storedName = localStorage.getItem('participantName');
        const storedGiftee = localStorage.getItem('giftee');
        const participants = [
        "Абдимомынова Дарина",
"Абдулла Ерасыл",
"Абишев Амир",
"Абсаттар Алдияр",
"Алмуханов Абдинур",
"Асанбаев Алишер",
"Абдрахманова Айзере",
"Әмірғали Айя",
"Батыргереев Тимур",
"Бежентаева Сабина",
"Бейсембай Ануар",
"Дорджиев Адиль",
"Елеусизова Айлин",
"Естаева Адия",
"Саукенова Алина",
"Керимбек Алижан",
"Кистаубаев Амирлан",
"Кунбулатов Тамерлан",
"Муратова Еркежан",
"Мусабаева Әлсафи",
"Мұрат Арсен",
"Сатпаева Альбина",
"Тыныстамов Алдияр"
        ];
        const santaPairs = secretSanta(participants);
        const result = document.getElementById('result');

        if (!inputName.value || inputName.value === storedName) {
          if (storedName && storedGiftee) {
            result.innerHTML = `Вы уже узнали для кого вы будете тайной сантой: ${storedGiftee}`;
            inputName.value = storedName;
            inputName.setAttribute('readonly', true);
            document.querySelector('button').disabled = true;
            return;
          } else {
            result.innerHTML = 'Введите ваше имя, пожалуйста.';
            return;
          }
        }

        const santa = santaPairs.find(pair => pair.Santa === inputName.value);

        if (santa) {
          result.innerHTML = `Ваш тайный Санта: ${santa.Giftee}`;
          localStorage.setItem('giftee', santa.Giftee);
          localStorage.setItem('participantName', inputName.value);
          inputName.setAttribute('readonly', true);
          document.querySelector('button').disabled = true;
        } else {
          result.innerHTML = `Извините, имя не найдено в списке участников.`;
        }
      }

      window.onload = function () {
        const storedName = localStorage.getItem('participantName');
        const storedGiftee = localStorage.getItem('giftee');
        const inputName = document.getElementById('participantName');
        const result = document.getElementById('result');

        if (storedName && storedGiftee) {
          result.innerHTML = `Вы уже узнали для кого вы будете тайной сантой: ${storedGiftee}`;
          inputName.value = storedName;
          inputName.setAttribute('readonly', true);
          document.querySelector('button').disabled = true;
        }
      };
    </script>
  </div>
</body>
</html>
