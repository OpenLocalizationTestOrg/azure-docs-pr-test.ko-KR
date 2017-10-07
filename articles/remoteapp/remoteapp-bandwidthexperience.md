---
title: "-RemoteApp aaaAzure 어떻게 네트워크 대역폭 및 품질 발생지 않습니다 작업 함께? | Microsoft Docs"
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
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - 네트워크 대역폭과 환경 품질을 함께 작동하는 방식은 무엇인가요?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Hello에 찾을 때 [전체 네트워크 대역폭](remoteapp-bandwidth.md) 유의 hello 요소 다음에 Azure RemoteApp에 대 한 필요한-영향 hello 전반적인 사용자 환경이 있는지 동적 시스템의 모든 일부입니다. 

* **사용 가능한 네트워크 대역폭 및 현재 네트워크 상태** -매개 변수 (손실, 대기 시간, 지터)에 지정된 된 시간에 동일한 네트워크 hello 집합이 hello 응용 프로그램 스트리밍 환경이, 낮아진된 전반적인 사용자 환경이 의미 영향을 줄 수 있습니다. 네트워크에서 사용할 수 있는 hello 대역폭은 이러한 모든 매개이 변수에 영향을 주므로 hello 정체 제어 메커니즘을 설정 컨트롤에는 전송 속도 tooavoid 충돌 hello 정체, 임의 손실, 대기 시간 함수.  예를 들어, 손실 네트워크 또는 네트워크 대기 시간이 긴 하면 hello 사용자 환경이 잘못 되었습니다. 1000MB 대역폭이 있는 네트워크에도 있습니다. hello 연결 끊김 및 지연과 hello hello에 있는 사용자 수에 따라 다릅니다. 동일한 네트워크 및 해당 사용자가 수행 하는 작업 (예: 감시 하는 비디오, 다운로드 또는 인쇄 큰 파일을 업로드) 합니다.
* **사용 시나리오 마다** -hello 경험 hello 사용자가 수행 하는 개인 및 hello에 그룹으로 동일한 의존 네트워크입니다. 예를 들어 한 슬라이드를 읽으려면; 업데이트 하는 단일 한 프레임 toobe만 hello 사용자 skims hello 내용의 텍스트 문서를 통해 스크롤 하는 경우 더 높은 수가 프레임 toobe 초당 업데이트 해야 합니다. 다시 통신 hello이 고이 시나리오에서 toohello 서버를 더 많은 네트워크 대역폭을 결국 세이프 사용할 합니다. 여러 사용자가 고화질 비디오(예: 4K 해상도)를 시청하거나, HD 전화 회의를 하거나, 3D 비디오 게임을 즐기거나, CAD 시스템에서 작업하는 등의 극단적인 예도 고려해야 합니다. 이 모든 시나리오에서는 고대역폭 네트워크도 실제로 사용하지 못하게 될 수 있습니다.
* **화면 해상도 및 hello 수 화면** -더 많은 네트워크 대역폭을 필요한 toofull 보다 작은 화면 보다 큰 화면 업데이트 합니다. hello 기본 기술은 인코딩 및 전송의 업데이트 된 hello 화면 hello 영역만의 효율적인 작업을 수행 하지만 가끔, hello 전체 화면 toobe 업데이트 합니다. Hello 사용자가 더 높은 해상도 화면 (예: 4k 해상도)을 사용 하는 경우 해당 업데이트는 화면 (예: 1024x768px) 더 낮은 해상도에 비해 더 많은 네트워크 대역폭이 필요 합니다. 이와 동일한 논리는 리디렉션에 둘 이상의 화면을 사용하는 경우에 적용됩니다. 대역폭 tooincrease hello 화면 수가 필요합니다.
* **장치 및 클립보드 리디렉션** -이 매우 명확한 원인 에서부터 문제 하지만 대부분의 경우에서 사용자는 대용량 데이터 toohello 클립보드에 저장 하는 경우 걸리는 시간의 hello 원격 데스크톱 클라이언트에서 해당 정보 tootransfer 비트 toohello 서버입니다. hello 다운스트림 경험 업스트림 hello 클립보드 내용을 보내는 hello 경험에 영향을 받을 수 있습니다. hello 장치 리디렉션-에 대 한 경우 마찬가지 스캐너 또는 웹캠의 많은 전송 toobe 업스트림 toohello 서버 해야 하는 데이터를 생성 합니다. 또는 프린터 tooreceive 큰 문서에 필요 하거나 로컬 저장소 hello 클라우드 toocopy에서 실행 중인 toobe tooan 사용할 수 있는 앱을 큰 파일을 사용자가 눈에 띄지 프레임이 떨어지지 또는 일시적으로 "고정 된" 비디오 hello 장치 리디렉션에 필요한 hello 데이터는 hello 네트워크 대역폭을 증가 하기 때문에 필요 합니다. 

네트워크 대역폭 요구를 평가할 때 확인 되었는지 tooconsider 이러한 모든 요소는 시스템에 따라 작동 합니다.

이제 돌아가서 toohello [주 네트워크 대역폭 문서](remoteapp-bandwidth.md), tootesting에서 이동 또는 프로그램 [네트워크 대역폭](remoteapp-bandwidthtests.md)합니다.

## <a name="learn-more"></a>자세한 정보
* [Azure RemoteApp 네트워크 대역폭 사용량 예측](remoteapp-bandwidth.md)
* [Azure RemoteApp - 몇 가지 일반적 시나리오로 네트워크 대역폭 사용량 테스트](remoteapp-bandwidthtests.md)
* [Azure RemoteApp 네트워크 대역폭 - 일반적인 지침(자체 테스트를 수행할 수 없는 경우)](remoteapp-bandwidthguidelines.md)

