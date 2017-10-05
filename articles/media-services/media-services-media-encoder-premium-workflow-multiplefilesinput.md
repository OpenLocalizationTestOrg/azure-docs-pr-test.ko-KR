---
title: "프리미엄 인코더를 통한 여러 입력 파일 및 구성 요소 속성 - Azure | Microsoft 문서"
description: "이 항목에서는 setRuntimeProperties를 사용하여 여러 입력 파일을 사용하고 사용자 지정 데이터를 미디어 인코더 Premium 워크플로 미디어 프로세서에 전달하는 방법을 설명합니다."
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
ms.openlocfilehash: df1ee5089a0af6ffce1431b658843fcb34a66ce5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="c69f8-103">프리미엄 인코더로 여러 입력 파일 및 구성 요소 속성 사용</span><span class="sxs-lookup"><span data-stu-id="c69f8-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="c69f8-104">개요</span><span class="sxs-lookup"><span data-stu-id="c69f8-104">Overview</span></span>
<span data-ttu-id="c69f8-105">**미디어 인코더 프리미엄 워크플로** 미디어 프로세서로 작업을 제출할 때 구성 요소 속성을 사용자 지정하고 클립 목록 XML 콘텐츠를 지정하거나 여러 입력 파일을 전송해야 하는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="c69f8-106">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="c69f8-106">Some examples are:</span></span>

* <span data-ttu-id="c69f8-107">각 입력 비디오에 대해 런타임에(예: 현재 날짜) 비디오 위에 텍스트 오버레이 및 텍스트 값 설정</span><span class="sxs-lookup"><span data-stu-id="c69f8-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="c69f8-108">클립 목록 XML 사용자 지정(잘라내기 등을 사용/사용하지 않고 하나 이상의 소스 파일 지정)</span><span class="sxs-lookup"><span data-stu-id="c69f8-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="c69f8-109">비디오를 인코딩하는 동안 입력 비디오에 로고 이미지 오버레이</span><span class="sxs-lookup"><span data-stu-id="c69f8-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="c69f8-110">다중 오디오 언어 인코딩</span><span class="sxs-lookup"><span data-stu-id="c69f8-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="c69f8-111">작업을 만들거나 여러 입력 파일을 전송할 때 **미디어 인코더 프리미엄 워크플로**에 사용자가 워크플로의 일부 속성을 변경하고 있음을 알리려면 **setRuntimeProperties** 및/또는 **transcodeSource**를 포함하는 구성 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="c69f8-112">이 항목에서는 이를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="c69f8-113">구성 문자열 구문</span><span class="sxs-lookup"><span data-stu-id="c69f8-113">Configuration string syntax</span></span>
<span data-ttu-id="c69f8-114">인코딩 작업에서 설정할 구성 문자열은 다음과 같은 XML 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="c69f8-115">다음은 파일에서 XML 구성을 읽고 적절한 비디오 파일 이름으로 업데이트한 후 해당 작업에 전달하는 C# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="c69f8-116">구성 요소 속성 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c69f8-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="c69f8-117">간단한 값이 있는 속성</span><span class="sxs-lookup"><span data-stu-id="c69f8-117">Property with a simple value</span></span>
<span data-ttu-id="c69f8-118">일부 경우 구성 요소 속성을 미디어 인코더 Premium 워크플로에서 실행할 워크플로 파일과 함께 사용자 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="c69f8-119">비디오에 텍스트를 오버레이하는 워크플로를 지정했고 텍스트(예: 현재 날짜)가 런타임에 설정된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="c69f8-120">인코딩 작업에서 오버레이 구성 요소의 텍스트 속성에 대한 새 값으로 설정할 텍스트를 전송하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="c69f8-121">이 메커니즘을 사용하여 워크플로 구성 요소의 다른 속성(예: 오버레이의 위치 또는 색, AVC 인코더의 비트 전송률 등)을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="c69f8-122">**setRuntimeProperties** 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="c69f8-123">예제:</span><span class="sxs-lookup"><span data-stu-id="c69f8-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="c69f8-124">XML 값이 있는 속성</span><span class="sxs-lookup"><span data-stu-id="c69f8-124">Property with an XML value</span></span>
<span data-ttu-id="c69f8-125">XML 값이 예상되는 속성을 설정하려면 `<![CDATA[ and ]]>`를 사용하여 캡슐화하세요.</span><span class="sxs-lookup"><span data-stu-id="c69f8-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="c69f8-126">예제:</span><span class="sxs-lookup"><span data-stu-id="c69f8-126">Example:</span></span>

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
> <span data-ttu-id="c69f8-127">`<![CDATA[` 바로 뒤에 캐리지 리턴을 두지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c69f8-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="c69f8-128">propertyPath 값</span><span class="sxs-lookup"><span data-stu-id="c69f8-128">propertyPath value</span></span>
<span data-ttu-id="c69f8-129">이전 예제에서 propertyPath는 "/Media File Input/filename", "/inactiveTimeout", "clipListXml"였습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="c69f8-130">일반적으로 구성 요소의 이름과 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="c69f8-131">경로는 "/primarySourceFile"(속성이 워크플로의 루트에 있으므로) 또는 "/Video Processing/Graphic Overlay/Opacity"(오버레이가 그룹에 있으므로)처럼 더 많거나 적은 수준을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="c69f8-132">경로 및 속성 이름을 확인하려면 각 속성 바로 옆의 동작 버튼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="c69f8-133">이 동작 버튼을 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="c69f8-134">그러면 속성의 실제 이름이 네임스페이스 바로 위에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![작업/편집](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![속성](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="c69f8-137">여러 입력 파일</span><span class="sxs-lookup"><span data-stu-id="c69f8-137">Multiple input files</span></span>
<span data-ttu-id="c69f8-138">**미디어 인코더 Premium 워크플로** 에 제출하는 각 작업에는 두 개의 자산이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="c69f8-139">첫 번째 자산은 워크플로 파일을 포함하는 *워크플로 자산* 입니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="c69f8-140">[워크플로 디자이너](media-services-workflow-designer.md)를 사용하여 워크플로 파일을 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="c69f8-141">두 번째 자산은 인코딩할 미디어 파일을 포함하는 *미디어 자산* 입니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="c69f8-142">여러 미디어 파일을 **미디어 인코더 Premium 워크플로** 인코더에 전송하는 경우 다음 제약 조건이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="c69f8-143">모든 미디어 파일이 동일한 *미디어 자산*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="c69f8-144">여러 미디어 자산의 사용은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="c69f8-145">이 미디어 자산에서 기본 파일을 설정해야 합니다(이상적으로 인코더가 처리를 요청하는 기본 비디오 파일).</span><span class="sxs-lookup"><span data-stu-id="c69f8-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="c69f8-146">**setRuntimeProperties** 및/또는 **transcodeSource** 요소를 포함하는 구성 데이터를 프로세서에 전달하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="c69f8-147">**setRuntimeProperties** 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="c69f8-148">**transcodeSource** 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="c69f8-149">워크플로에서 연결:</span><span class="sxs-lookup"><span data-stu-id="c69f8-149">Connections in the workflow:</span></span>

* <span data-ttu-id="c69f8-150">하나 이상의 미디어 파일 입력 구성 요소를 사용하고 파일 이름을 지정하는 데 **setRuntimeProperties** 를 사용할 계획인 경우 여기에 기본 파일 구성 요소 PIN을 연결하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c69f8-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="c69f8-151">기본 파일 개체와 미디어 파일 입력 간에 연결이 없는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c69f8-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="c69f8-152">클립 목록 XML과 하나의 미디어 원본 구성 요소를 사용하려는 경우 둘 다를 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![기본 원본 파일에서 미디어 파일 입력으로 연결 없음](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="c69f8-154">*파일 이름 속성을 설정하기 위해 setRuntimeProperties를 사용하는 경우 기본 파일에서 미디어 파일 입력 구성 요소로 연결이 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="c69f8-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![클립 목록 XML에서 클립 목록 원본으로 연결](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="c69f8-156">*클립 목록 XML을 미디어 원본에 연결하고 transcodeSource를 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="c69f8-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="c69f8-157">클립 목록 XML 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c69f8-157">Clip List XML customization</span></span>
<span data-ttu-id="c69f8-158">구성 문자열 XML에서 **transcodeSource** 를 사용하여 워크플로에서 런타임에 클립 목록 XML을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="c69f8-159">이를 위해서는 클립 목록 XML 핀을 워크플로에서 미디어 원본 구성 요소에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

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

<span data-ttu-id="c69f8-160">'Expressions'를 사용하여 출력 파일의 이름을 지정하는 데 이 속성을 사용하도록 /primarySourceFile을 지정하는 경우, 클립 목록이 /primarySourceFile 설정으로 재정의되지 않도록 클립 목록 XML을 /primarySourceFile 속성 *이후의* 속성으로 전달하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

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

<span data-ttu-id="c69f8-161">추가 프레임 정확한 트리밍 사용:</span><span class="sxs-lookup"><span data-stu-id="c69f8-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="c69f8-162">예 1: 비디오 위에 이미지 오버레이</span><span class="sxs-lookup"><span data-stu-id="c69f8-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="c69f8-163">프레젠테이션</span><span class="sxs-lookup"><span data-stu-id="c69f8-163">Presentation</span></span>
<span data-ttu-id="c69f8-164">비디오를 인코딩하는 동안 로고 이미지를 입력 비디오에 오버레이하는 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="c69f8-165">이 예제에서 입력 비디오의 이름은 "Microsoft_HoloLens_Possibilities_816p24.mp4", 로고 이름은 "logo.png"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="c69f8-166">다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-166">You should perform the following steps:</span></span>

* <span data-ttu-id="c69f8-167">워크플로 파일로 워크플로 자산 만들기(아래 예제 참조)</span><span class="sxs-lookup"><span data-stu-id="c69f8-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="c69f8-168">두 파일(기본 파일로 MyInputVideo.mp4 및 MyLogo.png)을 포함하는 미디어 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="c69f8-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="c69f8-169">위의 입력 자산과 함께 미디어 인코더 Premium 워크플로 미디어 프로세서에 작업 보내기 및 다음 구성 문자열 지정</span><span class="sxs-lookup"><span data-stu-id="c69f8-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="c69f8-170">구성:</span><span class="sxs-lookup"><span data-stu-id="c69f8-170">Configuration:</span></span>

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

<span data-ttu-id="c69f8-171">위 예제에서 비디오 파일의 이름이 미디어 파일 입력 구성 요소 및 primarySourceFile 속성으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="c69f8-172">로고 파일의 이름은 그래픽 오버레이 구성 요소에 연결되어 있는 다른 미디어 파일 입력으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="c69f8-173">비디오 파일 이름은 primarySourceFile 속성에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="c69f8-174">그 이유는 예를 들어 Expressions를 사용하여 올바른 출력 파일 이름을 작성하기 위해 워크플로에서 이 속성을 사용해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="c69f8-175">단계별 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="c69f8-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="c69f8-176">입력으로 두 개의 파일(비디오 및 이미지)을 사용하는 워크플로를 만드는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="c69f8-177">비디오 맨 위에서 이미지를 오버레이합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="c69f8-178">**워크플로 디자이너**를 열고 **파일** > **새 작업 영역** > **청사진 트랜스코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="c69f8-179">새 워크플로는 3개의 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="c69f8-180">기본 원본 파일</span><span class="sxs-lookup"><span data-stu-id="c69f8-180">Primary Source File</span></span>
* <span data-ttu-id="c69f8-181">클립 목록 XML</span><span class="sxs-lookup"><span data-stu-id="c69f8-181">Clip List XML</span></span>
* <span data-ttu-id="c69f8-182">출력 파일/자산</span><span class="sxs-lookup"><span data-stu-id="c69f8-182">Output File/Asset</span></span>  

![새 인코딩 워크플로](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="c69f8-184">*새 인코딩 워크플로*</span><span class="sxs-lookup"><span data-stu-id="c69f8-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="c69f8-185">입력 미디어 파일을 허용하기 위해 미디어 파일 입력 구성 요소를 추가하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="c69f8-186">워크플로에 구성 요소를 추가하려면 리포지토리 검색 상자에서 구성 요소를 찾고 디자이너 창으로 원하는 항목을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="c69f8-187">다음으로, 워크플로 디자인에 사용할 비디오 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="c69f8-188">이렇게 하려면 워크플로 디자이너에서 배경 창을 클릭하고 오른쪽 속성 창에서 기본 원본 파일 속성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="c69f8-189">폴더 아이콘을 클릭하고 적절한 비디오 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-189">Click the folder icon and select the appropriate video file.</span></span>

![기본 파일 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="c69f8-191">*기본 파일 원본*</span><span class="sxs-lookup"><span data-stu-id="c69f8-191">*Primary File Source*</span></span>

<span data-ttu-id="c69f8-192">다음으로, 미디어 파일 입력 구성 요소에서 비디오 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-192">Next, specify the video file in the Media File Input component.</span></span>   

![미디어 파일 입력 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="c69f8-194">*미디어 파일 입력 원본*</span><span class="sxs-lookup"><span data-stu-id="c69f8-194">*Media File Input Source*</span></span>

<span data-ttu-id="c69f8-195">이 작업이 완료되는 즉시 미디어 파일 입력 구성 요소는 파일을 검사하고 해당 출력 핀을 채워서 검사한 파일을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="c69f8-196">다음 단계는 "비디오 데이터 형식 업데이터"를 추가하여 색 공간을 Rec.709로 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="c69f8-197">데이터 레이아웃/레이아웃 형식 = 구성 가능한 평면으로 설정된 "비디오 형식 변환기"를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="c69f8-198">그러면 비디오 스트림이 오버레이 구성 요소의 원본으로 사용할 수 있는 형식으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![비디오 데이터 형식 업데이터 및 형식 변환기](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="c69f8-200">*비디오 데이터 형식 업데이터 및 형식 변환기*</span><span class="sxs-lookup"><span data-stu-id="c69f8-200">*Video Data Type Updater and Format Converter*</span></span>

![레이아웃 형식 = 구성 가능한 평면](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="c69f8-202">*구성 가능한 평면의 레이아웃 형식*</span><span class="sxs-lookup"><span data-stu-id="c69f8-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="c69f8-203">다음으로, 비디오 오버레이 구성 요소를 추가하고 (압축되지 않은) 비디오 핀을 미디어 파일 입력의 (압축되지 않은) 비디오 핀에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="c69f8-204">다른 미디어 파일 입력(로고 파일 로드)을 추가하고 이 구성 요소를 클릭한 후 "미디어 파일 입력 로고"로 이름을 변경하고 파일 속성에서 이미지(예를 들어 png 파일)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="c69f8-205">압축되지 않은 이미지 핀을 오버레이의 압축되지 않은 이미지 핀에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![오버레이 구성 요소 및 이미지 파일 원본](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="c69f8-207">*오버레이 구성 요소 및 이미지 파일 원본*</span><span class="sxs-lookup"><span data-stu-id="c69f8-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="c69f8-208">비디오에서 로고의 위치를 수정하려면(예를 들어 비디오의 왼쪽 상단에서 10% 떨어진 위치로 지정할 수 있음) "수동 입력" 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="c69f8-209">오버레이 구성 요소에 로고 파일을 제공하는 데 미디어 파일 입력을 사용하고 있으므로 이와 같은 동작이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![오버레이 위치](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="c69f8-211">*오버레이 위치*</span><span class="sxs-lookup"><span data-stu-id="c69f8-211">*Overlay position*</span></span>

<span data-ttu-id="c69f8-212">비디오 스트림을 H.264로 인코딩하려면 AVC 비디오 인코더 및 AAC 인코더 구성 요소를 디자이너 화면에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="c69f8-213">핀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-213">Connect the pins.</span></span>
<span data-ttu-id="c69f8-214">AAC 인코더를 설정하고 오디오 형식 변환/사전 설정 : 2.0 (L, R)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![오디오 및 비디오 인코더](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="c69f8-216">*오디오 및 비디오 인코더*</span><span class="sxs-lookup"><span data-stu-id="c69f8-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="c69f8-217">이제 **ISO Mpeg-4 멀티플렉서** 및 **파일 출력** 구성 요소를 추가하고 표시된 것과 같이 핀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![MP4 멀티플렉서 및 파일 출력](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="c69f8-219">*MP4 멀티플렉서 및 파일 출력*</span><span class="sxs-lookup"><span data-stu-id="c69f8-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="c69f8-220">출력 파일의 이름을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-220">You need to set the name for the output file.</span></span> <span data-ttu-id="c69f8-221">**파일 출력** 구성 요소를 클릭하고 파일에 대한 식을 다음과 같이 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![파일 출력 이름](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="c69f8-223">*파일 출력 이름*</span><span class="sxs-lookup"><span data-stu-id="c69f8-223">*File output name*</span></span>

<span data-ttu-id="c69f8-224">로컬에서 워크플로를 실행하여 올바르게 실행되고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="c69f8-225">완료되면 Azure 미디어 서비스에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="c69f8-226">먼저 Azure 미디어 서비스에서 안에 두 파일(비디오 파일 및 로고)이 있는 자산을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="c69f8-227">.NET 또는 REST API를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="c69f8-228">또한 Azure 포털이나 [AMSE(Azure 미디어 서비스 탐색기)](https://github.com/Azure/Azure-Media-Services-Explorer) 를 사용하여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="c69f8-229">이 자습서에는 AMSE를 사용하여 자산을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="c69f8-230">두 가지 방법으로 자산에 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="c69f8-231">로컬 폴더를 만들고, 안에 두 개의 파일을 복사하고 해당 폴더를 **자산** 탭으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="c69f8-232">비디오 파일을 자산으로 업로드한 다음 자산 정보를 표시하고 파일 탭으로 이동하여 추가 파일(로고)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="c69f8-233">자산에서 기본 파일을 설정해야 합니다(기본 비디오 파일).</span><span class="sxs-lookup"><span data-stu-id="c69f8-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![AMSE에서 자산 파일](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="c69f8-235">*AMSE에서 자산 파일*</span><span class="sxs-lookup"><span data-stu-id="c69f8-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="c69f8-236">자산을 선택하고 프리미엄 인코더를 사용하여 인코딩하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="c69f8-237">워크플로를 업로드하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="c69f8-238">프로세서에 데이터를 전달하는 버튼을 클릭하고 다음 XML을 추가하여 런타임 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![AMSE에서 프리미엄 인코더](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="c69f8-240">*AMSE에서 프리미엄 인코더*</span><span class="sxs-lookup"><span data-stu-id="c69f8-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="c69f8-241">그런 다음, 다음 XML 데이터를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-241">Then, paste the following XML data.</span></span> <span data-ttu-id="c69f8-242">미디어 파일 입력 및 primarySourceFile 모두에 대한 비디오 파일의 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="c69f8-243">로고에 대한 파일 이름도 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-243">Specify the name of the file name for the logo too.</span></span>

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

<span data-ttu-id="c69f8-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="c69f8-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="c69f8-246">.NET SDK를 사용하여 작업을 만들고 실행한 경우 이 XML 데이터를 구성 문자열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="c69f8-247">작업이 완료되면 출력 자산의 MP4 파일이 오버레이를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![비디오에서 오버레이](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="c69f8-249">*비디오에서 오버레이*</span><span class="sxs-lookup"><span data-stu-id="c69f8-249">*Overlay on the video*</span></span>

<span data-ttu-id="c69f8-250">[GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/)에서 샘플 워크플로를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="c69f8-251">예 2: 다중 오디오 언어 인코딩</span><span class="sxs-lookup"><span data-stu-id="c69f8-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="c69f8-252">다중 오디오 언어 인코딩 워크플로의 예는 [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding)에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="c69f8-253">이 폴더에는 MXF 파일을 여러 오디오 트랙이 있는 다중 MP4 파일 자산으로 인코딩하는 데 사용할 수 있는 샘플 워크플로가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="c69f8-254">이 워크플로는 MXF 파일에 오디오 트랙 하나가 포함된 것으로 가정하며, 추가 오디오 트랙은 별도의 오디오 파일(WAV 또는 MP4)로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="c69f8-255">인코딩하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="c69f8-256">MXF 파일 및 오디오 파일(0~18개 오디오 파일)을 사용하여 Media Services 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="c69f8-257">MXF 파일을 기본 파일로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="c69f8-258">Premium 워크플로 인코더 프로세서를 사용하여 작업 및 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="c69f8-259">제공된 워크플로(MultiMP4-1080p-19audio-v1.workflow)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="c69f8-260">setruntime.xml 데이터를 작업에 전달합니다(Azure Media Services 탐색기를 사용하는 경우 “xml 데이터를 워크플로에 전달” 단추를 사용).</span><span class="sxs-lookup"><span data-stu-id="c69f8-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="c69f8-261">XML 데이터를 업데이트하여 올바른 파일 이름 및 언어 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="c69f8-262">워크플로에는 Audio 1부터 Audio 18까지 오디오 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="c69f8-263">RFC5646은 언어 태그에 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-263">RFC5646 is supported for the language tag.</span></span>

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

* <span data-ttu-id="c69f8-264">인코딩된 자산은 다중 언어 오디오 트랙을 포함하며 이러한 트랙을 Azure Media Player에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69f8-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="c69f8-265">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c69f8-265">See also</span></span>
* [<span data-ttu-id="c69f8-266">Azure 미디어 서비스의 프리미엄 인코딩 소개</span><span class="sxs-lookup"><span data-stu-id="c69f8-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="c69f8-267">Azure 미디어 서비스의 프리미엄 인코딩 사용 방법</span><span class="sxs-lookup"><span data-stu-id="c69f8-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="c69f8-268">Azure 미디어 서비스로 주문형 콘텐츠 인코딩</span><span class="sxs-lookup"><span data-stu-id="c69f8-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="c69f8-269">미디어 인코더 Premium 워크플로 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="c69f8-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="c69f8-270">샘플 워크플로 파일</span><span class="sxs-lookup"><span data-stu-id="c69f8-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="c69f8-271">Azure 미디어 서비스 탐색기 도구</span><span class="sxs-lookup"><span data-stu-id="c69f8-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="c69f8-272">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="c69f8-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c69f8-273">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c69f8-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
