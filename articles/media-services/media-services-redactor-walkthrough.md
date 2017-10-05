---
title: "Azure 미디어 분석으로 얼굴 편집 안내 | Microsoft Docs"
description: "이 항목에서는 AMSE(Azure Media Services 탐색기) 및 Azure Media Redactor Visualizer(오픈 소스 도구)를 사용하여 전체 교정 워크플로를 실행하는 방법에 대한 단계별 지침을 보여줍니다."
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
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="55fbf-103">Azure 미디어 분석으로 얼굴 편집 안내</span><span class="sxs-lookup"><span data-stu-id="55fbf-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="55fbf-104">개요</span><span class="sxs-lookup"><span data-stu-id="55fbf-104">Overview</span></span>

<span data-ttu-id="55fbf-105">**Azure Media Redactor** 는 클라우드에서 확장성 있는 얼굴 편집 기능을 제공하는 [Azure Media Analytics](media-services-analytics-overview.md) MP(미디어 프로세서)입니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="55fbf-106">얼굴 편집을 사용하면 선택한 개인의 얼굴을 흐리게 표시하기 위해 동영상을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="55fbf-107">공공 안전과 새 미디어 시나리오를 위해 얼굴 편집 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="55fbf-108">짧은 장면이라도 여러 명의 얼굴이 포함된 경우 수동으로 편집하려면 많은 시간이 걸릴 수 있지만 이 서비스를 사용하면 몇 번의 간단한 단계를 통해 얼굴을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="55fbf-109">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-redactor/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55fbf-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="55fbf-110">**Azure Media Redactor**에 대한 자세한 내용은 [얼굴 교정 개요](media-services-face-redaction.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55fbf-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="55fbf-111">이 항목에서는 AMSE(Azure Media Services 탐색기) 및 Azure Media Redactor Visualizer(오픈 소스 도구)를 사용하여 전체 교정 워크플로를 실행하는 방법에 대한 단계별 지침을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="55fbf-112">**Azure Media Redactor** MP는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="55fbf-113">이 기능은 모든 공용 Azure 지역과 미국 정부 및 중국 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="55fbf-114">이 미리 보기는 현재 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-114">This preview is currently free of charge.</span></span> <span data-ttu-id="55fbf-115">현재 릴리스에서 처리되는 비디오 길이는 10분으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="55fbf-116">자세한 내용은 [이 블로그](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55fbf-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="55fbf-117">Azure Media Services 탐색기 워크플로</span><span class="sxs-lookup"><span data-stu-id="55fbf-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="55fbf-118">Redactor를 시작하는 가장 쉬운 방법은 github에서 오픈 소스 AMSE 도구를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="55fbf-119">주석 json 또는 얼굴 jpg 이미지에 액세스할 필요가 없는 경우 **결합** 모드를 통해 간소화된 워크플로를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="55fbf-120">다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="55fbf-120">Download and setup</span></span>

1. <span data-ttu-id="55fbf-121">AMSE 도구를 [여기서](https://github.com/Azure/Azure-Media-Services-Explorer) 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="55fbf-122">서비스 키를 사용하여 Media Services 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="55fbf-123">계정 이름 및 키 정보를 가져오려면 [Azure Portal](https://portal.azure.com/)로 이동하여 AMS 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="55fbf-124">그런 후 설정 > 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="55fbf-125">키 관리 창에 계정 이름과 기본 및 보조 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="55fbf-126">계정 이름 및 기본 키 값을 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-126">Copy values of the account name and the primary key.</span></span>

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="55fbf-128">1 패스 – 분석 모드</span><span class="sxs-lookup"><span data-stu-id="55fbf-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="55fbf-129">자산 –> 업로드를 통해 또는 끌어서 놓기를 통해 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="55fbf-130">마우스 오른쪽 단추를 클릭하고 Media Analytics –> Azure Media Redactor –> 분석 모드를 사용하여 미디어 파일을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="55fbf-133">출력에는 얼굴 위치 데이터가 있는 주석 json 파일과 감지된 각 얼굴의 jpg가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="55fbf-135">2 패스 – 교정 모드</span><span class="sxs-lookup"><span data-stu-id="55fbf-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="55fbf-136">1 패스의 출력으로 원본 비디오 자산을 업로드하고 기본 자산으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="55fbf-138">(선택 사항) 교정하려는 ID의 줄 바꿈으로 구분된 목록이 포함된 'Dance_idlist.txt' 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="55fbf-140">(선택 사항) 경계 상자 경계를 늘리는 등, annotations.json 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="55fbf-141">1 패스의 출력 자산을 마우스 오른쪽 단추로 클릭하고 Redactor를 선택한 후 **교정** 모드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="55fbf-143">교정된 최종 출력 자산을 다운로드하거나 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-143">Download or share the final redacted output asset.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="55fbf-145">Azure Media Redactor Visualizer 오픈 소스 도구</span><span class="sxs-lookup"><span data-stu-id="55fbf-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="55fbf-146">오픈 소스 [Visualizer 도구](https://github.com/Microsoft/azure-media-redactor-visualizer)는 개발자가 주석 형식부터 시작해서 출력을 구문 분석하고 사용할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="55fbf-147">리포지토리를 복제한 후에 프로젝트를 실행하기 위해 해당 [공식 사이트](https://ffmpeg.org/download.html)에서 FFMPEG를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="55fbf-148">JSON 주석 데이터를 구문 분석하려는 개발자는 Models.MetaData 내부에서 샘플 코드 예제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="55fbf-149">도구 설정</span><span class="sxs-lookup"><span data-stu-id="55fbf-149">Set up the tool</span></span>

1.  <span data-ttu-id="55fbf-150">전체 솔루션을 다운로드하고 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-150">Download and build the entire solution.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="55fbf-152">[여기](https://ffmpeg.org/download.html)에서 FFMPEG를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="55fbf-153">이 프로젝트는 정적 링크가 있는 be1d324(2016-10-04)를 사용하여 개발되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="55fbf-154">ffmpeg.exe 및 ffprobe.exe를 AzureMediaRedactor.exe와 동일한 출력 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="55fbf-156">AzureMediaRedactor.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="55fbf-157">도구 사용</span><span class="sxs-lookup"><span data-stu-id="55fbf-157">Use the tool</span></span>

1. <span data-ttu-id="55fbf-158">분석 모드에서 Redactor MP를 사용하여 Azure Media Services 계정에서 비디오를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="55fbf-159">원본 비디오 파일 및 교정 - 분석 작업의 출력을 모두 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="55fbf-160">Visualizer 응용 프로그램을 실행하고 위의 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-160">Run the visualizer application and choose the files above.</span></span> 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="55fbf-162">파일을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-162">Preview your file.</span></span> <span data-ttu-id="55fbf-163">오른쪽의 사이드바에서 흐리게 표시하려는 얼굴을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="55fbf-165">아래쪽 텍스트 필드는 얼굴 ID로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="55fbf-166">줄 바꿈으로 구분된 이러한 ID 목록으로 "idlist.txt"라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="55fbf-167">idlist.txt는 ANSI로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="55fbf-168">ANSI로 저장하려면 메모장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="55fbf-169">1단계의 출력 자산에 이 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="55fbf-170">이 자산에도 원본 비디오를 업로드하고 기본 자산으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="55fbf-171">"Redact" 모드를 사용하여 이 자산에 대해 교정 작업을 실행하여 교정된 최종 비디오를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="55fbf-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="55fbf-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55fbf-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="55fbf-173">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="55fbf-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="55fbf-174">관련 링크</span><span class="sxs-lookup"><span data-stu-id="55fbf-174">Related links</span></span>
[<span data-ttu-id="55fbf-175">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="55fbf-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="55fbf-176">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="55fbf-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="55fbf-177">Azure Media Analytics의 얼굴 편집 발표</span><span class="sxs-lookup"><span data-stu-id="55fbf-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
