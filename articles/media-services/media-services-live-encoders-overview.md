---
title: "Azure Media Services를 사용하여 다중 비트 전송률 스트림을 만들 때 온-프레미스 인코더 구성 | Microsoft Docs"
description: "이 토픽에서는 추가 처리를 위해 라이브 이벤트를 캡처하고 단일 비트 전송률 라이브 스트림을 AMS 채널(라이브 인코딩 사용)로 보내는 데 사용할 수 있는 온-프레미스 라이브 인코더를 나열합니다. 토픽은 나열된 인코더의 구성 방법을 보여 주는 자습서에 연결합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0ec6f046-0841-4673-9057-883bdbc30d5c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 68aaf0fda2e60c5736ab020c15e516144e11d68e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-on-premises-encoders-when-using-azure-media-services-to-create-multi-bitrate-streams"></a><span data-ttu-id="80508-104">Azure Media Services를 사용할 때 온-프레미스 인코더를 구성하여 다중 비트 전송률 스트림을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="80508-104">How to configure on-premises encoders when using Azure Media Services to create multi-bitrate streams</span></span>
<span data-ttu-id="80508-105">이 토픽에서는 추가 처리를 위해 라이브 이벤트를 캡처하고 단일 비트 전송률 라이브 스트림을 AMS 채널(라이브 인코딩 사용)로 보내는 데 사용할 수 있는 온-프레미스 라이브 인코더를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="80508-105">This topic lists on-premises live encoders that you can use to capture your live events and send a single bitrate live stream to AMS channels (that are live encoding enabled) for further processing.</span></span> <span data-ttu-id="80508-106">또한 나열된 인코더의 구성 방법을 보여 주는 자습서에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80508-106">The topic also links to tutorials that show how to configure listed encoders.</span></span>

## <a name="elemental-live"></a><span data-ttu-id="80508-107">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="80508-107">Elemental Live</span></span>
<span data-ttu-id="80508-108">단일 비트 전송률 라이브 스트림을 AMS 채널로 전송하도록 [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) 인코더를 구성하는 방법에 대한 정보는 [Elemental Live 구성](media-services-configure-elemental-live-encoder.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80508-108">For information on how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate live stream to an AMS Channel, see [Configuring Elemental Live](media-services-configure-elemental-live-encoder.md).</span></span>

## <a name="flash-media-live-encoder"></a><span data-ttu-id="80508-109">Flash Media Live Encoder</span><span class="sxs-lookup"><span data-stu-id="80508-109">Flash Media Live Encoder</span></span>
<span data-ttu-id="80508-110">단일 비트 전송률 라이브 스트림을 AMS 채널로 전송하도록 [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html)(FMLE) 인코더를 구성하는 방법에 대한 정보는 [FMLE 구성](media-services-configure-fmle-live-encoder.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80508-110">For information on how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate live stream to an AMS Channel, see [Configuring FMLE](media-services-configure-fmle-live-encoder.md) .</span></span>

## <a name="telestream-wirecast"></a><span data-ttu-id="80508-111">Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="80508-111">Telestream Wirecast</span></span>
<span data-ttu-id="80508-112">단일 비트 전송률 라이브 스트림을 AMS 채널로 전송하도록 [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) 인코더를 구성하는 방법에 대한 정보는 [Wirecast 구성](media-services-configure-wirecast-live-encoder.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80508-112">For information on how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) encoder to send a single bitrate live stream to an AMS Channel, see [Configuring Wirecast](media-services-configure-wirecast-live-encoder.md).</span></span>

## <a name="newtek-tricaster"></a><span data-ttu-id="80508-113">NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="80508-113">NewTek TriCaster</span></span>
<span data-ttu-id="80508-114">단일 비트 전송률 라이브 스트림을 AMS 채널로 전송하도록 [Tricaster](http://newtek.com/products/tricaster-40.html) 인코더를 구성하는 방법에 대한 정보는 [Tricaster 구성](media-services-configure-tricaster-live-encoder.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80508-114">For information on how to configure the [Tricaster](http://newtek.com/products/tricaster-40.html) encoder to send a single bitrate live stream to an AMS Channel, see [Configuring Tricaster](media-services-configure-tricaster-live-encoder.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="80508-115">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="80508-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="80508-116">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="80508-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="80508-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="80508-117">See also</span></span>
<span data-ttu-id="80508-118">[Azure 미디어 서비스를 사용하여 다중 비트 전송률 스트림을 만드는 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)</span><span class="sxs-lookup"><span data-stu-id="80508-118">[Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

