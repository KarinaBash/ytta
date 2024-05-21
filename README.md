# ParticleNetwork
[![Telegram channel](https://img.shields.io/endpoint?url=https://runkit.io/damiankrawczyk/telegram-badge/branches/master?url=https://t.me/oxcode1)](https://t.me/oxcode1)

✈️[Telegram Channel](https://t.me/oxcode1)

![img1](data/demo/demo.png)

## 💡Функционал  
| Функционал                                                     | Поддерживается  |
|----------------------------------------------------------------|:---------------:|
| Многопоточность                                                |        ✅       |
| Локальная база данных                                          |        ✅       |
| Поддержка капчи CapMonster, Twocaptcha, AntiCaptcha            |        ✅       |
| Поддержка прокси любого формата (HTTP ONLY)                    |        ✅       |
| Загрузка списком REFCODE                                       |        ✅       |
| Поддержка всех сетей EVM                                       |        ✅       |
| Выполняет Daily CHECK-IN                                       |        ✅       |
| Выполняет DEPOSIT UNIVERSAL GAS                                |        ✅       |
| Выполняет USE UNIVERSAL GAS TO TRANSACT (100 транзакций/24ч)   |        ✅       |
| Выполняет RETWEET PARTICLE NETWORK'S TWEET                     |        ✅       |
| Сбор информации об аккаунте и кошельках EVM                    |        ✅       |
| Экспорт информации об аккаунтах в txt, excel                   |        ✅       |
| Генерация кошельков EVM                                        |        ✅       |
| И прочее :)                                                    |        ✅       |

## [⚙️Настройки](https://github.com/NikeAK/ParticleNetwork/blob/main/data/config.py)
| Настройка                  | Описание (см. config.py)                                                  |
|----------------------------|---------------------------------------------------------------------------|
| **MAIN_NETWORK**           | Выберите основную сеть, указав число                                      |
| **DEPOSIT_USDG**           | Укажите числа [min, max] для суммы депозита USDG в вашей сети             |
| **DEPOSIT_PRATICLE**       | Укажите числа [min, max] для суммы пополнения ParticleWallet в вашей сети |
| **MAKE_TRANSACTIONS**      | Накручивать 100 транзакций для выполнение ежедневного задания?            |
| **MAX_GAS_USDG**           | Максимальный газ USDG для оплаты, у каждой сети сильно отличается.        |
| **TRANSFER_AMOUNT**        | Укажите числа [min, max] для суммы перевода при накрутки транзакций.      |
| **DELAY_TRANSACTIONS**     | Укажите числа [min, max] для выставления задержки между транзакциями.     |
| **RANDOM_TX**              | Включить случайные транзакции?                                            |
| **TIMEOUT_PROXY**          | Максимальное время ожидания при проверке прокси в секундах                |
| **REQUEST_ATTEMPTS**       | Количество попыток при не удачных запросах                                |
| **CAPTCHA_API_KEY**        | Ключ качи                                                                 |
| **GET_ALL_BALANCES**       | Получать актуальный баланс всех EVM сетей?                                |
| **DELAY_ALL_BALANCES**     | Задержка в сек. между получением баланса в 1 сети/1 кошелька              |
| **EXPORT_DATA**            | Используемые данные для экспорта                                          |
| **EXPORT_SEPARATOR**       | Символ разделения данных для экспорта в TXT                               |

## 📝Пояснение
1. Заполните config.py
2. Загрузите аккаунты в текстовики
3. При первом запуске выберите в терминале Launch - Add account to database
    - Софт выполняет вход в аккаунт ParticleNetwork и проверяет, установлен ли реферальный код. Если рефкод не установлен, он присваивает его аккаунту. Затем проверяет, привязан ли уже Discord. Если привязан, то пропускает привязку Discord, если нет, то берет один токен из файла, проверяет его на валидность и привязывает к аккаунту. То же самое происходит с Twitter. После этого аккаунт добавляется в базу данных.
    - При таком запуске ни в коем случае не нажимайте CTRL+C, иначе данные будут удалены из TXT-файла и нет гарантии, что они успели добавиться в базу данных, или Discord или Twitter уже привязался к какому-то аккаунту. Если вы думаете, что сможете просто снова залить эти аккаунты и всё будет в порядке, то это не так. Софт не проверяет, привязаны ли аккаунты Twitter и Discord к другому аккаунту, что может привести к ошибкам в дальнейшем. (Тут на самом деле сложно объяснить, просто не нажимайте CTRL+C)
4. После успешного добавления аккаунтов, вы можете выбрать в терминале Launch -> DataBase
    - Здесь софт просто выполняет задания и крутит транзакции, после успешного выполнения, обновляет информация/статистику аккаунта и кошельков(если вкл. GET_ALL_BALANCES)
    - Отмечу, что софт для выполнения задания USE UNIVERSAL GAS TO TRANSACT выводит небольшие суммы с Particle Wallet на ваш основной кошелек EVM. Если баланс Particle Wallet недостаточен, выполняется операция DEPOSIT_PARTICLE. Для газа USDG применяется аналогичный процесс DEPOSIT_USDG.
    - Также для транзакций можно выставить максимальный газ для оплаты комиссий в USDG. Для оплаты комиссий с EVM кошельков не стал добавлять максимальный газ, но вы можете регулировать его MULTIPLIER_GAS.
    - Также чтобы при накрутке транзакций не было отправки только с ParticleWallet. Можно включить случайные транзакции. Софт генерирует случайное число от 1 до 12. Если выпадет число 1, софт сделает долнительную транзакцию DEPOSIT_PRATICLE. Если выпадет число 12, софт сделает дополнительную транзакцию DEPOSIT_USDG.
5. После того как вы прошлись по все базе данных, вы можете экспортировать всю доступные информацию.
    - Вам будет предложено выбрать, какую информацию экспортировать: по умолчанию используется config.py (см. config.py), либо вы можете выбрать нужную информацию с помощью стрелок. Далее выберите формат экспорта: TXT или Excel.
6. Повторяете 4 пункт каждый день и ждите Profit, т.к тестнет должен быть награждаемый :)

## ⚡️Быстрый запуск
1. Запустите $\color{orange}{\textsf{Setup.bat}}$. Этот скрипт автоматически создаст виртуальное окружение, активирует его, установит все необходимые зависимости из файла requirements.txt и удалит не нужные файлы.
2. После успешного выполнения $\color{orange}{\textsf{Setup.bat}}$, вы можете запустить $\color{orange}{\textsf{Main.bat}}$. Этот скрипт активирует виртуальное окружение и запустит софт.

## 🛠️Ручная установка
```shell
~ >>> python -m venv Venv              #Создание виртуального окружения
~ >>> Venv/Scripts/activate            #Активация виртуального окружения
~ >>> pip install -r requirements.txt  #Установка зависимостей
~ >>> python main.py                   #Запуск
```

## 💰DONATION EVM ADDRESS: 
**0x1C6E533DCb9C65BD176D36EA1671F7463Ce8C843**

