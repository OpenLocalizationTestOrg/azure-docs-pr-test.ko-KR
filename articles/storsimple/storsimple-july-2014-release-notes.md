---
title: "8000 aaaStorSimple 릴리스 버전 릴리스 정보 | Microsoft Docs"
description: "2014 년 7 월 hello 새로운 기능, 미해결 문제 및 hello에 대 한 사용 가능한 해결 방법에 설명 Microsoft Azure StorSimple 릴리스 합니다."
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
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>StorSimple 8000 시리즈 릴리스 버전 릴리스 정보-2014 년 7 월
## <a name="overview"></a>개요
hello 다음 릴리스 정보 hello hello StorSimple 8000 시리즈에 대 한 중요 한 미해결 문제를 식별 합니다. Microsoft Azure StorSimple의 2014 년 7 월 GA (일반 공급) 릴리스 합니다. 이 릴리스에서 toosoftware 버전 6.3.9600.17215에 해당 합니다.  

이러한 릴리스 정보를 지정 하지 않으면 hello StorSimple 장치의 tooall 모델을 적용 합니다. hello 릴리스 정보는 계속 업데이트 됩니다. 해결 방법이 필요한 중요 한 문제가 발견 되 면 추가 됩니다. Microsoft Azure StorSimple 솔루션을 배포 하기 전에 hello 다음 정보를 고려 합니다.  

## <a name="known-issues-in-this-release"></a>이 릴리스의 알려진 문제
다음 표에서 hello이이 릴리스의 알려진된 문제에에서 대 한 요약을 제공 합니다.  

| 아니요. | 기능 | 문제 | 주석/해결 방법 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- | --- |
| 1 |공장 재설정 |경우에 따라 공장 재설정을 수행할 때 StorSimple 장치 hello 남아 있을 수 있습니다 및이 메시지를 표시: **재설정 toofactory가 진행 중인 (8 단계)**합니다. 이 hello cmdlet이 진행 중일 동안 CTRL + C를 누르면 발생 합니다. |공장 재설정을 시작한 후 CTRL+C를 누르지 마세요. 이미 이 상태에 있다면 다음 단계에 대해 Microsoft 지원에 문의하세요. |예 |아니요 |
| 2 |디스크 쿼럼 |경우에 따라에서 hello 대부분의 디스크 8600 장치의 EBOD 인클로저에 hello 끊어져서 디스크 쿼럼이 없게 하는 경우 다음 hello 저장소 풀이 오프 라인 상태가 됩니다. Hello 디스크가 다시 연결 하는 경우에 오프 라인으로 유지 됩니다. |Tooreboot hello 장치가 필요 합니다. Hello 문제가 지속 되 면 Microsoft 지원에 다음 단계에 문의 하세요. |예 |아니요 |
| 3 |클라우드 스냅숏 실패 |클라우드 스냅숏 드물게에서 hello 오류가 발생할 수 있습니다 **최대 백업 한계 도달**합니다. Hello에서 온라인 복제가 255 개를 초과 하는 경우이 경고가 발생 hello에서 동일한 장치 삭제 된 동일한 원래 볼륨입니다. | |예 |예 |
| 4 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 하는 동안 hello 이미지 hello 피어 노드에서 로드 되 면 hello 컨트롤러 ID 수 처음으로 나타나도록 hello 피어 컨트롤러의 id입니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |별도의 작업이 필요하지 않습니다. 이 경우 hello 컨트롤러 교체를 완료 한 후 자체적으로 해결 됩니다. |예 |아니요 |
| 5 |장치 모니터링 차트 |StorSimple Manager 서비스 hello, 기본 hello 장치 모니터링 차트가 작동 하지 않습니다 또는 hello 장치에 대 한 hello 프록시 서버 구성에서 NTLM 인증을 사용 합니다. |StorSimple Manager 서비스로 등록 인증을 tooNONE 설정 되므로 hello 장치에 대 한 hello 웹 프록시 구성을 수정 합니다. toodo StorSimple Set-hcswebproxy cmdlet에 대 한 실행된 hello hello Windows PowerShell이 합니다. |예 |예 |
| 6 |저장소 계정 |Hello 저장소 서비스 toodelete hello 저장소 계정을 사용 하는 지원 되지 않는 시나리오입니다. 이렇게 하면 tooa 상황 사용자 데이터를 검색할 수 없습니다. | |예 |예 |
| 7 |장애 복구 |DR(재해 복구) 24시간 이내 장애 복구가 지원되지 않습니다. | |예 |아니요 |
| 8 |장치 장애 조치 |다중에서 동일한 원본 장치 toodifferent 대상 장치는 지원 되지 않습니다 hello는 볼륨 컨테이터의 장애 조치 합니다. 단일 데드 장치 toomultiple 장치에서 장애 조치에는 먼저 장애 장치 조치 hello 장치의 hello 볼륨 컨테이너가 데이터 소유권을 잃게 생성 됩니다. 이러한 장애 조치 후 이러한 볼륨 컨테이너 나타나거나 hello Azure 클래식 포털에서에서 볼 때 다르게 동작 합니다. | |예 |아니요 |
| 9 |설치 |SharePoint 용 StorSimple 어댑터를 하는 동안 필요 tooprovide 장치 IP hello 설치 toofinish 성공적으로 합니다. | |예 |아니요 |
| 10 |네트워크 인터페이스 |네트워크 인터페이스 DATA 2 및 DATA 3 hello 소프트웨어에서 교체 되었습니다. |이러한 인터페이스 tooconfigure 필요한 경우 Microsoft 지원에 문의 하세요. |예 |아니요 |

