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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="40532-103">프리미엄 인코더로 여러 입력 파일 및 구성 요소 속성 사용</span><span class="sxs-lookup"><span data-stu-id="40532-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="40532-104">개요</span><span class="sxs-lookup"><span data-stu-id="40532-104">Overview</span></span>
<span data-ttu-id="40532-105">클립 목록 XML 콘텐츠 지정 시나리오가 toocustomize 구성 요소 속성을 할 수 있습니다 또는 hello로 작업을 제출 하면 여러 개의 입력된 파일을 보낼 **미디어 인코더 프리미엄 워크플로** 미디어 프로세서.</span><span class="sxs-lookup"><span data-stu-id="40532-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="40532-106">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="40532-106">Some examples are:</span></span>

* <span data-ttu-id="40532-107">텍스트 비디오에 오버레이 및 입력된의 각 비디오에 대 한 런타임 시 hello 텍스트 값 (예를 들어 현재 날짜 hello)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="40532-108">Hello 클립 목록 XML (toospecify 하나 또는 여러 소스 파일, 유무에 관계 없이 잘라내기 등.)를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="40532-109">Hello 비디오 인코딩 되는 동안 hello 입력된 비디오에 로고 이미지를 중첩 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="40532-110">다중 오디오 언어 인코딩</span><span class="sxs-lookup"><span data-stu-id="40532-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="40532-111">toolet hello **미디어 인코더 프리미엄 워크플로** hello 작업을 만들거나 여러 개의 입력된 파일을 보낼 때 hello 워크플로에서 일부 속성을 변경 하려는, 포함 하는 구성 문자열 toouse 있는 알고  **setRuntimeProperties** 및/또는 **transcodeSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="40532-112">이 항목에서는 설명 어떻게 toouse 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="40532-113">구성 문자열 구문</span><span class="sxs-lookup"><span data-stu-id="40532-113">Configuration string syntax</span></span>
<span data-ttu-id="40532-114">hello 구성 문자열 tooset hello 인코딩 작업에에서는 다음과 같은 XML 문서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="40532-115">hello 다음은 hello C# 코드 hello XML 구성 파일에서 읽을 수 있는로 업데이트 하 고 작업 toohello 작업 전달 hello 비디오 파일 이름:</span><span class="sxs-lookup"><span data-stu-id="40532-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

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

## <a name="customizing-component-properties"></a><span data-ttu-id="40532-116">구성 요소 속성 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="40532-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="40532-117">간단한 값이 있는 속성</span><span class="sxs-lookup"><span data-stu-id="40532-117">Property with a simple value</span></span>
<span data-ttu-id="40532-118">일부 경우에는 유용한 toocustomize toobe 미디어 인코더 프리미엄 워크플로 실행을 이동 하는 hello 워크플로 파일과 함께 구성 요소 속성</span><span class="sxs-lookup"><span data-stu-id="40532-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="40532-119">비디오에는 워크플로 그 오버레이 텍스트 설계 hello 텍스트 (예를 들어 hello 현재 날짜) 런타임 시 toobe 집합 해야 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="40532-120">이렇게 하려면 보내는 hello 텍스트 toobe hello 인코딩 작업에서에서 hello hello 오버레이 구성 요소의 hello 텍스트 속성에 대 한 새 값으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="40532-121">이 메커니즘 toochange 구성 요소의 다른 속성 (예: hello 위치 또는 hello 오버레이의 색, hello 비트 전송률 hello AVC 인코더, 등입니다.) hello 워크플로에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="40532-122">**setRuntimeProperties** 사용 되는 toooverride hello 워크플로의 hello 구성 요소의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="40532-123">예제:</span><span class="sxs-lookup"><span data-stu-id="40532-123">Example:</span></span>

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

### <a name="property-with-an-xml-value"></a><span data-ttu-id="40532-124">XML 값이 있는 속성</span><span class="sxs-lookup"><span data-stu-id="40532-124">Property with an XML value</span></span>
<span data-ttu-id="40532-125">tooset 16는 XML 값을 사용 하는 속성을 사용 하 여 캡슐화 `<![CDATA[ and ]]>`합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="40532-126">예제:</span><span class="sxs-lookup"><span data-stu-id="40532-126">Example:</span></span>

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
> <span data-ttu-id="40532-127">Tooput 캐리지 하지 직후 반환 `<![CDATA[`합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="40532-128">propertyPath 값</span><span class="sxs-lookup"><span data-stu-id="40532-128">propertyPath value</span></span>
<span data-ttu-id="40532-129">Hello propertyPath 된 hello 이전 예제에서 "/ 미디어 파일 입력/파일 이름" 또는 "/ inactiveTimeout" 또는 "clipListXml"입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="40532-130">이것이, 일반적으로 hello 속성의 hello 이름을 차례로 hello 구성 요소의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="40532-131">hello 경로 수준을 가질 수 있습니다 더 많거나 적은, like "/ primarySourceFile" (hello 속성에 있으므로 hello 워크플로 루트 hello) 또는 "비디오 / 처리/그래픽 오버레이/불투명도" (오버레이 hello 그룹 이므로).</span><span class="sxs-lookup"><span data-stu-id="40532-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="40532-132">toocheck hello 경로 및 속성 이름, 각 속성 옆에 바로 사용 하 여 hello 실행 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="40532-133">이 동작 버튼을 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="40532-134">이 작업은 표시 하면 hello 실제 hello 속성 및 그 위에 즉시 이름, 네임 스페이스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![작업/편집](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![속성](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="40532-137">여러 입력 파일</span><span class="sxs-lookup"><span data-stu-id="40532-137">Multiple input files</span></span>
<span data-ttu-id="40532-138">각 작업 toohello를 제출 하면 **미디어 인코더 프리미엄 워크플로** 두 개의 자산 필요:</span><span class="sxs-lookup"><span data-stu-id="40532-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="40532-139">hello 먼저 하나는 *워크플로 자산* 워크플로 파일이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="40532-140">Hello를 사용 하 여 워크플로 파일을 디자인할 수 [워크플로 디자이너](media-services-workflow-designer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="40532-141">hello 다른 하나는 한 *미디어 자산* tooencode 원하는 hello 미디어 파일을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="40532-142">여러 미디어 파일 toohello 보내는 경우 **미디어 인코더 프리미엄 워크플로** 인코더 hello 다음 제약 조건을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="40532-143">동일한 파일에 있어야 하는 모든 hello 미디어 hello *미디어 자산*합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="40532-144">여러 미디어 자산의 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="40532-145">이 미디어 자산에 hello 주 파일을 설정 해야 합니다 (이상적으로이 hello 인코더 hello 기본 비디오 파일 tooprocess 요청)입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="40532-146">Hello를 포함 하는 데 필요한 toopass 구성 데이터를은 **setRuntimeProperties** 및/또는 **transcodeSource** 요소 toohello 프로세서.</span><span class="sxs-lookup"><span data-stu-id="40532-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="40532-147">**setRuntimeProperties** 사용 되는 toooverride hello filename 속성 또는 다른 속성 hello 워크플로의 hello 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="40532-148">**transcodeSource** 는 사용 되는 toospecify hello 클립 목록 XML 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="40532-149">Hello 워크플로에서 연결:</span><span class="sxs-lookup"><span data-stu-id="40532-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="40532-150">하나 또는 여러 미디어 파일 입력 구성 요소를 사용 하는 경우 및 toouse 계획 **setRuntimeProperties** toospecify 파일 이름을 hello 다음 hello 주 파일 구성 요소 pin toothem 연결 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="40532-151">미디어 파일 입력은 hello hello 주 파일 개체와 연결 되지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="40532-152">원할 경우 toouse 클립 목록 XML 및 미디어 원본 구성 요소를 다음 모두 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![기본 소스 파일 tooMedia 파일 입력에서에서 연결 없음](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="40532-154">*SetRuntimeProperties tooset hello filename 속성을 사용 하 여 hello 주 파일 tooMedia 파일 입력 구성 요소에서에서 연결 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="40532-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![클립 목록 XML tooClip 목록 소스에서 연결](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="40532-156">*클립 목록 XML tooMedia 소스 연결 수 있으며 transcodeSource를 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="40532-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="40532-157">클립 목록 XML 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="40532-157">Clip List XML customization</span></span>
<span data-ttu-id="40532-158">사용 하 여 런타임 시 hello 워크플로에서 hello 클립 목록 XML을 지정할 수 있습니다 **transcodeSource** hello 구성의 XML 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="40532-159">그러려면 hello 클립 목록 XML pin 연결 toobe toohello 미디어의에서 원본 구성 요소 hello 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

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

<span data-ttu-id="40532-160">Toospecify /primarySourceFile toouse 'Expressions'를 사용 하 여이 속성 tooname hello 출력 파일을 원하는 경우 속성으로 hello 클립 목록 XML을 전달 하는 것이 좋습니다 *후* hello /primarySourceFile 속성, tooavoid hello 있으면 클립 목록 hello /primarySourceFile 설정으로 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40532-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

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

<span data-ttu-id="40532-161">추가 프레임 정확한 트리밍 사용:</span><span class="sxs-lookup"><span data-stu-id="40532-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="40532-162">예제 1: hello 비디오 위에 이미지 오버레이</span><span class="sxs-lookup"><span data-stu-id="40532-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="40532-163">프레젠테이션</span><span class="sxs-lookup"><span data-stu-id="40532-163">Presentation</span></span>
<span data-ttu-id="40532-164">Hello 비디오 인코딩 되는 동안 toooverlay 원하는 예 hello 입력된 비디오에 로고 이미지를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="40532-165">이 예제에서는 hello 입력된 비디오가 "Microsoft_HoloLens_Possibilities_816p24.mp4" 이름이 고 hello 로고 "logo.png" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="40532-166">Hello 다음 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="40532-167">Hello 워크플로 파일로 워크플로 자산 만들기 (다음 예제는 hello 참조).</span><span class="sxs-lookup"><span data-stu-id="40532-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="40532-168">두 개의 파일을 포함 하는 미디어 자산을 만듭니다: MyInputVideo.mp4 주 파일과 MyLogo.png hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="40532-169">작업 toohello 미디어 인코더 프리미엄 워크플로 미디어 입력 위의 hello 프로세서 자산 보내고 다음 구성 문자열 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="40532-170">구성:</span><span class="sxs-lookup"><span data-stu-id="40532-170">Configuration:</span></span>

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

<span data-ttu-id="40532-171">Hello 위의 예에서 hello 비디오 파일의 hello 이름 toohello 미디어 파일 입력 구성 요소와 hello primarySourceFile 속성을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40532-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="40532-172">hello 로고 파일의 이름은 hello tooanother는 연결 된 toohello 그래픽 오버레이 구성 요소 미디어 파일 입력 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40532-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="40532-173">hello 비디오 파일 이름은 toohello primarySourceFile 속성을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40532-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="40532-174">이러한 이유로 hello toouse hello 올바른 출력 파일 이름 예를 들어 식을 사용 하 여 구축 하기 위한 hello 워크플로에서이 속성은 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="40532-175">단계별 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="40532-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="40532-176">다음 두 개의 파일을 입력으로 사용 하는 워크플로 hello 단계 toocreate를은: 비디오 및 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="40532-177">것 비디오 hello 위에 hello 이미지를 오버레이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="40532-178">**워크플로 디자이너**를 열고 **파일** > **새 작업 영역** > **청사진 트랜스코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="40532-179">새 워크플로 hello 세 개의 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40532-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="40532-180">기본 원본 파일</span><span class="sxs-lookup"><span data-stu-id="40532-180">Primary Source File</span></span>
* <span data-ttu-id="40532-181">클립 목록 XML</span><span class="sxs-lookup"><span data-stu-id="40532-181">Clip List XML</span></span>
* <span data-ttu-id="40532-182">출력 파일/자산</span><span class="sxs-lookup"><span data-stu-id="40532-182">Output File/Asset</span></span>  

![새 인코딩 워크플로](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="40532-184">*새 인코딩 워크플로*</span><span class="sxs-lookup"><span data-stu-id="40532-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="40532-185">순서 tooaccept hello 입력된 미디어 파일 미디어 파일 입력 구성 요소를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="40532-186">구성 요소 toohello 워크플로 tooadd hello 리포지토리 검색 상자에 검색할 끌어서 hello 디자이너 창에 놓을 hello 원하는 항목 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="40532-187">Hello 비디오 파일 toobe 워크플로 디자인에 사용 되는 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="40532-188">따라서 toodo 워크플로 디자이너에서 hello 배경 창을 클릭 하 고 hello 오른쪽 속성 창에서 hello 소스 파일을 기본 속성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="40532-189">Hello 폴더 아이콘을 클릭 하 고 hello 적절 한 비디오 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-189">Click hello folder icon and select hello appropriate video file.</span></span>

![기본 파일 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="40532-191">*기본 파일 원본*</span><span class="sxs-lookup"><span data-stu-id="40532-191">*Primary File Source*</span></span>

<span data-ttu-id="40532-192">다음으로 hello 미디어 파일 입력 구성 요소에서 hello 비디오 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![미디어 파일 입력 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="40532-194">*미디어 파일 입력 원본*</span><span class="sxs-lookup"><span data-stu-id="40532-194">*Media File Input Source*</span></span>

<span data-ttu-id="40532-195">이 도구를 실행 하는 즉시 hello 미디어 파일 입력 구성 요소가 hello 파일을 검사를 업데이트 하 고 해당 출력 핀 tooreflect hello 파일을 검사 하는 것을 채우는 됨.</span><span class="sxs-lookup"><span data-stu-id="40532-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="40532-196">hello 다음 단계에는 "데이터 형식 업데이트 프로그램 비디오" toospecify hello 색 공간 tooRec.709 tooadd입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="40532-197">추가 "비디오 형식 변환기를" tooData 레이아웃/레이아웃 형식을 설정 된 구성 가능한 평면 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="40532-198">그러면 hello 오버레이 구성 요소의 원본으로 수행할 수 있는 hello 비디오 스트림 tooa 형식을 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40532-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![비디오 데이터 형식 업데이터 및 형식 변환기](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="40532-200">*비디오 데이터 형식 업데이터 및 형식 변환기*</span><span class="sxs-lookup"><span data-stu-id="40532-200">*Video Data Type Updater and Format Converter*</span></span>

![레이아웃 형식 = 구성 가능한 평면](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="40532-202">*구성 가능한 평면의 레이아웃 형식*</span><span class="sxs-lookup"><span data-stu-id="40532-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="40532-203">다음으로 비디오 오버레이 구성 요소를 추가 하 고 hello (압축 되지 않은) 비디오 pin toohello (압축 되지 않은) 비디오의 pin hello 미디어 파일 입력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="40532-204">다른 미디어 파일 입력 (tooload hello 로고 파일)를이 구성 요소에서 클릭 하 고 너무 이름 바꾸기 "미디어 파일 입력 로고" 및 hello 파일 속성에 이미지 (예:.png 파일)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="40532-205">Hello 오버레이의 hello 압축 되지 않은 이미지 핀 toohello 압축 되지 않은 이미지 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![오버레이 구성 요소 및 이미지 파일 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="40532-207">*오버레이 구성 요소 및 이미지 파일 원본*</span><span class="sxs-lookup"><span data-stu-id="40532-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="40532-208">Hello 비디오에 hello 로고의 toomodify hello 위치를 원하는 경우 (예를 들어 tooposition 경우가 오프 hello 상위 10%에서의 왼쪽 아래 hello 비디오), clear hello "수동 입력" 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="40532-209">미디어 파일 입력 tooprovide hello 로고 파일 toohello 오버레이 구성 요소를 사용 중 이므로이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![오버레이 위치](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="40532-211">*오버레이 위치*</span><span class="sxs-lookup"><span data-stu-id="40532-211">*Overlay position*</span></span>

<span data-ttu-id="40532-212">tooencode 비디오 스트림 tooH.264 hello, hello AVC 비디오 인코더 및 AAC 인코더 구성 요소 toohello 디자이너 화면을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="40532-213">Hello 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-213">Connect hello pins.</span></span>
<span data-ttu-id="40532-214">Hello AAC 인코더를 설정 하 고 오디오 형식 변환/사전 설정을 선택: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="40532-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![오디오 및 비디오 인코더](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="40532-216">*오디오 및 비디오 인코더*</span><span class="sxs-lookup"><span data-stu-id="40532-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="40532-217">이제 hello 추가 **ISO mpeg-4 멀티플렉서** 및 **파일 출력** 구성 요소와 같이 hello 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![MP4 멀티플렉서 및 파일 출력](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="40532-219">*MP4 멀티플렉서 및 파일 출력*</span><span class="sxs-lookup"><span data-stu-id="40532-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="40532-220">Hello 출력 파일에 대 한 tooset hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="40532-221">Hello 클릭 **파일 출력** hello 파일에 대 한 구성 요소 및 편집 hello 식:</span><span class="sxs-lookup"><span data-stu-id="40532-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![파일 출력 이름](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="40532-223">*파일 출력 이름*</span><span class="sxs-lookup"><span data-stu-id="40532-223">*File output name*</span></span>

<span data-ttu-id="40532-224">Hello 워크플로 실행할 수 있습니다 올바르게 실행 toocheck 로컬로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="40532-225">완료되면 Azure 미디어 서비스에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="40532-226">먼저, Azure 미디어 서비스에서 자산에 두 개의 파일을 준비: hello 비디오 파일과 hello 로고입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="40532-227">Hello.NET 또는 REST API를 사용 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="40532-228">Hello Azure 포털을 사용 하 여이 수행할 수 또는 [Azure 미디어 서비스 탐색기](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="40532-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="40532-229">이 자습서에서는 어떻게 AMSE 사용 하 여 toomanage 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="40532-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="40532-230">두 가지 방법으로 tooadd 파일 tooan 자산 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="40532-231">로컬 폴더를 만들고, hello 두 파일을 복사 하 고 끌어서 놓기 hello 폴더 toohello **자산** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="40532-232">Hello 비디오 파일을 자산으로 업로드, hello 자산 정보를 표시, toohello 파일 탭으로 이동 및 추가 파일 (로고)을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="40532-233">Hello 자산 (hello 주 비디오 파일)에 있는지 tooset 주 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![AMSE에서 자산 파일](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="40532-235">*AMSE에서 자산 파일*</span><span class="sxs-lookup"><span data-stu-id="40532-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="40532-236">Hello 자산을 선택 하 고 선택 tooencode 프리미엄 인코더와 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="40532-237">Hello 워크플로 업로드 하 고 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="40532-238">Hello 단추 toopass 데이터 toohello 프로세서를 클릭 하 고 hello 다음과 같은 XML tooset hello 런타임 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![AMSE에서 프리미엄 인코더](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="40532-240">*AMSE에서 프리미엄 인코더*</span><span class="sxs-lookup"><span data-stu-id="40532-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="40532-241">그런 다음 hello를 다음 XML 데이터를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="40532-242">미디어 파일 입력 hello와 primarySourceFile hello 비디오 파일의 toospecify hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="40532-243">너무 hello 로고에 대 한 hello 파일 이름의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-243">Specify hello name of hello file name for hello logo too.</span></span>

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

<span data-ttu-id="40532-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="40532-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="40532-246">.NET SDK toocreate hello를 사용 하 여 hello 작업을 실행 하는 경우이 XML 데이터에 toobe hello 구성 문자열 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="40532-247">Hello 작업이 완료 되 면 hello 오버레이 표시 하는 자산 hello에 hello MP4 파일 출력!</span><span class="sxs-lookup"><span data-stu-id="40532-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Hello 비디오에 오버레이](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="40532-249">*Hello 비디오에 오버레이*</span><span class="sxs-lookup"><span data-stu-id="40532-249">*Overlay on hello video*</span></span>

<span data-ttu-id="40532-250">샘플 워크플로 hello를 다운로드할 수 있습니다 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/)합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="40532-251">예 2: 다중 오디오 언어 인코딩</span><span class="sxs-lookup"><span data-stu-id="40532-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="40532-252">다중 오디오 언어 인코딩 워크플로의 예는 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding)에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="40532-253">이 폴더는 MXF 파일 tooa 다중 MP4 파일 자산 여러 오디오 트랙을 사용 하는 tooencode 될 수 있는 샘플 워크플로가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="40532-254">이 워크플로 hello MXF 파일에 특정 오디오 트랙; 가정 hello 추가 오디오 트랙 (WAV 또는 MP4...) 별도 오디오 파일 형식으로 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="40532-255">tooencode, 다음이 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="40532-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="40532-256">오디오 파일 (0 too18 오디오 파일) hello MXF 파일 및 hello와 미디어 서비스 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40532-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="40532-257">해당 hello MXF 파일을 주 파일로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="40532-258">작업과 hello 프리미엄 워크플로 인코더 프로세서를 사용 하 여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40532-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="40532-259">(MultiMP4-1080p-19audio-v1.workflow)를 제공 하는 hello 워크플로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="40532-260">Hello setruntime.xml 데이터 toohello 작업 (Azure 미디어 서비스 탐색기를 사용 하 여 hello "xml 데이터 toohello 워크플로 pass" 단추 사용) 하는 경우에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="40532-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="40532-261">Hello XML 데이터 toospecify hello 올바른 파일 이름 및 언어 태그를 업데이트 하십시오.</span><span class="sxs-lookup"><span data-stu-id="40532-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="40532-262">hello 워크플로에 오디오 1 tooAudio 18 라는 오디오 구성 요소는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="40532-263">RFC5646은 hello 언어 태그에 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40532-263">RFC5646 is supported for hello language tag.</span></span>

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

* <span data-ttu-id="40532-264">hello 인코딩된 자산 다중 언어 오디오 트랙 있고 이러한 트랙을 Azure 미디어 플레이어에서 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40532-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="40532-265">참고 항목</span><span class="sxs-lookup"><span data-stu-id="40532-265">See also</span></span>
* [<span data-ttu-id="40532-266">Azure 미디어 서비스의 프리미엄 인코딩 소개</span><span class="sxs-lookup"><span data-stu-id="40532-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="40532-267">어떻게 toouse Azure 미디어 서비스에서 프리미엄 인코딩</span><span class="sxs-lookup"><span data-stu-id="40532-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="40532-268">Azure 미디어 서비스로 주문형 콘텐츠 인코딩</span><span class="sxs-lookup"><span data-stu-id="40532-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="40532-269">미디어 인코더 Premium 워크플로 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="40532-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="40532-270">샘플 워크플로 파일</span><span class="sxs-lookup"><span data-stu-id="40532-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="40532-271">Azure 미디어 서비스 탐색기 도구</span><span class="sxs-lookup"><span data-stu-id="40532-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="40532-272">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="40532-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="40532-273">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="40532-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
