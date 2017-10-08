---
title: "aaaAzure RemoteApp 네트워크 대역폭-일반적인 지침 | Microsoft Docs"
description: "Azure RemoteApp 컬렉션 및 앱에 대한 몇 가지 기본 네트워크 대역폭 지침을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="a83a0-103">Azure RemoteApp 네트워크 대역폭 - 일반적인 지침(자체 테스트를 수행할 수 없는 경우)</span><span class="sxs-lookup"><span data-stu-id="a83a0-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a83a0-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a83a0-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a83a0-106">Hello 시간 또는 용량 toorun hello 있는지 [대역폭 테스트 네트워크](remoteapp-bandwidthtests.md) 은 사용자 당 네트워크 대역폭을 예측 하는 데 도움이 되는 몇 가지 매우 일반적인 지침 여기 Azure RemoteApp에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="a83a0-107">이러한 시나리오를 혼합 하 여, 있는 경우 권장 됩니다 아무 것도 보다 작거나 (을) 10MB/s 원격 환경에서 인터넷에 연결 된 최신 앱에 대 한 최소 네트워크 대역폭을 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="a83a0-108">이는 평균 사용자 환경보다 더 나은 환경을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="a83a0-109">복잡한 PowerPoint, 단순한 PowerPoint</span><span class="sxs-lookup"><span data-stu-id="a83a0-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="a83a0-110">Azure RemoteApp은 100MB LAN에서 가장 효율적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="a83a0-111">hello 10MB/s 네트워크 프로필을 120 ms 위에 지터 이상 5%, hello 사용자 때 평균 경험 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="a83a0-112">1 m B/초 hello에 다른는 명백한-예를 들어, 슬라이드 쇼에서, 프레임은 생략 hello 사용자 전환 애니메이션된을 전혀 표시 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="a83a0-113">Internet Explorer, 혼합된 PDF, PDF, 텍스트</span><span class="sxs-lookup"><span data-stu-id="a83a0-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="a83a0-114">10 MB/s 네트워크 프로필은 대부분의 측면에서 닫기 tooLAN입니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="a83a0-115">1 m B/초 있을 수 있지만 일부 지터 스크롤할 hello 화면에 이미지 상태일 때 확인 된 경험을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="a83a0-116">Flash 비디오(YouTube)</span><span class="sxs-lookup"><span data-stu-id="a83a0-116">Flash video (YouTube)</span></span>
<span data-ttu-id="a83a0-117">10MB/s는 허용 가능한 (의미 hello 프레임 속도를 따라갈 म 하지만 증가 지터) 100MB/s LAN hello 최고의 사용 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="a83a0-118">1MB/s에서는 지터가 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="a83a0-119">Word 입력(Word 원격 입력)</span><span class="sxs-lookup"><span data-stu-id="a83a0-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="a83a0-120">낮은 대역폭을 사용하는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="a83a0-121">256KB/s에서 LAN만큼 적절한 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a83a0-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a83a0-122">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a83a0-122">Learn more</span></span>
* [<span data-ttu-id="a83a0-123">Azure RemoteApp 네트워크 대역폭 사용량 예측</span><span class="sxs-lookup"><span data-stu-id="a83a0-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="a83a0-124">Azure RemoteApp - 네트워크 대역폭과 환경 품질을 함께 작동하는 방식은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="a83a0-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="a83a0-125">Azure RemoteApp - 몇 가지 일반적인 시나리오로 네트워크 대역폭 사용량 테스트</span><span class="sxs-lookup"><span data-stu-id="a83a0-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

