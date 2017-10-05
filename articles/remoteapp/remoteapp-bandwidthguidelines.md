---
title: "Azure RemoteApp 네트워크 대역폭 - 일반 지침 | Microsoft 문서"
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
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="8e18b-103">Azure RemoteApp 네트워크 대역폭 - 일반적인 지침(자체 테스트를 수행할 수 없는 경우)</span><span class="sxs-lookup"><span data-stu-id="8e18b-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8e18b-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8e18b-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="8e18b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8e18b-106">Azure RemoteApp에 대한 [네트워크 대역폭 테스트](remoteapp-bandwidthtests.md) 를 실행할 시간 또는 능력이 없는 경우 사용자당 네트워크 대역폭을 예측하는 데 도움이 될 수 있는 일반적인 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="8e18b-107">이러한 시나리오가 혼합된 경우에는 원격 환경의 최신 인터넷 연결 앱에 대해 10MB/s 이하는 최소 네트워크 대역폭으로 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="8e18b-108">이는 평균 사용자 환경보다 더 나은 환경을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="8e18b-109">복잡한 PowerPoint, 단순한 PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8e18b-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="8e18b-110">Azure RemoteApp은 100MB LAN에서 가장 효율적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="8e18b-111">10MB/s 네트워크 프로필에서 120밀리초가 넘는 지터가 5%를 초과하는 경우 평균적인 사용자 환경이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="8e18b-112">1MB/s에서는 다릅니다. 예를 들어 슬라이드 쇼에서 프레임을 건너뛰어 애니메이션된 전환이 보이지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="8e18b-113">Internet Explorer, 혼합된 PDF, PDF, 텍스트</span><span class="sxs-lookup"><span data-stu-id="8e18b-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="8e18b-114">10MB/s 네트워크 프로필은 대부분의 측면에서 LAN에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="8e18b-115">1MB/s는 화면에 이미지가 있는 경우 사용자가 스크롤할 때 일부 지터가 발생할 수 있지만 정상적인 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="8e18b-116">Flash 비디오(YouTube)</span><span class="sxs-lookup"><span data-stu-id="8e18b-116">Flash video (YouTube)</span></span>
<span data-ttu-id="8e18b-117">100MB/s LAN은 최상의 환경을 제공하고, 10MB/s는 허용되는 환경(즉, 프레임 속도를 유지하지만 지터가 증가함)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="8e18b-118">1MB/s에서는 지터가 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="8e18b-119">Word 입력(Word 원격 입력)</span><span class="sxs-lookup"><span data-stu-id="8e18b-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="8e18b-120">낮은 대역폭을 사용하는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="8e18b-121">256KB/s에서 LAN만큼 적절한 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e18b-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="8e18b-122">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="8e18b-122">Learn more</span></span>
* [<span data-ttu-id="8e18b-123">Azure RemoteApp 네트워크 대역폭 사용량 예측</span><span class="sxs-lookup"><span data-stu-id="8e18b-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="8e18b-124">Azure RemoteApp - 네트워크 대역폭과 환경 품질을 함께 작동하는 방식은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8e18b-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="8e18b-125">Azure RemoteApp - 몇 가지 일반적인 시나리오로 네트워크 대역폭 사용량 테스트</span><span class="sxs-lookup"><span data-stu-id="8e18b-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

