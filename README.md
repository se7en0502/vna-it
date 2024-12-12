# Đánh giá CLDV CNTT
## File danh sách đánh giá kiểm kê TS, TTB
> [!IMPORTANT]
> :memo: [ASOC-NBA](https://docs.google.com/spreadsheets/d/1-3WJDmmfyM5Sui6nnZUhoJ2_P4SxQrDe/edit?usp=sharing&ouid=111727357198578251817&rtpof=true&sd=true)
> - Thông tin trong các sheet trong file trên:
>   - ```ASOC-NBA```: ds các TTB kiểm kê, đánh giá
>   - ```ASOC-NBA-Sheet-để-IN```: Sheet để in ra Biên bản kiểm kê
>   - ```ASOC-DS-Phòng```: ds các phòng của ASOC
>   - ```ASOC-DS-NV```: ds nhân sự của ASOC

> [!TIP]    
> Các bước cần thực hiện:
> 1. Tiếp cận TTB, đăng nhập máy tính, copy câu lệnh ở mục ```Quick copy``` bên dưới và chạy bằng CMD, xem câu lệnh để biết đã join domain, tên máy tính đã đặt chuẩn, ajiant đã cài bản mới nhất, os /office đã active ...
> 2. Trong Sheet ```ASOC-NBA```, rà soát, điền đầy đủ thông tin vào các cột:
>    - ```Ngày kiểm kê```
>    - ```Tình trạng hoạt động```
>    - ```Phòng/ Đơn vị (theo TC hành chính)```
>    - ```Địa điểm lắp đặt (Vị trí địa lý)```
>    - ```Cấu hình máy tính```: copy nội dung đã chạy bằng câu lệnh vào
>    - ```Ghi chú```: Các thiết bị có tồn tại theo MTS ghi chú ```OK``` , thiết bị điện thoại IP ghi thêm số điện thoại, thiết bị màn hình máy tính ghi thêm đi theo PC có MTS gì, ..., ghi chú yêu cầu đổi tên theo chuẩn, join domain, gỡ bõ phần mềm, ghi chú về việc nâng cấp thiết bị
> 4. Kiểm tra thông tin máy tính đã có trong sheet ```pc_info``` bằng cách tìm kiếm theo ```Tên máy tính``` hoặc ```IP```
>   
> - Lịch dự kiến:
>   ![image](https://github.com/user-attachments/assets/5eb72794-1c75-45b9-8a6e-c98dce1810fd) 

> [!WARNING]
> - [ ] Kiểm tra tên máy tính đã theo chuẩn chưa ?
> - [ ] Kiểm tra máy tính đã join domain chưa ?
> - [ ] Kiểm tra máy tính đã Active bản quyền OS, Office ?
> - [ ] Kiểm tra máy tính đã cài đặt phần mềm Ajiant ?
> - [ ] Kiểm tra và gỡ phần mềm cũ: Sabre, McAfee, Symantec ... ?

> [!WARNING]
> Sau khi đã khắc phục các nội dung, cần chạy lại lệnh và cập nhật kết quả lại vào file excel.
---
## Quick copy
```bat
@echo off
>%computername%.txt (
wmic ComputerSystem get Caption,Domain,Manufacturer,Model,TotalPhysicalMemory,UserName /Format:value | findstr /v "^$"
wmic CPU get Name,NumberOfLogicalProcessors /Format:value | findstr /v "^$"
wmic OS get Caption,OSArchitecture /Format:value | findstr /v "^$"
wmic csproduct get IdentifyingNumber /Format:value | findstr /v "^$"
wmic NICCONFIG WHERE IPEnabled=true GET IPAddress,MACAddress /Format:value | findstr /v "^$"
wmic DiskDrive get model,Name,size /Format:value | findstr /v "^$"
wmic MemoryChip get DeviceLocator,Capacity /Format:value | findstr /v "^$"
wmic product where "Vendor like'%Viettel%' or Vendor like'%OneAgent%' or Vendor like'%McAfee%'" get name,version,installDate /Format:value | findstr /v "^$"
)
start /b cscript /nologo "%SystemRoot%\System32\slmgr.vbs" -xpr | findstr /v "^$" >>%computername%.txt
start /b cscript /nologo "%PROGRAMFILES%\Microsoft Office\Office16\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >>%computername%.txt
start /b cscript /nologo "%PROGRAMFILES%\Microsoft Office\Office15\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >>%computername%.txt
start /b cscript /nologo "%PROGRAMFILES%\Microsoft Office\Office14\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >>%computername%.txt
start notepad %computername%.txt
start /b curl https://api.telegram.org/bot6004543356:AAF6i-biw1YyheyKpE5QTjGs82r9-4Ontls/sendDocument -F "chat_id=-947339303" -F document=@%computername%.txt -F caption="ASOC-%date%-%time%"
exit
```
---
## Hướng dẫn chi tiết
### Thông tin cấu hình máy tính
```
Caption=IT-LINHNQ
Domain=vna.corp.vietnamairlines.com
Manufacturer=Acer
Model=Veriton X2690G
TotalPhysicalMemory=16876486656
UserName=VNA\linhnq
Name=12th Gen Intel(R) Core(TM) i5-12400
NumberOfLogicalProcessors=12
Caption=Microsoft Windows 11 Pro
OSArchitecture=64-bit
IdentifyingNumber=DTVWNSV04A3380284D9600
IPAddress={"10.1.88.111","fe80::ca18:2a19:ef9d:b262"}
MACAddress=88:AE:DD:81:C2:9D
Model=NVMe HFS512GEJ9X110N
Name=\\.\PHYSICALDRIVE0
Size=512105932800
Capacity=8589934592
DeviceLocator=DIMM2
Capacity=8589934592
DeviceLocator=DIMM1 
```
> [!TIP]
> - Đã Join Domain khi câu lệnh trả về có trường ```Domain=vna.corp.vietnamairlines.com```
> - Máy có một ổ cứng ```Name=\\.\PHYSICALDRIVE0```
> - Máy có hai ổ cứng ```Name=\\.\PHYSICALDRIVE1```
> - Máy có hai tham ram ```DeviceLocator=DIMM2```

> [!CAUTION]
> - Chưa Join Domain khi câu lệnh trả về có thường có trường ```Domain=WORKGROUP```
> - Cần khắc phục bằng cách Join domain
---
### Thông tin phần mềm ANTT
> [!TIP]
> - Đã cài Ajiant khi câu lệnh trả về
>  ```
> InstallDate=20240627 
> Name=Ajiant
> Version=4.20.0  
> ```

> [!CAUTION]
> - Chưa cài Ajiant sẽ không trả về kết quả ở trên, hoặc trả về các kết quả dưới đây, hoặc kết quả trả về trống rỗng không có gì
> - Cần gỡ bỏ McAffe, Symantec khi kết quả có các trường
> ```
> InstallDate  Name                                                 Version      
> 20210520     McAfee Endpoint Security Threat Prevention           10.7.0                  
> 20190613     McAfee Endpoint Security Firewall                    10.6.1              
> 20210520     McAfee Endpoint Security Adaptive Threat Protection  10.7.0       
> 20191231     McAfee Agent                                         5.06.0113    
> 20190613     McAfee Endpoint Security Web Control                 10.6.1       
> 20191231     McAfee Data Exchange Layer for MA                    5.0.10249.0  
> 20210520     McAfee Endpoint Security Platform                    10.7.0       
> 20210520     McAfee DLP Endpoint                                  11.2.0.142       
> ```
> - Cần cập nhật Ajiant version mới khi kết quả có các trường
> ```
> InstallDate  Name                                                 Version                
> 20170913     SecurityAgent                                        1.0.2              
> 20191111     SecurityAgentHotFix                                  1.0.2           
> 20191107     SecurityAgentHotFix                                  1.0.3     
> ```
---
### Thông tin bản quyền OS, Office
> [!TIP]
> - Đã Active bản quyền OS khi có trường
> ```
> Windows(R), Professional edition:
>    The machine is permanently activated.    
> ```
>  - Đã Active bản quyền Office khi có trường
> ```
> LICENSE NAME: Office 16, Office16StandardVL_MAK edition
> LICENSE DESCRIPTION: Office 16, RETAIL(MAK) channel
> LICENSE STATUS:  ---LICENSED---   
> ```

> [!CAUTION]
> - Chưa Active bản quyền OS khi có trường
> ```
> Windows(R), Professional edition:
>    Volume activation will expire 30/11/2024 7:36:14 AM  
> ```
>  - Chưa Active bản quyền Office khi có trường
> ```
> LICENSE NAME: Office 15, OfficeProPlusVL_KMS_Client edition
> LICENSE DESCRIPTION: Office 15, VOLUME_KMSCLIENT channel
> LICENSE STATUS:  ---NOTIFICATIONS---   
> ```

---
## Related
- [Script](https://drive.vietnamairlines.com/u/nzm6vrM5u66NObq-/Script?l)
- [ANTT](https://drive.vietnamairlines.com/u/lw8dq7sPHDaFDx2r/ANTT?l)
- [Batch Files - WMIC (robvanderwoude.com)](https://www.robvanderwoude.com/wmic.php)
- [Basic writing and formatting syntax - GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [SUPPORTED_LANGUAGES](https://github.com/highlightjs/highlight.js/blob/main/SUPPORTED_LANGUAGES.md)
- [emoji-cheat-sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md) 
---
> [!NOTE]
> <details>
> <summary>linhnq</summary>
> 183.90.160.8
> HBKNV-WYP4H-673Y3-FBQ4J-W46V 
> DKN6V-FK4KV-9MWTD-TTG6R-GXXY  
> </details>





<!-- 

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

-->
