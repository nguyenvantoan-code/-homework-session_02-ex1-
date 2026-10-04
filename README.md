# Exercise 1: Khởi tạo Droplet trên DigitalOcean

## 1. Mục tiêu

Thực hành khởi tạo một Droplet trên DigitalOcean sử dụng hệ điều hành Ubuntu Server và cấu hình xác thực bằng SSH Key.

Sau khi tạo Droplet, thực hiện kết nối từ máy tính cá nhân tới server thông qua SSH bằng tài khoản `root` mà không cần nhập mật khẩu.

## 2. Cấu hình Droplet

Các thông số yêu cầu:

| Thành phần | Cấu hình |
|---|---|
| Cloud Provider | DigitalOcean |
| Droplet Type | Basic |
| CPU | Shared CPU |
| Storage | Regular SSD |
| Operating System | Ubuntu 22.04 LTS |
| Region | Singapore |
| Authentication | SSH Key |
| User | root |

## 3. Tạo SSH Key

Trên máy tính cá nhân sử dụng Git Bash và chạy:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Khi chương trình hỏi vị trí lưu file, nhấn `Enter` để sử dụng vị trí mặc định.

Khi chương trình hỏi passphrase, nhấn `Enter` để bỏ qua passphrase theo yêu cầu bài.

SSH Key được tạo gồm:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

Trong đó:

- `id_ed25519` là Private Key, chỉ lưu trên máy cá nhân và không đưa lên GitHub.
- `id_ed25519.pub` là Public Key, được sử dụng để thêm vào DigitalOcean.

Kiểm tra Public Key bằng:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy toàn bộ dòng Public Key bắt đầu bằng `ssh-ed25519`.

## 4. Thêm SSH Key vào DigitalOcean

Truy cập DigitalOcean và vào phần **Security → SSH Keys**.

Chọn **Add SSH Key**.

Đặt tên SSH Key:

```text
my-windows-key
```

Dán toàn bộ nội dung của `id_ed25519.pub` vào ô SSH Key Content rồi chọn **Add SSH Key**.

## 5. Khởi tạo Droplet

Chọn **Create → Droplets**.

Cấu hình Droplet:

- Image: Ubuntu 22.04 LTS
- Region: Singapore
- Plan: Basic
- CPU: Shared CPU
- Storage: Regular SSD
- Chọn cấu hình có chi phí thấp nhất theo yêu cầu bài
- Authentication Method: SSH Key
- SSH Key: `my-windows-key`

Đặt tên Droplet:

```text
devops-session02
```

Sau đó chọn **Create Droplet**.

## 6. Lấy địa chỉ IP

Sau khi Droplet được tạo thành công, trạng thái Droplet là `Running`.

DigitalOcean cung cấp một Public IP cho Droplet.

Ví dụ:

```text
<IP_ADDRESS_DROPLET>
```

Thay giá trị trên bằng IP thực tế của Droplet khi thực hiện bài.

## 7. Kết nối SSH

Mở Git Bash trên máy tính cá nhân và chạy:

```bash
ssh -i ~/.ssh/id_ed25519 root@<IP_ADDRESS_DROPLET>
```

Ví dụ:

```bash
ssh -i ~/.ssh/id_ed25519 root@167.xxx.xxx.xxx
```

Ở lần kết nối đầu tiên, nếu hệ thống hỏi xác nhận host, nhập:

```text
yes
```

Sau khi xác thực thành công, terminal hiển thị thông báo chào mừng của Ubuntu và đưa người dùng vào tài khoản `root`.

Ví dụ:

```text
Welcome to Ubuntu 22.04.x LTS

root@devops-session02:~#
```

## 8. Kiểm tra kết nối

Chạy:

```bash
whoami
```

Kết quả mong đợi:

```text
root
```

Kiểm tra phiên bản Ubuntu:

```bash
lsb_release -a
```

Kết quả cho thấy Droplet đang chạy Ubuntu 22.04 LTS.

## 9. Hình ảnh minh chứng

### Ảnh 1 - Cấu hình Droplet

Chèn ảnh chụp giao diện DigitalOcean thể hiện:

- Ubuntu 22.04 LTS
- Region: Singapore
- Basic Plan
- Shared CPU
- Regular SSD
- Authentication bằng SSH Key

### Ảnh 2 - Droplet đã được tạo

Chèn ảnh chụp Droplet có trạng thái `Running` và Public IP.

### Ảnh 3 - Kết nối SSH thành công

Chèn ảnh chụp Git Bash thể hiện lệnh SSH và giao diện Ubuntu Server sau khi đăng nhập.

Ví dụ:

```text
ssh -i ~/.ssh/id_ed25519 root@<IP_ADDRESS_DROPLET>

Welcome to Ubuntu 22.04.x LTS
root@devops-session02:~#
```

### Ảnh 4 - Kiểm tra tài khoản

Chèn ảnh kết quả:

```bash
whoami
```

với kết quả:

```text
root
```

## 10. Kết luận

Đã thực hành quy trình khởi tạo Droplet trên DigitalOcean với Ubuntu 22.04 LTS, cấu hình Basic Shared CPU và Regular SSD tại Singapore.

Droplet được cấu hình xác thực bằng SSH Key thay cho mật khẩu. Kết nối từ máy tính cá nhân tới Droplet bằng tài khoản `root` thông qua SSH thành công.

## 11. Lưu ý bảo mật

Không đưa private key `id_ed25519` lên GitHub.

Chỉ Public Key `id_ed25519.pub` được thêm vào DigitalOcean. Private Key phải được giữ an toàn trên máy cá nhân.
## LOG 
Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ ssh-keygen -t ed22519 -c "nguyenvantoan200608@gmail.com"
Too many arguments.
usage: ssh-keygen [-q] [-a rounds] [-b bits] [-C comment] [-f output_keyfile]
                  [-m format] [-N new_passphrase] [-O option]
                  [-t dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa]
                  [-w provider] [-Z cipher]
       ssh-keygen -p [-a rounds] [-f keyfile] [-m format] [-N new_passphrase]
                   [-P old_passphrase] [-Z cipher]
       ssh-keygen -i [-f input_keyfile] [-m key_format]
       ssh-keygen -e [-f input_keyfile] [-m key_format]
       ssh-keygen -y [-f input_keyfile]
       ssh-keygen -c [-a rounds] [-C comment] [-f keyfile] [-P passphrase]
       ssh-keygen -l [-v] [-E fingerprint_hash] [-f input_keyfile]
       ssh-keygen -B [-f input_keyfile]
       ssh-keygen -D pkcs11
       ssh-keygen -F hostname [-lv] [-f known_hosts_file]
       ssh-keygen -H [-f known_hosts_file]
       ssh-keygen -K [-a rounds] [-w provider]
       ssh-keygen -R hostname [-f known_hosts_file]
       ssh-keygen -r hostname [-g] [-f input_keyfile]
       ssh-keygen -M generate [-O option] output_file
       ssh-keygen -M screen [-f input_file] [-O option] output_file
       ssh-keygen -I certificate_identity -s ca_key [-hU] [-D pkcs11_provider]
                  [-n principals] [-O option] [-V validity_interval]
                  [-z serial_number] file ...
       ssh-keygen -L [-f input_keyfile]
       ssh-keygen -A [-a rounds] [-f prefix_path]
       ssh-keygen -k -f krl_file [-u] [-s ca_public] [-z version_number]
                  file ...
       ssh-keygen -Q [-l] -f krl_file [file ...]
       ssh-keygen -Y find-principals -s signature_file -f allowed_signers_file
       ssh-keygen -Y match-principals -I signer_identity -f allowed_signers_file
       ssh-keygen -Y check-novalidate -n namespace -s signature_file
       ssh-keygen -Y sign -f key_file -n namespace file [-O option] ...
       ssh-keygen -Y verify -f allowed_signers_file -I signer_identity
                  -n namespace -s signature_file [-r krl_file] [-O option]

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ ssh-keygen -t ed22519 -C "nguyenvantoan200608@gmail.com"
unknown key type ed22519

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ ^C

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ ssh-ketgen -t ed25519 -C "nguyenvantoan200608@gmail.com"
bash: ssh-ketgen: command not found

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ ^C

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ ssh-keygen -t ed25519 -C "nguyenvantoan200608@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/Toan/.ssh/id_ed25519):
/c/Users/Toan/.ssh/id_ed25519 already exists.
Overwrite (y/n)? y
Enter passphrase for "/c/Users/Toan/.ssh/id_ed25519" (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/Toan/.ssh/id_ed25519
Your public key has been saved in /c/Users/Toan/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:Mldxkh8HQE5SG5ZyuqmpxjTWZub2JNa1cF86WNipEjw nguyenvantoan200608@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|        .oX+o.   |
|        .=+*. .  |
|         ++. o   |
|       ... o..   |
|     .o Eo+ + .  |
|    + ==o* * o   |
|   + *oo+ + +    |
|    o.=o .   .   |
|   ..o ..        |
+----[SHA256]-----+

Toan@DESKTOP-635P77T MINGW32 ~/Downloads/New folder (main)
$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJqXJyfrSc4tWxRxbAxAn2dsRyNU9LDzwj/lSORlv3EK nguyenvantoan200608@gmail.com
