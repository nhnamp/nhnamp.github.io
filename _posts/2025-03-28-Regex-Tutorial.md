---
title: "Regex Tutorial"
date: 2025-03-28
categories: [Tutorial, Regex]
tags: [UIT]
---


# [IT003.P21.CTTN] Bài thu hoạch tìm hiểu về thư viện Regular Expression
Sinh viên: Phan Bản Nhật Nam.

MSSV: 24521122.

## 1. Khái niệm
Regular Expression (viết tắt là Regex) là các mẫu ký tự (pattern), hay hiểu đơn giản là một bộ cú pháp mẫu, nó được dùng để thao tác với các chuỗi văn bản, cụ thể là các thao tác như tìm (find), thay thế (replace), ...

Regular Expression được rất nhiều ngôn ngữ lập trình hỗ trợ, được cung cấp dưới dạng các thư viện (libraries) hoặc hàm (functions). Ví dụ:
- Python: `re` (thêm vào chương trình bằng câu lệnh `import re`), trong thư viện có các hàm hỗ trợ như:
    - `re.match(pattern, string)` - Kiểm tra từ đầu chuỗi.
    - `re.search(pattern, string)` - Tìm mẫu trong chuỗi.
    - `re.findall(patter, string)` - Tìm tất cả kết quả khớp.
    - `re.sub(pattern, replacement, string)` - Thay thế chuỗi.
    - `re.split(pattern, string)` - Tách chuỗi theo regex.
    - ...
- JavaScript: `RegExp`.
Các phương thức quan trọng:

    - pattern.test(string) – Trả về true/false nếu chuỗi khớp.

    - string.match(pattern) – Trả về mảng kết quả khớp.

    - string.replace(pattern, replacement) – Thay thế chuỗi.

    - string.split(pattern) – Tách chuỗi.

- PHP: Hàm `preg_` - PHP hỗ trợ regex thông qua các hàm `preg_match`, `preg_replace`,...

## 2. Ứng dụng của Regular Expression
Một vài ứng dụng tiêu biểu của Regular Expression:
- Kiểm tra tính hợp lệ (validation) của một trường dữ liệu nhập vào ô text.

- Tìm kiếm một chuỗi văn bản nằm ở nhiều nơi trong code.

- Lấy dữ liệu (crawl data) từ một trang web để lưu lại vào cơ sở dữ liệu riêng.

- Chuyển một chuỗi văn bản thuần (plain text) hoặc một dạng khác được lưu trong cơ sở dữ liệu sang dạng ngày tháng (DateTime).

- ...

## 3. Bộ cú pháp cơ bản của Regular Expression

| Ký hiệu  | Ý Nghĩa                                  | Ví Dụ     | Giải Thích  |
|:--------:|-----------------------------------------|:---------:|-----------------------------------------|
| `.`      | Bất kỳ ký tự nào                        | `a.c`     | Tìm các chuỗi như `abc`, `a1c`, nhưng không phải `ac` |
| `\d`     | Chữ số (0-9)                            | `\d{3}`   | Tìm ba chữ số liên tiếp, ví dụ: `123`  |
| `\D`     | Không phải chữ số                       | `\D{2}`   | Tìm hai ký tự không phải chữ số |
| `\w`     | Ký tự chữ và số (a-z, A-Z, 0-9, _)      | `\w+`     | Tìm một hoặc nhiều ký tự chữ và số |
| `\W`     | Ký tự không phải chữ và số             | `\W+`     | Tìm một hoặc nhiều ký tự không phải chữ và số |
| `\s`     | Ký tự khoảng trắng (space, tab, line break) | `\s+` | Tìm một hoặc nhiều ký tự khoảng trắng |
| `\S`     | Ký tự không phải khoảng trắng          | `\S+`     | Tìm một hoặc nhiều ký tự không phải khoảng trắng |
| `^`      | Bắt đầu chuỗi                           | `^abc`    | Tìm chuỗi bắt đầu bằng `abc` |
| `$`      | Kết thúc chuỗi                          | `abc$`    | Tìm chuỗi kết thúc bằng `abc` |
| `*`      | Lặp lại 0 hoặc nhiều lần               | `a*`      | Tìm 0 hoặc nhiều ký tự 'a' |
| `+`      | Lặp lại 1 hoặc nhiều lần               | `a+`      | Tìm 1 hoặc nhiều ký tự 'a' |
| `?`      | Tùy chọn (0 hoặc 1 lần)                | `a?`      | Tìm 0 hoặc 1 ký tự 'a' |
| `{n}`    | Lặp lại chính xác n lần                | `a{3}`    | Tìm ba ký tự 'a' liên tiếp |
| `{n,}`   | Lặp lại ít nhất n lần                  | `a{2,}`   | Tìm ít nhất hai ký tự 'a' |
| `{n,m}`  | Lặp lại từ n đến m lần                 | `a{2,4}`  | Tìm từ hai đến bốn ký tự 'a' |
| `[]`     | Nhóm ký tự                              | `[abc]`   | Tìm một ký tự trong nhóm 'a', 'b', hoặc 'c' |
| `[^]`    | Ký tự không nằm trong nhóm            | `[^a-c]`  | Tìm ký tự không phải 'a', 'b', hoặc 'c' |
| `\`      | Escape ký tự đặc biệt                  | `\.`      | Tìm ký tự '.' (giá trị chính xác của dấu chấm) |
| `()`     | Nhóm ký tự                              | `(abc)+`  | Tìm nhóm 'abc' lặp lại một hoặc nhiều lần |

Phía trên chỉ là những cú pháp cơ bản, nếu muốn sử dụng nhiều hơn, ta có thể lên Internet tìm các trang web tổng hợp cú pháp của Regular Expression với từ khoá ví dụ như: **"Regular Expression (Regex) syntax/ cheat sheet"**.

Một vài nguồn tham khảo: 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet

https://www.cheatography.com/davechild/cheat-sheets/regular-expressions/

## 4. Một số ví dụ về Regular Expression
### 4.1. Tìm chuỗi số

Sử dụng cú pháp: `\d`.

![alt text](/assets/images/image.png)

### 4.2. Tìm ngày tháng (dd/mm/yyyy)

Sử dụng cú pháp: `/\b\d{1,2}\/\d{1,2}\/(\d{4}|\d{2})\b/g`.

![alt text](/assets/images/image-1.png)

Giải thích cú pháp: 

- `\b`: Word boundary, tức là đảm bảo chuỗi phải tìm chỉ khớp với ngày tháng hoàn chỉnh, không phải là một phần của chuỗi lớn hơn.

- `\d{1, 2}`: Tìm số có 1 hoặc 2 chữ số.

- `\/`: Tìm ký tự đặc biệt '/' (dùng để tách giữa ngày và tháng).

- `\d{4} | \d{2}`: Tìm số có 4 chữ số hoặc 2 chữ số (số năm), ký tự '|' là ký hiệu của phép hoặc (OR).

- `g`: global flag, dùng để tìm tất cả kết quả trong văn bản, nếu không có thì chỉ tìm kết quả đầu tiên.

→ Nếu dùng cú pháp trên thì có thể tìm luôn những ngày tháng không hợp lệ (ví dụ ngày 99/99/2025 vẫn thoả mãn cú pháp trên).

Cú pháp tìm ngày tháng hợp lệ: 

```
/\b(0?[1-9]|[12]\d|3[01])[\/\-.](0?[1-9]|[12]\d|3[01])[\/\-.](\d{2}|\d{4})\b/g
```
![alt text](/assets/images/image-2.png)

Ngày tháng không hợp lệ ở dòng `Thời gian` không được chọn.

### 4.3. Xác thực địa chỉ email hợp lệ

Sử dụng cú pháp: `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`

![alt text](/assets/images/image-3.png)

### 4.4. Xác thực số điện thoại hợp lệ

Sử dụng cú pháp: `/(?:\+84|0)(3[2-9]|5[2689]|7[06-9]|8[1-9]|9[0-9])\d{7}/g`

![alt text](/assets/images/image-4.png)

## 5. Một số công cụ cho phép thử nghiệm cú pháp Regex

https://regex101.com/

http://regexr.com/

http://www.regexpal.com/

http://regexper.com/