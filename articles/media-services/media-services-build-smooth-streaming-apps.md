---
title: "aaaSmooth 스트리밍 Windows 스토어 응용 프로그램 자습서 | Microsoft Docs"
description: "Azure 미디어 서비스 toocreate toouse XML MediaElement는 C# Windows 스토어 응용 프로그램 tooplayback 부드러운 스트림 콘텐츠를 제어 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="a5be0-103">어떻게 tooBuild 부드러운 스트리밍 Windows 스토어 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a5be0-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="a5be0-104">hello 부드러운 스트리밍 클라이언트 SDK for Windows 8을 사용 하면 주문형 및 라이브 부드러운 스트리밍 콘텐츠를 재생할 수 있는 개발자 toobuild Windows 스토어 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="a5be0-105">부드러운 스트리밍 콘텐츠를 hello SDK 또한의 기본적인 재생 toohello Microsoft PlayReady 보호, 품질 수준 제한 DVR, 전환, 상태 업데이트 (예: 품질 수준 변경 내용 수신 대기 하는 오디오 스트림 Live와 같은 다양 한 기능을 제공 하는 또한 ) 및 오류 이벤트 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="a5be0-106">지원 되는 hello 기능의 자세한 내용은 참조 hello [릴리스 정보](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="a5be0-107">자세한 내용은 [Windows 8용 플레이어 프레임워크](http://playerframework.codeplex.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5be0-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="a5be0-108">이 자습서에는 4개 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="a5be0-109">기본 부드러운 스트리밍 스토어 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a5be0-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="a5be0-110">슬라이더 tooControl hello 미디어 진행률 막대를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="a5be0-111">부드러운 스트리밍 스트림 선택</span><span class="sxs-lookup"><span data-stu-id="a5be0-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="a5be0-112">부드러운 스트리밍 트랙 선택</span><span class="sxs-lookup"><span data-stu-id="a5be0-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5be0-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a5be0-113">Prerequisites</span></span>
* <span data-ttu-id="a5be0-114">Windows 8 32비트 또는 64비트.</span><span class="sxs-lookup"><span data-stu-id="a5be0-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="a5be0-115">MSDN에서 [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) 을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="a5be0-116">Visual Studio 2012 또는 Visual Studio Express 2012(또는 이후 버전).</span><span class="sxs-lookup"><span data-stu-id="a5be0-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="a5be0-117">Hello에서 평가판 버전을 얻을 수 있습니다 [여기](http://www.microsoft.com/visualstudio/11/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="a5be0-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)</span><span class="sxs-lookup"><span data-stu-id="a5be0-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="a5be0-119">각 단원 완료 hello 솔루션 MSDN 개발자 코드 샘플 (코드 갤러리)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="a5be0-120">[단원 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - 간단한 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="a5be0-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="a5be0-121">[단원 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - 슬라이더 막대 컨트롤이 있는 간단한 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="a5be0-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="a5be0-122">[단원 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - 스트림 선택 항목이 있는 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="a5be0-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="a5be0-123">[단원 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - 트랙 선택 항목이 있는 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="a5be0-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="a5be0-124">단원 1: 기본 부드러운 스트리밍 스토어 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a5be0-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="a5be0-125">이 단원에서는 만들어집니다는 Windows 스토어 응용 프로그램 MediaElement 컨트롤 tooplay 부드러운 스트림을 사용 하 여 콘텐츠.</span><span class="sxs-lookup"><span data-stu-id="a5be0-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="a5be0-126">실행 중인 응용 프로그램 hello는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-126">hello running application looks like:</span></span>

![부드러운 스트리밍 Windows 스토어 응용 프로그램 예][PlayerApplication]

<span data-ttu-id="a5be0-128">Windows 스토어 응용 프로그램 개발에 대한 자세한 내용은 [유용한 Windows 8용 앱 개발](http://msdn.microsoft.com/windows/apps/br229512.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="a5be0-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="a5be0-129">이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="a5be0-130">Windows 스토어 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a5be0-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="a5be0-131">Hello 사용자 인터페이스 디자인 (XAML)</span><span class="sxs-lookup"><span data-stu-id="a5be0-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="a5be0-132">Hello 코드 숨김 파일 수정</span><span class="sxs-lookup"><span data-stu-id="a5be0-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="a5be0-133">컴파일 및 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="a5be0-133">Compile and test hello application</span></span>

<span data-ttu-id="a5be0-134">**Windows 스토어 프로젝트 toocreate**</span><span class="sxs-lookup"><span data-stu-id="a5be0-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="a5be0-135">Visual Studio 2012 이상을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="a5be0-136">Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="a5be0-137">Hello 새 프로젝트 대화 상자에서 값 형식 또는 다음 선택 hello:</span><span class="sxs-lookup"><span data-stu-id="a5be0-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="a5be0-138">이름</span><span class="sxs-lookup"><span data-stu-id="a5be0-138">Name</span></span> | <span data-ttu-id="a5be0-139">값</span><span class="sxs-lookup"><span data-stu-id="a5be0-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a5be0-140">템플릿 그룹</span><span class="sxs-lookup"><span data-stu-id="a5be0-140">Template group</span></span> |<span data-ttu-id="a5be0-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="a5be0-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="a5be0-142">Template</span><span class="sxs-lookup"><span data-stu-id="a5be0-142">Template</span></span> |<span data-ttu-id="a5be0-143">새 응용 프로그램(XAML)</span><span class="sxs-lookup"><span data-stu-id="a5be0-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="a5be0-144">이름</span><span class="sxs-lookup"><span data-stu-id="a5be0-144">Name</span></span> |<span data-ttu-id="a5be0-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="a5be0-145">SSPlayer</span></span> |
| <span data-ttu-id="a5be0-146">위치</span><span class="sxs-lookup"><span data-stu-id="a5be0-146">Location</span></span> |<span data-ttu-id="a5be0-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="a5be0-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="a5be0-148">솔루션 이름</span><span class="sxs-lookup"><span data-stu-id="a5be0-148">Solution Name</span></span> |<span data-ttu-id="a5be0-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="a5be0-149">SSPlayer</span></span> |
| <span data-ttu-id="a5be0-150">솔루션에 대한 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="a5be0-150">Create directory for solution</span></span> |<span data-ttu-id="a5be0-151">(선택됨)</span><span class="sxs-lookup"><span data-stu-id="a5be0-151">(selected)</span></span> |

1. <span data-ttu-id="a5be0-152">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-152">Click **OK**.</span></span>

<span data-ttu-id="a5be0-153">**tooadd 참조 toohello 부드러운 스트리밍 클라이언트 SDK**</span><span class="sxs-lookup"><span data-stu-id="a5be0-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="a5be0-154">[솔루션 탐색기]에서 **SSPlayer**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="a5be0-155">입력 하거나 다음 값에는 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="a5be0-155">Type or select hello following values:</span></span>

| <span data-ttu-id="a5be0-156">이름</span><span class="sxs-lookup"><span data-stu-id="a5be0-156">Name</span></span> | <span data-ttu-id="a5be0-157">값</span><span class="sxs-lookup"><span data-stu-id="a5be0-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a5be0-158">참조 그룹</span><span class="sxs-lookup"><span data-stu-id="a5be0-158">Reference group</span></span> |<span data-ttu-id="a5be0-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="a5be0-159">Windows/Extensions</span></span> |
| <span data-ttu-id="a5be0-160">참조</span><span class="sxs-lookup"><span data-stu-id="a5be0-160">Reference</span></span> |<span data-ttu-id="a5be0-161">Microsoft Smooth Streaming Client SDK for Windows 8 및 Microsoft Visual C++ 런타임 패키지 선택</span><span class="sxs-lookup"><span data-stu-id="a5be0-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="a5be0-162">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-162">Click **OK**.</span></span> 

<span data-ttu-id="a5be0-163">Hello 참조를 추가한 후 hello 대상 플랫폼 (x64 또는 x86)을 선택 해야, Any CPU 플랫폼 구성에 대 한 참조 추가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="a5be0-164">솔루션 탐색기에서 추가된 이 참조에 대해 노란색 경고 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="a5be0-165">**toodesign hello 플레이어 사용자 인터페이스**</span><span class="sxs-lookup"><span data-stu-id="a5be0-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="a5be0-166">솔루션 탐색기에서 두 번 클릭 **MainPage.xaml** tooopen hello 디자인에서 보기.</span><span class="sxs-lookup"><span data-stu-id="a5be0-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="a5be0-167">Hello 찾을  **&lt;그리드&gt;**  및  **&lt;/Grid&gt;**  hello 두 태그 사이 붙여넣기 hello 다음 코드 및 태그 hello XAML 파일:</span><span class="sxs-lookup"><span data-stu-id="a5be0-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   <span data-ttu-id="a5be0-168">hello MediaElement 컨트롤에 사용 되는 tooplayback 미디어입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="a5be0-169">hello 다음 단원에서는 toocontrol hello 미디어 진행에서 sliderProgress 라는 hello 슬라이더 컨트롤 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="a5be0-170">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-171">hello MediaElement 컨트롤에는 부드러운 스트리밍 콘텐츠-기본적으로 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="a5be0-172">tooenable hello 부드러운 스트리밍을 지원, 파일 이름 확장명 및 MIME 형식에 따라 hello 부드러운 스트리밍 바이트 스트림 처리기를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="a5be0-173">tooregister, 방법을 사용 하 여 hello MediaExtensionManager.RegisterByteStremHandler hello Windows.Media 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="a5be0-174">이 XAML 파일에서 일부 이벤트 처리기 hello 컨트롤 연관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="a5be0-175">해당 이벤트 처리기를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-175">You must define those event handlers.</span></span>

<span data-ttu-id="a5be0-176">**toomodify hello 코드 숨김 파일**</span><span class="sxs-lookup"><span data-stu-id="a5be0-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="a5be0-177">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-178">Hello 파일의 hello 위쪽 hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="a5be0-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="a5be0-179">Hello hello 시작 시 **MainPage** 클래스 hello 데이터 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="a5be0-180">Hello hello 끝나기 전에 **MainPage** 생성자 hello 다음 두 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="a5be0-181">Hello hello 끝나기 전에 **MainPage** 클래스, hello 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="a5be0-182">hello sliderProgress_PointerPressed 이벤트 처리기 여기에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="a5be0-183">더 많은 works toodo tooget는 작업 하 고, 있는에서 설명 합니다.이 자습서의 다음 단원 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="a5be0-184">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-185">hello 완성 된 hello 코드 숨김 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-185">hello finished hello code behind file shall look like this:</span></span>

![부드러운 스트리밍 Windows 스토어 응용 프로그램에 대한 Visual Studio의 Codeview][CodeViewPic]

<span data-ttu-id="a5be0-187">**toocompile 및 테스트 hello 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="a5be0-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="a5be0-188">Hello에서 **빌드** 메뉴를 클릭 하 여 **Configuration Manager**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="a5be0-189">변경 **활성 솔루션 플랫폼** toomatch 개발 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="a5be0-190">키를 눌러 **F6** toocompile hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="a5be0-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="a5be0-191">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="a5be0-192">Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="a5be0-193">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-193">Click **Set Source**.</span></span> <span data-ttu-id="a5be0-194">때문에 **자동 재생** hello 미디어를 자동으로 재생은 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="a5be0-195">Hello를 사용 하 여 hello 미디어를 제어할 수 있습니다 **재생**, **일시 중지** 및 **중지** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="a5be0-196">Hello 세로 슬라이더를 사용 하 여 hello 미디어 볼륨을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="a5be0-197">그러나 hello 가로 슬라이더 제어 hello 미디어 진행률 완전히 아직 구현 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="a5be0-198">lesson1을 완성했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-198">You have completed lesson1.</span></span>  <span data-ttu-id="a5be0-199">이 단원에서는 MediaElement 컨트롤 tooplayback 부드러운 스트리밍 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="a5be0-200">Hello 다음 단원에서는 부드러운 스트리밍 콘텐츠를 hello의 슬라이더 toocontrol hello 진행률을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="a5be0-201">2 단원: 슬라이더 tooControl hello 미디어 진행률 막대를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="a5be0-202">1 단원에서 MediaElement XAML 컨트롤 tooplayback 부드러운 스트리밍 미디어 콘텐츠를 Windows 스토어 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="a5be0-203">시작, 중지, 일시 중지 등의 기본 미디어 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="a5be0-204">이 단원에서는 슬라이더 막대 컨트롤 toohello 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="a5be0-205">이 자습서에서는 hello hello MediaElement 컨트롤의 현재 위치에 따라 타이머 tooupdate hello 슬라이더 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="a5be0-206">hello 슬라이더 시작 및 종료 시간도 필요 toobe 발생 한 경우 라이브 콘텐츠를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="a5be0-207">Hello 적응 소스 update 이벤트에 보다 잘 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="a5be0-208">미디어 원본은 미디어 데이터를 생성하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="a5be0-209">hello 소스 확인자는 URL 또는 바이트 스트림을 사용 하 고 해당 콘텐츠에 대 한 hello 적절 한 미디어 소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="a5be0-210">hello 소스 확인자는 hello 응용 프로그램 toocreate 미디어 원본에 대 한 hello 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="a5be0-211">이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="a5be0-212">Hello 부드러운 스트리밍 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="a5be0-213">Hello 적응 소스 관리자 수준의 이벤트 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="a5be0-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="a5be0-214">Hello 적응 소스 수준 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="a5be0-215">MediaElement 이벤트 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="a5be0-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="a5be0-216">슬라이더 막대 관련 코드 추가</span><span class="sxs-lookup"><span data-stu-id="a5be0-216">Add slider bar related code</span></span>
6. <span data-ttu-id="a5be0-217">컴파일 및 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="a5be0-217">Compile and test hello application</span></span>

<span data-ttu-id="a5be0-218">**tooregister hello 부드러운 스트리밍 바이트 스트림 처리기와 패스 hello propertyset**</span><span class="sxs-lookup"><span data-stu-id="a5be0-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="a5be0-219">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-220">Hello 파일 시작 부분의 hello, hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="a5be0-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="a5be0-221">Hello MainPage 클래스의 hello 맨 hello 다음 데이터 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="a5be0-222">내부 hello **MainPage** 생성자 hello hello 후 코드를 다음 추가 **이 있습니다. Components(); 초기화**  줄과 hello 이전 단원에서 작성 된 hello 등록 코드 줄:</span><span class="sxs-lookup"><span data-stu-id="a5be0-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="a5be0-223">내부 hello **MainPage** 생성자 매개 변수 2 hello RegisterByteStreamHandler 메서드 tooadd hello 세이프 수정:</span><span class="sxs-lookup"><span data-stu-id="a5be0-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. <span data-ttu-id="a5be0-224">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-225">**tooadd hello 적응 소스 관리자 수준의 이벤트 처리기**</span><span class="sxs-lookup"><span data-stu-id="a5be0-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="a5be0-226">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-227">내부 hello **MainPage** 클래스 hello 데이터 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="a5be0-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="a5be0-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="a5be0-229">Hello hello 끝나기 전에 **MainPage** 클래스 hello 다음 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="a5be0-230">Hello hello 끝나기 전에 **MainPage** 생성자를 다음 줄 toosubscribe toohello 적응 소스 open 이벤트 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="a5be0-231">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-232">**tooadd 적응 소스 수준 이벤트 처리기**</span><span class="sxs-lookup"><span data-stu-id="a5be0-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="a5be0-233">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-234">내부 hello **MainPage** 클래스 hello 데이터 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="a5be0-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="a5be0-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="a5be0-236">Hello hello 끝나기 전에 **MainPage** 클래스 hello 다음 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. <span data-ttu-id="a5be0-237">Hello hello 끝나기 전에 **mediaElement AdaptiveSourceOpened** 메서드를 hello toosubscribe toohello 이벤트 코드를 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="a5be0-238">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-239">hello 적응 소스 manger 수준에도 hello 앱의 기능 일반적인 tooall 미디어 요소를 처리 하기 위한 사용할 수 있는 동일한 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="a5be0-240">각 AdaptiveSource에는 고유한 이벤트가 포함되어 있으며 모든 AdaptiveSource 이벤트가 AdaptiveSourceManager 아래에 계단식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="a5be0-241">**tooadd 미디어 요소의 이벤트 처리기**</span><span class="sxs-lookup"><span data-stu-id="a5be0-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="a5be0-242">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-243">Hello hello 끝나기 전에 **MainPage** 클래스 hello 다음 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. <span data-ttu-id="a5be0-244">Hello hello 끝나기 전에 **MainPage** 생성자 hello toosubscript toohello 이벤트 코드를 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="a5be0-245">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-246">**tooadd 슬라이더 막대를 관련 된 코드**</span><span class="sxs-lookup"><span data-stu-id="a5be0-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="a5be0-247">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-248">Hello 파일 시작 부분의 hello, hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="a5be0-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="a5be0-249">내부 hello **MainPage** 클래스, 데이터 멤버를 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="a5be0-250">Hello hello 끝나기 전에 **MainPage** 생성자 코드 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="a5be0-251">Hello hello 끝나기 전에 **MainPage** 클래스 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
><span data-ttu-id="a5be0-252">CoreDispatcher은 비 UI 스레드에서 toohello UI 스레드 사용 되는 toomake 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="a5be0-253">발송자 스레드의 병목 현상이 발생할 경우 개발자는 toouse 발송자 tooupdate 노드가 받지 않으려는 UI 요소에서 제공 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="a5be0-254">예:</span><span class="sxs-lookup"><span data-stu-id="a5be0-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="a5be0-255">Hello hello 끝나기 전에 **mediaElement_AdaptiveSourceStatusUpdated** 메서드를 코드 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="a5be0-256">Hello hello 끝나기 전에 **MediaOpened** 메서드를 코드 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="a5be0-257">키를 눌러 **CTRL + S** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="a5be0-258">**toocompile 및 테스트 hello 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="a5be0-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="a5be0-259">키를 눌러 **F6** toocompile hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="a5be0-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="a5be0-260">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="a5be0-261">Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="a5be0-262">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="a5be0-263">Hello 슬라이더 막대를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-263">Test hello slider bar.</span></span>

<span data-ttu-id="a5be0-264">단원 2를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-264">You have completed lesson 2.</span></span>  <span data-ttu-id="a5be0-265">이 단원에서는 슬라이더 tooapplication을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="a5be0-266">단원 3: 부드러운 스트리밍 스트림 선택</span><span class="sxs-lookup"><span data-stu-id="a5be0-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="a5be0-267">부드러운 스트리밍은 hello 뷰어에서 선택할 수 있는 여러 언어 오디오 트랙 사용 가능 toostream 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="a5be0-268">이 단원에서는 뷰어 tooselect 스트림을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="a5be0-269">이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="a5be0-270">Hello XAML 파일을 수정</span><span class="sxs-lookup"><span data-stu-id="a5be0-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="a5be0-271">Hello 코드 behand 파일 수정</span><span class="sxs-lookup"><span data-stu-id="a5be0-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="a5be0-272">컴파일 및 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="a5be0-272">Compile and test hello application</span></span>

<span data-ttu-id="a5be0-273">**toomodify hello XAML 파일**</span><span class="sxs-lookup"><span data-stu-id="a5be0-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="a5be0-274">솔루션 탐색기에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="a5be0-275">찾을 &lt;Grid.RowDefinitions&gt;, 처럼 보이는 hello RowDefinitions 수정:</span><span class="sxs-lookup"><span data-stu-id="a5be0-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="a5be0-276">내부 hello &lt;그리드&gt;&lt;/Grid&gt; hello 다음 코드 toodefine listbox 컨트롤 사용자가 사용할 수 있는 스트림의 hello 목록을 참조를 업데이트 하 고 스트림을 선택할 수 있으므로 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. <span data-ttu-id="a5be0-277">키를 눌러 **CTRL + S** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="a5be0-278">**toomodify hello 코드 숨김 파일**</span><span class="sxs-lookup"><span data-stu-id="a5be0-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="a5be0-279">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-280">Hello SSPlayer 네임 스페이스 내부 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. <span data-ttu-id="a5be0-281">Hello MainPage 클래스의 hello 맨 hello 변수 정의 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="a5be0-282">Hello MainPage 클래스, 내부 hello 다음 영역을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-282">Inside hello MainPage class, add hello following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. <span data-ttu-id="a5be0-283">Hello 코드 hello 함수 hello 끝에 다음 추가 hello mediaElement_ManifestReady 메서드를 찾아:</span><span class="sxs-lookup"><span data-stu-id="a5be0-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="a5be0-284">따라서 MediaElement 매니페스트 준비 되 면 hello 코드 hello 사용 가능한 스트림의 목록을 가져옵니다 바뀌고 hello 목록 사용 하 여 hello UI 목록 상자를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="a5be0-285">Hello MainPage 클래스, 내부 찾을 hello UI 단추 이벤트 영역을 클릭 한 다음 함수 정의 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="a5be0-286">**toocompile 및 테스트 hello 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="a5be0-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="a5be0-287">키를 눌러 **F6** toocompile hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="a5be0-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="a5be0-288">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="a5be0-289">Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="a5be0-290">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="a5be0-291">hello 기본 언어는 audio_eng입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-291">hello default language is audio_eng.</span></span> <span data-ttu-id="a5be0-292">Audio_eng 사이의 audio_es tooswitch 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a5be0-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="a5be0-293">새 스트림 선택 될 때마다, hello 전송 단추를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="a5be0-294">단원 3을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-294">You have completed lesson 3.</span></span>  <span data-ttu-id="a5be0-295">이 단원에서는 hello 기능 toochoose 스트림을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="a5be0-296">단원 4: 부드러운 스트리밍 트랙 선택</span><span class="sxs-lookup"><span data-stu-id="a5be0-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="a5be0-297">부드러운 스트리밍 프레젠테이션에는 여러 품질 수준(비트 전송률) 및 해상도로 인코딩된 여러 비디오 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="a5be0-298">이 단원에서는 사용자가 tooselect 트랙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="a5be0-299">이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="a5be0-300">Hello XAML 파일을 수정</span><span class="sxs-lookup"><span data-stu-id="a5be0-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="a5be0-301">Hello 코드 behand 파일 수정</span><span class="sxs-lookup"><span data-stu-id="a5be0-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="a5be0-302">컴파일 및 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="a5be0-302">Compile and test hello application</span></span>

<span data-ttu-id="a5be0-303">**toomodify hello XAML 파일**</span><span class="sxs-lookup"><span data-stu-id="a5be0-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="a5be0-304">솔루션 탐색기에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="a5be0-305">Hello 찾을 &lt;그리드&gt; hello 이름의 태그 **gridStreamAndBitrateSelection**, hello 코드 hello 태그의 hello 끝에 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="a5be0-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. <span data-ttu-id="a5be0-306">키를 눌러 **CTRL + S** toosave로 변경 하 고</span><span class="sxs-lookup"><span data-stu-id="a5be0-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="a5be0-307">**toomodify hello 코드 숨김 파일**</span><span class="sxs-lookup"><span data-stu-id="a5be0-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="a5be0-308">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="a5be0-309">Hello SSPlayer 네임 스페이스 내부 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. <span data-ttu-id="a5be0-310">Hello MainPage 클래스의 hello 맨 hello 변수 정의 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="a5be0-311">Hello MainPage 클래스, 내부 hello 다음 영역을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-311">Inside hello MainPage class, add hello following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. <span data-ttu-id="a5be0-312">Hello 코드 hello 함수 hello 끝에 다음 추가 hello mediaElement_ManifestReady 메서드를 찾아:</span><span class="sxs-lookup"><span data-stu-id="a5be0-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="a5be0-313">Hello MainPage 클래스, 내부 찾을 hello UI 단추 이벤트 영역을 클릭 한 다음 함수 정의 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="a5be0-314">**toocompile 및 테스트 hello 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="a5be0-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="a5be0-315">키를 눌러 **F6** toocompile hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="a5be0-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="a5be0-316">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="a5be0-317">Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="a5be0-318">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="a5be0-319">기본적으로 hello 비디오 스트림의 hello 트랙의 모든 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="a5be0-320">tooexperiment hello 비트 전송률 변경 hello 가장 낮은 비트 전송률을 사용할 수를 선택 하 고 hello 가장 높은 비트 전송률 사용할 수 있는 다음 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="a5be0-321">각 변경 후에 제출을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-321">You must click Submit after each change.</span></span>  <span data-ttu-id="a5be0-322">Hello 비디오 품질 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="a5be0-323">단원 4를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-323">You have completed lesson 4.</span></span>  <span data-ttu-id="a5be0-324">이 단원에서는 hello 기능 toochoose 트랙 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5be0-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a5be0-325">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a5be0-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a5be0-326">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a5be0-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="a5be0-327">기타 리소스:</span><span class="sxs-lookup"><span data-stu-id="a5be0-327">Other Resources:</span></span>
* [<span data-ttu-id="a5be0-328">어떻게 toobuild 부드러운 스트리밍 Windows 8 JavaScript 응용 프로그램을 고급 기능</span><span class="sxs-lookup"><span data-stu-id="a5be0-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="a5be0-329">부드러운 스트리밍 기술 개요</span><span class="sxs-lookup"><span data-stu-id="a5be0-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

