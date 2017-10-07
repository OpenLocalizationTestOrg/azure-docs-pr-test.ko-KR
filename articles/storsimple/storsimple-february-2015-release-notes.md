---
title: "8000 aaaStorSimple 업데이트 0.3 릴리스 정보 | Microsoft Docs"
description: "2015 년 2 월 hello 새로운 기능 및 수정, 미해결 문제 및 hello에 대 한 사용 가능한 해결 방법에 설명 Microsoft Azure StorSimple 릴리스 (업데이트 0.3)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>StorSimple 8000 시리즈 업데이트 0.3 릴리스 정보 - 2015년 2월
## <a name="overview"></a>개요
hello 다음 릴리스 정보는 StorSimple 8000 시리즈 업데이트 0.3 2015 년 2 월에에서 출시에 대 한 hello 중요 한 미해결 문제를 식별 합니다. 또한이 릴리스에 포함 된 펌웨어 업데이트 및 hello StorSimple 소프트웨어 목록이 포함 됩니다. 이 hello StorSimple 8000 시리즈 릴리스 버전은 2014 년 7 월에서에서 일반적으로 사용할 수 있는 변경 된 후 hello 세 번째 릴리스입니다.

이 업데이트 hello 년 1 월 업데이트에서 hello 장치 소프트웨어 버전을 변경 하지 않습니다. Toobe 버전 6.3.9600.17312 계속 유지 됩니다. Hello를 확인 하 여 해당 hello 업데이트가 설치 되었는지 확인할 수 있습니다 **마지막 업데이트** 날짜입니다. Hello 날짜가 2015 년 2 월 10 일 이상 이면 다음 hello 업데이트 설치 되었습니다.  

StorSimple 장치를 설치한 후 즉시 사용 가능한 업데이트를 검색하고 적용하는 것이 좋습니다. 자동 업데이트 toodownload 설정 수 있고 릴리스될 때 Microsoft에서 우선 순위가 높은 업데이트를 설치할 수도 있습니다. 자세한 내용은 [StorSimple 장치 업데이트](storsimple-update-device.md)를 참조하세요.  

Hello 릴리스 노트 hello를 배포 하기 전에 StorSimple 솔루션의 업데이트에 포함 된 hello 정보를 검토 하십시오.  

> [!IMPORTANT]
> * StorSimple tooinstall hello 년 2 월 업데이트에 대 한 hello StorSimple Manager 서비스 및 Windows PowerShell이 아닌를 사용 합니다.   
> * 이 업데이트는 약 1 시간 tooinstall이 필요합니다. 그러나 누적 업데이트를 설치 하는 경우 hello 프로세스 시간 toocomplete 3 번 정도 걸릴 수 있습니다.  
> * hello StorSimple 2 월 릴리스에 모든 업데이트 toohello StorSimple 가상 장치입니다. 모든 사용 가능한 Windows 업데이트 toohello 가상 장치에 적용할 수 있습니다, 최근 보안 포함 하지만 수정, 표시 되지 않습니다 hello 가상 장치에 대 한 버전의 변경 합니다.  
> 
> 

해당 hello 있는지 확인 다음 필수 구성 요소는 이전 met tooupdating StorSimple 장치입니다.  

* 업데이트를 검색하기 전에 두 장치 컨트롤러가 모두 실행되고 있는지 확인합니다. 컨트롤러 중 하나가 실행 되지 않는 경우 hello 검색이 실패 합니다. hello 컨트롤러는 정상 상태에 있는 tooverify 너무 이동**하드웨어 상태** hello에서 **유지 관리** 페이지. **주의가 필요한**구성 요소가 있는 경우, 더 진행하기 전에 Microsoft 지원에 문의합니다.
* 모두 컨트롤러 0과 컨트롤러 1의 고정된 Ip 라우팅할 수 있고 hello 업데이트 toohello 장치를 서비스에 대해 사용 되는 이러한 toohello 인터넷에 연결할 수 있는지 확인 합니다. Hello를 사용할 수 있습니다 [Test-connection cmdlet](https://technet.microsoft.com/library/hh849808.aspx) tooping 컨트롤러 hello tooverify outlook.com과 같은 hello 네트워크 외부의 알려진된 주소 연결 toohello 네트워크 외부에 있습니다.
* 80 및 443 포트가 아웃바운드 통신을 위한 StorSimple 장치에서 사용할 수 있는지 확인합니다. 자세한 내용은 참조 hello [StorSimple 장치의 네트워킹 요구 사항](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)합니다.
* Hello 장치 소프트웨어 버전 6.3.9600.17312 (2014 년 10 월 업데이트) 보다 오래 된 경우 hello 업데이트를 시작 하기 전에 사용 하는 경우 hello 데이터 2 및 Data 3 포트를 사용 하지 않도록 설정 합니다. Hello 데이터 2 또는 데이터 3 포트를 hello 업데이트를 적용할 때 사용 된 종료를 복구 모드로 장치 컨트롤러 toogo를 발생할 수 있습니다. Hello 네트워크 인터페이스를 해제 하면 모든 hello 연결 된 볼륨을 오프 라인으로 설정한 및 hello hello 업데이트 기간에 대 한 hello I/o가 중단 note 하십시오.  

## <a name="whats-new-in-hello-february-release"></a>Hello 년 2 월 릴리스의 새로운 기능
이 업데이트에는 hello hello GA 릴리스 toohello 2014 년 10 월 릴리스를에서 업그레이드 하는 장치에서 발생 한 공장 재설정 문제에 대 한 수정 포함 되어 있습니다. 자세한 내용은 참조 [이 릴리스에서 수정된 문제](#issues-fixed-in-the-february-release)를 참조하세요.   

이 업데이트에는 새로운 특징 또는 기능은 포함되지 않습니다.  

## <a name="issues-fixed-in-hello-february-release"></a>Hello 2 월 릴리스에서 해결 된 문제
hello 다음 표에 hello 해결 된 문제에이 업데이트에 있습니다.  

| 아니요. | 기능 | 문제 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- |
| 1 |공장 재설정 |시키면 tooperform hello GA 릴리스 (버전 6.3.9600.17215)에 원래 있던 장치에서 공장 재설정 설치 되었지만 업데이트 된 toohello 년 10 월 릴리스 (버전 6.3.9600.17312) 되었습니다. hello 공장 재설정이 실패 하 고 hello 장치 불안정 합니다. |예 |아니요 |

## <a name="known-issues-in-hello-february-release"></a>Hello 년 2 월 릴리스의 알려진된 문제
다음 표에서 hello이이 릴리스의 알려진된 문제에에서 대 한 요약을 제공 합니다.

| 아니요. | 기능 | 문제 | 주석/해결 방법 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- | --- |
| 1 |공장 재설정 |경우에 따라 공장 재설정을 수행할 때 StorSimple 장치 hello 남아 있을 수 있습니다 및이 메시지를 표시: **재설정 toofactory가 진행 중인 (8 단계)**합니다. 이 hello cmdlet이 진행 중일 동안 CTRL + C를 누르면 발생 합니다. |공장 재설정을 시작한 후 CTRL+C를 누르지 마세요. 이미 이 상태에 있다면 다음 단계에 대해 Microsoft 지원에 문의하세요. |예 |아니요 |
| 2 |디스크 쿼럼 |경우에 따라에서 hello 대부분의 디스크는 8600device hello EBOD 인클로저에 있는 끊어져서 디스크 쿼럼이 없게 하는 경우 다음 hello 저장소 풀이 오프 라인 상태가 됩니다. Hello 디스크가 다시 연결 하는 경우에 오프 라인으로 유지 됩니다. |Tooreboot hello 장치가 필요 합니다. Hello 문제가 지속 되 면 Microsoft 지원에 다음 단계에 문의 하세요. |예 |아니요 |
| 3 |클라우드 스냅숏 실패 |클라우드 스냅숏 드물게에서 hello 오류가 발생할 수 있습니다 **최대 백업 한계 도달**합니다. Hello에서 온라인 복제가 255 개를 초과 하는 경우이 경고가 발생 hello에서 동일한 장치 삭제 된 동일한 원래 볼륨입니다. | |예 |예 |
| 4 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 하는 동안 hello 이미지 hello 피어 노드에서 로드 되 면 hello 컨트롤러 ID 수 처음으로 나타나도록 hello 피어 컨트롤러의 id입니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |별도의 작업이 필요하지 않습니다. 이 경우 hello 컨트롤러 교체를 완료 한 후 자체적으로 해결 됩니다. |예 |아니요 |
| 5 |장치 모니터링 차트 |StorSimple Manager 서비스 hello, 기본 hello 장치 모니터링 차트가 작동 하지 않습니다 또는 hello 장치에 대 한 hello 프록시 서버 구성에서 NTLM 인증을 사용 합니다. |StorSimple Manager 서비스로 등록 인증을 tooNONE 설정 되므로 hello 장치에 대 한 hello 웹 프록시 구성을 수정 합니다. toodo StorSimple Set-hcswebproxy cmdlet에 대 한 실행된 hello hello Windows PowerShell이 합니다. |예 |예 |
| 6 |저장소 계정 |Hello 저장소 서비스 toodelete hello 저장소 계정을 사용 하는 지원 되지 않는 시나리오입니다. 이렇게 하면 tooa 상황 사용자 데이터를 검색할 수 없습니다. | |예 |예 |
| 7 |장치 장애 조치 |다중에서 동일한 원본 장치 toodifferent 대상 장치는 지원 되지 않습니다 hello는 볼륨 컨테이터의 장애 조치 합니다.    단일 데드 장치 toomultiple 장치에서 장애 조치에는 먼저 장애 장치 조치 hello 장치의 hello 볼륨 컨테이너가 데이터 소유권을 잃게 생성 됩니다. 이러한 장애 조치 후 이러한 볼륨 컨테이너 나타나거나 hello Azure 클래식 포털에서에서 볼 때 다르게 동작 합니다. | |예 |아니요 |
| 8 |설치 |SharePoint 용 StorSimple 어댑터를 하는 동안 필요한 tooprovide hello 설치 toofinish 위해에서 장치 IP 성공적으로 합니다. | |예 |아니요 |
| 9 |웹 프록시 |웹 프록시 구성에 있으면 hello로는 HTTPS 프로토콜을 지정 다음 장치를 서비스 통신 영향을 받고 hello 장치는 오프 라인 상태가 유지 됩니다. 지원 패키지도 장치에서 많은 리소스를 소모 hello 프로세스에서 생성 됩니다. |지정한 프로토콜이 hello으로 hello 웹 프록시 URL에 HTTP 있는지 확인 합니다. 방법에 대 한 자세한 내용은 너무[장치에 대 한 웹 프록시 구성](storsimple-configure-web-proxy.md)합니다. |예 |아니요 |
| 10 |웹 프록시 |구성 하 고 등록된 된 장치에서 웹 프록시를 사용 하는 경우 장치에서 toorestart hello 활성 컨트롤러가 필요 합니다. | |예 |아니요 |
| 11 |긴 클라우드 대기 시간 및 많은 I/O 작업 |StorSimple 장치 매우 긴 클라우드 대기 시간 (초) 및 높은 수준의 I/O 작업의 조합을 발견 하면 hello 장치 볼륨 상태가 저하 및 hello I/o "장치가 준비 되지 않음" 오류가 발생할 수 있습니다. |Toomanually 재부팅 hello 장치 컨트롤러 필요 하거나이 상황에서 장치 장애 조치 toorecover를 수행 합니다. |예 |아니요 |

## <a name="physical-device-updates-in-hello-february-release"></a>Hello 년 2 월 릴리스에서 물리적 장치 업데이트
이 업데이트 수정 hello 공장 재설정 문제 hello GA 릴리스 toohello 2014 년 10 월 릴리스를에서 업그레이드 하는 장치에서 발생 합니다. 다른 업데이트 toohello StorSimple 장치는 포함 되지 않습니다.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Serial attached SCSI (SAS) 컨트롤러 및 펌웨어 업데이트 hello 년 2 월 릴리스에서
이 릴리스에서 모든 업데이트 toohello serial attached SCSI (SAS) 컨트롤러 또는 펌웨어 hello 없습니다. hello 10 월, 2014 릴리스의 hello 드라이버 업데이트가 했습니다.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Hello 년 2 월 릴리스에서 가상 장치 업데이트
이 릴리스에서 hello 가상 장치에 대 한 업데이트 합니다. 이 업데이트를 적용 하는 경우에 가상 장치의 소프트웨어 버전 hello 변경 되지 않습니다.

