## Bước 1: Tải phiên bản 0.8.2 tại: https://zeppelin.apache.org/download.html 

Bản 0.8.2 ở cuối trang web nha các em. Tên file là zeppelin-0.8.2-bin-all.tgz

## Bước 2: Giải nén bằng WinRAR hay 7-zip
Giả sử ta giải nén ra thư mục C:\zeppelin-0.8.2-bin-all. 

## Bước 3: Cài đặt Java RE: 
+ SE 8 (64 bit): https://javadl.oracle.com/webapps/download/GetFile/1.8.0_331-b09/165374ff4ea84ef0bbd821706e29b123/windows-i586/jre-8u331-windows-x64.exe
+ Sau bước này, thử chạy câu lệnh "java -version" trong command prompt xem có bị lỗi không. 

## Bước 4: Cài đặt Python3 mới nhất. Khỏi hướng dẫn bước này nha
+ Sau bước này, thử chạy câu lệnh "python --version" trong command prompt xem có bị lỗi không. 

## Bước 5: Tạo virtual environment cho Zeppelin
Mở command prompt, gõ lần lượt các câu lệnh sau: 
```
cd C:\zeppelin-0.8.2-bin-all
mkdir python\venv
python -m venv python\venv
python\venv\scripts\activate.bat
```

## Bước 6: Cài các package Python 
+ py4j==0.10.4
+ pyspark==2.2.1

## Bước 7: Chỉnh sửa file C:\zeppelin-0.8.2-bin-all\bin\zeppelin.cmd  
Thêm dòng sau ở ngay sau dòng REM cuối cùng: 
```
set PATH=C:\zeppelin-0.8.2-bin-all\python\venv\Scripts;C:\Progra~2\Common Files\Oracle\Java\javapath;
```

## Bước 8: Chạy Zeppelin 
Nhấp đúp vào file C:\zeppelin-0.8.2-bin-all\bin\zeppelin.cmd. 

## Bước 9: Vào giao diện Zeppelin
Mở trình duyệt, vào http://localhost:8080 để bắt đầu sử dụng Zeppelin. 

## Bước 10: Tạo note mới 
Chọn "Create new note", đặt tên và chọn "Default Interpreter" là "spark". Bấm create. 

## Bước 11: Gõ thử dòng code chạy thử 
```
%pyspark

print('hello world')
```

* Bước 12 trở đi sẽ thực hiện fix lỗi. 

## Bước 12: Dừng Zeppelin server 
Chuyển qua cửa số command prompt, giữ ctrl + C. Nếu nó hỏi Y/N thì gõ "Y" và enter. 

## Bước 13: Thay thế một số tập tin
Tải các file patches tại https://cloud.vinhthanh.net/s/xfztc4JfcjAJtxA . Lần lượt thay thế như sau: 
+ spark-interpreter-0.8.2.jar -> C:\zeppelin-0.8.2-bin-all\interpreter\spark\spark-interpreter-0.8.2.jar
+ py4j-0.10.4-src.zip -> C:\zeppelin-0.8.2-bin-all\interpreter\spark\pyspark\py4j-0.10.4-src.zip
+ resultiterable.py -> C:\zeppelin-0.8.2-bin-all\python\venv\Lib\site-packages\pyspark\resultiterable.py

## Bước 14: Quay lại bước 8 để chạy thử lại xem còn lỗi không. 

## Check list để các em tự kiểm tra lỗi 
1. Mở cmd và chạy lần lượt: 
```
python --version
"C:\Progra~2\Common Files\Oracle\Java\javapath\java.exe" -version
```
Nếu làm đúng, màn hình hiện phiên bản Python >= 3.10 và java là 1.8.0_331. 

2. Bước 5 và 6 phải thực hiện trên cùng một cửa sổ command prompt. 
3. Ở bước 6, cài đặt package chính xác phiên bản đã nêu ở trên. 
```
pip install py4j==0.10.4
pip install pyspark==2.2.1
```
4. Ở bước 2, em có giải nén trong thư mục nào khác C:\zeppelin-0.8.2-bin-all không? Nếu có thì các bước sau (như bước 7) có thể sẽ phải sửa đường dẫn nhé. 
5. Bước 13 cực kỳ quan trọng. Toàn bộ 3 files phải chép đè lên files có sẵn cùng tên. Nếu không có sẵn những file gốc ban đầu tức ta đã làm sai bước nào đó rồi. 
6. Kiểm tra xem có chương trình nào chiếm cổng 8080 không. Mở cmd bằng quyền admin. Chạy: 
```
netstat -ano
```
Trong bảng xuất hiện, tìm hàng nào đang dùng cổng 8080. Số ở cột cuối cùng là PID (process ID), ta nhớ số đó. Mở task manager, chuyển qua mục Details, tìm process có PID giống vậy, chọn nó và bấm end task. 
Chạy lại Zeppelin để xem thử kết quả. 

5. Lỗi AttributeError: module 'collections' has no attribute 'Iterable'

Quay lại bước 13, tải thêm file spark.zip và thay thế như sau: 
+ spark.zip -> C:\zeppelin-0.8.2-bin-all\interpreter\spark\pyspark\spark.zip


Reference: Thầy Lê Minh Tân - HCMUTE