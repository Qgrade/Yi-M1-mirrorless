# Xiaomi Yi-M1 Mirrorless 3.2-int JSON Protocol Reverse Engineering
Someone could write code for simple application for use on windows or linux pc.
To obtain the password for wifi, a network scanner must be used on the mobile, eg Logcat [NO ROOT].
Start Logcat and launch the YI Mirrorless app and connect to the camera, when the mobile is connected to the camera's wifi network stop the app and switch to the Logcat app and filter the search for "password" in the log. It is 8 characters and numbers only.
First connect via YI Mirrorless on your mobile, then connect your PC to the same wifi network (YI_M1 _...) you must put the wifi connection's IP address to the same subnet as the camera's network in this case 192.168.0.10 is the camera's IP address.

**URL=http://192.168.0.10/?data={"command":"[any command from list here]"}**
Now you can try to send a request to the camera from (chrome browser) eg: 192.168.0.10/?data={"command":"GetCameraStatus"}
The answer should be eg: {"code": 200, "data": {"batteryLevel": "25", "SurplusPhotoCnts": "3008", "lenVer": "0.0", "lenType": ""}}

GetFileList
  range_start:int
  range_end:int
  filetype:all, JPG, DNG, raw
**{"command":"GetFileList","range_start":1,"range_end":1,"filetype":"DNG"}**

Response(if there are DNG file):
**{"code":200,"data":[{"path":"/DCIM/100YICAM/PA140017.DNG","date":"1602693860","filetype":"raw","protectStatus":false}]}**

GetFileInfo
  path
**{"command":"GetFileInfo","path":"/DCIM/100YICAM/PA100001.JPG"}**

Response:
**{"code":200,"data":{"type":"PICNORMAL","size":"4353766","width":"5184","height":"3888","capture_date":"1602358126","shutter_speed":"1/25s","FNumber":"3.5","WB":"Auto","ISO":"800","FocalLength":"12","Make":"YI TECHNOLOGY","focus_mode":"C-AF","model":"M1"}}**

DeleteFile
file_list:path
**{"command":"DeleteFile","file_list":["/DCIM/100YICAM/PA100009.JPG"]}**

Response:
**{"code":200}**

RCStopRemoteCtl
**{"command":"RCStopRemoteCtl"}**

Response:
**{"code":200}**

RCStartRemoteCtl
**{"command":"RCStartRemoteCtl"}**

Response:
**{"code":200}**

RCDoShooting #do one shoot
**{"command":"RCDoShooting"}**

Response:
**{"code":200}**

RCFocusModeSet
FocusMode:"S-AF", "C-AF", "MF"
**{"command":"RCFocusModeSet","FocusMode":"MF"}**

Response:
**{"code":200}**

RCShutterSpeedSet
ShutterSpeed:TIME, BULB, 60s - 1/4000s
**{"command":"RCShutterSpeedSet","ShutterSpeed":"1/1000s"}**

RCImageAspect
ImageAspect:"4:3","3:2","16:9","1:1"
**{"command":"RCImageAspect","ImageAspect":"4:3"}**

Response:
**{"code":200}**

RCFileFormatSet
FileFormat:JPG-S, JPG-M, JPG-L, RAW, RAWJ-S, RAWJ-M, RAWJ-L
**{"command":"RCFileFormatSet","FileFormat":"JPG-S"}**

Response:
**{"code":200}**

RCDriveModeSet
DriveMode:"Single", "Continuous", "2SDelay", "10SDelay"
**{"command":"RCDriveModeSet","DriveMode":"2SDelay"}**

Response:
**{"code":200}**

RCFNSet
Fnumber:
**{"command":"RCFNSet","Fnumber":"3.2"}**

Response:
**{"code":200}**

RCISOSet
ISO:Auto, 100, 200, 400, 800, 1600, 3200, 6400, 12800, 25600
**{"command":"RCISOSet","ISO":"400"}**

Response:
**{"code":200}**

RCWBSet
WB:Auto, Sunny, Shadow, Cloudy, Incandescent, 2000 - 11500
**{"command":"RCWBSet","WB":"Auto"}**

Response:
**{"code":200}**

RCChooseColorMode
ColorMode:Standard, Portrait, Vivid, NaturalBW, HContrastBW
**{"command":"RCChooseColorMode","ColorMode":"Vivid"}**

Response:
**{"code":200}**

**They are probaly few more commands to find..**
