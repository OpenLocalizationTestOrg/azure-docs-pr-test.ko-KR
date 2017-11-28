---
title: "Azure Media Services를 사용하여 라이브 스트리밍을 수행하여 .NET으로 다중 비트 전송률 스트림을 만드는 방법 | Microsoft Docs"
description: "이 자습서에서는 .NET SDK를 사용하여 단일 비트 전송률 라이브 스트림을 받아서 다중 비트 전송률 스트림으로 인코딩하는 채널을 만드는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22d63ff5e9fd33db8711b0c5125ab0882b9f6a74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-using-azure-media-services-to-create-multi-bitrate-streams-with-net"></a><span data-ttu-id="f1851-103">Azure 미디어 서비스를 사용하여 라이브 스트리밍을 수행하여 .NET으로 다중 비트 스트림을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f1851-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1851-104">포털</span><span class="sxs-lookup"><span data-stu-id="f1851-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="f1851-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f1851-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="f1851-106">REST API</span><span class="sxs-lookup"><span data-stu-id="f1851-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="f1851-107">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="f1851-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="f1851-109">개요</span><span class="sxs-lookup"><span data-stu-id="f1851-109">Overview</span></span>
<span data-ttu-id="f1851-110">이 자습서에서는 단일 비트 전송률 라이브 스트림을 받아서 다중 비트 전송률 스트림으로 인코딩하는 **채널** 을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-110">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span></span>

<span data-ttu-id="f1851-111">라이브 인코딩에 대해 사용할 수 있는 채널과 관련하여 더욱 개념적인 정보는 [Azure 미디어 서비스를 사용하여 다중 비트 전송률 스트림을 만드는 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-111">For more conceptual information related to Channels that are enabled for live encoding, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="f1851-112">일반적인 라이브 스트리밍 시나리오</span><span class="sxs-lookup"><span data-stu-id="f1851-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="f1851-113">다음 단계에서는 일반적인 라이브 스트리밍 응용 프로그램을 만드는 데 포함되는 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-113">The following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="f1851-114">현재 라이브 이벤트의 최대 권장 기간은 8시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-114">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="f1851-115">더 오랜 시간 채널을 실행해야 하는 경우 amslived@microsoft.com으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-115">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="f1851-116">비디오 카메라를 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-116">Connect a video camera to a computer.</span></span> <span data-ttu-id="f1851-117">RTMP, 부드러운 스트리밍 또는 RTP(MPEG-TS) 프로토콜 중 하나에서 단일 비트 전송률 스트림을 출력할 수 있는 온-프레미스 라이브 인코더를 시작하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="f1851-118">자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="f1851-119">이 단계는 채널을 만든 후에도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="f1851-120">채널을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="f1851-121">채널 수집 URL을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-121">Retrieve the Channel ingest URL.</span></span>

    <span data-ttu-id="f1851-122">수집 URL은 스트림을 채널로 보내기 위해 라이브 인코더를 통해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-122">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>

4. <span data-ttu-id="f1851-123">채널 미리 보기 URL을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-123">Retrieve the Channel preview URL.</span></span>

    <span data-ttu-id="f1851-124">이 URL을 사용하여 채널이 라이브 스트림을 제대로 받고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-124">Use this URL to verify that your channel is properly receiving the live stream.</span></span>

5. <span data-ttu-id="f1851-125">자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-125">Create an asset.</span></span>
6. <span data-ttu-id="f1851-126">재생하는 동안 자산을 동적으로 암호화하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-126">If you want for the asset to be dynamically encrypted during playback, do the following:</span></span>
7. <span data-ttu-id="f1851-127">콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-127">Create a content key.</span></span>
8. <span data-ttu-id="f1851-128">콘텐츠 키의 인증 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-128">Configure the content key's authorization policy.</span></span>
9. <span data-ttu-id="f1851-129">자산 배달 정책(동적 패키징 및 동적 암호화에서 사용)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="f1851-130">프로그램을 만들고 만들어진 자산을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-130">Create a program and specify to use the asset that you created.</span></span>
11. <span data-ttu-id="f1851-131">주문형 로케이터를 만들어 프로그램과 관련된 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-131">Publish the asset associated with the program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f1851-132">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="f1851-133">콘텐츠를 스트리밍하려는 스트리밍 끝점이 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-133">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

12. <span data-ttu-id="f1851-134">스트리밍 및 보관을 시작할 준비가 되었으면 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-134">Start the program when you are ready to start streaming and archiving.</span></span>
13. <span data-ttu-id="f1851-135">필요에 따라 라이브 인코더는 광고를 시작하라는 신호를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-135">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="f1851-136">광고는 출력 스트림에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-136">The advertisement is inserted in the output stream.</span></span>
14. <span data-ttu-id="f1851-137">이벤트 스트리밍 및 보관을 중지할 때마다 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-137">Stop the program whenever you want to stop streaming and archiving the event.</span></span>
15. <span data-ttu-id="f1851-138">프로그램을 삭제하고 필요에 따라 자산을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-138">Delete the Program (and optionally delete the asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f1851-139">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="f1851-139">What you'll learn</span></span>
<span data-ttu-id="f1851-140">이 항목에서는 Media Services .NET SDK를 사용하여 채널과 프로그램에 대한 다양한 작업을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-140">This topic shows you how to execute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="f1851-141">많은 작업이 오래 실행되기 때문에 오래 실행되는 작업을 관리하는 .NET API가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="f1851-142">이 항목에서는 다음을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-142">The topic shows how to do the following:</span></span>

1. <span data-ttu-id="f1851-143">채널을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-143">Create and start a channel.</span></span> <span data-ttu-id="f1851-144">오래 실행되는 API가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="f1851-145">채널 수집(입력) 끝점을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-145">Get the channels ingest (input) endpoint.</span></span> <span data-ttu-id="f1851-146">이 끝점은 단일 비트 전송률 라이브 스트림을 보낼 수 있는 인코더에 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-146">This endpoint should be provided to the encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="f1851-147">미리 보기 끝점을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-147">Get the preview endpoint.</span></span> <span data-ttu-id="f1851-148">이 끝점은 스트림을 미리 보는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-148">This endpoint is used to preview your stream.</span></span>
4. <span data-ttu-id="f1851-149">콘텐츠를 저장하는 데 사용할 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-149">Create an asset that will be used to store your content.</span></span> <span data-ttu-id="f1851-150">자산 배달 정책도 이 예와 같이 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-150">The asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="f1851-151">프로그램을 만들고 이전에 만든 자산을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-151">Create a program and specify to use the asset that was created earlier.</span></span> <span data-ttu-id="f1851-152">프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-152">Start the program.</span></span> <span data-ttu-id="f1851-153">오래 실행되는 API가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="f1851-154">자산의 로케이터를 만들어 콘텐츠가 게시되고 클라이언트로 스트리밍될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-154">Create a locator for the asset, so the content gets published and can be streamed to your clients.</span></span>
7. <span data-ttu-id="f1851-155">슬레이트를 표시하고 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-155">Show and hide slates.</span></span> <span data-ttu-id="f1851-156">광고를 시작하고 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-156">Start and stop advertisements.</span></span> <span data-ttu-id="f1851-157">오래 실행되는 API가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="f1851-158">채널과 모든 연결된 리소스를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-158">Clean up your channel and all the associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1851-159">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f1851-159">Prerequisites</span></span>
<span data-ttu-id="f1851-160">자습서를 완료하는 데 필요한 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-160">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="f1851-161">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f1851-161">An Azure account.</span></span> <span data-ttu-id="f1851-162">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f1851-163">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="f1851-164">유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-164">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="f1851-165">크레딧을 모두 사용한 후에도 계정을 유지하고 무료 Azure 서비스 및 기능(예: Azure 앱 서비스의 웹앱 기능)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-165">Even after the credits are used up, you can keep the account and use free Azure services and features, such as the Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="f1851-166">미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="f1851-166">A Media Services account.</span></span> <span data-ttu-id="f1851-167">Media Services 계정을 만들려면 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-167">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="f1851-168">Visual Studio 2010 SP1(Professional, Premium, Ultimate 또는 Express) 이상 버전.</span><span class="sxs-lookup"><span data-stu-id="f1851-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="f1851-169">미디어 서비스 .NET SDK 버전 3.2.0.0 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="f1851-170">단일 비트 전송률 라이브 스트림을 보낼 수 있는 웹캠 및 인코더.</span><span class="sxs-lookup"><span data-stu-id="f1851-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="f1851-171">고려 사항</span><span class="sxs-lookup"><span data-stu-id="f1851-171">Considerations</span></span>
* <span data-ttu-id="f1851-172">현재 라이브 이벤트의 최대 권장 기간은 8시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-172">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="f1851-173">더 오랜 시간 채널을 실행해야 하는 경우 amslived@microsoft.com으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-173">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
* <span data-ttu-id="f1851-174">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f1851-175">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-175">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f1851-176">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1851-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="f1851-177">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="f1851-177">Download sample</span></span>

<span data-ttu-id="f1851-178">[여기](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)에서 이 항목에 설명된 샘플을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-178">You can download the sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="f1851-179">.NET용 미디어 서비스 SDK를 사용한 개발을 위한 설정</span><span class="sxs-lookup"><span data-stu-id="f1851-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="f1851-180">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-180">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="f1851-181">코드 예제</span><span class="sxs-lookup"><span data-stu-id="f1851-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // The channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use the previewEndpoint to preview and verify 
            // that the input from the encoder is actually reaching the Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of the live feed as it reaches the Channel. 
            // This can be a valuable tool to check whether your live feed is actually reaching the Channel. 
            // The thumbnail is exposed via the same end-point as the Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if the channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set to StreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order to be able to publish and stream the video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with the channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting to track ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, the operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created entity Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the entity Id associated with the sucessful operation is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle the failure. 
                // For example, throw an exception. 
                // Use the following information in the exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="f1851-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1851-182">Next step</span></span>
<span data-ttu-id="f1851-183">미디어 서비스 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f1851-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f1851-184">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f1851-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


