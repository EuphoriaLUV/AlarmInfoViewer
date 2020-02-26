# AlarmInfoViewer
- Alarm File Load(XML)
- Alarm 발생 위치 Image Load(jpg) 및 Pointer
- Alarm 관련 Cause / Management 관련 다국어 지원
- MFC에서 Alarm Screen 없을 시 UI 대체
- File Remover
<br>
<br>
<br>
### Alarm File Load(XML)
- File Path
> C:\Program Files\ISoft\Common\AlarmInfoViewer\AlarmInfoViewer.exe.config

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
	<appSettings>
		<add key="AlarmInfoFile" value="D:\\XXXXX\\Config\\Data\\AlarmInfo.xml"/>
		<add key="Opacity" value="1.0"/>
	</appSettings>
</configuration>
```
> <add key="AlarmInfoFile" value="D:\XXXXX\Config\Data\AlarmInfo.xml"/>
  Program 실행 시 Load 할 Alarm file 경로

 - Alarm File 구조
 ```Xml
 <?xml version="1.0" standalone="yes"?>
 <Group Attr1="AlarmTable" Attr2="KAlarmEnum" Attr3="" Attr4="" Attr5="" Type="eKAlarmEnumType">
     ......
     <Table>
          <Name>eERR_DISCONNECTION1_ALARM</Name>
          <NO>1</NO>
          <CODE>2</CODE>
          <PART>HOST</PART>
          <TYPE>1</TYPE>
          <Message>eERR_DISCONNECTION1_ALARM</Message>
          <Image>D:\XXXXX\Config\GUI\Image\XXXX.jpg</Image>
          <POS_X>419.4</POS_X>
          <POS_Y>534.35</POS_Y>
          <Cause>이것을 어떻게 조치하냐?</Cause>
          <Management>나도 모르겠다.</Management>
    </Table>
    ......
 </Group>
 ```

 |Value|Description|
 |:---|:---|
 | 0 | Local Storage SQLite DB |
 | 1 | Network Drive Storage SQLite DB |
 | 2 | IPV6 MySQL or Maria DB |

 |Element|Description|Type|
 |:---|:---||:---|

 <br>
 <br>

### Alarm 발생 위치 Image Load(jpg) 및 Pointer
  - jpg File Load 만 가능 Alarm File의 Table의 Image Element 값의 경로에서 Image Load
    ex) <Image>D:\XXXXX\Config\GUI\Image\XXXX.jpg</Image>

  - Pointer 위치 등록 방법
> Xml Direct 편집
  : Alarm File의 POS_X, POS_Y Element 값을 직접 수정.
  ```Xml
           <POS_X>419.4</POS_X>
           <POS_Y>534.35</POS_Y>
  ```
> AlarmInfoViewer Edit 기능 활성화
![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/Edit1.jpg)
![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/Edit2.jpg)
<br>
<br>

### Alarm 관련 Cause / Management 관련 다국어 지원




```c#
    public class xAppEnvUx : IxAppEnvUx
    {
        public xAppEnvUx(string fullPath)
        {  
            ...
        }

        public xAppEnv Get();
        public void Save(xAppEnv env);
    }
```

## View
> Environment View interface
```c#
    public interface IxAppEnvUxView
    {
        int UseWebItemTitle { get; set; }
        int UseDBItemChk { get; set; }
        int DatabaseType { get; set; }

        xReviewEnv Review { get; set; }
        xPurchaseEnv Purchases { get; set; }

        Presenter.xAppEnvUxPresenter Presenter { set; }
    }

```
## Presenter
> Environment Presenter
```c#
    public xAppEnvUxPresenter(IxAppEnvUxView view, IxAppEnvUx repository)
    {
        ...
    }

    public void UpdateAppEnvView();
    public void ApplyEnv();
    public void SaveEnv();
```
