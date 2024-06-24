# Đánh giá CLDV CNTT
## File danh sách đánh giá kiểm kê TS, TTB
> [!IMPORTANT]
:memo: [Quy Nhơn & Tuy Hòa](https://docs.google.com/)
  
> [!WARNING]
> - [x] Check license OS, chưa có cần ghi vào cột kiến nghị để Active
> - [x] Check license Office, chưa có báo Mr Hùng Active
> - [x] Cần kiểm tra và gỡ phần mềm Sabre cũ không sử dụng nữa

> [!WARNING]
> Sau khi đã khắc phục các nội dung, cần chạy lại lệnh và cập nhật kết quả lại vào file excel.

## Thông tin cấu hình máy tính
```bat
wmic ComputerSystem get Caption,Domain,Manufacturer,Model,TotalPhysicalMemory,UserName /Format:value | findstr /v "^$" >%computername%.txt && wmic CPU get Name,NumberOfLogicalProcessors /Format:value | findstr /v "^$" >>%computername%.txt && wmic DiskDrive get model,Name,size /Format:value | findstr /v "^$" >>%computername%.txt && wmic os get Caption,OSArchitecture /Format:value | findstr /v "^$" >>%computername%.txt && wmic csproduct get IdentifyingNumber /Format:value | findstr /v "^$" >>%computername%.txt && wmic NICCONFIG WHERE IPEnabled=true GET IPAddress,MACAddress /Format:value | findstr /v "^$" >>%computername%.txt && type %computername%.txt && start notepad %computername%.txt 
```
> [!TIP]
> Đã Join Domain

> [!CAUTION]
> Chưa Join Domain

## Thông tin phần mềm ANTT
```bat
wmic product where "Vendor like'%Viettel%' or Vendor like'%OneAgent%' or Vendor like'%McAfee%'" get name,version,installDate /Format:table >%computername%_ANTT.txt && type %computername%_ANTT.txt && start notepad %computername%_ANTT.txt 
```
> [!TIP]
> Đã cài Ajiant

> [!CAUTION]
> Cần gỡ bỏ McAffe, Symantec

## Thông tin bản quyền OS, Office
> [!TIP]
> Chạy script nhớ gõ Enter thêm 2,3 lần
```bat
cscript //nologo c:\windows\system32\slmgr.vbs -xpr | findstr /v "^$" > %computername%_lic_status.txt 
cscript //nologo "%PROGRAMFILES%\Microsoft Office\Office16\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
cscript //nologo "%PROGRAMFILES%\Microsoft Office\Office15\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
cscript //nologo" %PROGRAMFILES%\Microsoft Office\Office14\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
start notepad %computername%_lic_status.txt 
```
> [!TIP]
> Đã Active bản quyền

> [!CAUTION]
> Chưa Active bản quyền

##
> [!NOTE]
> 183.90.160.8

## Related
- [Script](https://drive.vietnamairlines.com/u/nzm6vrM5u66NObq-/Script?l)
- [ANTT](https://drive.vietnamairlines.com/u/qZ3qQ4Wd61G7nepD/ANTT?l)
- [Batch Files - WMIC (robvanderwoude.com)](https://www.robvanderwoude.com/wmic.php)
- [Basic writing and formatting syntax - GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [SUPPORTED_LANGUAGES](https://github.com/highlightjs/highlight.js/blob/main/SUPPORTED_LANGUAGES.md)
- [emoji-cheat-sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md) 


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
