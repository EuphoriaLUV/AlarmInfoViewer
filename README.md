# AlarmInfoViewer
* Alarm File Load(XML)
* Alarm 발생 위치 Image Load(jpg) 및 Pointer
* Alarm 관련 Cause / Management 관련 다국어 지원
* MFC에서 Alarm Screen 없을 시 UI 대체
* File Remover
* Interface Solution

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

    ```Xml
    <Table>
        <Name>eERR_DOOR_OPEN1</Name>
        <NO>310</NO>
        <CODE>2</CODE>
        <PART>SYSTEM</PART>
        <TYPE>1</TYPE>
        <Message>ERR_DOOR_OPEN1</Message>
        <Image>D:\XXXX\Config\GUI\Image\Flower1.jpg</Image>
        <POS_X>156.15</POS_X>
        <POS_Y>236.85</POS_Y>
        <Cause>이 것을 어떻게 조치하냐?</Cause>
        <Management>나도 모르겠다.</Management>
      </Table>
      <Table>
        <Name>eERR_DOOR_OPEN2</Name>
        <NO>311</NO>
        <CODE>2</CODE>
        <PART>SYSTEM</PART>
        <TYPE>1</TYPE>
        <Message>ERR_DOOR_OPEN2</Message>
        <Image>D:\XXXX\Config\GUI\Image\Flower2.jpg</Image>
        <POS_X>432.7</POS_X>
        <POS_Y>221.6</POS_Y>
        <Cause>怎么做</Cause>
        <Management>我也不知道</Management>
      </Table>
      <Table>
        <Name>eERR_DOOR_OPEN3</Name>
        <NO>312</NO>
        <CODE>2</CODE>
        <PART>SYSTEM</PART>
        <TYPE>1</TYPE>
        <Message>ERR_DOOR_OPEN3</Message>
        <Image>D:\XXXX\Config\GUI\Image\Flower3.jpg</Image>
        <POS_X>595.95</POS_X>
        <POS_Y>104.9</POS_Y>
        <Cause>Làm thế nào tôi nên đối phó với điều này?</Cause>
        <Management>Tôi cũng không biết.</Management>
      </Table>

    ```
 >![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/ImageLoad1.jpg "eERR_DOOR_OPEN1 Click")
  ![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/ImageLoad2.jpg "eERR_DOOR_OPEN2 Click")
  ![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/ImageLoad3.jpg "eERR_DOOR_OPEN3 Click")




 * Pointer 위치 등록 방법
    * Xml Direct 편집 : Alarm File의 POS_X, POS_Y Element 값을 직접 수정
        >
        ```Xml
        <POS_X>419.4</POS_X>
        <POS_Y>534.35</POS_Y>
        ```

    * AlarmInfoViewer Edit 기능 활성화

    [![Video Label]]
    (https://www.youtube.com/watch?v=bnaUTZk4SoM)

    >![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/Edit1.jpg "Window 화면을 늘리면 Edit Mode 버튼이 보임")
    ![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/Edit2.jpg "Edit Mode 버튼을 클릭하면 Pos->List 와 Save 버튼이 보임")
    ![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/Edit3.jpg "Mouse 및 Touch로 Pointer 위치 변경 후  Pos->List 클릭 ! 후 Save 버튼 클릭 !")
<br>
<br>

### Alarm 관련 Cause / Management 관련 다국어 지원
 > Cause 와 Management에 관해서만 지원(Alarm 발생 위치 Image Load 참고)



### MFC에서 Alarm Screen 없을 시 UI 대체
> Interface 방법에 의해 MFC에서 Alarm Happen 및 Reset 처리
    ![title](https://github.com/EuphoriaLUV/AlarmInfoViewer/blob/master/Image/AlarmHappen.jpg "Alarm Happen")


### File Remover
* File Path
> C:\Program Files\ISoft\Common\AlarmInfoViewer\RemoverCfg.xml

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<Remover>
	<DiffDays>90</DiffDays>
	<Paths>
		<Path>D:\XXXX\Setting\Backup\</Path>
		<Path>D:\XXXX\Log\</Path>
        <Path>D:\XXXX\Data\Backup\</Path>

        ......

	</Paths>
</Remover>
```
> Path Element 들의 Value 값 경로의 하위 Directory에서 DiffDays(ex. 90일) 이전의 File 들을 Background에서 삭제시킴



### Access Solution
