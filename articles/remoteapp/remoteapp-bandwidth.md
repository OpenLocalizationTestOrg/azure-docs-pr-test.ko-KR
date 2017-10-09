---
title: "Azure RemoteApp 네트워크 대역폭 사용량 aaaEstimate | Microsoft Docs"
description: "Azure RemoteApp 컬렉션 및 앱에 대 한 hello 네트워크 대역폭 요구 사항에 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Azure RemoteApp 네트워크 대역폭 사용량 예측
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp hello Azure 클라우드 및 사용자가 실행 중인 응용 프로그램 간의 프로토콜 RDP (원격 데스크톱) toocommunicate hello를 사용 합니다. 이 문서에서는 네트워크 사용량 및 잠재적으로 Azure RemoteApp 사용자 당 네트워크 대역폭 사용량을 평가 하는 몇 가지 기본 지침 tooestimate를 사용할 수 있습니다.

사용자당 대역폭 사용량 예측은 매우 복잡하며, 멀티태스킹 시나리오에서 여러 응용 프로그램을 실행해야 합니다. 이 경우 응용 프로그램은 네트워크 대역폭 수요에 따라 서로의 성능에 영향을 줄 수 있습니다. 원격 데스크톱 클라이언트 (예: Mac 클라이언트 HTML5 클라이언트 및)에 hello 유형의 toodifferent 대역폭 결과 초래할 수 있습니다. 이러한 복잡성을 진행할 때는 toohelp, 일반적인 일부의 hello 범주 tooreplicate 실제 시나리오에 hello 사용 시나리오를 분석할 수 있습니다. (여기서 hello 실제 업무 시나리오, 물론, 다양 한 범주 및 사용자에 따라 다릅니다.)

RDP 좋은 tooexcellent 환경을 제공 대부분 사용 시나리오에 대 한 네트워크 대역폭 및 120 m 아래 대기 시간으로 5 개 Mb-이 RDP의 능력 toodynamically 기반 가정 하는 hello 사용 가능한 네트워크를 사용 하 여 조정 추가-진행 하기 전에 대역폭 및 hello 응용 프로그램 대역폭 요구를 예상 합니다. 이 문서는 "대부분 사용 시나리오" toolook hello 경계 면 시나리오 toounwind 시작 하 고 사용자 환경을 시작 toodegrade 위치 이외의 이동 합니다.

이제 다음 요인 tooconsider, 초기 권장 사항 및 기능을 포함 하지 않았습니다 예측 결과에 포함 하는 hello 세부 정보에 대 한 아티클을 hello 확인해 보세요.

* [네트워크 대역폭과 환경 품질을 함께 작동하는 방식은 무엇인가요?](remoteapp-bandwidthexperience.md)
* [몇 가지 일반적 시나리오로 네트워크 대역폭 사용량 테스트](remoteapp-bandwidthtests.md)
* [빠른 지침 hello 시간 또는 기능 tootest 없는 경우](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>포함하지 않은 항목
테스트 및 전반적인 (및 일반 인정) 권장 되는 제안 된 hello를 검토할 때는 것으로 간주 되지 않은 여러 가지 요소는 수입니다. 예를 들어 hello hello 업로드 및 다운로드 대역폭의 비대칭 특성에서 제공 하는 사용자 경험 복잡 합니다. 대부분의 Wi-fi 네트워크의 비대칭 특성 hello hello 성능과 hello 사용자 경험에 대 한 인식 또한 영향을 줍니다. 대화형 시나리오에 대 한 hello 다운스트림 트래픽 우선 순위가 더 미만의 hello 업스트림 되 hello 손실된 비디오 또는 오디오 프레임 수가 증가 하 고 따라서 hello 사용자가 경험 스트리밍 hello 인식에 영향을 수 있습니다. 가 특정 사용 사례 및 네트워크에 대해 사용자 고유의 실험 toosee를 실행할 수 있습니다.

장치 리디렉션 설명, 않지만 म 고려 하지 않은 연결 된 장치, 저장소, 프린터, 스캐너, 웹 카메라, 및 기타 USB 장치 등으로 인해 발생 하는 네트워크 트래픽의 hello의 hello 대역폭 영향을 고려 합니다. 일반적으로 이러한 장치의 hello 효과 hello는 대역폭 요구를 일시적으로 급증 하 고 hello 작업이 완료 될 때. 그러나 자주 수행되는 경우 대역폭 수요가 상당히 증가할 수 있습니다.

또한 다루지 않습니다 방법을 한 명의 사용자 hello에 따라 다른 사용자에 영향을 줄 수 같은 네트워크입니다. 예를 들어 60MB/s 네트워크 4k 비디오를 사용 하는 한 명의 사용자 크게 영향을 줄 다른 toodo 시도 동일한 네트워크의 사용자가 동일한 작업 hello 합니다. 불행 하 게도 점진적으로 쉽다는 점 toodetermine hello 영향의 동시 사용량 toogive hello 시스템 집계에서 수행 하는 방법에 대 한 공용 또는 포괄적인 권장 사항을 가져옵니다. 기본 프로토콜 기술 hello hello hello 사용 가능한 네트워크 대역폭의 사용에 가장 적합 하면 있지만 한계는 말할 수 됩니다.

