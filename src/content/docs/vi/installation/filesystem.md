---
title: Các Hệ thống Tệp
description: Mô tả và khuyến nghị cho các hệ thống tệp có sẵn. (ext4, f2fs, btrfs, xfs, zfs, bcachefs)
---

CachyOS cung cấp 5 hệ thống tệp khác nhau để cho phép người dùng chọn những gì phù hợp nhất với nhu cầu của họ. Phần sau sẽ đi qua các ưu điểm, nhược điểm và khuyến nghị cho mỗi hệ thống tệp. Mỗi hệ thống tệp đi kèm với các yêu cầu/công cụ của nó được cài đặt sẵn trên CachyOS.

:::note
BTRFS là hệ thống tệp mặc định và được khuyến nghị cho CachyOS. Hãy chọn nó nếu không chắc chắn.
:::

## XFS

XFS là một hệ thống tệp ghi nhật ký được tạo và phát triển bởi Silicon Graphics, Inc. Nó được tạo vào năm 1993, được mang sang linux vào năm 2001, và hiện được hỗ trợ rộng rãi bởi hầu hết các bản phân phối Linux.

### Ưu điểm

- Nhanh, XFS ban đầu được thiết kế với tốc độ và khả năng mở rộng cực độ.
- Đáng tin cậy, XFS sử dụng một số công nghệ để ngăn chặn hỏng dữ liệu.
- Chống phân mảnh do bản chất dựa trên mở rộng và chiến lược phân bổ trì hoãn.

### Nhược điểm

- Không thể thu nhỏ.

### Công cụ userspace

Gói chứa các công cụ userspace để quản lý các hệ thống tệp XFS là `xfsprogs`.

### Khuyến nghị

XFS là hệ thống tệp được khuyến nghị cho người dùng không cần các tính năng nâng cao và chỉ muốn một hệ thống tệp nhanh và đáng tin cậy.

## BTRFS

BTRFS là một hệ thống tệp copy-on-write(COW) hiện đại được tạo vào năm 2007 và ổn định trong kernel linux vào năm 2013. Nó được hỗ trợ rộng rãi và chủ yếu được biết đến với bộ tính năng nâng cao của nó.

### Ưu điểm

- Nén trong suốt. BTRFS hỗ trợ nén các tệp một cách trong suốt để cho phép tiết kiệm không gian đáng kể mà không cần sự can thiệp của người dùng. **CachyOS đi kèm với nén ZSTD được đặt ở mức 3 theo mặc định.**
- Chức năng snapshot. BTRFS tận dụng bản chất COW của nó để cho phép tạo ra các snapshot của các subvolume chiếm rất ít không gian thực tế.
- Chức năng subvolume cho phép kiểm soát lớn hơn đối với hệ thống tệp.
- Có thể mở rộng hoặc thu nhỏ.
- Mở rộng rất nhanh.

### Nhược điểm

- Đôi khi yêu cầu chống phân mảnh hoặc cân bằng.
- Tệ hơn trên các ổ đĩa quay do phân mảnh đã đề cập.

### Công cụ userspace

Gói công cụ userspace Btrfs là `btrfs-progs`

### Bố cục Subvolume

CachyOS cung cấp một bố cục subvolume ngay lập tức để cho phép chức năng snapshot dễ dàng.

- Subvol @ = /
- Subvol @home = /home
- Subvol @root = /root
- Subvol @srv = /srv
- Subvol @cache = /var/cache
- Subvol @tmp = /var/tmp
- Subvol @log = /var/log

### Khuyến nghị

BTRFS được khuyến nghị cho người dùng muốn chức năng snapshot/sao lưu và nén trong suốt.

## EXT4

EXT4 (fourth extended filesystem) là hệ thống tệp Linux được sử dụng phổ biến nhất. EXT4 ổn định trong kernel linux vào năm 2008.

### Ưu điểm

- Rất phổ biến, cho phép truy cập dễ dàng vào nhiều tài nguyên.
- Đáng tin cậy. EXT4 có lịch sử được chứng minh là rất đáng tin cậy.
- Có thể mở rộng hoặc thu nhỏ.
  - Việc thu nhỏ chỉ được hỗ trợ ngoại tuyến và yêu cầu hệ thống tệp phải được gỡ kết nối.

### Nhược điểm

- Xây dựng trên một cơ sở mã cũ.
- Thiếu nhiều tính năng nâng cao mà các hệ thống tệp khác cung cấp.

### Công cụ userspace

Gói để quản lý ext4 là `e2fsprogs`

### Khuyến nghị

EXT4 được khuyến nghị cho người dùng muốn hệ thống tệp đơn giản và được sử dụng phổ biến nhất.

## ZFS

ZFS là một hệ thống tệp nâng cao ban đầu được phát triển bởi Sun Microsystems vào năm 2005. ZFS có nhiều tính năng, nhưng được cấp phép theo CDDL có nghĩa là nó không thể được bao gồm bên trong kernel linux và yêu cầu một module riêng được cài đặt.

:::caution
Không sử dụng nhân Real-time cùng với ZFS, nó không tương thích do các vấn đề về cấp phép.
:::

### Ưu điểm

- Lưu trữ gộp (zpool)
- Snapshot sử dụng COW
- Nén
- Hỗ trợ Raid-Z
- Bộ nhớ đệm ARC cho phép thời gian đọc cực nhanh trên các tệp được truy cập thường xuyên.

### Nhược điểm

- Rất phức tạp để sử dụng và hiểu do các tính năng như zpool và ARC.
- ARC yêu cầu nhiều ram để hiệu quả.
- Không được bao gồm trong kernel linux do đó phụ thuộc vào một module kernel của bên thứ ba (OpenZFS)
- Không tương thích với việc chiếm trước Real-time

### Công cụ cần thiết

'ZFS-Module' CachyOS cung cấp một module zfs được biên dịch sẵn cho mỗi phiên bản kernel.
`zfs-utils` cho các công cụ userspace.

### Khuyến nghị

ZFS chỉ nên được sử dụng bởi người dùng nâng cao muốn sử dụng các tính năng nâng cao của nó, chẳng hạn như lưu trữ gộp hoặc bộ nhớ đệm ARC.

## F2FS

F2FS (Flash-Friendly File System) là một hệ thống tệp flash ban đầu được tạo và phát triển bởi Samsung cho kernel linux. F2FS được tạo để phục vụ cụ thể cho flash NAND được sử dụng trong lưu trữ hiện đại.

### Ưu điểm

- Được thiết kế với tính thân thiện với flash.
- Nén trong suốt được sử dụng để giảm ghi đĩa (tiết kiệm không gian hiện tại không thể sử dụng được bởi người dùng).
- Nhanh hơn các hệ thống tệp khác như EXT4.
- Kéo dài tuổi thọ của flash NAND.

### Nhược điểm

- Không thể thu nhỏ.
- Tiết kiệm không gian từ nén hiện tại không thể sử dụng được bởi người dùng. Điều này có thể được thêm vào trong tương lai.
- fsck (kiểm tra hệ thống tệp) tương đối yếu.
- Hạ cấp xuống một kernel cũ hơn phiên bản đã tạo hệ thống tệp có thể gây ra vấn đề.
- Yêu cầu một giải pháp thay thế khi được sử dụng với GRUB trên hệ thống MBR/BIOS.

### Công cụ userspace

Công cụ chính cho f2fs là `f2fs-tools`

### Khuyến nghị

- F2FS được khuyến nghị cho người dùng muốn tối đa hóa tuổi thọ của các thiết bị flash NAND của họ.
- Limine là trình quản lý khởi động được khuyến nghị cho người dùng F2FS trên hệ thống MBR/BIOS vì nó không yêu cầu giải pháp thay thế như GRUB.

## BcacheFS

Bcachefs là một hệ thống tệp mới nâng cao cho Linux, với sự nhấn mạnh vào độ tin cậy và tính mạnh mẽ và bộ tính năng hoàn chỉnh mà người ta mong đợi từ một hệ thống tệp hiện đại.

:::caution[THÔNG BÁO]
Bcachefs vẫn được coi là thử nghiệm và có thể có vấn đề.
:::

### Ưu điểm

- Copy on write (CoW) - như BTRFS hoặc ZFS
- Nén
- Bộ nhớ đệm, Đặt dữ liệu
- Sao chép
- Có thể mở rộng

### Nhược điểm

- Thử nghiệm
- Cài đặt có thể phức tạp

### Công cụ cần thiết

`bcachefs-dkms` cung cấp hỗ trợ module kernel out-of-tree.
`bcachefs-tools` cho các công cụ userspace.

## Tóm tắt

Sử dụng hệ thống tệp mặc định **BTRFS** vì nó được coi là ổn định và có nhiều tính năng hay (snapshot, nén, v.v.). Sử dụng **XFS** hoặc **EXT4** cho một hệ thống tệp đơn giản
và nhanh.
