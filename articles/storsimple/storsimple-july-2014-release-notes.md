---
title: "StorSimple 8000 릴리스 버전 릴리스 정보 | Microsoft Docs"
description: "2014년 7월 Microsoft Azure StorSimple 릴리스에 대한 새 기능, 미해결 문제 및 해결 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 303cdffa15fdfe9b83d0612edecafc6943d218f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>StorSimple 8000 시리즈 릴리스 버전 릴리스 정보-2014 년 7 월
## <a name="overview"></a>개요
다음 릴리스 정보는 Microsoft Azure StorSimple의 StorSimple 8000 시리즈 2014년 7월 GA(General Availability) 릴리스에 대한 중요한 미해결 문제를 식별합니다. 이 릴리스는 6.3.9600.17215 소프트웨어 버전에 해당합니다.  

따로 지정한 경우가 아니면 이 릴리스 정보는 StorSimple 장치의 모든 모델에 적용됩니다. 릴리스 정보는 계속 업데이트 됩니다. 해결 방법이 필요한 중요 한 문제가 발견되면 추가됩니다. Microsoft Azure StorSimple 솔루션을 배포하기 전에 다음 정보를 고려합니다.  

## <a name="known-issues-in-this-release"></a>이 릴리스의 알려진 문제
다음 표에서 이 릴리스의 알려진 문제를 간략하게 설명합니다.  

| 번호 | 기능 | 문제 | 주석/해결 방법 | 실제 장치에 적용 | 가상 장치에 적용 |
| --- | --- | --- | --- | --- | --- |
| 1 |공장 재설정 |일부 경우에 공장 재설정을 수행하면 StorSimple 장치가 중단될 수 있으며 **공장 기본 설정으로 재설정 진행 중(8단계)**메시지를 표시할 수 있습니다. cmdlet가 진행 중인 동안 CTRL+C를 누르면 발생합니다. |공장 재설정을 시작한 후 CTRL+C를 누르지 마세요. 이미 이 상태에 있다면 다음 단계에 대해 Microsoft 지원에 문의하세요. |예 |아니요 |
| 2 |디스크 쿼럼 |드문 경우에 8600 장치의 EBOD 인클로저에 있는 대부분의 디스크의 연결이 끊겨 디스크 쿼럼이 없는 경우, 저장소 풀이 오프라인 상태가 됩니다. 디스크가 다시 연결되더라도 오프라인 상태로 유지됩니다. |장치를 다시 부팅해야 합니다. 문제가 지속되면 다음 단계에 대해 Microsoft 지원에 문의하세요. |예 |아니요 |
| 3 |클라우드 스냅숏 실패 |드문 경우에 클라우드 스냅숏이 **최대 백업 한계에 도달했습니다**라는 오류와 함께 실패할 수 있습니다. 삭제된 볼륨과 동일한 원래 볼륨에서 동일한 장치에 255개의 온라인 복제가 초과하는 경우 발생합니다. | |예 |예 |
| 4 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 중, 이미지가 피어 노드에서 로드되면 컨트롤러 ID는 처음에 피어 컨트롤러의 ID로 표시될 수 있습니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |별도의 작업이 필요하지 않습니다. 컨트롤러 교체를 완료 한 후 이 상황이 저절로 해결됩니다. |예 |아니요 |
| 5 |장치 모니터링 차트 |StorSimple 관리자 서비스에서 해당 장치에 대한 프록시 서버 구성에서 기본 또는 NTLM 인증이 사용되면 장치 모니터링 차트가 동작하지 않습니다. |인증이 NONE으로 설정되도록 StorSimple 관리자 서비스와 함께 등록된 장치에 대한 웹 프록시 구성을 수정합니다. 수정하려면 StorSimple Set-HcsWebProxy cmdlet에 대해 Windows PowerShell을 실행합니다. |예 |예 |
| 6 |저장소 계정 |저장소 계정 삭제에 저장소 서비스를 사용하는 것은 지원되지 않는 시나리오입니다. 이렇게 되면 사용자 데이터를 검색할 수 없게 됩니다. | |예 |예 |
| 7 |장애 복구 |DR(재해 복구) 24시간 이내 장애 복구가 지원되지 않습니다. | |예 |아니요 |
| 8 |장치 장애 조치 |동일한 원본 장치에서 다른 대상 장치로의 볼륨 컨테이너의 다중 장애 조치는 지원되지 않습니다. 단일 데드 장치에서 여러 장치로의 장애 조치로 첫 번째 장애 조치된 장치의 볼륨 컨테이너에서 데이터 소유권이 손실됩니다. 이러한 장애 조치 후 Azure 클래식 포털에서 볼 때 이 볼륨 컨테이너가 나타나거나 다르게 동작합니다. | |예 |아니요 |
| 9 |설치 |SharePoint용 StorSimple 어댑터 설치 중, 성공적으로 설치를 완료하려면 장비 IP를 입력해야 합니다. | |예 |아니요 |
| 10 |네트워크 인터페이스 |네트워크 인터페이스 데이터 2 및 데이터 3은 소프트웨어에서 전환되었습니다. |이러한 인터페이스를 구성해야 하는 경우 Microsoft 지원에 문의하세요. |예 |아니요 |

