# AlarmInfoViewer
* Alarm File Load(XML)
* Alarm 발생 위치 Image Load(jpg) 및 Pointer
* Alarm 관련 Cause / Management 관련 다국어 지원
* MFC에서 Alarm Screen 없을 시 UI 대체
* File Remover
<br>
<br>

### Alarm File Load(XML)
 * File Path
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
  value attribute 값 Program 실행 시 Load 할 Alarm file 경로로 수정

 * Alarm File 구조
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
 |Element|Description|Type|
 |:---|:---|:---|
 | Name | Alarm Name | String(English Only) |
 | NO | Alarm No | Integer |
 | CODE | 1 : Light | 1 or 2 |
 |      | 2 : Heavy |        |
 | PART | Alarm 발생 Unit | String(English Only) |
 | TYPE | Alarm Type(내부적으로 사용하지는 않음.) | Integer |
 | Message | Alarm Message(English Only) | String(English Only) |
 | Image | Background Image File 경로(jpg만 지원) | String |
 | POS_X | Alarm 발생 부위 포인터 활성화 X 위치 | Double |
 | POS_Y | Alarm 발생 부위 포인터 활성화 Y 위치 | Double |
 | Cause | Alarm 발생 원인 | String(다국어) |
 | Management | Alarm 조치 방법 | String(다국어) |

 <br>
 <br>

### Alarm 발생 위치 Image Load(jpg) 및 Pointer
 * jpg File Load 만 가능 Alarm File Table의 Image Element 값에서 Image Load
 > ex) <Image>D:\XXXXX\Config\GUI\Image\XXXX.jpg</Image>

 * Pointer 위치 등록 방법
    * Xml Direct 편집 : Alarm File의 POS_X, POS_Y Element 값을 직접 수정
        > ex)```XML <POS_X>419.4</POS_X>
                 <POS_Y>534.35</POS_Y> ``` 

        + AlarmInfoViewer Edit 기능 활성화
        >![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/Edit1.jpg)
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
