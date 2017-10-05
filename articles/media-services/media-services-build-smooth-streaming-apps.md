---
title: "부드러운 스트리밍 Windows 스토어 앱 자습서 | Microsoft 문서"
description: "Azure 미디어 서비스를 사용하여 부드러운 스트림 콘텐츠를 재생하기 위해 XML MediaElement 컨트롤이 포함된 C# Windows 스토어 응용 프로그램을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="5dca2-103">부드러운 스트리밍 Windows 스토어 응용 프로그램을 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="5dca2-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="5dca2-104">Smooth Streaming Client SDK for Windows 8을 사용하면 개발자가 주문형 및 Live Smooth Streaming 콘텐츠를 재생할 수 있는 Windows 스토어 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="5dca2-105">부드러운 스트리밍 콘텐츠의 기본 재생뿐 아니라 SDK는 Microsoft PlayReady 보호, 품질 수준 제한, Live DVR, 오디오 스트림 전환, 상태 업데이트(예: 품질 수준 변경) 수신 대기, 오류 이벤트 등의 풍부한 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="5dca2-106">지원되는 기능에 대한 자세한 내용은 [릴리스 정보](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5dca2-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="5dca2-107">자세한 내용은 [Windows 8용 플레이어 프레임워크](http://playerframework.codeplex.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5dca2-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="5dca2-108">이 자습서에는 4개 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="5dca2-109">기본 부드러운 스트리밍 스토어 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="5dca2-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="5dca2-110">미디어 진행을 제어하는 슬라이더 막대 추가</span><span class="sxs-lookup"><span data-stu-id="5dca2-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="5dca2-111">부드러운 스트리밍 스트림 선택</span><span class="sxs-lookup"><span data-stu-id="5dca2-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="5dca2-112">부드러운 스트리밍 트랙 선택</span><span class="sxs-lookup"><span data-stu-id="5dca2-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dca2-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5dca2-113">Prerequisites</span></span>
* <span data-ttu-id="5dca2-114">Windows 8 32비트 또는 64비트.</span><span class="sxs-lookup"><span data-stu-id="5dca2-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="5dca2-115">MSDN에서 [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) 을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="5dca2-116">Visual Studio 2012 또는 Visual Studio Express 2012(또는 이후 버전).</span><span class="sxs-lookup"><span data-stu-id="5dca2-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="5dca2-117">[여기](http://www.microsoft.com/visualstudio/11/downloads)에서 평가판을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="5dca2-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)</span><span class="sxs-lookup"><span data-stu-id="5dca2-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="5dca2-119">각 단원에 대해 완성된 솔루션은 MSDN 개발자 코드 샘플(코드 갤러리)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="5dca2-120">[단원 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - 간단한 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="5dca2-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="5dca2-121">[단원 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - 슬라이더 막대 컨트롤이 있는 간단한 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="5dca2-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="5dca2-122">[단원 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - 스트림 선택 항목이 있는 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="5dca2-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="5dca2-123">[단원 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - 트랙 선택 항목이 있는 Windows 8 부드러운 스트리밍 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="5dca2-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="5dca2-124">단원 1: 기본 부드러운 스트리밍 스토어 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="5dca2-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="5dca2-125">이 단원에서는 부드러운 스트림 콘텐츠를 재생하기 위해 MediaElement 컨트롤이 포함된 Windows 스토어 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="5dca2-126">실행 중인 응용 프로그램은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-126">The running application looks like:</span></span>

![부드러운 스트리밍 Windows 스토어 응용 프로그램 예][PlayerApplication]

<span data-ttu-id="5dca2-128">Windows 스토어 응용 프로그램 개발에 대한 자세한 내용은 [유용한 Windows 8용 앱 개발](http://msdn.microsoft.com/windows/apps/br229512.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5dca2-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="5dca2-129">이 단원에는 다음 절차가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5dca2-130">Windows 스토어 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5dca2-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="5dca2-131">사용자 인터페이스 디자인(XAML)</span><span class="sxs-lookup"><span data-stu-id="5dca2-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="5dca2-132">코드 숨김 파일 수정</span><span class="sxs-lookup"><span data-stu-id="5dca2-132">Modify the code behind file</span></span>
4. <span data-ttu-id="5dca2-133">응용 프로그램 컴파일 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5dca2-133">Compile and test the application</span></span>

<span data-ttu-id="5dca2-134">**Windows 스토어 프로젝트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="5dca2-135">Visual Studio 2012 이상을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="5dca2-136">**파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="5dca2-137">[새 프로젝트] 대화 상자에서 다음 값을 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="5dca2-138">이름</span><span class="sxs-lookup"><span data-stu-id="5dca2-138">Name</span></span> | <span data-ttu-id="5dca2-139">값</span><span class="sxs-lookup"><span data-stu-id="5dca2-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5dca2-140">템플릿 그룹</span><span class="sxs-lookup"><span data-stu-id="5dca2-140">Template group</span></span> |<span data-ttu-id="5dca2-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="5dca2-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="5dca2-142">Template</span><span class="sxs-lookup"><span data-stu-id="5dca2-142">Template</span></span> |<span data-ttu-id="5dca2-143">새 응용 프로그램(XAML)</span><span class="sxs-lookup"><span data-stu-id="5dca2-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="5dca2-144">이름</span><span class="sxs-lookup"><span data-stu-id="5dca2-144">Name</span></span> |<span data-ttu-id="5dca2-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="5dca2-145">SSPlayer</span></span> |
| <span data-ttu-id="5dca2-146">위치</span><span class="sxs-lookup"><span data-stu-id="5dca2-146">Location</span></span> |<span data-ttu-id="5dca2-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="5dca2-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="5dca2-148">솔루션 이름</span><span class="sxs-lookup"><span data-stu-id="5dca2-148">Solution Name</span></span> |<span data-ttu-id="5dca2-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="5dca2-149">SSPlayer</span></span> |
| <span data-ttu-id="5dca2-150">솔루션에 대한 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="5dca2-150">Create directory for solution</span></span> |<span data-ttu-id="5dca2-151">(선택됨)</span><span class="sxs-lookup"><span data-stu-id="5dca2-151">(selected)</span></span> |

1. <span data-ttu-id="5dca2-152">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-152">Click **OK**.</span></span>

<span data-ttu-id="5dca2-153">**부드러운 스트리밍 클라이언트 SDK에 대한 참조를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="5dca2-154">[솔루션 탐색기]에서 **SSPlayer**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="5dca2-155">다음 값을 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-155">Type or select the following values:</span></span>

| <span data-ttu-id="5dca2-156">이름</span><span class="sxs-lookup"><span data-stu-id="5dca2-156">Name</span></span> | <span data-ttu-id="5dca2-157">값</span><span class="sxs-lookup"><span data-stu-id="5dca2-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5dca2-158">참조 그룹</span><span class="sxs-lookup"><span data-stu-id="5dca2-158">Reference group</span></span> |<span data-ttu-id="5dca2-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="5dca2-159">Windows/Extensions</span></span> |
| <span data-ttu-id="5dca2-160">참조</span><span class="sxs-lookup"><span data-stu-id="5dca2-160">Reference</span></span> |<span data-ttu-id="5dca2-161">Microsoft Smooth Streaming Client SDK for Windows 8 및 Microsoft Visual C++ 런타임 패키지 선택</span><span class="sxs-lookup"><span data-stu-id="5dca2-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="5dca2-162">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-162">Click **OK**.</span></span> 

<span data-ttu-id="5dca2-163">참조를 추가한 후 대상 플랫폼(x64 또는 x86)을 선택해야 합니다. 임의 CPU 플랫폼 구성에서는 참조 추가가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="5dca2-164">솔루션 탐색기에서 추가된 이 참조에 대해 노란색 경고 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="5dca2-165">**플레이어 사용자 인터페이스를 디자인하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="5dca2-166">솔루션 탐색기에서 **MainPage.xaml** 을 두 번 클릭하여 디자인 보기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="5dca2-167">XAML 파일에서 **&lt;Grid&gt;** 및 **&lt;/Grid&gt;** 태그를 찾아 두 태그 사이에 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="5dca2-168">MediaElement 컨트롤은 미디어를 재생하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="5dca2-169">sliderProgress라는 슬라이더 컨트롤은 다음 단원에서 미디어 진행을 제어하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="5dca2-170">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-171">MediaElement 컨트롤은 기본적으로 부드러운 스트리밍 콘텐츠를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="5dca2-172">부드러운 스트리밍 지원을 사용하도록 설정하려면 파일 이름 확장명과 MIME 형식으로 부드러운 스트리밍 바이트 스트림 처리기를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="5dca2-173">등록하려면 Windows.Media 네임스페이스의 MediaExtensionManager.RegisterByteStremHandler 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="5dca2-174">이 XAML 파일에서는 일부 이벤트 처리기가 컨트롤과 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="5dca2-175">해당 이벤트 처리기를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-175">You must define those event handlers.</span></span>

<span data-ttu-id="5dca2-176">**코드 숨김 파일을 수정하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="5dca2-177">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-178">파일 맨 위에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="5dca2-179">**MainPage** 클래스의 시작 부분에 다음 데이터 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="5dca2-180">**MainPage** 생성자의 끝에 다음 두 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="5dca2-181">**MainPage** 클래스의 끝에 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="5dca2-182">여기에는 sliderProgress_PointerPressed 이벤트 처리기가 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="5dca2-183">작동하는 데 필요한 추가 작업이 있으며, 이 자습서의 다음 단원에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="5dca2-184">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-185">완성된 코드 숨김 파일은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-185">The finished the code behind file shall look like this:</span></span>

![부드러운 스트리밍 Windows 스토어 응용 프로그램에 대한 Visual Studio의 Codeview][CodeViewPic]

<span data-ttu-id="5dca2-187">**응용 프로그램을 컴파일 및 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="5dca2-188">**빌드** 메뉴에서 **구성 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="5dca2-189">개발 플랫폼과 일치하도록 **활성 솔루션 플랫폼** 을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="5dca2-190">**F6** 키를 눌러 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="5dca2-191">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="5dca2-192">응용 프로그램 맨 위에 기본 부드러운 스트리밍 URL을 사용하거나 다른 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="5dca2-193">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-193">Click **Set Source**.</span></span> <span data-ttu-id="5dca2-194">기본적으로 **자동 재생** 이 사용되기 때문에 미디어가 자동으로 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="5dca2-195">**재생**, **일시 중지** 및 **중지** 단추를 사용하여 미디어를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="5dca2-196">세로 슬라이더를 사용하여 미디어 볼륨을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="5dca2-197">그러나 미디어 진행을 제어하기 위한 가로 슬라이더는 아직 완전히 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="5dca2-198">lesson1을 완성했습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-198">You have completed lesson1.</span></span>  <span data-ttu-id="5dca2-199">이 단원에서는 MediaElement 컨트롤을 사용하여 부드러운 스트리밍 콘텐츠를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="5dca2-200">다음 단원에서는 부드러운 스트리밍 콘텐츠 진행을 제어하는 슬라이더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="5dca2-201">단원 2: 미디어 진행을 제어하는 슬라이더 막대 추가</span><span class="sxs-lookup"><span data-stu-id="5dca2-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="5dca2-202">단원 1에서는 부드러운 스트리밍 미디어 콘텐츠를 재생하기 위해 MediaElement XAML 컨트롤이 포함된 Windows 스토어 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="5dca2-203">시작, 중지, 일시 중지 등의 기본 미디어 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="5dca2-204">이 단원에서는 응용 프로그램에 슬라이더 막대 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="5dca2-205">이 자습서에서는 타이머를 사용하여 MediaElement 컨트롤의 현재 위치에 따라 슬라이더 위치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="5dca2-206">라이브 콘텐츠의 경우 슬라이더 시작 및 종료 시간도 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="5dca2-207">이 작업은 적응 원본 업데이트 이벤트를 통해 더 효율적으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="5dca2-208">미디어 원본은 미디어 데이터를 생성하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="5dca2-209">원본 확인자는 URL 또는 바이트 스트림을 사용하고 해당 콘텐츠에 적합한 미디어 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="5dca2-210">원본 확인자는 응용 프로그램에서 미디어 원본을 만드는 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="5dca2-211">이 단원에는 다음 절차가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5dca2-212">부드러운 스트리밍 처리기 등록</span><span class="sxs-lookup"><span data-stu-id="5dca2-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="5dca2-213">적응 원본 관리자 수준 이벤트 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="5dca2-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="5dca2-214">적응 원본 수준 이벤트 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="5dca2-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="5dca2-215">MediaElement 이벤트 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="5dca2-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="5dca2-216">슬라이더 막대 관련 코드 추가</span><span class="sxs-lookup"><span data-stu-id="5dca2-216">Add slider bar related code</span></span>
6. <span data-ttu-id="5dca2-217">응용 프로그램 컴파일 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5dca2-217">Compile and test the application</span></span>

<span data-ttu-id="5dca2-218">**부드러운 스트리밍 바이트 스트림 처리기를 등록하고 propertyset를 전달하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="5dca2-219">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-220">파일의 시작 부분에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="5dca2-221">MainPage 클래스의 시작 부분에 다음 데이터 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="5dca2-222">**MainPage** 생성자 내에서 **this.Initialize Components();** 줄과 이전 단원에서 작성한 등록 코드 줄 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="5dca2-223">**MainPage** 생성자 내에서 RegisterByteStreamHandler 메서드 두 개를 수정하여 네 번째 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="5dca2-224">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-225">**적응 원본 관리자 수준 이벤트 처리기를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="5dca2-226">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-227">**MainPage** 클래스 내에 다음 데이터 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="5dca2-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="5dca2-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="5dca2-229">**MainPage** 클래스의 끝에 다음 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="5dca2-230">**MainPage** 생성자의 끝에 다음 줄을 추가하여 적응 원본 열기 이벤트를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="5dca2-231">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-232">**적응 원본 수준 이벤트 처리기를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="5dca2-233">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-234">**MainPage** 클래스 내에 다음 데이터 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="5dca2-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="5dca2-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="5dca2-236">**MainPage** 클래스의 끝에 다음 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="5dca2-237">**mediaElement AdaptiveSourceOpened** 메서드의 끝에 다음 코드를 추가하여 이벤트를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="5dca2-238">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-239">앱의 모든 미디어 요소에 공통된 기능을 처리하는 데 사용할 수 있는 적응 원본 관리자 수준에서도 동일한 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="5dca2-240">각 AdaptiveSource에는 고유한 이벤트가 포함되어 있으며 모든 AdaptiveSource 이벤트가 AdaptiveSourceManager 아래에 계단식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="5dca2-241">**미디어 요소 이벤트 처리기를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="5dca2-242">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-243">**MainPage** 클래스의 끝에 다음 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="5dca2-244">**MainPage** 생성자의 끝에 다음 코드를 추가하여 이벤트를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="5dca2-245">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-246">**슬라이더 막대 관련 코드를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="5dca2-247">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-248">파일의 시작 부분에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="5dca2-249">**MainPage** 클래스 내에 다음 데이터 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="5dca2-250">**MainPage** 생성자의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="5dca2-251">**MainPage** 클래스의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="5dca2-252">CoreDispatcher는 비UI 스레드에서 UI 스레드를 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="5dca2-253">디스패처 스레드에서 병목이 발생할 경우 개발자는 업데이트하려는 UI 요소에서 제공하는 디스패처를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="5dca2-254">예:</span><span class="sxs-lookup"><span data-stu-id="5dca2-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="5dca2-255">**mediaElement_AdaptiveSourceStatusUpdated** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="5dca2-256">**MediaOpened** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="5dca2-257">**Ctrl+S** 를 눌러 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="5dca2-258">**응용 프로그램을 컴파일 및 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="5dca2-259">**F6** 키를 눌러 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="5dca2-260">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="5dca2-261">응용 프로그램 맨 위에 기본 부드러운 스트리밍 URL을 사용하거나 다른 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="5dca2-262">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="5dca2-263">슬라이더 막대를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-263">Test the slider bar.</span></span>

<span data-ttu-id="5dca2-264">단원 2를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-264">You have completed lesson 2.</span></span>  <span data-ttu-id="5dca2-265">이 단원에서는 응용 프로그램에 슬라이더를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="5dca2-266">단원 3: 부드러운 스트리밍 스트림 선택</span><span class="sxs-lookup"><span data-stu-id="5dca2-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="5dca2-267">부드러운 스트리밍은 사용자가 선택할 수 있는 여러 언어 오디오 트랙으로 콘텐츠를 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="5dca2-268">이 단원에서는 사용자가 스트림을 선택할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="5dca2-269">이 단원에는 다음 절차가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5dca2-270">XAML 파일 수정</span><span class="sxs-lookup"><span data-stu-id="5dca2-270">Modify the XAML file</span></span>
2. <span data-ttu-id="5dca2-271">코드 숨김 파일 수정</span><span class="sxs-lookup"><span data-stu-id="5dca2-271">Modify the code behand file</span></span>
3. <span data-ttu-id="5dca2-272">응용 프로그램 컴파일 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5dca2-272">Compile and test the application</span></span>

<span data-ttu-id="5dca2-273">**XAML 파일을 수정하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="5dca2-274">솔루션 탐색기에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="5dca2-275">&lt;Grid.RowDefinitions&gt;를 찾아 RowDefinitions를 다음과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="5dca2-276">사용 가능한 스트림 목록을 보고 스트림을 선택할 수 있도록 &lt;Grid&gt;&lt;/Grid&gt; 태그 안에 다음 코드를 추가하여 목록 상자 컨트롤을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="5dca2-277">**Ctrl+S** 를 눌러 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="5dca2-278">**코드 숨김 파일을 수정하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="5dca2-279">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-280">SSPlayer 네임스페이스 내에 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="5dca2-281">MainPage 클래스의 시작 부분에 다음 변수 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="5dca2-282">MainPage 클래스 내에 다음 지역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="5dca2-283">mediaElement_ManifestReady 메서드를 찾은 후 함수의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="5dca2-284">따라서 MediaElement 매니페스트가 준비되면 코드가 사용 가능한 스트림 목록을 가져오고 UI 목록 상자에 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="5dca2-285">MainPage 클래스 내에서 UI 단추 클릭 이벤트 지역을 찾은 후 다음 함수 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="5dca2-286">**응용 프로그램을 컴파일 및 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="5dca2-287">**F6** 키를 눌러 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="5dca2-288">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="5dca2-289">응용 프로그램 맨 위에 기본 부드러운 스트리밍 URL을 사용하거나 다른 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="5dca2-290">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="5dca2-291">기본 언어는 audio_eng입니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-291">The default language is audio_eng.</span></span> <span data-ttu-id="5dca2-292">audio_eng와 audio_es 간에 전환해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5dca2-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="5dca2-293">새 스트림을 선택할 때마다 제출 단추를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="5dca2-294">단원 3을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-294">You have completed lesson 3.</span></span>  <span data-ttu-id="5dca2-295">이 단원에서는 스트림을 선택하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="5dca2-296">단원 4: 부드러운 스트리밍 트랙 선택</span><span class="sxs-lookup"><span data-stu-id="5dca2-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="5dca2-297">부드러운 스트리밍 프레젠테이션에는 여러 품질 수준(비트 전송률) 및 해상도로 인코딩된 여러 비디오 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="5dca2-298">이 단원에서는 사용자가 트랙을 선택할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="5dca2-299">이 단원에는 다음 절차가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="5dca2-300">XAML 파일 수정</span><span class="sxs-lookup"><span data-stu-id="5dca2-300">Modify the XAML file</span></span>
2. <span data-ttu-id="5dca2-301">코드 숨김 파일 수정</span><span class="sxs-lookup"><span data-stu-id="5dca2-301">Modify the code behand file</span></span>
3. <span data-ttu-id="5dca2-302">응용 프로그램 컴파일 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5dca2-302">Compile and test the application</span></span>

<span data-ttu-id="5dca2-303">**XAML 파일을 수정하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="5dca2-304">솔루션 탐색기에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="5dca2-305">이름이 **gridStreamAndBitrateSelection**인 &lt;Grid&gt; 태그를 찾아 그 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="5dca2-306">**Ctrl+S** 를 눌러 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="5dca2-307">**코드 숨김 파일을 수정하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="5dca2-308">[솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="5dca2-309">SSPlayer 네임스페이스 내에 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="5dca2-310">MainPage 클래스의 시작 부분에 다음 변수 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="5dca2-311">MainPage 클래스 내에 다음 지역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="5dca2-312">mediaElement_ManifestReady 메서드를 찾은 후 함수의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="5dca2-313">MainPage 클래스 내에서 UI 단추 클릭 이벤트 지역을 찾은 후 다음 함수 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="5dca2-314">**응용 프로그램을 컴파일 및 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="5dca2-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="5dca2-315">**F6** 키를 눌러 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="5dca2-316">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="5dca2-317">응용 프로그램 맨 위에 기본 부드러운 스트리밍 URL을 사용하거나 다른 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="5dca2-318">**원본 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="5dca2-319">기본적으로 비디오 스트림의 모든 트랙이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="5dca2-320">비트 전송률 변경을 실험하려면 사용 가능한 가장 낮은 비트 전송률을 선택한 후 사용 가능한 가장 높은 비트 전송률을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="5dca2-321">각 변경 후에 제출을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-321">You must click Submit after each change.</span></span>  <span data-ttu-id="5dca2-322">비디오 품질 변경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-322">You can see the video quality changes.</span></span>

<span data-ttu-id="5dca2-323">단원 4를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-323">You have completed lesson 4.</span></span>  <span data-ttu-id="5dca2-324">이 단원에서는 트랙을 선택하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5dca2-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5dca2-325">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="5dca2-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5dca2-326">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5dca2-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="5dca2-327">기타 리소스:</span><span class="sxs-lookup"><span data-stu-id="5dca2-327">Other Resources:</span></span>
* [<span data-ttu-id="5dca2-328">고급 기능이 포함된 부드러운 스트리밍 Windows 8 JavaScript 응용 프로그램을 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="5dca2-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="5dca2-329">부드러운 스트리밍 기술 개요</span><span class="sxs-lookup"><span data-stu-id="5dca2-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

