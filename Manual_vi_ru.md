# OpenIPC cho Xiaomi MJSXJ03HL 
![Hình ảnh](https://user-images.githubusercontent.com/88727968/222164240-66044bf1-16da-4ea2-af38-6fd3d3fb1b92.png)

## Chú ý! Phiên bản hướng dẫn này đã lỗi thời và đang được cập nhật. Thực hiện các hành động có thể gây hại cho thiết bị của bạn!

Chú ý! Bất kỳ thay đổi nào bạn thực hiện sẽ làm mất bảo hành cho thiết bị này! Tác giả không chịu trách nhiệm về bất kỳ thiệt hại nào phát sinh từ bất kỳ hành động nào của người dùng!
_________
## Chuẩn bị
### Kết nối UART Adapter

Chúng ta sẽ cần:

- Máy tính với cổng USB
- Một thiết bị đo điện áp hoặc voltmet
- UART Adapter 3,3V, tương tự như hình dưới đây

![Hình ảnh](https://user-images.githubusercontent.com/88727968/222174358-5203eb83-14ce-4f55-89bd-24775af82599.png)

Tất cả các hành động sẽ được thực hiện trên hệ điều hành Linux (Kubuntu), nếu hệ điều hành của bạn khác, vui lòng tham khảo hướng dẫn chuyên biệt về cài đặt UART trên hệ điều hành của bạn.

Các bước thực hiện:
1) Xem xét kỹ UART Adapter. Tìm các chân ***GND***,***TX***,***RX***. Nếu adapter của bạn hỗ trợ chức năng chọn điện áp làm việc, hãy đảm bảo rằng nó được chuyển sang chế độ làm việc 3,3V!
2) Sử dụng thiết bị đo điện áp để đảm bảo rằng UART Adapter của bạn cung cấp điện áp 3.3V. Để làm điều này, hãy thực hiện đo điện áp giữa các chân ***GND*** và ***TX***, cũng như ***GND*** và ***RX***. Đừng sử dụng adapter nếu điện áp là 5V! Điều này sẽ hủy camera của bạn!
3) Kết nối UART Adapter vào cổng của máy tính của bạn. Bạn cần biết điểm gắn kết của adapter trong hệ điều hành của bạn.
4) Sử dụng terminal. Thực hiện lệnh ***lsusb*** và xem kỹ kết quả. Tìm UART Adapter của bạn.
5) Sử dụng terminal. Thực hiện lệnh ***dmesg | grep attached*** từ superuser. So sánh kết quả của cả hai lệnh và tìm điểm gắn kết của adapter. Hãy tham khảo hình ảnh dưới đây: ![Screenshot_20230301_210433](https://user-images.githubusercontent.com/88727968/222186693-932e241c-5f92-4876-b4de-e51271ea6ae9.png)
6) Vậy, chúng ta đã xác định rằng thiết bị của chúng ta được gắn kết tại địa chỉ ***/dev/ttyUSB0***. Trong trường hợp của bạn, địa chỉ gắn kết có thể khác. Chúng ta sẽ sử dụng địa chỉ này khi kết nối qua UART. Hãy cẩn thận, khi kết nối nhiều thiết bị tương tự, cũng như khi ngắt kết nối không đúng cách, địa chỉ gắn kết có thể thay đổi.
________

### Tháo dỡ

Hiện tại, camera chỉ hỗ trợ nâng cấp firmware thông qua UART adapter, do đó, để thực hiện các thao tác, chúng ta sẽ phải tháo camera.
**Hãy nhớ rằng điều này sẽ làm mất bảo hành của nhà sản xuất!**

Chúng ta sẽ cần:
- Chính thiết bị
- Máy sấy hoặc thiết bị gia nhiệt khác
- Vật dẹp và mỏng, ví dụ như dao văn phòng
- Tuốc-nơ-vít dài và mỏng kiểu x
- Sự cẩn thận

Vậy, hãy bắt đầu:
1) Gently heat the front of the camera (where the lens is)
2) Sử dụng dao văn phòng hoặc vật nhọn khác, nhẹ nhàng gạt phần trước. Hãy nhớ rằng dưới phần trước có các dây quan trọng, ***đừng làm hỏng chúng!***
3) Di chuyển xung quanh, nhẹ nhàng tách phần trước ra khỏi thân máy camera. ***Hãy nhớ rằng nó được kết nối bằng dây với bo mạch chính của camera!***
4) Dưới đáy, bạn sẽ tìm thấy hai ốc vít cần phải tháo ra. Sau đó, nhẹ nhàng tách hai nửa thân máy camera. Hãy cẩn thận, đừng tự làm hại mình và không làm hỏng các dây kết nối cũng như các bộ phận của camera!
5) Tháo ra thêm một số ốc vít, giải phóng bo mạch chính của thiết bị. Cũng giải phóng cổng type C
______________

### Nghiên cứu

Hãy nghiên cứu kỹ camera, tìm các phần cần thiết, vì trong các bước tiếp theo, chúng ta sẽ phải tương tác vật lý với một số trong số đó.
Nhà sản xuất có thể thay đổi một số thành phần của thiết bị mà không thông báo cho người tiêu dùng. Vì lý do này, hai camera được sản xuất vào thời gian khác nhau có thể có nội thất khác nhau và phần mềm khác nhau. Vì vậy, hãy nghiên cứu kỹ các thành phần một lần nữa, đảm bảo rằng chúng tương ứng với những gì được chỉ ra trong hướng dẫn này. Nếu có bất kỳ câu hỏi nào, vui lòng liên hệ với chúng tôi qua [Kênh Telegram](https://t.me/openipc_modding)

##### Bo mạch chính (nhìn từ mặt trước)
![IMG_20210904_194002](https://user-images.githubusercontent.com/88727968/222473262-913af0d1-0fee-4ae6-843f-256784381163.jpg)Bo mạch chính (nhìn từ mặt trước).

Phần quan trọng nhất đối với chúng ta trên đây là chip nhớ.
##### Chip nhớ trên đó
![IMG_20210904_194034](https://user-images.githubusercontent.com/88727968/222473270-dfb08412-0019-4a57-aecc-3820421263e8.jpg)Chip nhớ trên đó.

Nó có dấu hiệu số và chữ. Hãy chắc chắn rằng chip trên bo mạch của bạn có dấu hiệu tương tự! Số 128 biểu thị số bit của bộ nhớ. 128/8=16, vì vậy bộ nhớ của chúng ta là 16 MB. Chọn firmware phù hợp với loại bộ nhớ này!
##### Bo mạch chính (nhìn từ mặt sau)
![IMG_20210904_194151](https://user-images.githubusercontent.com/88727968/222473288-c3efcdc6-2691-452f-aebb-9ab1789d4d2d.jpg)Bo mạch chính (nhìn từ mặt sau).

Ở đây có mô-đun không dây, bộ xử lý trung tâm và các thành phần khác. Nhưng điều quan trọng nhất đối với chúng ta là ba điểm tiếp xúc có lỗ, nằm cạnh nhau ở góc trên bên phải của bo mạch. Chính qua chúng mà chúng ta gửi các tín hiệu điều khiển cho camera.

##### Bộ xử lý trung tâm
![IMG_20210904_194132](https://user-images.githubusercontent.com/88727968/222473285-9c00e6d9-f585-4481-a48b-867b0c1f3a85.jpg)Bộ xử lý trung tâm.

Trong trường hợp của chúng ta, nó có dấu hiệu số và chữ. Ingenic T31N. Chữ N - là dòng. Nó được chỉ ra ở hàng thứ hai. [Chi tiết](https://wiki.openipc.org/en/installation.html#step-1-determine-the-system-on-chip)
_______________
### Kết nối camera và UART adapter

Để kết nối UART adapter với bo mạch camera, bạn cần sử dụng các dây có kẹp. Chúng có thể đi kèm với UART adapter. Tuy nhiên, bạn có thể thay thế chúng bằng những cái tương tự. Các loại kết nối tương tự xuất hiện trong nhiều thiết bị điện tử. Đầu dây kết nối với bo mạch nên được hàn để đảm bảo liên lạc không bị mất vào thời điểm cần thiết. Hãy cẩn thận khi hàn, đừng làm hỏng các thành phần mạch và không làm ngắn mạch các điểm tiếp xúc với nhau!
![IMG_20210904_1941511](https://user-images.githubusercontent.com/88727968/222906480-dea0a59c-2dab-45e3-96fa-81cf335b745b.jpg)

Kết nối các dây từ UART adapter với bo mạch như hình vẽ. Nếu bạn làm đúng, camera sẽ hiển thị log khi khởi động. Hãy kiểm tra điều này.

#### Проверка работоспособности терминала, камеры и соединения

Для начала нам потребуется установить программу-терминал для отправки управляющих команд с камеры и приема обратных сигналов. В ОС linux достаточно большое количество терминалов, вы можете выбрать себе наиболее удобный. Среди них можно выделить **screen, picocom, minicom, cutecom**. Последний имеет GUI.
Установите программу-терминал:

```sudo apt install <ИМЯПАКЕТА>```
Команды будут приведены для программы picocom.
Для начала ознакомьтесь с возможностями программы и синтаксисом команд:
```picocom --help``` 
Подключите UART-переходник и выполните в терминале команду:
```
picocom -b 115200 /dev/ttyUSB0
```
где опция ***-b*** задает управляющую частоту, а ***/dev/ttyUSB0*** - адрес точки монтирования, который мы узнали ранее.
Если вы все сделали верно, программа напишет, что терминал готов к работе. Ознакомьтесь с управляющими командами терминала, нажав последовательность клавиш ***Ctrl+A   Ctrl+H***. Для более подробного изучения программы-терминала обратитесь к соответствующим руководствам в сети.

Если вы подадите питание на камеру, то увидите лог загрузки. Попробуйте нажать клавиши, например ***Enter*** и убедитесь, что терминал на них реагирует и отправляет события. Если все сделано верно, можно переходить к следующему пункту.
_____________

### Получение доступа к консоли загрузчика
К сожалению, камера MJSXJ03HL на стоковой прошивке не поддерживает прерывание загрузки через отправку комбинации клавиш. По этой причине прерывание загрузки и получение доступа к консоли загрузчика будет призводиться нами вручную. Для этого необходимо будет замкнуть некоторые контакты [чипа памяти](https://github.com/OpenIPC/device-mjsxj03hl/blob/master/Manual_ru.md#%D1%87%D0%B8%D0%BF-%D0%BF%D0%B0%D0%BC%D1%8F%D1%82%D0%B8-%D0%BD%D0%B0-%D0%BD%D0%B5%D0%B9).
О том, как это сделать, прочтите [здесь](https://github.com/OpenIPC/wiki/blob/master/en/help-uboot.md#shorting-pins-on-flash-chip).
Внимательно изучите приведенный выше мануал, найдите чип памяти и нужные контакты, приготовьте то, чем будете замыкать контакты. Все манипуляции придется производить достаточно быстро.
ВНИМАНИЕ!!! Всю ответственность за производимые вами действия принимаете на себя! 
Далее последовательность действий по получению доступа к консоли загрузчика:
1. Соедините камеру с UART-переходником
2. Соедините UART-переходник c USB портом компьютера.
3. Запустите терминал на компьютере, убедитесь что он видит UART-переходник
4. Приготовьтесь замкнуть контакты
5. Подайте питание на плату
6. В окне терминала должен появиться лог загрузки
7. Замкните контакты чипа памяти (Это нужно сделать спустя 0,5-1 сек после подачи питания)
8. Загрузка должна прерваться. Контакты можно разомкнуть.
9. Если вы все сделали правильно, на экране появится консоль U-boot c символом ***#*** и возможностью ввода.
10. Введите ***help*** чтобы вывести список команд, присутствующих в загрузчике

К сожалению производитель для данной камеры сильно граничил возможности U-boot, это создаст нам серию препятствий в дальнейшем, пока мы не прошьем U-boot от OpenIPC. Но сперва нам следует сохранить стоковую прошивку камеры.
__________
### Сохранение заводской прошивки
Внимание! Не пропускайте этот пункт! Бэкап заводской прошивки позволит вам восстановить работоспособность устройства, если вдруг что-то пойдет не так.

Нам понадобятся:

- Камера в разобранном виде с подключенным UART
- Компьютер
- SD карта емкостью не менее 16 Мб
Предварительно рекомендуется ознакомиться с [исходной статьей](https://github.com/OpenIPC/wiki/blob/master/en/help-uboot.md#saving-firmware-via-sd-card)

ВНИМАНИЕ! В ходе следующих манипуляций вся информация с SD карты окажется недоступной, а самой картой нельзя будет пользоваться до форматирования! Все данные, находящиеся на карте будут безвозвратно утеряны!

Карту необходимо вставить в слот камеры. UART-переходник должен быть присоединен к компьютеру, а программа-терминал запущена.

1) Прерываем загрузку камеры путем замыкания контактов, попадаем в консоль загрузчика.
2) Если SD карта была вставлена после прерывания загрузки, выполните ***mmc rescan***
3) Для начала очистим требуемое пространство для записи туда дампа исходной прошивки: 
```
mmc dev 0
mmc erase 0x10 0x8000
```
4) Теперь вам надо скопировать содержимое прошивки из микросхемы флэш-памяти в оперативную память камеры. Для этого очистите участок оперативной памяти, получите доступ к микросхеме флэш-памяти и скопируйте весь объем флэш-памяти в очищенное пространство оперативной памяти. После чего сохраните скопированные данные из оперативной памяти на карту. Команды вставлять построчно!
```
mw.b 0x80600000 ff 0x1000000
sf probe 0
sf read 0x80600000 0x0 0x1000000
mmc write 0x80600000 0x10 0x8000
```
_где ***0x80600000*** - Стартовый адрес для Ingenic T31N._

Извлеките карту из камеры и вставьте в компьютер с ОС Linux. Используя команду ***dd***, скопируйте данные с карты в бинарный файл на диске компьютера.
```
dd bs=512 skip=16 count=32768 if=/dev/sdc of=./fulldump.bin
```
_Внимание! Точка монтирования ***sdc*** может отличаться (sda, sdb), в зависимости от подключенного оборудования вашего компьютера._
_________
## Прошивка
### Генерация прошивки
Для получения прошивки и инструкций, воспользуйтесь [автоматическим генератором инструкция для нашего процессора](https://openipc.org/cameras/vendors/ingenic/socs/t31n)

**ВНИМАНИЕ! Lite версия рекомендуется!** 
Все приведенные далее манипуляции описалы для Lite версии

Заполните Требуемые поля и укажите свой MAC адрес. 

![изображение](https://github.com/OpenIPC/device-mjsxj03hl/assets/88727968/e5b8e124-02bb-427e-a2c4-16b16575fce7)

Сгенерируйте прошивку. Внимательно изучите страницу с прошивкой и инструкциями.
К сожалению, производитель не добавил в заводской загрузчик программу tftp, следовательно шить нашу прошивку мы будем по частям и вручную.
Перейдите в раздел **В качестве альтернативы прошивайте прошивку OpenIPC по частям.** и загрузите двоичный файл загрузчика по ссылке. У вас должен получиться бинарный файл **u-boot-t31n-universal.bin**. Не закрывайте страницу с инструкциями. Она нам позже еще понадобится.

Поместите полученный файл на свою SD карту. **ВНИМАНИЕ!** Если вы используете ту же самую карту памяти, что и в прошлом пункте, предварительно отформатируйте ее в Файловой системе Fat32 c таблицей MBR (MS-DOS). Не используйте таблицу GPT! Если вы используете ОС Windows - это самое обычное форматирование. Просто подключите карту памяти и Windiows сама предложит ее отформатировать.
_________________

### Прошивка загрузчика (UBoot)
Итак, мы имеем нашу камеру, подключенную к UART, в слот которой вставлена карта памяти, отформатированная в Fat32 c бинарным файлом загрузчика на ней.
На всякий случай выполним 
```
mmc rescan
```
и дополнительно проверим, что вы все сделали правильно
```
fatls mmc 0:1
```
Должны выйти данные вашей карты памяти. Если вышли какие-либо ошибки, не продолжайте до тех пор, пока они не будут устранены! В противном случае перепрошивка камеры будет возможно только на специальном оборудовании.

В начале введем переменные окружения командой ***setenv***
```
setenv baseaddr 0x80600000
setenv flashsize 0x1000000
```
Заводской загрузчик не поддерживает сохранение переменных, поэтому если камера была перезагружена, вводить придется по-новой.

Теперь приступаем к самому ответственному моменту - прошивке U-Boot. Вставляйте команды построчно! Внимательно следите, чтобы команды не возвращали ошибок! Не продолжайте, если что-то пойдет не так, не пробуйте перезагрузить камеру, попросите помощи в нашем [Телеграм-канале](https://t.me/openipc_modding)
```
mw.b ${baseaddr} 0xff 0x50000
sf probe 0
sf erase 0x0 0x50000
fatload mmc 0:1 ${baseaddr} u-boot-t31n-universal.bin
sf write ${baseaddr} 0x0 ${filesize}
```
Если всё прошло успешно, то у вас теперь новый загрузчик от OpenIPC, поддерживающий все необходимые команды.
Скомандуйте ***reset*** в консоли загрузчика, камера перезагрузится. Теперь загрузку камеры можно прерывать нажатием комбинации ***Ctrl+C***
________________

### Установка OpenIPC

Теперь, когда у нас есть загрузчик с нужным набором команд, мы можем прошить остальную часть прошивки.
Вернитесь на страницу с инструкциями, которую мы получили в пункте [Генерация прошивки](https://github.com/OpenIPC/device-mjsxj03hl/edit/master/README_ru.md#%D0%B3%D0%B5%D0%BD%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D0%BF%D1%80%D0%BE%D1%88%D0%B8%D0%B2%D0%BA%D0%B8)
Далее в разделе **Flash OpenIPC Linux kernel and root filesystem** Загрузите архив по ссылке _Download OpenIPC Firmware (Ultimate) bundle_
В нем вы найдете 4 файла: образ корневой ФС и ядро, а также контрольные суммы к ним. Разархивируйте их на вашу карту памяти и поместите ее в слот камеры.

Далее:
1) Подключаем UART, запускаем терминал!
2) Подаем питание на камеру и быстро останавливаем загрузку нажатием ***Ctrl+C***. Попадаем в консоль загрузчика
3) Проверяем доступ к карте памяти 
```
mmc rescan
```
4)Вводим переменные окружения и сохраняем их:
```
setenv baseaddr 0x80600000
setenv flashsize 0x1000000
saveenv
```
5) Переназначаем разделы ПЗУ. Несмотря на то, что у нас 16Mb памяти, использование такой разметки в сочетании с Lite версией позволит получить больше свободного пространства.
```
run setnor8m
```
После исполненния программы камера перезагрузится. 

6) Прошиваем ядро (Команды вводятся построчно!)
```
mw.b 0x80600000 0xff 0x200000
fatload mmc 0:1 0x80600000 uImage.t31n
sf probe 0; sf lock 0;
sf erase 0x50000 0x200000; sf write 0x80600000 0x50000 ${filesize}
```
7) Прошиваем корневую файловую систему (Команды вводятся построчно!)
```
mw.b 0x80600000 0xff 0x500000
fatload mmc 0:1 0x80600000 rootfs.squashfs.t31n
sf probe 0; sf lock 0;
sf erase 0x250000 0x500000; sf write 0x80600000 0x250000 ${filesize}
```

9) Скомандуем ***reset*** и камера перезагрузится с новой прошивкой. 

Если вы все сделали верно, в окне терминала появится:
```
Welcome to OpenIPC
openipc-t31 login: 
```
Введите логин ***root*** , вход без пароля

![изображение](https://user-images.githubusercontent.com/88727968/223940074-c9f63e1a-b19c-4905-a7fb-66faca1aca52.png)

В полученном поле для ввода скомандуйте 
```
firstboot
```
**Поздравляем с успешной установкой OpenIPC!**
______________
## Настройка
### Предварительная настройка через SD карту

_ВНИМАНИЕ! Используйте отдельную SD карту для базовых настроек или удаляйте содержимое папки **autoconfig** после данного шага!_

Нам потребуется:
- Компьютер с картридером
- Карточка  MicroSD
- Камера

_ВНИМАНИЕ!!! После данной процедуры все настройки камеры будут удалены!_
Если это неприемлимо, или у вас не имеется MicroSD карты - выполните настройку [вручную](https://github.com/OpenIPC/device-mjsxj03hl/blob/master/old_setting_up_ru.md)

Скачайте на компьютер и распакуйте на карту памяти содержимое папки [flash](https://github.com/OpenIPC/device-mjsxj03hl/tree/master/flash)

Содержимое папки должно быть распаковано в корневой каталог, а структура каталогов и файлов должна быть сохранена!

Вставьте карту памяти в камеру, подайте питание. Камера в автоматическом режими выполнит все предварительные настройки и перезагрузится.


**ВНИМАНИЕ! Не забудьте извлечь карту памяти и удалить папку _autoconfig_ или замените карту памяти!**

### Указание данных точки доступа и пароля
Чтобы камера смогла подключиться к Wi-Fi необходимо в консоли ввести следующие переменные:

(переменные вводятся построчно)
```
fw_setenv wlandev rtl8188eu-hi3518ev200-qvc-ipc-136w
fw_setenv wlanssid ИМЯ_ТОЧКИ_ДОСТУПА
fw_setenv wlanpass ПАРОЛЬ
```
Перезагрузите камеру, например командой ***reboot***

После этих манипуляций сеть должна появиться. Войдите в веб-интерфейс и выполните настройки, как описано в [статье](https://github.com/OpenIPC/wiki/blob/master/ru/configuration.md#%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF-%D0%B2-%D0%B2%D0%B5%D0%B1-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81).



### Завершение.
Теперь вы можете управлять камерой через SSH и Web-интерфейс. Аккуратно отсоедините провода от платы. Выполниите сборку камеры. Помните, камера собирается легко, не стоит прикладывать силу. Будьте внимательны и не повредите вашу камеру.

**Успехов в использовании OpenIPC!**
