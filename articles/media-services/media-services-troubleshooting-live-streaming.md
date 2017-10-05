---
title: "라이브 스트리밍 문제 해결 가이드 | Microsoft Docs"
description: "이 토픽에서는 라이브 스트리밍 문제를 해결하는 방법에 대한 제안을 제공합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="812e9-103">라이브 스트리밍 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="812e9-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="812e9-104">이 토픽에서는 일부 라이브 스트리밍 문제를 해결하는 방법에 대한 제안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="812e9-105">온-프레미스 인코더와 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="812e9-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="812e9-106">이 섹션에서는 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내도록 구성된 온-프레미스 인코더와 관련된 문제를 해결하는 방법에 대한 제안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="812e9-107">문제: 로그를 참조하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="812e9-108">**잠재적인 문제**: 문제를 디버그할 때 도움이 될 만한 인코더 로그를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="812e9-109">**Telestream Wirecast**: 보통 C:\Users\{username}\AppData\Roaming\Wirecast\에서 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="812e9-110">**Elemental Live**: 관리 포털에서 로그에 대한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="812e9-111">**통계**, **로그**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="812e9-112">**로그 파일** 페이지에 모든 LiveEvent 항목에 대한 로그의 목록이 표시됩니다. 현재 세션과 일치하는 로그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="812e9-113">**Flash Media Live Encoder**: **Encoding 로그** 탭으로 이동하여 **로그 디렉터리...**를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="812e9-114">문제: 점진적 스트림을 출력하기 위한 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="812e9-115">**잠재적인 문제**: 사용 중인 인코더가 자동으로 디인터레이스하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="812e9-116">**문제해결 단계**: 인코더 인터페이스 내에서 디인터레이스 옵션을 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="812e9-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="812e9-117">디인터레이스를 사용하도록 설정한 후 다시 점진적 출력 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="812e9-118">문제: 여러 인코더 출력 설정을 시도했는데 여전히 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="812e9-119">**잠재적인 문제**: Azure 인코딩 채널이 올바르게 다시 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="812e9-120">**문제 해결 단계**: 인코더가 더 이상 AMS에 푸시하지 않는지 확인하고 채널을 중지한 다음 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="812e9-121">다시 실행한 후 새 설정으로 인코더를 연결해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="812e9-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="812e9-122">여전히 문제가 해결되지 않으면 새 채널을 전체적으로 다시 만들어 보십시오. 때에 따라 여러 번 시도가 실패한 후 채널이 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="812e9-123">**잠재적인 문제**: GOP 크기 또는 키프레임 설정이 최적의 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="812e9-124">**문제 해결 단계**: 권장 GOP 크기 또는 키프레임 간격은 2초입니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="812e9-125">일부 인코더는 이 설정을 프레임 단위로 계산하는 반면, 다른 인코더는 초를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="812e9-126">예: 30fps를 출력할 때 GOP 크기는 60 프레임이며, 이는 2초와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="812e9-127">**잠재적인 문제**: 닫힌 포트가 스트림을 차단하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="812e9-128">**문제 해결 단계**: RTMP 통해 스트리밍할 때 방화벽 및/또는 프록시 설정을 점검하여 아웃바운드 포트 1935 및 1936이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="812e9-129">RTP 스트리밍을 사용하는 경우 아웃바운드 포트 2010이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="812e9-130">문제: RTP 프로토콜을 사용하여 인코더를 스트림으로 구성하면 호스트 이름을 입력할 장소가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="812e9-131">**잠재적인 문제**: 많은 인코더는 호스트 이름에 허용되지 않으며 IP 주소를 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="812e9-132">**문제 해결 단계**: IP 주소를 찾으려면 모든 컴퓨터에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="812e9-133">Windows에서 이 작업을 수행하려면 실행 시작 관리자(WIN + R)를 열고 "cmd"를 입력하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="812e9-134">명령 프롬프트를 연 후에 "Ping [AMS 호스트 이름]"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="812e9-135">호스트 이름은 다음 예제에서 강조한 것처럼 Azure Ingest URL에서 포트 번호를 생략하여 파생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812e9-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="812e9-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="812e9-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="812e9-138">문제 해결 단계를 수행한 후에도 여전히 성공적으로 스트리밍되지 않으면 Azure Portal을 사용하여 지원 티켓을 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="812e9-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="812e9-139">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="812e9-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="812e9-140">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="812e9-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

