---
title: Tại sao là CachyOS?
description: Tại sao CachyOS có thể tốt hơn cho bạn
tableOfContents:
  minHeadingLevel: 1
  maxHeadingLevel: 4
---

CachyOS là một bản phân phối Arch Linux tập trung vào hiệu suất, được thiết kế để cung cấp một môi trường máy tính ổn định, hiệu quả và thân thiện với người dùng. Nó cung cấp sức mạnh và tính linh hoạt của một hệ thống phát hành liên tục, được nâng cao bởi các tối ưu hóa tiên tiến và một chuỗi công cụ tùy chỉnh giúp đơn giản hóa trải nghiệm người dùng cho cả người mới và người dùng có kinh nghiệm.

## Hiệu suất và Tối ưu hóa

### Các Gói và Kho lưu trữ đã Tối ưu hóa

CachyOS cung cấp một lựa chọn lớn các **[gói đã tối ưu hóa](https://packages.cachyos.org/)** được biên dịch cụ thể cho các kiến trúc CPU hiện đại. Điều này bao gồm hỗ trợ cho các hệ thống `x86-64-v3`, `x86-64-v4`, và `Zen4+`, đảm bảo rằng phần mềm của bạn được xây dựng để tận dụng tối đa các khả năng của phần cứng để tăng hiệu suất đáng kể.

Để có cái nhìn sâu hơn về các kho lưu trữ đã tối ưu hóa của chúng tôi, xem hướng dẫn chi tiết của chúng tôi về **[Kho lưu trữ đã Tối ưu hóa](/vi/features/optimized_repos)**.

### Nhân Tùy chỉnh cho Hiệu suất và Ổn định

Ngoài bộ vá nhân cơ bản của CachyOS điều chỉnh các tham số nhân khác nhau để cải thiện độ phản hồi của desktop, CachyOS chọn lọc các bộ vá chưa được đưa vào mainline hoặc không được bao gồm trong bản sửa đổi ổn định của nhân.

Do đó, các bản vá này trải qua kiểm thử nội bộ trước khi được phát hành cho người dùng để đảm bảo rằng sự ổn định không bị ảnh hưởng. Để có danh sách đầy đủ các bản vá mà CachyOS cung cấp, xem [Nhân](/vi/features/kernel).

### Hỗ trợ Bộ lập lịch CPU Tiên tiến

CachyOS phân phối các nhân với các tối ưu hóa bộ lập lịch CPU mới nhất để đảm bảo một desktop mượt mà, ngay cả dưới tải nặng.

* **EEVDF (Bộ lập lịch nhân Linux mặc định):** Mặc dù xuất sắc cho thông lượng chung, nhân CachyOS bao gồm các **[tham số có thể tùy chỉnh EEVDF](https://github.com/CachyOS/linux/blob/6.15/cachy/kernel/sched/fair.c#L79-81)** để cải thiện độ phản hồi của desktop.

* **[BORE](https://github.com/firelzrd/bore-scheduler) (Burst-Oriented Response Enhancer):** Đối với người dùng cần tối đa tính tương tác, các nhân của chúng tôi hỗ trợ bộ lập lịch BORE, một bộ vá mà nó cải thiện EEVDF để cung cấp một trải nghiệm mượt mà hơn trong các khối lượng công việc chuyên sâu.

Để biết thêm thông tin về các nhân được cung cấp bởi CachyOS và sched-ext, xem tài liệu **[Nhân](/vi/features/kernel)** và **[sched-ext](/vi/configuration/sched-ext)**.

## Công cụ Thân thiện với Người dùng và Tùy chỉnh

### [Phát hiện Phần cứng Tự động](/vi/features/chwd/chwd/)

CachyOS bao gồm một công cụ phát hiện phần cứng tùy chỉnh tự động nhận dạng và cài đặt các driver và gói cần thiết cho hệ thống của bạn. Điều này loại bỏ nhu cầu tìm kiếm driver thủ công, tiết kiệm thời gian và công sức của bạn sau khi cài đặt.

### Quy trình Cài đặt Có thể Tùy chỉnh

Trình cài đặt CachyOS cho phép người dùng tùy chỉnh hệ thống của họ bằng cách chọn môi trường desktop, gói, hệ thống tệp, trình quản lý khởi động, nhân và nhiều hơn để phù hợp với nhu cầu của họ:

- [Môi trường Desktop](/vi/installation/desktop_environments/)
- [Trình quản lý Khởi động](/vi/installation/boot_managers/)
- [Các biến thể Nhân](/vi/features/kernel#variants)
- [Hệ thống tệp](/vi/installation/filesystem)
- [Các gói tùy chỉnh để bao gồm trong quá trình cài đặt](https://github.com/CachyOS/cachyos-calamares/blob/cachyos-limine-qt6/src/modules/netinstall/netinstall.yaml)

### Các ứng dụng Tùy chỉnh của CachyOS

CachyOS phát triển và duy trì bộ ứng dụng của riêng mình để đơn giản hóa quản lý hệ thống và nâng cao trải nghiệm của bạn.

Danh sách các ứng dụng mà CachyOS hiện đang phát triển và duy trì:

-   **[CachyOS Hello](https://github.com/CachyOS/CachyOS-Welcome):** Một ứng dụng chào mừng để điều khiển các tinh chỉnh, áp dụng các sửa lỗi, và cài đặt các gói.
-   **[CachyOS Package Installer](https://github.com/CachyOS/packageinstaller):** Một giao diện người dùng đồ họa (GUI) để cài đặt dễ dàng các ứng dụng.
-   **[CachyOS Kernel Manager](https://github.com/CachyOS/kernel-manager):** Dễ dàng cài đặt các nhân từ kho lưu trữ, cấu hình nhân của riêng bạn, và quản lý khung `sched-ext`.
-   **[cachyos-rate-mirrors](https://github.com/CachyOS/rate-mirrors):** Tự động xếp hạng các mirror Arch và CachyOS để có tốc độ tải xuống tối ưu với `pacman`.
-   **[systemd-boot-manager](https://github.com/CachyOS/systemd-boot-manager):** Tự động tạo các mục khởi động mới cho `systemd-boot`, có thể dễ dàng cấu hình qua `/etc/sdboot-manage.conf`.

## Một Cộng đồng Thân thiện và Tích cực

Điểm mạnh nhất của CachyOS là cộng đồng đang mở rộng của nó. Các thành viên cộng đồng giúp đỡ lẫn nhau bằng cách chia sẻ các mẹo, cung cấp hỗ trợ, và đóng góp vào thành công của dự án. Phản hồi của bạn giúp chúng tôi liên tục cải thiện trải nghiệm CachyOS.

Hãy tham gia cùng chúng tôi và trở thành một phần của cộng đồng trên **[Discord CachyOS](https://discord.gg/cachyos-862292009423470592)** và **[Diễn đàn CachyOS](https://discuss.cachyos.org/)**.
