---
title: "aaaMultiple 입력 파일과 프리미엄 인코더-Azure 사용 하 여 구성 요소 속성 | Microsoft Docs"
description: "이 방법을 toouse setRuntimeProperties toouse 여러 입력 파일 및 사용자 지정 데이터 toohello 미디어 인코더 프리미엄 워크플로 미디어 프로세서 전달 설명 합니다."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>프리미엄 인코더로 여러 입력 파일 및 구성 요소 속성 사용
## <a name="overview"></a>개요
클립 목록 XML 콘텐츠 지정 시나리오가 toocustomize 구성 요소 속성을 할 수 있습니다 또는 hello로 작업을 제출 하면 여러 개의 입력된 파일을 보낼 **미디어 인코더 프리미엄 워크플로** 미디어 프로세서. 일부 사례:

* 텍스트 비디오에 오버레이 및 입력된의 각 비디오에 대 한 런타임 시 hello 텍스트 값 (예를 들어 현재 날짜 hello)를 설정 합니다.
* Hello 클립 목록 XML (toospecify 하나 또는 여러 소스 파일, 유무에 관계 없이 잘라내기 등.)를 사용자 지정 합니다.
* Hello 비디오 인코딩 되는 동안 hello 입력된 비디오에 로고 이미지를 중첩 합니다.
* 다중 오디오 언어 인코딩

toolet hello **미디어 인코더 프리미엄 워크플로** hello 작업을 만들거나 여러 개의 입력된 파일을 보낼 때 hello 워크플로에서 일부 속성을 변경 하려는, 포함 하는 구성 문자열 toouse 있는 알고  **setRuntimeProperties** 및/또는 **transcodeSource**합니다. 이 항목에서는 설명 어떻게 toouse 해당 합니다.

## <a name="configuration-string-syntax"></a>구성 문자열 구문
hello 구성 문자열 tooset hello 인코딩 작업에에서는 다음과 같은 XML 문서를 사용 합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

hello 다음은 hello C# 코드 hello XML 구성 파일에서 읽을 수 있는로 업데이트 하 고 작업 toohello 작업 전달 hello 비디오 파일 이름:

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>구성 요소 속성 사용자 지정
### <a name="property-with-a-simple-value"></a>간단한 값이 있는 속성
일부 경우에는 유용한 toocustomize toobe 미디어 인코더 프리미엄 워크플로 실행을 이동 하는 hello 워크플로 파일과 함께 구성 요소 속성

비디오에는 워크플로 그 오버레이 텍스트 설계 hello 텍스트 (예를 들어 hello 현재 날짜) 런타임 시 toobe 집합 해야 한다고 가정 합니다. 이렇게 하려면 보내는 hello 텍스트 toobe hello 인코딩 작업에서에서 hello hello 오버레이 구성 요소의 hello 텍스트 속성에 대 한 새 값으로 설정 합니다. 이 메커니즘 toochange 구성 요소의 다른 속성 (예: hello 위치 또는 hello 오버레이의 색, hello 비트 전송률 hello AVC 인코더, 등입니다.) hello 워크플로에서 사용할 수 있습니다.

**setRuntimeProperties** 사용 되는 toooverride hello 워크플로의 hello 구성 요소의 속성입니다.

예제:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>XML 값이 있는 속성
tooset 16는 XML 값을 사용 하는 속성을 사용 하 여 캡슐화 `<![CDATA[ and ]]>`합니다.

예제:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> Tooput 캐리지 하지 직후 반환 `<![CDATA[`합니다.

### <a name="propertypath-value"></a>propertyPath 값
Hello propertyPath 된 hello 이전 예제에서 "/ 미디어 파일 입력/파일 이름" 또는 "/ inactiveTimeout" 또는 "clipListXml"입니다.
이것이, 일반적으로 hello 속성의 hello 이름을 차례로 hello 구성 요소의 hello 이름입니다. hello 경로 수준을 가질 수 있습니다 더 많거나 적은, like "/ primarySourceFile" (hello 속성에 있으므로 hello 워크플로 루트 hello) 또는 "비디오 / 처리/그래픽 오버레이/불투명도" (오버레이 hello 그룹 이므로).    

toocheck hello 경로 및 속성 이름, 각 속성 옆에 바로 사용 하 여 hello 실행 단추입니다. 이 동작 버튼을 클릭하고 **편집**을 선택합니다. 이 작업은 표시 하면 hello 실제 hello 속성 및 그 위에 즉시 이름, 네임 스페이스 hello 합니다.

![작업/편집](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![속성](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>여러 입력 파일
각 작업 toohello를 제출 하면 **미디어 인코더 프리미엄 워크플로** 두 개의 자산 필요:

* hello 먼저 하나는 *워크플로 자산* 워크플로 파일이 들어 있는입니다. Hello를 사용 하 여 워크플로 파일을 디자인할 수 [워크플로 디자이너](media-services-workflow-designer.md)합니다.
* hello 다른 하나는 한 *미디어 자산* tooencode 원하는 hello 미디어 파일을 포함 하 합니다.

여러 미디어 파일 toohello 보내는 경우 **미디어 인코더 프리미엄 워크플로** 인코더 hello 다음 제약 조건을 적용 합니다.

* 동일한 파일에 있어야 하는 모든 hello 미디어 hello *미디어 자산*합니다. 여러 미디어 자산의 사용은 지원되지 않습니다.
* 이 미디어 자산에 hello 주 파일을 설정 해야 합니다 (이상적으로이 hello 인코더 hello 기본 비디오 파일 tooprocess 요청)입니다.
* Hello를 포함 하는 데 필요한 toopass 구성 데이터를은 **setRuntimeProperties** 및/또는 **transcodeSource** 요소 toohello 프로세서.
  * **setRuntimeProperties** 사용 되는 toooverride hello filename 속성 또는 다른 속성 hello 워크플로의 hello 구성 요소에 있습니다.
  * **transcodeSource** 는 사용 되는 toospecify hello 클립 목록 XML 콘텐츠입니다.

Hello 워크플로에서 연결:

* 하나 또는 여러 미디어 파일 입력 구성 요소를 사용 하는 경우 및 toouse 계획 **setRuntimeProperties** toospecify 파일 이름을 hello 다음 hello 주 파일 구성 요소 pin toothem 연결 하지 않습니다. 미디어 파일 입력은 hello hello 주 파일 개체와 연결 되지 있는지 확인 합니다.
* 원할 경우 toouse 클립 목록 XML 및 미디어 원본 구성 요소를 다음 모두 함께 연결할 수 있습니다.

![기본 소스 파일 tooMedia 파일 입력에서에서 연결 없음](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*SetRuntimeProperties tooset hello filename 속성을 사용 하 여 hello 주 파일 tooMedia 파일 입력 구성 요소에서에서 연결 되지 않습니다.*

![클립 목록 XML tooClip 목록 소스에서 연결](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*클립 목록 XML tooMedia 소스 연결 수 있으며 transcodeSource를 사용할 수 있습니다.*

### <a name="clip-list-xml-customization"></a>클립 목록 XML 사용자 지정
사용 하 여 런타임 시 hello 워크플로에서 hello 클립 목록 XML을 지정할 수 있습니다 **transcodeSource** hello 구성의 XML 문자열입니다. 그러려면 hello 클립 목록 XML pin 연결 toobe toohello 미디어의에서 원본 구성 요소 hello 워크플로 합니다.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Toospecify /primarySourceFile toouse 'Expressions'를 사용 하 여이 속성 tooname hello 출력 파일을 원하는 경우 속성으로 hello 클립 목록 XML을 전달 하는 것이 좋습니다 *후* hello /primarySourceFile 속성, tooavoid hello 있으면 클립 목록 hello /primarySourceFile 설정으로 재정의 됩니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

추가 프레임 정확한 트리밍 사용:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>예제 1: hello 비디오 위에 이미지 오버레이

### <a name="presentation"></a>프레젠테이션
Hello 비디오 인코딩 되는 동안 toooverlay 원하는 예 hello 입력된 비디오에 로고 이미지를 고려 합니다. 이 예제에서는 hello 입력된 비디오가 "Microsoft_HoloLens_Possibilities_816p24.mp4" 이름이 고 hello 로고 "logo.png" 라고 합니다. Hello 다음 단계를 수행 해야 합니다.

* Hello 워크플로 파일로 워크플로 자산 만들기 (다음 예제는 hello 참조).
* 두 개의 파일을 포함 하는 미디어 자산을 만듭니다: MyInputVideo.mp4 주 파일과 MyLogo.png hello으로 합니다.
* 작업 toohello 미디어 인코더 프리미엄 워크플로 미디어 입력 위의 hello 프로세서 자산 보내고 다음 구성 문자열 hello를 지정 합니다.

구성:

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Hello 위의 예에서 hello 비디오 파일의 hello 이름 toohello 미디어 파일 입력 구성 요소와 hello primarySourceFile 속성을 전송 됩니다. hello 로고 파일의 이름은 hello tooanother는 연결 된 toohello 그래픽 오버레이 구성 요소 미디어 파일 입력 전송 됩니다.

> [!NOTE]
> hello 비디오 파일 이름은 toohello primarySourceFile 속성을 전송 됩니다. 이러한 이유로 hello toouse hello 올바른 출력 파일 이름 예를 들어 식을 사용 하 여 구축 하기 위한 hello 워크플로에서이 속성은 합니다.

### <a name="step-by-step-workflow-creation"></a>단계별 워크플로 만들기
다음 두 개의 파일을 입력으로 사용 하는 워크플로 hello 단계 toocreate를은: 비디오 및 이미지입니다. 것 비디오 hello 위에 hello 이미지를 오버레이 사용 합니다.

**워크플로 디자이너**를 열고 **파일** > **새 작업 영역** > **청사진 트랜스코딩**을 선택합니다.

새 워크플로 hello 세 개의 요소를 보여 줍니다.

* 기본 원본 파일
* 클립 목록 XML
* 출력 파일/자산  

![새 인코딩 워크플로](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*새 인코딩 워크플로*

순서 tooaccept hello 입력된 미디어 파일 미디어 파일 입력 구성 요소를 추가 하 여 시작 합니다. 구성 요소 toohello 워크플로 tooadd hello 리포지토리 검색 상자에 검색할 끌어서 hello 디자이너 창에 놓을 hello 원하는 항목 합니다.

Hello 비디오 파일 toobe 워크플로 디자인에 사용 되는 다음을 추가 합니다. 따라서 toodo 워크플로 디자이너에서 hello 배경 창을 클릭 하 고 hello 오른쪽 속성 창에서 hello 소스 파일을 기본 속성을 찾습니다. Hello 폴더 아이콘을 클릭 하 고 hello 적절 한 비디오 파일을 선택 합니다.

![기본 파일 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*기본 파일 원본*

다음으로 hello 미디어 파일 입력 구성 요소에서 hello 비디오 파일을 지정 합니다.   

![미디어 파일 입력 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*미디어 파일 입력 원본*

이 도구를 실행 하는 즉시 hello 미디어 파일 입력 구성 요소가 hello 파일을 검사를 업데이트 하 고 해당 출력 핀 tooreflect hello 파일을 검사 하는 것을 채우는 됨.

hello 다음 단계에는 "데이터 형식 업데이트 프로그램 비디오" toospecify hello 색 공간 tooRec.709 tooadd입니다. 추가 "비디오 형식 변환기를" tooData 레이아웃/레이아웃 형식을 설정 된 구성 가능한 평면 = 합니다. 그러면 hello 오버레이 구성 요소의 원본으로 수행할 수 있는 hello 비디오 스트림 tooa 형식을 변환 됩니다.

![비디오 데이터 형식 업데이터 및 형식 변환기](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*비디오 데이터 형식 업데이터 및 형식 변환기*

![레이아웃 형식 = 구성 가능한 평면](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*구성 가능한 평면의 레이아웃 형식*

다음으로 비디오 오버레이 구성 요소를 추가 하 고 hello (압축 되지 않은) 비디오 pin toohello (압축 되지 않은) 비디오의 pin hello 미디어 파일 입력을 연결 합니다.

다른 미디어 파일 입력 (tooload hello 로고 파일)를이 구성 요소에서 클릭 하 고 너무 이름 바꾸기 "미디어 파일 입력 로고" 및 hello 파일 속성에 이미지 (예:.png 파일)를 선택 합니다. Hello 오버레이의 hello 압축 되지 않은 이미지 핀 toohello 압축 되지 않은 이미지 핀을 연결 합니다.

![오버레이 구성 요소 및 이미지 파일 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*오버레이 구성 요소 및 이미지 파일 원본*

Hello 비디오에 hello 로고의 toomodify hello 위치를 원하는 경우 (예를 들어 tooposition 경우가 오프 hello 상위 10%에서의 왼쪽 아래 hello 비디오), clear hello "수동 입력" 확인란 합니다. 미디어 파일 입력 tooprovide hello 로고 파일 toohello 오버레이 구성 요소를 사용 중 이므로이 수행할 수 있습니다.

![오버레이 위치](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*오버레이 위치*

tooencode 비디오 스트림 tooH.264 hello, hello AVC 비디오 인코더 및 AAC 인코더 구성 요소 toohello 디자이너 화면을 추가 합니다. Hello 핀을 연결 합니다.
Hello AAC 인코더를 설정 하 고 오디오 형식 변환/사전 설정을 선택: 2.0 (L, R).

![오디오 및 비디오 인코더](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*오디오 및 비디오 인코더*

이제 hello 추가 **ISO mpeg-4 멀티플렉서** 및 **파일 출력** 구성 요소와 같이 hello 핀을 연결 합니다.

![MP4 멀티플렉서 및 파일 출력](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*MP4 멀티플렉서 및 파일 출력*

Hello 출력 파일에 대 한 tooset hello 이름이 필요 합니다. Hello 클릭 **파일 출력** hello 파일에 대 한 구성 요소 및 편집 hello 식:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![파일 출력 이름](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*파일 출력 이름*

Hello 워크플로 실행할 수 있습니다 올바르게 실행 toocheck 로컬로 합니다.

완료되면 Azure 미디어 서비스에서 실행할 수 있습니다.

먼저, Azure 미디어 서비스에서 자산에 두 개의 파일을 준비: hello 비디오 파일과 hello 로고입니다. Hello.NET 또는 REST API를 사용 하 여이 수행할 수 있습니다. Hello Azure 포털을 사용 하 여이 수행할 수 또는 [Azure 미디어 서비스 탐색기](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

이 자습서에서는 어떻게 AMSE 사용 하 여 toomanage 자산입니다. 두 가지 방법으로 tooadd 파일 tooan 자산 가지가 있습니다.

* 로컬 폴더를 만들고, hello 두 파일을 복사 하 고 끌어서 놓기 hello 폴더 toohello **자산** 탭 합니다.
* Hello 비디오 파일을 자산으로 업로드, hello 자산 정보를 표시, toohello 파일 탭으로 이동 및 추가 파일 (로고)을 업로드 합니다.

> [!NOTE]
> Hello 자산 (hello 주 비디오 파일)에 있는지 tooset 주 파일을 확인 합니다.

![AMSE에서 자산 파일](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*AMSE에서 자산 파일*

Hello 자산을 선택 하 고 선택 tooencode 프리미엄 인코더와 합니다. Hello 워크플로 업로드 하 고 선택 합니다.

Hello 단추 toopass 데이터 toohello 프로세서를 클릭 하 고 hello 다음과 같은 XML tooset hello 런타임 속성을 추가 합니다.

![AMSE에서 프리미엄 인코더](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*AMSE에서 프리미엄 인코더*

그런 다음 hello를 다음 XML 데이터를 붙여 넣습니다. 미디어 파일 입력 hello와 primarySourceFile hello 비디오 파일의 toospecify hello 이름이 필요 합니다. 너무 hello 로고에 대 한 hello 파일 이름의 hello 이름을 지정 합니다.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

.NET SDK toocreate hello를 사용 하 여 hello 작업을 실행 하는 경우이 XML 데이터에 toobe hello 구성 문자열 변수로 전달 합니다.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Hello 작업이 완료 되 면 hello 오버레이 표시 하는 자산 hello에 hello MP4 파일 출력!

![Hello 비디오에 오버레이](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Hello 비디오에 오버레이*

샘플 워크플로 hello를 다운로드할 수 있습니다 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/)합니다.

## <a name="example-2--multiple-audio-language-encoding"></a>예 2: 다중 오디오 언어 인코딩

다중 오디오 언어 인코딩 워크플로의 예는 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding)에서 제공합니다.

이 폴더는 MXF 파일 tooa 다중 MP4 파일 자산 여러 오디오 트랙을 사용 하는 tooencode 될 수 있는 샘플 워크플로가 포함 되어 있습니다.

이 워크플로 hello MXF 파일에 특정 오디오 트랙; 가정 hello 추가 오디오 트랙 (WAV 또는 MP4...) 별도 오디오 파일 형식으로 전달 되어야 합니다.

tooencode, 다음이 단계를 수행 하십시오.

* 오디오 파일 (0 too18 오디오 파일) hello MXF 파일 및 hello와 미디어 서비스 자산을 만듭니다.
* 해당 hello MXF 파일을 주 파일로 설정 되어 있는지 확인 합니다.
* 작업과 hello 프리미엄 워크플로 인코더 프로세서를 사용 하 여 작업을 만듭니다. (MultiMP4-1080p-19audio-v1.workflow)를 제공 하는 hello 워크플로 사용 합니다.
* Hello setruntime.xml 데이터 toohello 작업 (Azure 미디어 서비스 탐색기를 사용 하 여 hello "xml 데이터 toohello 워크플로 pass" 단추 사용) 하는 경우에 전달 합니다.
  * Hello XML 데이터 toospecify hello 올바른 파일 이름 및 언어 태그를 업데이트 하십시오.
  * hello 워크플로에 오디오 1 tooAudio 18 라는 오디오 구성 요소는 있습니다.
  * RFC5646은 hello 언어 태그에 지원 됩니다.

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* hello 인코딩된 자산 다중 언어 오디오 트랙 있고 이러한 트랙을 Azure 미디어 플레이어에서 선택할 수 없습니다.

## <a name="see-also"></a>참고 항목
* [Azure 미디어 서비스의 프리미엄 인코딩 소개](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [어떻게 toouse Azure 미디어 서비스에서 프리미엄 인코딩](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Azure 미디어 서비스로 주문형 콘텐츠 인코딩](media-services-encode-asset.md#media-encoder-premium-workflow)
* [미디어 인코더 Premium 워크플로 형식 및 코덱](media-services-premium-workflow-encoder-formats.md)
* [샘플 워크플로 파일](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Azure 미디어 서비스 탐색기 도구](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
