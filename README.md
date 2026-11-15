# -telegram-clone/
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