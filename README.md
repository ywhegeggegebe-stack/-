// --- 1. Настройка (для теста храним в localStorage) ---
// В реальном проекте это должно храниться в базе данных на сервере

function getStreak(chatId) {
  const data = localStorage.getItem(`streak_${chatId}`);
  return data ? JSON.parse(data) : { count: 0, lastDate: null };
}

function saveStreak(chatId, streak) {
  localStorage.setItem(`streak_${chatId}`, JSON.stringify(streak));
}
// --- Магазин NFT (можно расширять) ---
const NFT_SHOP = [
  { id: 'star_bronze', name: 'Бронзовая звезда', price: 10, emoji: '⭐' },
  { id: 'fire_small',  name: 'Малый огонь',    price: 50, emoji: '🔥' },
  { id: 'crown_silver', name: 'Серебряная корона', price: 200, emoji: '👑' },
  { id: 'diamond_blue', name: 'Голубой алмаз', price: 1000, emoji: '💎' },
  { id: 'galaxy_gold',  name: 'Золотая галактика', price: 5000, emoji: '🌌' }
];

// --- Хранилище (пока в localStorage) ---
function getNFTData(userId) {
  const data = localStorage.getItem(`nft_${userId}`);
  return data ? JSON.parse(data) : { streak: 0, owned: [], equipped: null };
}

function saveNFTData(userId, data) {
  localStorage.setItem(`nft_${userId}`, JSON.stringify(data));
}




// --- 2. Логика обновления огонька ---
function updateStreak(chatId) {
  const today = new Date().toISOString().split('T')[0]; // "2026-11-16"
  let streak = getStreak(chatId);

  // Если уже писали сегодня — ничего не меняем
  if (streak.lastDate === today) return streak;

  // Вычисляем вчерашнюю дату
  const yesterday = new Date();
  yesterday.setDate(yesterday.getDate() - 1);
  const yesterdayStr = yesterday.toISOString().split('T')[0];

  if (streak.lastDate === yesterdayStr) {
    // Писали вчера -> огонёк растёт
    streak.count += 1;
  } else {
    // Пропустили день (или первый раз) -> огонёк начинается заново
    streak.count = 1;
  }

  streak.lastDate = today;
  saveStreak(chatId, streak);
  return streak;
}

// --- 3. Отображение огонька в интерфейсе ---
function renderStreak(chatId, elementId) {
  const streak = getStreak(chatId);
  const el = document.getElementById(elementId);
  if (!el) return;

  if (streak.count > 0) {
    el.innerHTML = `🔥 ${streak.count}`;
    el.style.display = 'inline-block';
    el.style.color = '#ff4500';
    el.style.fontWeight = 'bold';
  } else {
    el.style.display = 'none';
  }
}

// --- 4. Как использовать (пример) ---
// Представьте, что это функция, которая вызывается при отправке сообщения
function onSendMessage(chatId) {
  updateStreak(chatId);
  renderStreak(chatId, 'streak-display');
}# -telegram-clone/
streak.count
streak.lastDate
├── server/
│   ├── index.js          # Express + Socket.io
│   ├── routes/auth.js    # Регистрация/вход
│   ├── routes/chats.js   # Чаты и сообщения
│   └── models/           # Схемы БД
├── client/
│   ├── src/
│   │   ├── pages/        # Login, Chats, Chat
│   │   ├── components/   # Message, ChatList
│   │   └── api/          # Запросы к серверу
└── docker-compose.yml
docker-compose.yml
Element / Matrix
docker compose up -d,