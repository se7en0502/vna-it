# Đánh giá CLDV CNTT
## File danh sách đánh giá kiểm kê TS, TTB
> [!IMPORTANT]
:memo: [Pleiku & Buôn Ma Thuộc]([https://docs.google.com/](https://docs.google.com/spreadsheets/d/1-1weXJLMdqk_Cp80A4dgilkg2j_AkxMS/edit?usp=sharing&ouid=111727357198578251817&rtpof=true&sd=true])
  
> [!WARNING]
> - [x] Check license OS, chưa có cần ghi vào cột kiến nghị để Active
> - [x] Check license Office, chưa có báo Mr Hùng Active
> - [x] Cần kiểm tra và gỡ phần mềm Sabre cũ không sử dụng nữa

> [!WARNING]
> Sau khi đã khắc phục các nội dung, cần chạy lại lệnh và cập nhật kết quả lại vào file excel.
---
## Quick copy
```bat
wmic ComputerSystem get Caption,Domain,Manufacturer,Model,TotalPhysicalMemory,UserName /Format:value | findstr /v "^$" >%computername%.txt && wmic CPU get Name,NumberOfLogicalProcessors /Format:value | findstr /v "^$" >>%computername%.txt && wmic DiskDrive get model,Name,size /Format:value | findstr /v "^$" >>%computername%.txt && wmic os get Caption,OSArchitecture /Format:value | findstr /v "^$" >>%computername%.txt && wmic csproduct get IdentifyingNumber /Format:value | findstr /v "^$" >>%computername%.txt && wmic NICCONFIG WHERE IPEnabled=true GET IPAddress,MACAddress /Format:value | findstr /v "^$" >>%computername%.txt && type %computername%.txt && start notepad %computername%.txt 
```
```bat
wmic product where "Vendor like'%Viettel%' or Vendor like'%OneAgent%' or Vendor like'%McAfee%'" get name,version,installDate /Format:table >%computername%_ANTT.txt && type %computername%_ANTT.txt && start notepad %computername%_ANTT.txt 
```
```bat
cscript //nologo c:\windows\system32\slmgr.vbs -xpr | findstr /v "^$" > %computername%_lic_status.txt 
cscript //nologo "%PROGRAMFILES%\Microsoft Office\Office16\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
cscript //nologo "%PROGRAMFILES%\Microsoft Office\Office15\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
cscript //nologo" %PROGRAMFILES%\Microsoft Office\Office14\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
start notepad %computername%_lic_status.txt 
```
---
## Hướng dẫn chi tiết
### Thông tin cấu hình máy tính
```bat
wmic ComputerSystem get Caption,Domain,Manufacturer,Model,TotalPhysicalMemory,UserName /Format:value | findstr /v "^$" >%computername%.txt && wmic CPU get Name,NumberOfLogicalProcessors /Format:value | findstr /v "^$" >>%computername%.txt && wmic DiskDrive get model,Name,size /Format:value | findstr /v "^$" >>%computername%.txt && wmic os get Caption,OSArchitecture /Format:value | findstr /v "^$" >>%computername%.txt && wmic csproduct get IdentifyingNumber /Format:value | findstr /v "^$" >>%computername%.txt && wmic NICCONFIG WHERE IPEnabled=true GET IPAddress,MACAddress /Format:value | findstr /v "^$" >>%computername%.txt && type %computername%.txt && start notepad %computername%.txt 
```
> [!TIP]
> - Đã Join Domain khi câu lệnh trả về có trường ```Domain=vna.corp.vietnamairlines.com```
> - Máy có một ổ cứng ```Name=\\.\PHYSICALDRIVE0```
> - Máy có hai ổ cứng ```Name=\\.\PHYSICALDRIVE1```

> [!CAUTION]
> - Chưa Join Domain khi câu lệnh trả về có thường có trường ```Domain=WORKGROUP```
> - Cần khắc phục bằng cách Join domain
---
### Thông tin phần mềm ANTT
```bat
wmic product where "Vendor like'%Viettel%' or Vendor like'%OneAgent%' or Vendor like'%McAfee%'" get name,version,installDate /Format:table >%computername%_ANTT.txt && type %computername%_ANTT.txt && start notepad %computername%_ANTT.txt 
```
> [!TIP]
> - Đã cài Ajiant khi câu lệnh trả về
>  ```
>  InstallDate  Name    Version  
> 20240616     Ajiant  4.20.0   
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
> Chạy script nhớ gõ Enter thêm 2,3 lần
```bat
cscript //nologo c:\windows\system32\slmgr.vbs -xpr | findstr /v "^$" > %computername%_lic_status.txt 
cscript //nologo "%PROGRAMFILES%\Microsoft Office\Office16\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
cscript //nologo "%PROGRAMFILES%\Microsoft Office\Office15\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
cscript //nologo" %PROGRAMFILES%\Microsoft Office\Office14\ospp.vbs" /dstatus | findstr /i "LICENSE STATUS" >> %computername%_lic_status.txt 
start notepad %computername%_lic_status.txt 
```
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
- [ANTT](https://drive.vietnamairlines.com/u/qZ3qQ4Wd61G7nepD/ANTT?l)
- [Batch Files - WMIC (robvanderwoude.com)](https://www.robvanderwoude.com/wmic.php)
- [Basic writing and formatting syntax - GitHub Docs](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [SUPPORTED_LANGUAGES](https://github.com/highlightjs/highlight.js/blob/main/SUPPORTED_LANGUAGES.md)
- [emoji-cheat-sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md) 
---
> [!NOTE]
> <details>
> <summary>linhnq</summary>
> 183.90.160.8
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
