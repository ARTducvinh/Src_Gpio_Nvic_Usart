## Tính năng
- **Bật/tắt LED** qua lệnh USART.
- **Nhấp nháy LED** với chu kỳ 5 giây hoặc chu kỳ tùy chọn (ms) qua lệnh USART.
- **Gửi phản hồi trạng thái** về máy tính qua USART.

## Cấu trúc thư mục
- `src/`: Chứa mã nguồn C (main, gpio, usart, timer, system, syscalls).
- `inc/`: Chứa file header định nghĩa hàm và thanh ghi.
- `startup_stm32f401xc.s`: File khởi động.
- `STM32F401XX_FLASH.ld`: Linker script.
- `Makefile`: Tập lệnh biên dịch.
- `flash.jlink`: Script nạp chương trình qua J-Link.

## Hướng dẫn biên dịch & nạp
1. Cài đặt toolchain `arm-none-eabi-gcc` và J-Link.
2. Biên dịch:
    ```sh
    make
    ```
3. Nạp chương trình:
    ```sh
    make flash
    ```

## Giao tiếp USART
- Baudrate: 115200, 8N1, TX/RX trên PA2/PA3.
- Gửi lệnh từ máy tính (kết thúc bằng ký tự `e`):
    - `1e`: Bật LED.
    - `0e`: Tắt LED.
    - `ie`: Nhấp nháy LED mỗi 5 giây.
    - `t<ms>e`: Nhấp nháy LED với chu kỳ `<ms>` mili giây (ví dụ: `t500e`).
- Phản hồi sẽ được gửi lại qua USART.

## Các file chính
- [src/main.c](src/main.c): Hàm `main`, khởi tạo và vòng lặp chính.
- [src/gpio.c](src/gpio.c), [inc/gpio.h](inc/gpio.h): Điều khiển LED.
- [src/usart.c](src/usart.c), [inc/usart.h](inc/usart.h): Khởi tạo USART2, nhận lệnh, gửi phản hồi.
- [src/timer.c](src/timer.c), [inc/timer.h](inc/timer.h): Khởi tạo và xử lý timer.
- [src/system_stm32f4xx.c](src/system_stm32f4xx.c): Cấu hình clock hệ thống.
- [inc/stm32f401xx.h](inc/stm32f401xx.h): Định nghĩa thanh ghi ngoại vi.

## Lưu ý
- Đảm bảo kết nối đúng chân UART trên board STM32F401.
- Có thể mở rộng thêm các lệnh hoặc chức năng khác tùy ý.

---