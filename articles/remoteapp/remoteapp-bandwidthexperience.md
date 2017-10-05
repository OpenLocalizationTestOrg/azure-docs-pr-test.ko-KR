---
title: "Azure RemoteApp - 네트워크 대역폭과 환경 품질을 함께 작동하는 방식은 무엇인가요? | Microsoft Docs"
description: "Azure RemoteApp의 네트워크 대역폭이 사용자 환경의 품질에 미칠 수 있는 영향을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 74116902e973fba440b3c662fdf76202d052b4c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - 네트워크 대역폭과 환경 품질을 함께 작동하는 방식은 무엇인가요?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
> 
> 

Azure RemoteApp에 필요한 [전체 네트워크 대역폭](remoteapp-bandwidth.md)을 확인할 때 다음 요소를 염두에 두어야 합니다. 이러한 요소는 모두 전반적인 사용자 환경에 영향을 주는 동적 시스템의 일부입니다. 

* **사용 가능한 네트워크 대역폭 및 현재 네트워크 상태** - 주어진 시간에 동일한 네트워크의 매개 변수 집합(손실, 대기 시간, 지터)은 응용 프로그램 스트리밍 환경에 영향을 줄 수 있습니다. 즉, 전반적인 사용자 환경을 저하시킬 수 있습니다. 네트워크에서 사용할 수 있는 대역폭은 정체, 임의 손실 및 대기 시간에 따라 다릅니다. 이러한 매개 변수는 모두 충돌을 방지하기 위해 전송 속도를 제어하는 정체 제어 메커니즘에 영향을 주기 때문입니다.  예를 들어, 손실된 네트워크 또는 대기 시간이 긴 네트워크는 1000MB 대역폭의 네트워크에서도 사용자 환경을 저하시킵니다. 손실 및 대기 시간은 동일한 네트워크에 있는 사용자 수 및 이러한 사용자가 수행하는 작업(예: 비디오 시청, 대용량 파일 다운로드 또는 업로드, 인쇄)에 따라 다릅니다.
* **사용 시나리오** - 사용자가 동일한 네트워크에서 개별적으로 수행하는 작업 및 그룹으로 수행하는 작업에 따라 환경이 다릅니다. 예를 들어 하나의 슬라이드를 읽을 때는 단일 프레임만 업데이트하면 되지만, 사용자가 텍스트 문서 내용을 스크롤하는 경우에는 초당 많은 수의 프레임을 업데이트해야 합니다. 이 시나리오에서 서버와 주고받는 통신은 더 많은 네트워크 대역폭을 소비합니다. 여러 사용자가 고화질 비디오(예: 4K 해상도)를 시청하거나, HD 전화 회의를 하거나, 3D 비디오 게임을 즐기거나, CAD 시스템에서 작업하는 등의 극단적인 예도 고려해야 합니다. 이 모든 시나리오에서는 고대역폭 네트워크도 실제로 사용하지 못하게 될 수 있습니다.
* **화면 해상도 및 화면 수** - 큰 화면을 전체 업데이트하려면 작은 화면보다 더 많은 네트워크 대역폭이 필요합니다. 기본 기술은 업데이트된 화면의 영역만 인코딩하고 전송하는 데 적절하므로 가끔 전체 화면을 업데이트해야 합니다. 사용자에게 더 높은 해상도의 화면(예: 4K 해상도)이 있는 경우 업데이트에 낮은 해상도의 화면(예: 1024x768px)보다 더 많은 네트워크 대역폭이 필요합니다. 이와 동일한 논리는 리디렉션에 둘 이상의 화면을 사용하는 경우에 적용됩니다. 화면 수에 따라 대역폭을 늘려야 합니다.
* **클립보드 및 장치 리디렉션** - 이는 매우 명확한 문제이지만 대부분의 경우 사용자가 많은 양의 데이터를 저장할 때는 이 정보를 원격 데스크톱 클라이언트에서 서버로 전송하는 데 시간이 오래 걸립니다. 클립보드 내용을 보내는 업스트림 환경으로 인해 다운스트림 환경이 영향을 받을 수 있습니다. 장치 리디렉션도 마찬가지입니다. 스캐너 또는 웹 캠에서 업스트림을 서버로 전송해야 하는 많은 데이터를 생성하거나, 프린터에서 대용량 문서를 받아야 하거나, 대용량을 파일을 복사하기 위해 클라우드에서 실행되는 앱에 로컬 저장소를 사용할 수 있어야 하는 경우 장치 리디렉션에 필요한 데이터로 인해 네트워크 대역폭 수요가 증가하기 때문에 프레임이 손실되거나 비디오가 일시적으로 "고정"될 수 있습니다. 

네트워크 대역폭 수요를 평가할 때 시스템으로 작동하는 이 모든 요소를 고려해야 합니다.

이제 [주 네트워크 대역폭 문서](remoteapp-bandwidth.md)로 돌아가거나 [네트워크 대역폭](remoteapp-bandwidthtests.md) 테스트를 진행합니다.

## <a name="learn-more"></a>자세한 정보
* [Azure RemoteApp 네트워크 대역폭 사용량 예측](remoteapp-bandwidth.md)
* [Azure RemoteApp - 몇 가지 일반적 시나리오로 네트워크 대역폭 사용량 테스트](remoteapp-bandwidthtests.md)
* [Azure RemoteApp 네트워크 대역폭 - 일반적인 지침(자체 테스트를 수행할 수 없는 경우)](remoteapp-bandwidthguidelines.md)

