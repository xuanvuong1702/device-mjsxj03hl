# OpenIPC cho Xiaomi MJSXJ03HL 
[Phiên bản tiếng Nga](https://github.com/OpenIPC/device-mjsxj03hl/blob/master/Manual_ru.md)

![Hình ảnh](https://user-images.githubusercontent.com/88727968/222164240-66044bf1-16da-4ea2-af38-6fd3d3fb1b92.png)

## Cảnh báo! Phiên bản hướng dẫn này đã lỗi thời và đang được xem xét lại. Thực hiện các hành động có thể làm hỏng thiết bị của bạn!

Chú ý! Bất kỳ thay đổi nào bạn thực hiện sẽ làm mất bảo hành cho thiết bị này! Tác giả không chịu trách nhiệm cho bất kỳ thiệt hại nào phát sinh từ bất kỳ hành động nào của người dùng!
_______________
## Chuẩn bị
### Kết nối UART adapter

Chúng ta sẽ cần:

- Máy tính với cổng USB 
- Máy đo điện tử hoặc voltmeter
- UART adapter 3,3V , giống như hình dưới

![hình ảnh](https://user-images.githubusercontent.com/88727968/222174358-5203eb83-14ce-4f55-89bd-24775af82599.png)

Tất cả các bước sẽ được thực hiện trên Linux OS, nếu hệ điều hành của bạn khác, vui lòng tham khảo cài đặt UART cụ thể [hướng dẫn trên hệ điều hành của bạn.](https://github.com/OpenIPC/wiki/blob/master/en/installation.md#step-3-connect-to-uart-port-of-your-camera)

Quy trình hoạt động:
1) Xem xét kỹ UART adapter. Tìm các chân ***GND***,***TX***,***RX***. Nếu adapter của bạn hỗ trợ chức năng chọn điện áp hoạt động, hãy đảm bảo rằng nó được đặt ở 3.3V!
2) Sử dụng máy đo điện tử (voltmeter), đảm bảo rằng UART adapter của bạn xuất ra 3.3V. Để làm điều này, thực hiện các phép đo giữa các liên hệ ***GND*** và ***TX***, cũng như ***GND*** và ***RX***. Không sử dụng adapter nếu giá trị điện áp là 5V! Điều này sẽ làm hỏng camera của bạn!
3) Kết nối UART adapter với cổng USB của máy tính. Bạn cần tìm ra điểm gắn kết của adapter trong hệ điều hành của bạn.
4) Sử dụng terminal. Chạy lệnh ***lsusb*** và xem xét kỹ lưỡng đầu ra. Tìm UART adapter của bạn.
5) Sử dụng terminal. Chạy lệnh ***dmesg | grep attached*** từ superuser. So sánh đầu ra của cả hai lệnh và tìm điểm gắn kết adapter. Ví dụ, sử dụng ảnh chụp màn hình dưới đây: ![Screenshot_20230301_210433](https://user-images.githubusercontent.com/88727968/222186693-932e241c-5f92-4876-b4de-e51271ea6ae9.png)
6) Vậy, chúng ta đã biết rằng thiết bị của chúng ta được gắn kết tại ***/dev/ttyUSB0***. Trong trường hợp của bạn, địa chỉ gắn kết có thể khác. Chúng tôi sẽ sử dụng địa chỉ này khi kết nối qua UART. Hãy cẩn thận, khi kết nối nhiều thiết bị như vậy, cũng như khi ngắt kết nối không đúng cách, địa chỉ gắn kết có thể thay đổi.
_____________________________

### Tháo máy

Hiện tại, camera chỉ hỗ trợ nạp firmware thông qua UART adapter, vì vậy chúng ta cần tháo máy để thực hiện các thao tác. **Lưu ý rằng việc này sẽ làm mất bảo hành của nhà sản xuất!**

Chúng ta sẽ cần:
- Thiết bị
- Máy sấy tóc hoặc thiết bị sưởi khác
- Vật dẹp, mỏng như dao rọc giấy
- Tuốc-nơ-vít dạng x dài và mỏng
- Sự tỉ mỉ

Vậy, hãy bắt đầu:
1) Hãy nhẹ nhàng làm ấm phần trước của camera (nơi có ống kính)
2) Sử dụng dao rọc giấy hoặc vật dụng nhọn khác, cẩn thận gỡ bỏ phần trước. Nhớ rằng, dưới phần trước có các dây quan trọng, ***đừng làm hỏng chúng!***
3) Làm việc theo hình tròn, cẩn thận tách phần trước ra khỏi thân camera. ***Nhớ rằng nó được kết nối với bo mạch chính của camera!***
4) Dưới đáy, bạn sẽ tìm thấy hai ốc vít cần phải tháo ra. Sau đó, cẩn thận tách hai nửa của thân camera. Hãy cẩn thận để không làm tổn thương bản thân hoặc làm hỏng các dây kết nối hoặc các bộ phận của camera!
5) Tháo một số ốc vít khác, giải phóng bo mạch chính của thiết bị. Cũng giải phóng cổng type C
________________

### Khám phá
Hãy xem xét kỹ camera, tìm các yếu tố cần thiết, vì trong các bước tiếp theo chúng ta sẽ phải tương tác vật lý với một số trong số chúng.
Nhà sản xuất có thể thay đổi một số thành phần của thiết bị mà không thông báo cho người tiêu dùng. Vì lý do này, hai camera được phát hành vào các thời điểm khác nhau có thể có phần cứng và phần mềm khác nhau. Do đó, một lần nữa hãy xem xét kỹ các thành phần, đảm bảo rằng chúng tương ứng với những gì được chỉ ra trong hướng dẫn này. Nếu bạn có bất kỳ câu hỏi nào, vui lòng liên hệ với [kênh Telegram của chúng tôi](https://t.me/OpenIPC)
##### Bo mạch chính (nhìn từ phía trước)

![IMG_20210904_194002](https://user-images.githubusercontent.com/88727968/222473262-913af0d1-0fee-4ae6-843f-256784381163.jpg "Bo mạch chính (nhìn từ phía trước)")

Phần quan trọng nhất đối với chúng ta trên đây là chip bộ nhớ.
##### Chip bộ nhớ
![IMG_20210904_194034](https://user-images.githubusercontent.com/88727968/222473270-dfb08412-0019-4a57-aecc-3820421263e8.jpg "Chip bộ nhớ trên đó.")

Nó có dấu hiệu số và chữ. Hãy đảm bảo rằng chip trên bo mạch của bạn có dấu hiệu tương tự! Số 128 nghĩa là số bit của bộ nhớ. 128/8=16, vì vậy bộ nhớ của chúng ta là 16 MB. Bạn cần chọn firmware cho loại bộ nhớ này!
##### Bo mạch chính (nhìn từ phía sau)
![IMG_20210904_194151](https://user-images.githubusercontent.com/88727968/222473288-c3efcdc6-2691-452f-aebb-9ab1789d4d2d.jpg "Bo mạch chính (nhìn từ phía sau)")

Ở đây là nơi có module không dây, CPU, và các thành phần khác. Nhưng điều quan trọng nhất đối với chúng ta là ba tiếp xúc với một lỗ, nằm cạnh nhau ở góc trên bên phải của bo mạch. Chính qua chúng mà chúng ta đưa ra các tín hiệu điều khiển cho camera.

##### CPU
![IMG_20210904_194132](https://user-images.githubusercontent.com/88727968/222473285-9c00e6d9-f585-4481-a48b-867b0c1f3a85.jpg "CPU")

Trong trường hợp của chúng ta, nó có dấu hiệu số và chữ. Ingenic T31N. Chữ N là một series. Nó được liệt kê ở hàng thứ hai. [Thêm](https://wiki.openipc.org/en/installation.html#step-1-determine-the-system-on-chip)
_________
### Kết nối camera và bộ chuyển đổi UART

Để kết nối bộ chuyển đổi UART với bo mạch camera, bạn cần sử dụng các dây có đầu nối. Chúng có thể đi kèm với bộ chuyển đổi UART. Tuy nhiên, chúng có thể được thay thế bằng những dây tương tự. Các loại kết nối tương tự có thể tìm thấy trong nhiều loại điện tử khác. Đầu dây thứ hai đến bo mạch nên được hàn để liên hệ không biến mất vào thời điểm quan trọng. Hãy cẩn thận khi hàn, không làm hỏng các yếu tố mạch và không ngắn mạch các liên hệ với nhau!

![IMG_20210904_1941511](https://user-images.githubusercontent.com/88727968/222906480-dea0a59c-2dab-45e3-96fa-81cf335b745b.jpg)

Kết nối các dây đến từ bộ chuyển đổi UART với bo mạch như hình vẽ. Nếu bạn làm đúng, camera sẽ hiển thị nhật ký trong quá trình khởi động. Hãy kiểm tra nó.

#### Kiểm tra chức năng của terminal, camera và kết nối

Đầu tiên, chúng ta cần cài đặt một chương trình terminal để gửi các lệnh điều khiển từ camera và nhận phản hồi. Linux có một số lượng terminal khá lớn, bạn có thể chọn terminal thuận tiện nhất cho bạn. Trong số đó có **screen, picocom, minicom, cutecom**. Phần cuối có giao diện người dùng đồ họa.
Cài đặt chương trình terminal:

``***sudo apt install <TÊN>***``
Các lệnh sẽ được đưa ra cho chương trình picocom.
Để bắt đầu, hãy làm quen với các khả năng của chương trình và cú pháp lệnh:
``***picocom --help***`` 

Kết nối bộ chuyển đổi UART và chạy lệnh trong terminal:

```
picocom -b 115200 /dev/ttyUSB0
```

trong đó tùy chọn ***-b*** chỉ định tốc độ baud, và ***/dev/ttyUSB0*** là địa chỉ điểm gắn mà chúng ta đã tìm hiểu trước đó.

Nếu bạn làm mọi thứ đúng, chương trình sẽ ghi rằng terminal đã sẵn sàng để làm việc. Hãy làm quen với các lệnh điều khiển terminal bằng cách nhấn chuỗi phím ***Ctrl+A Ctrl+H***. Để hiểu rõ hơn về chương trình terminal, hãy tham khảo các hướng dẫn liên quan trên web.

Nếu bạn khởi động camera, bạn sẽ thấy nhật ký khởi động. Hãy thử nhấn các phím như ***Enter*** và đảm bảo rằng terminal phản hồi chúng và gửi sự kiện. Nếu mọi thứ được thực hiện đúng, bạn có thể tiếp tục bước tiếp theo.

____________
### Truy cập vào bootloader
Rất tiếc, camera MJSXJ03HL không hỗ trợ gián đoạn khởi động bằng cách gửi một tổ hợp phím. Vì lý do này, việc gián đoạn khởi động và truy cập vào console downloader sẽ được thực hiện bởi chúng ta theo cách thủ công. Để làm điều này, sẽ cần phải đóng một số liên hệ của [chip bộ nhớ](https://github.com/OpenIPC/device-mjsxj03hl#memory-chip).
Để biết cách làm điều này, hãy đọc [ở đây](https://github.com/OpenIPC/wiki/blob/master/en/help-uboot.md#shorting-pins-on-flash-chip).
Hãy cẩn thận nghiên cứu hướng dẫn trên, tìm chip bộ nhớ và các liên hệ cần thiết, chuẩn bị những gì bạn sẽ đóng các liên hệ với. Tất cả các thao tác sẽ phải được thực hiện đủ nhanh.
CHÚ Ý!!! Bạn chịu trách nhiệm hoàn toàn cho hành động của mình!
Dưới đây là trình tự các hành động để truy cập vào console bootloader:
1. Kết nối camera với bộ chuyển đổi UART
2. Kết nối bộ chuyển đổi UART với cổng USB của máy tính.
3. Khởi chạy terminal trên máy tính, đảm bảo rằng nó nhìn thấy bộ chuyển đổi UART
4. Chuẩn bị đóng các liên hệ
5. Cung cấp nguồn cho bo mạch
6. Nhật ký tải xuống nên xuất hiện trong cửa sổ terminal
7. Đóng các liên hệ của chip bộ nhớ (Điều này phải được thực hiện 0.5-1 giây sau khi nguồn được cung cấp)
8. Việc tải xuống nên bị hủy. Các liên hệ có thể được mở.
9. Nếu bạn làm mọi thứ đúng, console U-boot sẽ xuất hiện trên màn hình với một ký hiệu ***>*** và khả năng nhập.
10. Gõ ***help*** để liệt kê các lệnh hiện có trong bootloader

Rất tiếc, nhà sản xuất cho camera này hạn chế rất nhiều khả năng của U-boot, điều này sẽ tạo ra một loạt rắc rối cho chúng ta trong tương lai cho đến khi chúng ta flash U-boot từ OpenIPC. Nhưng trước tiên, chúng ta cần lưu firmware gốc của camera.
__________
### Lưu firmware gốc
Chú ý! Đừng bỏ qua điểm này! Việc sao lưu firmware gốc sẽ cho phép bạn khôi phục lại hiệu suất của thiết bị, nếu như đột nhiên có điều gì đó không đúng.

Chúng ta sẽ cần:
- Camera đã tháo rời với UART kết nối
- Máy tính
- Thẻ SD có dung lượng ít nhất 16 MB
Đầu tiên, bạn nên làm quen với [bài viết gốc](https://github.com/OpenIPC/wiki/blob/master/en/help-uboot.md#saving-firmware-via-sd-card)

CHÚ Ý! Trong quá trình thao tác sau đây, tất cả thông tin từ thẻ SD sẽ không thể truy cập được, và thẻ không thể sử dụng trước khi định dạng! Tất cả dữ liệu, nằm trên bản đồ sẽ bị mất vĩnh viễn!

Thẻ phải được chèn vào khe của camera. Bộ chuyển đổi UART phải được gắn vào máy tính, và chương trình terminal được khởi chạy.

1) Gián đoạn việc tải camera bằng cách đóng các liên hệ, chúng ta vào console bootloader.
2) Nếu thẻ SD được chèn sau khi gián đoạn tải, thực hiện ***mmc rescan***
3) Đầu tiên, chúng ta dọn dẹp không gian cần thiết để ghi một bản sao của firmware gốc:
```
mmc dev 0
mmc erase 0x10 0x8000
```
4) Bây giờ bạn cần sao chép nội dung của firmware từ chip bộ nhớ flash vào RAM của camera. Để làm điều này, dọn dẹp site của RAM, truy cập vào chip bộ nhớ flash và sao chép toàn bộ dung lượng bộ nhớ flash vào không gian RAM đã được làm sạch. Sau đó lưu dữ liệu đã sao chép từ RAM vào thẻ. Chèn các lệnh từng dòng một!
```
mw.b 0x80600000 ff 0x1000000
sf probe 0
sf read 0x80600000 0x0 0x1000000
mmc write 0x80600000 0x10 0x8000
```
_trong đó ***0x80600000*** - Địa chỉ tải của Ingenic T31N._

Rút thẻ ra khỏi camera và gắn vào máy tính chạy hệ điều hành Linux. Sử dụng lệnh ***dd***, sao chép dữ liệu từ thẻ vào tệp nhị phân trên ổ đĩa máy tính.
```
dd bs=512 skip=16 count=32768 if=/dev/sdc of=./fulldump.bin
```
_Chú ý! Điểm gắn kết của ***sdc*** có thể khác nhau (sda, sdb), tùy thuộc vào thiết bị kết nối của máy tính của bạn._
_______

## Ghi Firmware

# DỪNG LẠI! NẾU BẠN TIẾP TỤC Ở ĐÂY, BẠN CÓ THỂ LÀM HỎNG CAMERA CỦA MÌNH!
> CHÚ Ý! Một số người đã báo cáo vấn đề với phương pháp cài đặt được mô tả dưới đây! Cho đến khi tất cả các vấn đề được giải quyết và repo được cập nhật, vui lòng sử dụng phương pháp cài đặt từ <https://github.com/themactep/device-mjsxj03hl>.

### Tạo Firmware
**LƯU Ý:  !Phiên bản Lite được khuyến nghị!** Tất cả các thao tác sau đây được mô tả cho phiên bản Lite

Để có được firmware và hướng dẫn, sử dụng [Hướng dẫn tạo tự động cho vi xử lý của chúng tôi](https://openipc.org/cameras/Vendors/ingenic/socs/t31n)
Điền vào các trường yêu cầu và chỉ ra địa chỉ MAC của bạn. Như thế này:

![hình ảnh](https://github.com/OpenIPC/device-mjsxj03hl/assets/88727968/e5b8e124-02bb-427e-a2c4-16b16575fce7)

Tạo firmware. Hãy nghiên cứu kỹ trang với firmware và hướng dẫn.
Rất tiếc, nhà sản xuất không thêm chương trình TFTP vào bootloader gốc, do đó chúng ta sẽ ghi firmware của chúng tôi theo từng phần và thủ công.
Đi đến phần **Ngoài ra, ghi Firmware OpenIPC theo từng phần** và tải xuống tệp nhị phân của bootloader tại liên kết. Bạn nên có một tệp nhị phân **u-boot-t31n-universal.bin**. Không đóng trang với hướng dẫn. Chúng tôi sẽ cần nó sau.

Đặt tệp kết quả trên thẻ SD của bạn. **Chú ý!** Nếu bạn sử dụng cùng một thẻ nhớ như trong đoạn cuối, hãy định dạng nó theo MBR (MS-DOS). Không sử dụng GPT! Nếu bạn sử dụng hệ điều hành Windows, đây là định dạng phổ biến nhất. Chỉ cần kết nối thẻ nhớ và Windows sẽ tự đề xuất định dạng nó.

### Ghi UBoot
Vậy là, chúng ta đã kết nối camera của mình với UART, trong khe của nó có một thẻ nhớ được chèn vào, được định dạng theo Fat32 với một tệp nhị phân bootloader trên đó.
Chỉ để đảm bảo, hãy thực hiện

```
mmc rescan
```
and additionally check that you did everything correctly
```
fatls mmc 0:1
```
Dữ liệu thẻ nhớ của bạn sẽ được hiển thị. Nếu có bất kỳ lỗi nào xuất hiện, đừng tiếp tục cho đến khi chúng được khắc phục! Nếu không, việc ghi camera chỉ có thể thực hiện trên các thiết bị đặc biệt.

Đầu tiên, chúng ta sẽ nhập các biến môi trường bằng lệnh ***setenv***
```
setenv baseaddr 0x80600000
setenv flashsize 0x1000000
```
Bootloader nhà máy không hỗ trợ lưu biến, vì vậy nếu camera được khởi động lại, bạn sẽ phải nhập lại.

Bây giờ chúng ta tiến hành phần quan trọng nhất - ghi U-Boot. Nhập các lệnh từng dòng một! Hãy cẩn thận để các lệnh không trả về lỗi! Đừng tiếp tục nếu có gì đó không đúng, đừng cố gắng khởi động lại camera, hãy yêu cầu sự giúp đỡ trong [kênh Telegram](https://t.me/openipc) của chúng tôi.
```
mw.b ${baseaddr} 0xff 0x50000
sf probe 0
sf erase 0x0 0x50000
fatload mmc 0:1 ${baseaddr} u-boot-t31n-universal.bin
sf write ${baseaddr} 0x0 ${filesize}
```
Nếu mọi thứ diễn ra tốt, thì bây giờ bạn có một bootloader mới từ OpenIPC hỗ trợ tất cả các lệnh cần thiết.
Lệnh ***reset*** trong console bootloader, camera sẽ khởi động lại. Việc tải camera giờ đây có thể bị gián đoạn bằng cách nhấn ***Ctrl+C***
________________
### Cài đặt OpenIPC

Bây giờ khi chúng ta có một bootloader với bộ lệnh đúng, chúng ta có thể ghi phần còn lại của firmware.
Quay lại trang hướng dẫn mà chúng ta đã nhận trong [Tạo Firmware](https://github.com/OpenIPC/device-mjsxj03hl#firmware-generation)
Tiếp theo trong phần **Flash OpenIPC Linux kernel và root filesystem**. Tải xuống lưu trữ từ liên kết _Tải xuống bộ Firmware OpenIPC (Ultimate)_
Bạn sẽ tìm thấy 4 tệp trong đó: hình ảnh FS gốc và kernel, cũng như checksums cho chúng. Giải nén chúng vào thẻ nhớ của bạn và đặt nó vào khe camera.
Tiếp theo:
1) Kết nối UART, khởi chạy terminal
2) Cung cấp nguồn cho camera và nhanh chóng dừng việc tải xuống bằng cách nhấn ***Ctrl+C***. Truy cập vào console bootloader
3) Kiểm tra quyền truy cập vào thẻ nhớ
```
mmc rescan
```
4) Nhập các biến môi trường và lưu chúng:
```
setenv baseaddr 0x80600000
setenv flashsize 0x1000000
saveenv
```
5) Gán lại các phân vùng ROM theo kích thước và loại bộ nhớ flash. Mặc dù chúng ta có 16Mb bộ nhớ, nhưng sử dụng cấu trúc này kết hợp với phiên bản Lite sẽ cho phép chúng ta có thêm không gian trống.
```
run setnor8m
```
6) Flash boot (Các lệnh được nhập từng dòng một!)
```
mw.b 0x80600000 0xff 0x200000
fatload mmc 0:1 0x80600000 uImage.t31n
sf probe 0; sf lock 0;
sf erase 0x50000 0x200000; sf write 0x80600000 0x50000 ${filesize}
```
7) Flash rootfs (Các lệnh được nhập từng dòng một!)
```
mw.b 0x80600000 0xff 0x500000
fatload mmc 0:1 0x80600000 rootfs.squashfs.t31n
sf probe 0; sf lock 0;
sf erase 0x250000 0x500000; sf write 0x80600000 0x250000 ${filesize}
```
8) Chúng ta sử dụng lệnh ***reset*** và camera sẽ khởi động lại với firmware mới.

Nếu bạn đã thực hiện mọi thứ đúng, sau đây sẽ xuất hiện trong cửa sổ terminal:
```
Welcome to OpenIPC
openipc-t31 login: 
```
Đăng nhập với tư cách ***root***, không cần mật khẩu

![hình ảnh](https://user-images.githubusercontent.com/88727968/223940074-c9f63e1a-b19c-4905-a7fb-66faca1aca52.png)

Trong trường nhập kết quả, hãy nhập lệnh
```
firstboot
```
**Chúc mừng bạn đã cài đặt thành công OpenIPC!**
_____
## Tinh chỉnh
### Cài đặt trước

_CHÚ Ý! Sử dụng một thẻ SD riêng biệt cho các cài đặt cơ bản hoặc xóa nội dung của thư mục **autoconfig** sau bước này!_

Chúng ta sẽ cần:
- Máy tính với đầu đọc thẻ
- Thẻ Micro SD
- Camera

_CHÚ Ý!!! Sau quy trình này, tất cả các cài đặt camera sẽ bị xóa!_
Nếu điều này không chấp nhận được, hoặc bạn không có thẻ microSD - hãy cấu hình theo cách thủ công theo [phiên bản cũ của hướng dẫn](https://github.com/OpenIPC/device-mjsxj03hl/blob/master/old_setting_up_en.md)

Tải về máy tính và giải nén nội dung của thư mục [flash](https://github.com/OpenIPC/device-mjsxj03hl/tree/master/flash) vào một thẻ nhớ.

Nội dung của thư mục phải được giải nén vào thư mục gốc, và cấu trúc thư mục và tệp phải được giữ nguyên!

Chèn thẻ nhớ vào camera, bật nguồn. Camera sẽ tự động hoàn thành tất cả các cài đặt trước và khởi động lại.

**CHÚ Ý! Đừng quên gỡ thẻ nhớ và xóa thư mục _autoconfig_ hoặc thay thế thẻ nhớ!**

### Xác định thông tin về điểm truy cập và mật khẩu
Để camera kết nối với Wi-Fi, bạn phải nhập các biến sau vào console:

(Các biến được nhập từng dòng một)
```
fw_setenv wlandev rtl8188eu-hi3518ev200-qvc-ipc-136w
fw_setenv wlanssid TÊN_ĐIỂM_TRUY_CẬP
fw_setenv wlanpass MẬT_KHẨU
```
Khởi động lại camera, ví dụ với lệnh ***reboot***

Sau những thao tác này, mạng nên xuất hiện. Bạn có thể đăng nhập vào giao diện web và tiếp tục cài đặt

### Kết thúc
Bây giờ bạn có thể điều khiển camera qua SSH và giao diện Web. Cẩn thận tháo các dây ra khỏi bo mạch. Lắp ráp camera. Hãy nhớ, camera dễ dàng lắp ráp, không sử dụng lực. Hãy cẩn thận để không làm hỏng camera của bạn.

**Chúc bạn thành công trong việc sử dụng OpenIPC!**
