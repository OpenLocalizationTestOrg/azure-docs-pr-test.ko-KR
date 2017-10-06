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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>어떻게 tooBuild 부드러운 스트리밍 Windows 스토어 응용 프로그램

hello 부드러운 스트리밍 클라이언트 SDK for Windows 8을 사용 하면 주문형 및 라이브 부드러운 스트리밍 콘텐츠를 재생할 수 있는 개발자 toobuild Windows 스토어 응용 프로그램입니다. 부드러운 스트리밍 콘텐츠를 hello SDK 또한의 기본적인 재생 toohello Microsoft PlayReady 보호, 품질 수준 제한 DVR, 전환, 상태 업데이트 (예: 품질 수준 변경 내용 수신 대기 하는 오디오 스트림 Live와 같은 다양 한 기능을 제공 하는 또한 ) 및 오류 이벤트 및 등입니다. 지원 되는 hello 기능의 자세한 내용은 참조 hello [릴리스 정보](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes)합니다. 자세한 내용은 [Windows 8용 플레이어 프레임워크](http://playerframework.codeplex.com/)를 참조하세요. 

이 자습서에는 4개 단원이 포함되어 있습니다.

1. 기본 부드러운 스트리밍 스토어 응용 프로그램 만들기
2. 슬라이더 tooControl hello 미디어 진행률 막대를 추가 합니다.
3. 부드러운 스트리밍 스트림 선택
4. 부드러운 스트리밍 트랙 선택

## <a name="prerequisites"></a>필수 조건
* Windows 8 32비트 또는 64비트. MSDN에서 [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) 을 다운로드할 수 있습니다.
* Visual Studio 2012 또는 Visual Studio Express 2012(또는 이후 버전). Hello에서 평가판 버전을 얻을 수 있습니다 [여기](http://www.microsoft.com/visualstudio/11/downloads)합니다.
* [Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)

각 단원 완료 hello 솔루션 MSDN 개발자 코드 샘플 (코드 갤러리)에서 다운로드할 수 있습니다. 

* [단원 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - 간단한 Windows 8 부드러운 스트리밍 미디어 플레이어 
* [단원 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - 슬라이더 막대 컨트롤이 있는 간단한 Windows 8 부드러운 스트리밍 미디어 플레이어 
* [단원 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - 스트림 선택 항목이 있는 Windows 8 부드러운 스트리밍 미디어 플레이어  
* [단원 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - 트랙 선택 항목이 있는 Windows 8 부드러운 스트리밍 미디어 플레이어

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>단원 1: 기본 부드러운 스트리밍 스토어 응용 프로그램 만들기

이 단원에서는 만들어집니다는 Windows 스토어 응용 프로그램 MediaElement 컨트롤 tooplay 부드러운 스트림을 사용 하 여 콘텐츠.  실행 중인 응용 프로그램 hello는 다음과 같습니다.

![부드러운 스트리밍 Windows 스토어 응용 프로그램 예][PlayerApplication]

Windows 스토어 응용 프로그램 개발에 대한 자세한 내용은 [유용한 Windows 8용 앱 개발](http://msdn.microsoft.com/windows/apps/br229512.aspx)을 참조하십시오. 이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.

1. Windows 스토어 프로젝트 만들기
2. Hello 사용자 인터페이스 디자인 (XAML)
3. Hello 코드 숨김 파일 수정
4. 컴파일 및 hello 응용 프로그램 테스트

**Windows 스토어 프로젝트 toocreate**

1. Visual Studio 2012 이상을 실행합니다.
2. Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
3. Hello 새 프로젝트 대화 상자에서 값 형식 또는 다음 선택 hello:

| 이름 | 값 |
| --- | --- |
| 템플릿 그룹 |Installed/Templates/Visual C#/Windows Store |
| Template |새 응용 프로그램(XAML) |
| 이름 |SSPlayer |
| 위치 |C:\SSTutorials |
| 솔루션 이름 |SSPlayer |
| 솔루션에 대한 디렉터리 만들기 |(선택됨) |

1. **확인**을 클릭합니다.

**tooadd 참조 toohello 부드러운 스트리밍 클라이언트 SDK**

1. [솔루션 탐색기]에서 **SSPlayer**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다.
2. 입력 하거나 다음 값에는 hello 선택:

| 이름 | 값 |
| --- | --- |
| 참조 그룹 |Windows/Extensions |
| 참조 |Microsoft Smooth Streaming Client SDK for Windows 8 및 Microsoft Visual C++ 런타임 패키지 선택 |

1. **확인**을 클릭합니다. 

Hello 참조를 추가한 후 hello 대상 플랫폼 (x64 또는 x86)을 선택 해야, Any CPU 플랫폼 구성에 대 한 참조 추가 작동 하지 않습니다.  솔루션 탐색기에서 추가된 이 참조에 대해 노란색 경고 표시가 나타납니다.

**toodesign hello 플레이어 사용자 인터페이스**

1. 솔루션 탐색기에서 두 번 클릭 **MainPage.xaml** tooopen hello 디자인에서 보기.
2. Hello 찾을  **&lt;그리드&gt;**  및  **&lt;/Grid&gt;**  hello 두 태그 사이 붙여넣기 hello 다음 코드 및 태그 hello XAML 파일:

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
   
   hello MediaElement 컨트롤에 사용 되는 tooplayback 미디어입니다. hello 다음 단원에서는 toocontrol hello 미디어 진행에서 sliderProgress 라는 hello 슬라이더 컨트롤 사용 됩니다.
3. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

hello MediaElement 컨트롤에는 부드러운 스트리밍 콘텐츠-기본적으로 지원 하지 않습니다. tooenable hello 부드러운 스트리밍을 지원, 파일 이름 확장명 및 MIME 형식에 따라 hello 부드러운 스트리밍 바이트 스트림 처리기를 등록 해야 합니다.  tooregister, 방법을 사용 하 여 hello MediaExtensionManager.RegisterByteStremHandler hello Windows.Media 네임 스페이스입니다.

이 XAML 파일에서 일부 이벤트 처리기 hello 컨트롤 연관 됩니다.  해당 이벤트 처리기를 정의해야 합니다.

**toomodify hello 코드 숨김 파일**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. Hello 파일의 hello 위쪽 hello 다음 추가 문을 사용 하 여:
   
        using Windows.Media;
3. Hello hello 시작 시 **MainPage** 클래스 hello 데이터 멤버를 추가 합니다.
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. Hello hello 끝나기 전에 **MainPage** 생성자 hello 다음 두 줄을 추가 합니다.
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. Hello hello 끝나기 전에 **MainPage** 클래스, hello 코드 다음에 붙여 넣습니다.
   
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

hello sliderProgress_PointerPressed 이벤트 처리기 여기에서 정의 됩니다.  더 많은 works toodo tooget는 작업 하 고, 있는에서 설명 합니다.이 자습서의 다음 단원 hello 합니다.
6. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

hello 완성 된 hello 코드 숨김 파일은 다음과 같습니다.

![부드러운 스트리밍 Windows 스토어 응용 프로그램에 대한 Visual Studio의 Codeview][CodeViewPic]

**toocompile 및 테스트 hello 응용 프로그램**

1. Hello에서 **빌드** 메뉴를 클릭 하 여 **Configuration Manager**합니다.
2. 변경 **활성 솔루션 플랫폼** toomatch 개발 플랫폼입니다.
3. 키를 눌러 **F6** toocompile hello 프로젝트. 
4. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.
5. Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다. 
6. **원본 설정**을 클릭합니다. 때문에 **자동 재생** hello 미디어를 자동으로 재생은 기본적으로 사용 됩니다.  Hello를 사용 하 여 hello 미디어를 제어할 수 있습니다 **재생**, **일시 중지** 및 **중지** 단추입니다.  Hello 세로 슬라이더를 사용 하 여 hello 미디어 볼륨을 제어할 수 있습니다.  그러나 hello 가로 슬라이더 제어 hello 미디어 진행률 완전히 아직 구현 되지 않았습니다. 

lesson1을 완성했습니다.  이 단원에서는 MediaElement 컨트롤 tooplayback 부드러운 스트리밍 콘텐츠를 사용할 수 있습니다.  Hello 다음 단원에서는 부드러운 스트리밍 콘텐츠를 hello의 슬라이더 toocontrol hello 진행률을 추가 합니다.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>2 단원: 슬라이더 tooControl hello 미디어 진행률 막대를 추가 합니다.

1 단원에서 MediaElement XAML 컨트롤 tooplayback 부드러운 스트리밍 미디어 콘텐츠를 Windows 스토어 응용 프로그램을 만들었습니다.  시작, 중지, 일시 중지 등의 기본 미디어 기능이 제공됩니다.  이 단원에서는 슬라이더 막대 컨트롤 toohello 응용 프로그램을 추가 합니다.

이 자습서에서는 hello hello MediaElement 컨트롤의 현재 위치에 따라 타이머 tooupdate hello 슬라이더 위치를 사용 합니다.  hello 슬라이더 시작 및 종료 시간도 필요 toobe 발생 한 경우 라이브 콘텐츠를 업데이트 합니다.  Hello 적응 소스 update 이벤트에 보다 잘 처리할 수 있습니다.

미디어 원본은 미디어 데이터를 생성하는 개체입니다.  hello 소스 확인자는 URL 또는 바이트 스트림을 사용 하 고 해당 콘텐츠에 대 한 hello 적절 한 미디어 소스를 만듭니다.  hello 소스 확인자는 hello 응용 프로그램 toocreate 미디어 원본에 대 한 hello 표준 방법입니다. 

이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.

1. Hello 부드러운 스트리밍 처리기를 등록 합니다. 
2. Hello 적응 소스 관리자 수준의 이벤트 처리기 추가
3. Hello 적응 소스 수준 이벤트 처리기를 추가 합니다.
4. MediaElement 이벤트 처리기 추가
5. 슬라이더 막대 관련 코드 추가
6. 컴파일 및 hello 응용 프로그램 테스트

**tooregister hello 부드러운 스트리밍 바이트 스트림 처리기와 패스 hello propertyset**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. Hello 파일 시작 부분의 hello, hello 다음 추가 문을 사용 하 여:

        using Microsoft.Media.AdaptiveStreaming;
3. Hello MainPage 클래스의 hello 맨 hello 다음 데이터 멤버를 추가 합니다.

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. 내부 hello **MainPage** 생성자 hello hello 후 코드를 다음 추가 **이 있습니다. Components(); 초기화**  줄과 hello 이전 단원에서 작성 된 hello 등록 코드 줄:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. 내부 hello **MainPage** 생성자 매개 변수 2 hello RegisterByteStreamHandler 메서드 tooadd hello 세이프 수정:

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
6. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

**tooadd hello 적응 소스 관리자 수준의 이벤트 처리기**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. 내부 hello **MainPage** 클래스 hello 데이터 멤버를 추가 합니다.
   
     private AdaptiveSource adaptiveSource = null;
3. Hello hello 끝나기 전에 **MainPage** 클래스 hello 다음 이벤트 처리기를 추가 합니다.
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. Hello hello 끝나기 전에 **MainPage** 생성자를 다음 줄 toosubscribe toohello 적응 소스 open 이벤트 hello 추가:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

**tooadd 적응 소스 수준 이벤트 처리기**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. 내부 hello **MainPage** 클래스 hello 데이터 멤버를 추가 합니다.
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. Hello hello 끝나기 전에 **MainPage** 클래스 hello 다음 이벤트 처리기를 추가 합니다.

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
4. Hello hello 끝나기 전에 **mediaElement AdaptiveSourceOpened** 메서드를 hello toosubscribe toohello 이벤트 코드를 다음 추가:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

hello 적응 소스 manger 수준에도 hello 앱의 기능 일반적인 tooall 미디어 요소를 처리 하기 위한 사용할 수 있는 동일한 이벤트를 사용할 수 있습니다. 각 AdaptiveSource에는 고유한 이벤트가 포함되어 있으며 모든 AdaptiveSource 이벤트가 AdaptiveSourceManager 아래에 계단식으로 표시됩니다.

**tooadd 미디어 요소의 이벤트 처리기**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. Hello hello 끝나기 전에 **MainPage** 클래스 hello 다음 이벤트 처리기를 추가 합니다.

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
3. Hello hello 끝나기 전에 **MainPage** 생성자 hello toosubscript toohello 이벤트 코드를 다음 추가:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

**tooadd 슬라이더 막대를 관련 된 코드**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. Hello 파일 시작 부분의 hello, hello 다음 추가 문을 사용 하 여:
      
        using Windows.UI.Core;
3. 내부 hello **MainPage** 클래스, 데이터 멤버를 다음 hello 추가:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. Hello hello 끝나기 전에 **MainPage** 생성자 코드 다음 hello 추가:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. Hello hello 끝나기 전에 **MainPage** 클래스 코드 다음 hello를 추가 합니다.

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
>CoreDispatcher은 비 UI 스레드에서 toohello UI 스레드 사용 되는 toomake 변경 합니다. 발송자 스레드의 병목 현상이 발생할 경우 개발자는 toouse 발송자 tooupdate 노드가 받지 않으려는 UI 요소에서 제공 선택할 수 있습니다.  예:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. Hello hello 끝나기 전에 **mediaElement_AdaptiveSourceStatusUpdated** 메서드를 코드 다음 hello 추가:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. Hello hello 끝나기 전에 **MediaOpened** 메서드를 코드 다음 hello 추가:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. 키를 눌러 **CTRL + S** toosave hello 파일입니다.

**toocompile 및 테스트 hello 응용 프로그램**

1. 키를 눌러 **F6** toocompile hello 프로젝트. 
2. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.
3. Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다. 
4. **원본 설정**을 클릭합니다. 
5. Hello 슬라이더 막대를 테스트 합니다.

단원 2를 완료했습니다.  이 단원에서는 슬라이더 tooapplication을 추가 했습니다. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>단원 3: 부드러운 스트리밍 스트림 선택
부드러운 스트리밍은 hello 뷰어에서 선택할 수 있는 여러 언어 오디오 트랙 사용 가능 toostream 콘텐츠입니다.  이 단원에서는 뷰어 tooselect 스트림을 설정 합니다. 이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.

1. Hello XAML 파일을 수정
2. Hello 코드 behand 파일 수정
3. 컴파일 및 hello 응용 프로그램 테스트

**toomodify hello XAML 파일**

1. 솔루션 탐색기에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.
2. 찾을 &lt;Grid.RowDefinitions&gt;, 처럼 보이는 hello RowDefinitions 수정:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. 내부 hello &lt;그리드&gt;&lt;/Grid&gt; hello 다음 코드 toodefine listbox 컨트롤 사용자가 사용할 수 있는 스트림의 hello 목록을 참조를 업데이트 하 고 스트림을 선택할 수 있으므로 태그를 추가 합니다.

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
4. 키를 눌러 **CTRL + S** toosave hello 변경 합니다.

**toomodify hello 코드 숨김 파일**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. Hello SSPlayer 네임 스페이스 내부 새 클래스를 추가 합니다.
   
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
3. Hello MainPage 클래스의 hello 맨 hello 변수 정의 뒤에 추가 합니다.
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Hello MainPage 클래스, 내부 hello 다음 영역을 추가 합니다.
   
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
5. Hello 코드 hello 함수 hello 끝에 다음 추가 hello mediaElement_ManifestReady 메서드를 찾아:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    따라서 MediaElement 매니페스트 준비 되 면 hello 코드 hello 사용 가능한 스트림의 목록을 가져옵니다 바뀌고 hello 목록 사용 하 여 hello UI 목록 상자를 채웁니다.
6. Hello MainPage 클래스, 내부 찾을 hello UI 단추 이벤트 영역을 클릭 한 다음 함수 정의 다음 hello를 추가 합니다.
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile 및 테스트 hello 응용 프로그램**

1. 키를 눌러 **F6** toocompile hello 프로젝트. 
2. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.
3. Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다. 
4. **원본 설정**을 클릭합니다. 
5. hello 기본 언어는 audio_eng입니다. Audio_eng 사이의 audio_es tooswitch 시도 하십시오. 새 스트림 선택 될 때마다, hello 전송 단추를 클릭 해야 합니다.

단원 3을 완료했습니다.  이 단원에서는 hello 기능 toochoose 스트림을 추가할 수 있습니다.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>단원 4: 부드러운 스트리밍 트랙 선택
부드러운 스트리밍 프레젠테이션에는 여러 품질 수준(비트 전송률) 및 해상도로 인코딩된 여러 비디오 파일이 포함될 수 있습니다. 이 단원에서는 사용자가 tooselect 트랙을 설정 합니다. 이 단원에서는 다음 절차를 수행 하는 hello를 포함 되어 있습니다.

1. Hello XAML 파일을 수정
2. Hello 코드 behand 파일 수정
3. 컴파일 및 hello 응용 프로그램 테스트

**toomodify hello XAML 파일**

1. 솔루션 탐색기에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.
2. Hello 찾을 &lt;그리드&gt; hello 이름의 태그 **gridStreamAndBitrateSelection**, hello 코드 hello 태그의 hello 끝에 다음 추가:
   
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
3. 키를 눌러 **CTRL + S** toosave로 변경 하 고

**toomodify hello 코드 숨김 파일**

1. [솔루션 탐색기]에서 **MainPage.xaml**을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.
2. Hello SSPlayer 네임 스페이스 내부 새 클래스를 추가 합니다.
   
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
3. Hello MainPage 클래스의 hello 맨 hello 변수 정의 뒤에 추가 합니다.
   
        private List<Track> availableTracks;
4. Hello MainPage 클래스, 내부 hello 다음 영역을 추가 합니다.
   
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
5. Hello 코드 hello 함수 hello 끝에 다음 추가 hello mediaElement_ManifestReady 메서드를 찾아:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Hello MainPage 클래스, 내부 찾을 hello UI 단추 이벤트 영역을 클릭 한 다음 함수 정의 다음 hello를 추가 합니다.
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile 및 테스트 hello 응용 프로그램**

1. 키를 눌러 **F6** toocompile hello 프로젝트. 
2. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.
3. Hello 응용 프로그램의 hello 위쪽 hello 기본 부드러운 스트리밍 URL을 사용 하거나 다른 이름을 입력 합니다. 
4. **원본 설정**을 클릭합니다. 
5. 기본적으로 hello 비디오 스트림의 hello 트랙의 모든 선택 됩니다. tooexperiment hello 비트 전송률 변경 hello 가장 낮은 비트 전송률을 사용할 수를 선택 하 고 hello 가장 높은 비트 전송률 사용할 수 있는 다음 선택 합니다. 각 변경 후에 제출을 클릭해야 합니다.  Hello 비디오 품질 변경 내용을 볼 수 있습니다.

단원 4를 완료했습니다.  이 단원에서는 hello 기능 toochoose 트랙 추가할 수 있습니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>기타 리소스:
* [어떻게 toobuild 부드러운 스트리밍 Windows 8 JavaScript 응용 프로그램을 고급 기능](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [부드러운 스트리밍 기술 개요](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

