# stm32joy 
инструкция по прошивки контроллера

## Прошивка stm32 через UART

Любой микроконтроллер stm32 можно прошивать через USART_1 и другие интерфейсы, подробно смотрите в AN2606. Для этого в МК есть специальный системный загрузчик, который зашивается в System memory (спец. область памяти) на этапе производства, его нельзя удалить или изменить. Это загрузчик инициализируется путём «подтягивания» пина BOOT_0 к «плюсу», после чего он ожидает поступления прошивки.


Через USART можно загружать любые .bin или .hex файлы.


Описание сделано на примере платы ``Blue Pill``, однако всё сказанное справедливо для любого stm32.

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/10/10/06c8f8.jpg)

`Фирменные платы типа Discovery и Nucleo тоже можно прошивать через USART.`

Для работы потребуется USB to UART конвертер…

![Alt text](https://istarik.ru/uploads/images/00/00/01/2016/01/24/3ad8f5.jpg)

Перед прошивкой необходимо подтянуть пин BOOT0 к «плюсу», это переведёт МК в режим «системного бутлоадера». На описываемой плате это осуществляется перестановкой джампера…

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/26/b317a1.png)

Соединяем конвертер и STM ``Blue Pill`` следующим образом…

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/27/fe9108.png)

- Конвертер `RX` -> `PA9` STM

- Конвертер `TX` -> `PA10` STM

- Конвертер `GND` -> `GND` STM

… и подключаем конвертер и STM к компьютеру.

## Инструкция по прошивке для Windows

Скачайте ``Flash Loader Demonstrator`` и распакуйте куда-нибудь. 
можете взять с сайта ST https://www.st.com/en/development-tools/flasher-stm32.html

`Нажмите Reset на плате. Бывает что на описываемой плате, плохо работает кнопочка, поэтому если МК не сбрасывается (не прошивается), тогда кратковременно замкните пин Reset на «землю».`

![Alt text](https://istarik.ru/uploads/images/00/00/01/2019/10/17/2fa39b.jpg)

Перейдите в папку ``Flash Loader Demonstrator`` и запустите ``Flash Loader Demonstrator.exe``

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/25/4f044e.png)

Выбираем СОМ-порт конвертера и жмем `Next...`

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/25/7cb0b0.png)

Если светофор даёт зеленый свет, то смело жмите `Next...`

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/25/624373.png)

Жмем `Next...`

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/10/16/d298fe.png)

В пункте ``Download to device`` указываем путь к нужному .bin или .hex файлу и жмем `Next...`

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/25/31f5bf.png)

Всё готово, верните джампер в исходное положение и нажмите `Reset` или выключите и включите плату.

![Alt text](https://istarik.ru/uploads/images/00/00/01/2018/07/26/761582.png)

## P.S.

Все описанные действия можно проделать с помощью фирменной утилиты — `STM32CubeProgrammer` (Windows®, Linux®, macOS®)
https://www.st.com/en/development-tools/stm32cubeprog.html
