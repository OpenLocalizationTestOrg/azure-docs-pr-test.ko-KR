---
title: "8000 aaaStorSimple 업데이트 0.1 릴리스 정보 | Microsoft Docs"
description: "Hello 새로운 기능 및 수정 프로그램, 미해결 문제 및 가능한 해결 방법을 설명 hello에 대 한 2014 년 10 월 Microsoft Azure StorSimple 릴리스 (업데이트 0.1)."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>StorSimple 8000 시리즈 업데이트 0.1 릴리스 정보-2014 년 10 월
## <a name="overview"></a>개요
hello 다음 릴리스 정보는 StorSimple 8000 시리즈 업데이트 0.1 2014 년 10 월에에서 출시에 대 한 hello 중요 한 미해결 문제를 식별 합니다. 또한이 릴리스에 포함 된 펌웨어 업데이트 및 hello StorSimple 소프트웨어 목록이 포함 됩니다. Hello StorSimple 8000 시리즈 릴리스 버전으로 2014 년 7 월에서에서 일반적으로 제공 된 및 toosoftware 버전 6.3.9600.17312에 해당 하는 후 첫 번째 릴리스에서 hello입니다.  

검색할 hello 장치를 설치한 후에 즉시 사용 가능한 업데이트를 적용 하는 것이 좋습니다. 자동 업데이트 toodownload 설정 수 있고 릴리스될 때 Microsoft에서 우선 순위가 높은 업데이트를 설치할 수도 있습니다. 자세한 내용은 참조 방법을 너무[StorSimple 장치 업데이트](storsimple-update-device.md)합니다.  

StorSimple 솔루션에 hello 업데이트를 배포 하기 전에 hello 릴리스 정보에 포함 된 hello 정보를 검토 하십시오.  

> [!IMPORTANT]
> * StorSimple tooinstall hello 년 10 월 업데이트에 대 한 hello StorSimple Manager 서비스 및 Windows PowerShell이 아닌를 사용 합니다.  
> * hello 업데이트에는 일반적으로 약 3 시간 toocomplete 적용.  
> * hello StorSimple 10 월 릴리스에 모든 업데이트 toohello StorSimple 가상 장치입니다. 최근 보안 픽스를 비롯 한 모든 사용 가능한 Windows 업데이트를 적용할 수 있습니다 하지만 hello 가상 장치에 대 한 버전의 변경을 표시 되지 않습니다.  
> 
> 

다음 필수 구성 요소 hello 있는지 확인 met 이전 tooupdating StorSimple 장치 됩니다.  

* 업데이트를 검색하기 전에 두 장치 컨트롤러가 모두 실행되고 있는지 확인합니다. 컨트롤러 중 하나가 실행 되지 않는 경우 hello 검색이 실패 합니다. hello 컨트롤러는 정상 상태에 있는 tooverify 너무 이동**하드웨어 상태** hello에서 **유지 관리** 페이지. **주의가 필요한**구성 요소가 있는 경우, 더 진행하기 전에 Microsoft 지원에 문의합니다.  
* 두 컨트롤러 0의 고정된 Ip과 컨트롤러 1 라우팅 가능 하 고 hello 업데이트 toohello 장치를 서비스에 대해 사용 되는 이러한 toohello 인터넷을 연결할 수 있는지 확인 합니다. Hello를 사용할 수 있습니다 [Test-connection cmdlet](https://technet.microsoft.com/library/hh849808.aspx) tooping 컨트롤러 hello tooverify outlook.com과 같은 hello 네트워크 외부의 알려진된 주소 연결 toohello 네트워크 외부에 있습니다.  
* 아웃 바운드 포트 아웃 바운드 통신에 대 한 StorSimple 장치에서 사용할 수 있는 해당 hello 필수 확인 합니다. 자세한 내용은 참조 hello [StorSimple 장치의 네트워킹 요구 사항](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)합니다.  
* Hello 장치 소프트웨어 버전 6.3.9600.17312 (2014 년 10 월 업데이트) 보다 오래 된 경우 hello 업데이트를 시작 하기 전에 사용 하는 경우 hello 데이터 2 및 Data 3 포트를 사용 하지 않도록 설정 합니다. 데이터 2 hello 또는 데이터 3 포트를 hello 업데이트를 적용할 때 사용 된를 두면 복구 모드로 장치 컨트롤러 toogo를 발생할 수 있습니다. Hello 네트워크 인터페이스를 해제 하면 모든 hello 연결 된 볼륨을 오프 라인으로 설정한 및 hello hello 업데이트 기간에 대 한 hello I/O가 중단 note 하십시오.  

## <a name="whats-new-in-hello-october-release"></a>Hello 년 10 월 릴리스의 새로운 기능
이 업데이트에 향상 된 기능을 수행 하는 hello를 포함 합니다.

* 이제 장치 컨트롤러 hello StorSimple 관리자 서비스 UI toomanage를 사용할 수 있습니다. 다시 시작, 종료, 컨트롤러에서 설정 하거나는 hello 관리 작업에 포함 합니다. 자세한 내용은 이동 너무[관리 StorSimple 장치 컨트롤러](storsimple-manage-device-controller.md)합니다.  
* Tooday 주 및 일 시간 조합에 따라 WAN 대역폭 할당을 예약할 수 있습니다. 이렇게 하면 toomake를 효과적으로 사용할 WAN 대역폭 사용량이 적은 시간 동안 있습니다. 다른 볼륨 컨테이너에 대해 다른 대역폭 템플릿이 허용됩니다. 자세한 내용은 이동 너무[StorSimple 대역폭 템플릿 관리](storsimple-manage-bandwidth-templates.md)합니다.  
* Tooproactively hello 관리자 및 다른 사용자가 기존 또는 향후 수 있는 문제를 알리는 전자 메일 알림을 구성할 수 있습니다. 자세한 내용은 이동 너무[경고 설정을 구성할](storsimple-manage-alerts.md#configure-alert-settings)합니다.  

## <a name="issues-fixed-in-hello-october-release"></a>Hello 년 10 월 릴리스에서 해결 된 문제
hello 다음 표에서이 업데이트에서 해결 된 문제에 대 한 요약 합니다.  

| 아니요. | 기능 | 문제 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- |
| 1 |네트워크 인터페이스 |Hello 이전에 해제, hello 네트워크 인터페이스 DATA 2 및 DATA 3 hello 소프트웨어에서 교체 되었습니다. 이 업데이트에서 수정되었습니다. Hello 설정의 선택을 취소 하 고 hello 업데이트를 설치 하기 전에 이러한 네트워크 인터페이스를 사용 하지 않도록 설정 하세요. Hello 업데이트를 설치 하면 tooreconfigure 이러한 인터페이스를 해야 합니다. |예 |아니요 |
| 2 |지원 패키지 |Hello 이전 릴리스에서 hello Windows PowerShell을 실행 한 경우 **Export-hcssupportpackage** cmdlet tooretrieve hello bmc (베이스 보드 관리 컨트롤러가) 로그, hello 작업에 따라 경고 hello로 실패 했습니다: "hello 작업이이 컨트롤러에 성공 했지만 toohello 다음 인해 hello 피어 컨트롤러에 실패 했습니다. 오류입니다. 확인 하십시오 hello 피어가 정상 상태 인지 여부 hello 현재 노드 toohello 피어를 연결할 수 있습니다. " 이제 이 문제는 해결되었습니다. |예 |아니요 |
| 3 |장치 장애 조치 |Hello 이전 릴리스에서 데이터가 불일치할 가능성이 경우 있었습니다는 **백업을 검색할** 장치 장애 조치 중 작업이 실패 했습니다. 이제 이 문제는 해결되었습니다. |예 |아니요 |
| 4 |장치 장애 조치 |Hello 이전에 해제, 장치 장애 조치 후 백업은 표시 되었지만 연결 된 볼륨 컨테이너 hello hello 대상 장치에 표시 되지 않았습니다. 이제 이 문제는 해결되었습니다. |예 |아니요 |
| 5 |장치 장애 조치 |Hello 이전 릴리스에서 클라우드 연결 문제가 없는 경우 toodata 불일치를 초래할 수 있는 hello 레지스트리 복원 작업 중의 클라우드 백업 hello 열거에 버그가 했습니다. |예 |아니요 |
| 6 |펌웨어 업데이트 |이전 릴리스에서 hello hello 장치 펌웨어 업데이트 작업이 실패 하 고 hello cmdlet 인식할 수 없습니다. 해당 hello 업데이트가 실패 했다는 오류가 표시 됩니다. hello 그러면 컨트롤러가 복구 모드로 합니다. 이제 이 문제는 해결되었습니다. |예 |아니요 |
| 7 |설치 |Hello 장치 하지 이미지가 올바르게 생성 하는 동안 설치로 인 한 오류 이제 수정 되었습니다. |예 |아니요 |
| 8 |공장 재설정 |이제 공장 재설정을 위한 펌웨어 확인 hello를 선택적으로 건너뛸 수 있습니다. 이 hello 이전 릴리스에서 변경 합니다. |예 |아니요 |
| 9 |공장 재설정 |Hello 이전 릴리스에서 공장 재설정 cmdlet 실행 시 일부 하드웨어 구성 요소에 대해서만 펌웨어 버전을 확인 적용 되었습니다. 추가 펌웨어 확인을 수행한 후 hello hello 재설정 toofail 될 수 있는 hello 프로세스의 첫 번째 다시 부팅 합니다. 이 문제를이 수정 하면 hello 공장 재설정 cmdlet을 실행 하 고 첫 번째 시스템 다시 부팅 hello 하기 전에 모든 hello 펌웨어 검사를 수행 합니다. |예 |아니요 |
| 10 |저장소 계정 키 회전 |hello **Invoke-hcsmservicedataencryptionkeychange** cmdlet 프롬프트 hello 사용자 tooenter hello 서비스 데이터 암호화 키 이제 toorotate hello 저장소 계정 키를 사용 합니다. 이 서비스 데이터 암호화 키가 인라인 매개 변수로 전달 하는 hello에는 hello 이전 릴리스에서 변경 합니다. |예 |아니요 |
| 11 |24시간 내에 장애 복구 |재해 복구 시 hello hello 원본 장치 정리가 정상적으로 장애 복구 toofail에서는 발생 하지 않았으며 합니다. 이 릴리스에서 수정되었습니다. |예 |아니요 |

## <a name="known-issues-in-hello-october-release"></a>Hello 년 10 월 릴리스의 알려진된 문제
다음 표에서 hello이이 릴리스의 알려진된 문제에에서 대 한 요약을 제공 합니다.

| 아니요. | 기능 | 문제 | 주석/해결 방법 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- | --- |
| 1 |공장 재설정 |경우에 따라 공장 재설정을 수행할 때 StorSimple 장치 hello 남아 있을 수 있습니다 및이 메시지를 표시: **재설정 toofactory가 진행 중인 (8 단계)**합니다. 이 hello cmdlet이 진행 중일 동안 CTRL + C를 누르면 발생 합니다. |공장 재설정을 시작한 후 CTRL+C를 누르지 마세요. 이미 이 상태에 있다면 다음 단계에 대해 Microsoft 지원에 문의하세요. |예 |아니요 |
| 2 |공장 재설정 |GA tooOctober 2014 릴리스의 업데이트는 StorSimple 장치 공장 재설정 하지 마세요. |이 작업은 패치를 설치하는 경우에만 작동합니다. 이 필수 패치를 tooget Microsoft 지원에 문의 하십시오. |예 |아니요 |
| 3 |디스크 쿼럼 |경우에 따라에서 hello 대부분의 디스크 8600 장치의 EBOD 인클로저에 hello 끊어져서 디스크 쿼럼이 없게 하는 경우 다음 hello 저장소 풀이 오프 라인 상태가 됩니다. Hello 디스크가 다시 연결 하는 경우에 오프 라인으로 유지 됩니다. |Tooreboot hello 장치가 필요 합니다. Hello 문제가 지속 되 면 Microsoft 지원에 다음 단계에 문의 하세요. |예 |아니요 |
| 4 |클라우드 스냅숏 실패 |클라우드 스냅숏 드물게에서 hello 오류가 발생할 수 있습니다 **최대 백업 한계 도달**합니다. Hello에서 온라인 복제가 255 개를 초과 하는 경우이 경고가 발생 hello에서 동일한 장치 삭제 된 동일한 원래 볼륨입니다. | |예 |예 |
| 5 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 하는 동안 hello 이미지 hello 피어 노드에서 로드 되 면 hello 컨트롤러 ID 수 처음으로 나타나도록 hello 피어 컨트롤러의 id입니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |별도의 작업이 필요하지 않습니다. 이 경우 hello 컨트롤러 교체를 완료 한 후 자체적으로 해결 됩니다. |예 |아니요 |
| 6 |장치 모니터링 차트 |StorSimple Manager 서비스 hello, 기본 hello 장치 모니터링 차트가 작동 하지 않습니다 또는 hello 장치에 대 한 hello 프록시 서버 구성에서 NTLM 인증을 사용 합니다. |StorSimple Manager 서비스로 등록 인증을 tooNONE 설정 되므로 hello 장치에 대 한 hello 웹 프록시 구성을 수정 합니다. toodo StorSimple Set-hcswebproxy cmdlet에 대 한 실행된 hello hello Windows PowerShell이 합니다. |예 |예 |
| 7 |저장소 계정 |Hello 저장소 서비스 toodelete hello 저장소 계정을 사용 하는 지원 되지 않는 시나리오입니다. 이렇게 하면 tooa 상황 사용자 데이터를 검색할 수 없습니다. | |예 |예 |
| 8 |장치 장애 조치 |다중에서 동일한 원본 장치 toodifferent 대상 장치는 지원 되지 않습니다 hello는 볼륨 컨테이터의 장애 조치 합니다. |단일 데드 장치 toomultiple 장치에서 장애 조치에는 먼저 장애 장치 조치 hello 장치의 hello 볼륨 컨테이너가 데이터 소유권을 잃게 생성 됩니다. 이러한 장애 조치 후 이러한 볼륨 컨테이너 나타나거나 hello Azure 클래식 포털에서에서 볼 때 다르게 동작 합니다. |예 |아니요 |
| 9 |설치 |SharePoint 용 StorSimple 어댑터를 하는 동안 필요한 tooprovide hello 설치 toofinish 위해에서 장치 IP 성공적으로 합니다. | |예 |아니요 |
| 10 |웹 프록시 |웹 프록시 구성에 있으면 hello로는 HTTPS 프로토콜을 지정 다음 장치를 서비스 통신 영향을 받고 hello 장치는 오프 라인 상태가 유지 됩니다. 지원 패키지도 장치에서 많은 리소스를 소모 hello 프로세스에서 생성 됩니다. |지정한 프로토콜이 hello으로 hello 웹 프록시 URL에 HTTP 있는지 확인 합니다. 방법에 대 한 자세한 내용은 너무[장치에 대 한 웹 프록시 구성](storsimple-configure-web-proxy.md)합니다. |예 |아니요 |
| 11 |웹 프록시 |구성 하 고 등록된 된 장치에서 웹 프록시를 사용 하는 경우 장치에서 toorestart hello 활성 컨트롤러가 필요 합니다. | |예 |아니요 |
| 12 |긴 클라우드 대기 시간 및 많은 I/O 작업 |StorSimple 장치 매우 긴 클라우드 대기 시간 (초) 및 높은 수준의 I/O 작업의 조합을 발견 하면 hello 장치 볼륨 상태가 저하 및 hello I/o "장치가 준비 되지 않음" 오류가 발생할 수 있습니다. |Toomanually 재부팅 hello 장치 컨트롤러 필요 하거나이 상황에서 장치 장애 조치 toorecover를 수행 합니다. |예 |아니요 |

## <a name="physical-device-updates-in-hello-october-release"></a>Hello 년 10 월 릴리스에서 물리적 장치 업데이트
이러한 업데이트를 적용된 tooa 물리적 장치 소프트웨어 버전 hello too6.3.9600.17312를 변경 됩니다. 이러한 릴리스 정보를 지정 하지 않으면 hello StorSimple 장치의 tooall 모델을 적용 합니다. 이 업데이트에 대한 자세한 내용은 [2014년 10월 Microsoft Azure StorSimple 어플라이언스용 실제 어플라이언스 소프트웨어 업데이트](http://support.microsoft.com/kb/2986997)를 참조하세요.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Serial attached SCSI (SAS) 컨트롤러 및 펌웨어 업데이트 hello 년 10 월 릴리스에서
이 릴리스는 hello 드라이버 및 물리적 장치의 SAS 컨트롤러 hello에 hello 펌웨어를 업데이트합니다. Hello SAS 컨트롤러 업데이트에 대 한 자세한 내용은 참조 [Microsoft Azure StorSimple 어플라이언스의 LSI SAS 컨트롤러용 2014 년 10 월 업데이트](http://support.microsoft.com/kb/2987020)합니다.   

이 버전에는 hello 장치 하드웨어 구성 요소의 안정성 문제를 해결 하는 누적 펌웨어 업데이트도를 적용 됩니다. Hello 펌웨어 업데이트에 대 한 자세한 내용은 참조 [Microsoft Azure StorSimple 어플라이언스 용 2014 년 10 월 펌웨어 업데이트](http://support.microsoft.com/kb/2987015)합니다.  

## <a name="virtual-device-updates-in-hello-october-release"></a>Hello 년 10 월 릴리스에서 가상 장치 업데이트
이 릴리스에서 hello 가상 장치에 대 한 업데이트 합니다. 이 업데이트를 적용 하는 경우에 가상 장치의 소프트웨어 버전 hello 변경 되지 않습니다.

