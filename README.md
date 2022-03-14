## Опис

### runner.sh - скрипт на bash, що керує [mhddos_proxy](https://github.com/porthole-ascend-cinnamon/mhddos_proxy)

* Запускається через one-liner в Linux і WSL (Windows Subsystem for Linux). Подальше втручання від користувача не обов'язкове. `curl -s https://raw.githubusercontent.com/KarboDuck/runner.sh/master/runner.sh | bash`

* Праюцює із центральною базою сайтів-цілей.

* Базу сайтів цілей можна оновлювати "на льоту". Всі клієнти перечитують її кожні 15 хвилин.

* Також кожні 15 хвилин перевіряється і завантажується оновлення mhddos_proxy і MHDDoS.

* Автоматично встановлює git, python3, pip, mhddos_proxy, MHDDoS і всі залежності.

* Цілі обираються із списку рандомно, тому не обовʼязково розкидувати користувачів по групам і координувати їх між собою. Рандом розподілить навантаження автоматично.

* Скрипт запускає кілька копій mhddos_proxy (по замовчуванню 2 але можна скільки завгодно). Кожна копія незалежно атакує іншу ціль.

Теоретично все це дозволяє залишити runner.sh на ПК/vps і він самостійно буде оновлювати все ПЗ та список з цілями.

Рекомендовано використовувати на Ubuntu 20.04. На інших системах не перевірялось. Можливо буде працювати на всіх Ubuntu починаючи з 18.04, усіх похідних Ubuntu та WSL2.

## Список цілей

![Screenshot 2022-03-13 at 23 43 03](https://user-images.githubusercontent.com/53382906/158080424-cb6f1c58-4be8-4146-97e2-2a814ce3a1eb.png)


runner.sh підтримує единий [список цілей](https://github.com/KarboDuck/runner.sh/blob/main/runner_targets), який можна тримати на github і постійно оновлювати.

Скрипт дозволяює запускати кілька копій mhddos_proxy. Кількість копій налаштовується і по замовчуванню = 2. Це зроблено через те, що із "великими" командами які містять 10+ IP багато копій mhddos_proxy інколи "вішають" недостатньо потужні ПК/vps. В той же час на "малих" командах (1-5 IP) mhddos_proxy використовує не всі наявні ресурси. То ж є можливість на потужному залізі запускати більше однієї копії програми.

Щоб запустити 3 копії:
`curl -s https://raw.githubusercontent.com/KarboDuck/karbo-wiki/master/runner.sh | bash -s -- 3`

Це відрізняється від вбудованої в mhddos_proxy можливості "multiple targets". Multiple targets вміє атакувати кілька різних IP, але метод атак при цьому буде той самий. Параметр num_of_copies в runner.sh запускае кілька копій mhddos_proxy які можуть атакувати різні цілі різними методами.

Цілі не обов'язково видаляти із списку. Їх можна просто закоментувати і розкоментувати пізніше, якщо вони знов знадобляться. Скрипт шукає лише строки, які починаються на 'runner.py'.
