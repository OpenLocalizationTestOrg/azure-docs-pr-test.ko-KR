---
title: "Azure 미디어 분석 연습을 aaaRedact 면 | Microsoft Docs"
description: "이 항목에서는 방법에 단계별 지침을 보여 줍니다. toorun Azure 미디어 서비스 탐색기 (AMSE) 및 Azure 미디어 Redactor 시각화 도우미 (오픈 소스 도구)를 사용 하 여 전체 교정 워크플로 합니다."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="50e71-103">Azure 미디어 분석으로 얼굴 편집 안내</span><span class="sxs-lookup"><span data-stu-id="50e71-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="50e71-104">개요</span><span class="sxs-lookup"><span data-stu-id="50e71-104">Overview</span></span>

<span data-ttu-id="50e71-105">**Azure 미디어 Redactor** 는 [Azure 미디어 분석](media-services-analytics-overview.md) hello 클라우드에서 확장 가능한 글꼴 교정에서 제공 하는 미디어 프로세서 (MP).</span><span class="sxs-lookup"><span data-stu-id="50e71-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="50e71-106">Face 교정 있습니다 toomodify 선택한 개인의 순서 tooblur 면에서 비디오를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="50e71-107">공용 안전과 뉴스 미디어 시나리오에서 toouse hello 얼굴 교정 서비스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="50e71-108">몇 분 정도 여러 글꼴로 포함 된 장면 시간 tooredact 수동으로 필요로 하지만이 서비스 hello 모양을 가진 교정 프로세스는 몇 가지 간단한 단계만 거치면 요구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="50e71-109">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-redactor/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50e71-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="50e71-110">에 대 한 세부 정보에 대 한 **Azure 미디어 Redactor**, hello 참조 [얼굴 교정 개요](media-services-face-redaction.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="50e71-111">이 항목에서는 방법에 단계별 지침을 보여 줍니다. toorun Azure 미디어 서비스 탐색기 (AMSE) 및 Azure 미디어 Redactor 시각화 도우미 (오픈 소스 도구)를 사용 하 여 전체 교정 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="50e71-112">hello **Azure 미디어 Redactor** MP는 현재 미리 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="50e71-113">이 기능은 모든 공용 Azure 지역과 미국 정부 및 중국 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="50e71-114">이 미리 보기는 현재 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-114">This preview is currently free of charge.</span></span> <span data-ttu-id="50e71-115">Hello 현재 릴리스에서 처리 된 비디오 길이 제한은 10 분은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="50e71-116">자세한 내용은 [이 블로그](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50e71-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="50e71-117">Azure Media Services 탐색기 워크플로</span><span class="sxs-lookup"><span data-stu-id="50e71-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="50e71-118">hello 가장 쉬운 방법은 tooget 시작 Redactor는 github에서 toouse hello 오픈 소스 AMSE 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="50e71-119">통해 간단한 워크플로 실행할 수 있습니다 **결합** toohello 주석 json 또는 hello 얼굴 jpg 이미지에 액세스할 필요 하지 않는 경우에 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="50e71-120">다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="50e71-120">Download and setup</span></span>

1. <span data-ttu-id="50e71-121">Hello AMSE 도구를 다운로드할 [여기](https://github.com/Azure/Azure-Media-Services-Explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="50e71-122">Tooyour 서비스 키를 사용 하 여 미디어 서비스 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="50e71-123">계정 이름 및 키 정보, 이동 toohello tooobtain hello [Azure 포털](https://portal.azure.com/) AMS 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="50e71-124">그런 후 설정 > 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="50e71-125">hello 관리 키 windows hello 계정 이름을 표시 하 고 hello 기본 및 보조 키 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="50e71-126">Hello 계정 이름 및 hello 기본 키의 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-126">Copy values of hello account name and hello primary key.</span></span>

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="50e71-128">1 패스 – 분석 모드</span><span class="sxs-lookup"><span data-stu-id="50e71-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="50e71-129">자산 –> 업로드를 통해 또는 끌어서 놓기를 통해 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="50e71-130">마우스 오른쪽 단추를 클릭하고 Media Analytics –> Azure Media Redactor –> 분석 모드를 사용하여 미디어 파일을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="50e71-133">hello 출력은 검색 된 각 면의 jpg 뿐만 아니라 얼굴 위치 데이터를 사용 하는 주석 json 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="50e71-135">2 패스 – 교정 모드</span><span class="sxs-lookup"><span data-stu-id="50e71-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="50e71-136">Hello 첫 번째 패스에서 출력 하 고 기본 자산으로 설정 하 여 원래 비디오 자산 toohello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="50e71-138">(선택 사항) 줄 바꿈 구분 된 목록이 hello tooredact 원하는 Id 포함 하는 'Dance_idlist.txt' 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="50e71-140">(선택 사항) 모든 편집 내용이 toohello annotations.json 파일을 늘리는 등 hello 경계 상자 경계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="50e71-141">Hello 첫 번째 패스에서 hello 출력 자산을 마우스 오른쪽 단추로 클릭 하 고 hello Redactor, 선택 hello를 사용 하 여 실행 **Redact** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="50e71-143">다운로드 하거나 hello 최종 교정된 출력 자산을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-143">Download or share hello final redacted output asset.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="50e71-145">Azure Media Redactor Visualizer 오픈 소스 도구</span><span class="sxs-lookup"><span data-stu-id="50e71-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="50e71-146">오픈 소스 [시각화 도우미 도구](https://github.com/Microsoft/azure-media-redactor-visualizer) 디자인 된 toohelp 개발자가 구문 분석 한 hello 출력을 사용 하 여 hello 주석 형식으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="50e71-147">Toodownload FFMPEG 할 순서 toorun hello 프로젝트에서 hello 리포지토리를 복제 한 후에서 자신의 [공식 사이트](https://ffmpeg.org/download.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="50e71-148">샘플 코드 예제에 대 한 JSON 주석 데이터 tooparse hello 시도 개발자 인 경우 Models.MetaData 내부 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="50e71-149">Hello 도구 설정</span><span class="sxs-lookup"><span data-stu-id="50e71-149">Set up hello tool</span></span>

1.  <span data-ttu-id="50e71-150">다운로드 하 고 hello 전체 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="50e71-150">Download and build hello entire solution.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="50e71-152">[여기](https://ffmpeg.org/download.html)에서 FFMPEG를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="50e71-153">이 프로젝트는 정적 링크가 있는 be1d324(2016-10-04)를 사용하여 개발되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="50e71-154">Ffmpeg.exe 및 ffprobe.exe toohello 복사 AzureMediaRedactor.exe 동일한 출력 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="50e71-156">AzureMediaRedactor.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="50e71-157">Hello 도구 사용</span><span class="sxs-lookup"><span data-stu-id="50e71-157">Use hello tool</span></span>

1. <span data-ttu-id="50e71-158">분석 모드 hello Redactor MP로 Azure 미디어 서비스 계정에서 비디오를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="50e71-159">원본 비디오 파일 hello와 hello 교정의 hello 출력을 다운로드 하-작업을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="50e71-160">Hello 시각화 도우미 응용 프로그램을 실행 하 고 위의 hello 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="50e71-162">파일을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-162">Preview your file.</span></span> <span data-ttu-id="50e71-163">선택 하면 향하도록 것인지 hello에 hello 사이드바 통해 tooblur 오른쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="50e71-165">hello 아래쪽 텍스트 필드는 hello 글꼴 Id로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="50e71-166">줄 바꿈으로 구분된 이러한 ID 목록으로 "idlist.txt"라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="50e71-167">hello idlist.txt은 ANSI에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="50e71-168">Ansi에서 메모장 toosave를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="50e71-169">1 단계에서이 파일 toohello 출력 자산을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="50e71-170">Hello 원래 비디오 toothis 자산으로 업로드 하 고 기본 자산으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="50e71-171">이 자산 "Redact" 모드 tooget hello 최종 교정 비디오 교정 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50e71-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="50e71-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50e71-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="50e71-173">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="50e71-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="50e71-174">관련 링크</span><span class="sxs-lookup"><span data-stu-id="50e71-174">Related links</span></span>
[<span data-ttu-id="50e71-175">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="50e71-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="50e71-176">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="50e71-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="50e71-177">Azure Media Analytics의 얼굴 편집 발표</span><span class="sxs-lookup"><span data-stu-id="50e71-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
