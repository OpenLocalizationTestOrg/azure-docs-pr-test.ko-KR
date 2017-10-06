---
title: "aaaTroubleshoot StorSimple 8000 시리즈 배포 문제 | Microsoft Docs"
description: "설명 방법을 StorSimple을 처음 배포할 때 발생 하는 오류 toodiagnose 및 수정 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: a55a4b277c8afe25f1d5a43ab8d7a90436123410
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>StorSimple 장치 배포 문제 해결
## <a name="overview"></a>개요
이 문서는 Microsoft Azure StorSimple 배포에 대한 유용한 문제 해결 지침을 제공합니다. 일반적인 문제, 가능한 원인 및 StorSimple을 구성할 때 발생할 수 있는 문제를 해결 하는 권장된 단계 toohelp를 설명 합니다. 

이 정보는 tooboth hello StorSimple 8000 시리즈 실제 장치 및 StorSimple 클라우드 어플라이언스에 hello 적용 됩니다.

> [!NOTE]
> 장치 구성 관련 문제 시 발생할 수 있는 hello에 대 한 hello 장치를 처음으로 배포 hello 장치가 작동 하는 경우, 나중에 수행 될 수 있습니다 때 발생할 수 있습니다. 이 문서는 처음 배포 시 문제 해결에 중점을 둡니다. 작동 하는 장치, tootroubleshoot 너무 이동[사용 하 여 hello 진단 도구 작동 하는 장치 설정 tootroubleshoot](storsimple-8000-diagnostics.md)합니다.

또한이 문서는 StorSimple 배포 문제 해결을 위한 hello 도구에 설명 하 고 단계별 문제 해결 예제를 제공 합니다.

## <a name="first-time-deployment-issues"></a>처음 배포 시 문제
처음으로 hello에 대 한 장치를 배포 하는 경우 문제를 실행 하면 hello 다음 사항을 고려 합니다.

* 물리적 장치를 해결 하는 경우 hello 하드웨어 설치 및에 설명 된 대로 구성 된가 있는지 확인 [StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [8600 StorSimple 장치설치](storsimple-8600-hardware-installation.md).
* 배포를 위한 필수 구성 요소를 확인합니다. Hello에 설명 된 모든 hello 정보 갖도록 [배포 구성 검사 목록](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist)합니다.
* Hello 문제가 설명 되어 있는 경우 hello StorSimple 릴리스 정보 toosee를 검토 합니다. hello 릴리스 정보에는 알려진된 설치 문제에 대 한 해결 방법이 포함 되어 있습니다. 

장치 배포 중 가장 일반적인 hello hello 설치 마법사를 실행할 때 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록 하 고가 발생 하는 발급 합니다. (있습니다 tooregister StorSimple에 대 한 Windows PowerShell을 사용 하 고 StorSimple 장치를 구성 합니다. 장치 등록에 대한 자세한 내용은 [3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)을 참조하세요.)

다음 섹션 hello hello에 대 한 hello StorSimple 장치를 처음으로 구성할 때 발생 하는 문제를 해결 하는 데 유용 합니다.

## <a name="first-time-setup-wizard-process"></a>처음 설치 마법사 프로세스
단계를 수행 하는 hello hello 설치 마법사 프로세스를 요약 합니다. 자세한 설치 정보는 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.

1. Hello 실행 [Invoke-hcssetupwizard](https://technet.microsoft.com/library/dn688135.aspx) hello 단계 나머지 과정을 안내 하는 cmdlet toostart hello 설정 마법사입니다. 
2. Hello 네트워크 구성: hello 설치 마법사를 사용 하면 StorSimple 장치에 hello DATA 0 네트워크 인터페이스에 대 한 네트워크 설정을 구성할 수 있습니다. 이러한 설정은 hello 다음과를 같습니다.
   * 가상 IP (VIP), 서브넷 마스크 및 게이트웨이 – hello [Set-hcsnetinterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet hello 백그라운드에서 실행 됩니다. StorSimple 장치에 hello IP 주소, 서브넷 마스크 및 hello DATA 0 네트워크 인터페이스에 대 한 게이트웨이 구성합니다.
   * 기본 DNS 서버 – hello [Set-hcsdnsclientserveraddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet hello 백그라운드에서 실행 됩니다. StorSimple 솔루션에 대 한 hello DNS 설정을 구성합니다.
   * NTP 서버 – hello [Set-hcsntpclientserveraddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet hello 백그라운드에서 실행 됩니다. StorSimple 솔루션에 대 한 hello NTP 서버 설정을 구성합니다.
   * 선택적 웹 프록시 – hello [Set-hcswebproxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet hello 백그라운드에서 실행 됩니다. 설정 하 고 StorSimple 솔루션에 대 한 hello 웹 프록시 구성을 사용 합니다.
3. Hello 암호를 설정: hello 다음 단계는 tooset hello 장치 관리자 암호를 구성 합니다.
   hello 장치 관리자 암호는 tooyour 장치에 사용 되는 toolog입니다. hello 기본 장치 암호는 **Password1**합니다.
        
     > [!IMPORTANT]
     > 암호는 등록 전에 수집 하지만 hello 장치를 성공적으로 등록 한 후에 적용 됩니다. 없을 경우 실패 tooapply 암호, 됩니다 증명된 toosupply hello 암호 다시 hello 필수 (hello 복잡성 요구 사항에 맞는) 암호를 수집할 때까지 합니다.
     
4. Hello 장치 등록: hello 마지막 단계는 Microsoft Azure에서 실행 되는 hello StorSimple 장치 관리자 서비스를 사용 하 여 tooregister hello 장치입니다. hello 등록 해야 너무[hello 서비스 등록 키 받기](storsimple-8000-manage-service.md#get-the-service-registration-key) 에서 Azure 포털 hello 및 hello 설치 마법사에서 제공 합니다. **Hello 장치를 등록 한 후에 서비스 데이터 암호화 키 tooyou를 제공 됩니다. Tookeep 수 있으므로이 암호화 키를 안전한 위치에 필요한 tooregister hello 서비스를 사용 하 여 모든 후속 장치 확인 해야 합니다.**

## <a name="common-errors-during-device-deployment"></a>장치 배포 중 일반 오류
hello 다음 테이블 목록 hello 일반적인 오류가 때 발생할 수 있습니다.

* Hello 필요한 네트워크 설정을 구성 합니다.
* Hello 선택적 웹 프록시 설정을 구성 합니다.
* Hello 장치 관리자 암호를 설정 합니다.
* Hello 장치를 등록 합니다.

## <a name="errors-during-hello-required-network-settings"></a>Hello 동안 발생 한 오류 필요한 네트워크 설정
| 아니요. | 오류 메시지 | 가능한 원인 | 권장 작업 |
| --- | --- | --- | --- |
| 1 |Invoke-hcssetupwizard:이 명령은 hello 활성 컨트롤러 에서만 실행할 수 있습니다. |Hello 수동 컨트롤러에서 수행 되 고 구성 합니다. |Hello 활성 컨트롤러에서이 명령을 실행 합니다. 자세한 내용은 [장치에서 활성 컨트롤러 식별](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device)을 참조하세요. |
| 2 |Invoke-HcsSetupWizard: 장치가 준비되지 않았습니다. |DATA 0에 hello 네트워크 연결 문제가 있습니다. |DATA 0에 hello 실제 네트워크 연결을 확인 합니다. |
| 3 |Invoke-hcssetupwizard: hello 네트워크에서 다른 시스템과 IP 주소 충돌이 발생 하는 (HRESULT의 예외: 0x80070263). |DATA 0에 제공 하는 hello IP 이미 다른 시스템에서 사용 합니다. |사용되지 않는 새 IP를 제공합니다. |
| 4 |Invoke-HcsSetupWizard: 클러스터 리소스가 실패했습니다. (HRESULT: 0x800713AE에서 예외 발생). |VIP가 중복되었습니다. 제공 된 hello IP 이미 사용 중입니다. |사용되지 않는 새 IP를 제공합니다. |
| 5 |Invoke-HcsSetupWizard: 잘못된 IPv4 주소입니다. |hello IP 주소는 잘못 된 형식으로 제공 됩니다. |Hello 형식을 확인 하 고 IP 주소를 다시 입력 합니다. 자세한 내용은 [Ipv4 주소 지정][1]을 참조하세요. |
| 6 |Invoke-HcsSetupWizard: 잘못된 IPv6 주소입니다. |hello IP 주소는 잘못 된 형식으로 제공 됩니다. |Hello 형식을 확인 하 고 IP 주소를 다시 입력 합니다. 자세한 내용은 [Ipv6 주소 지정][2]을 참조하세요. |
| 7 |Invoke-hcssetupwizard: 있는 끝점이 더 이상 hello 끝점 매퍼에서 사용할 수 있습니다. (HRESULT: 0x800706D9에서 예외 발생). |hello 클러스터 기능이 작동 하지 않습니다. |[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Hello 선택적 웹 프록시 설정 하는 동안 오류가 발생
| 아니요. | 오류 메시지 | 가능한 원인 | 권장 작업 |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: 잘못된 매개 변수(HRESULT: 0x80070057에서 예외 발생) |Hello 프록시 설정에 대해 제공 된 hello 매개 변수 중 하나가 올바르지 않습니다. |hello URI 형식이 잘못 된 hello 제공 되지 않습니다. 형식에 따라 사용 하 여 hello: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: RPC 서버 사용 불가능(HRESULT: 0x800706ba에서 예외 발생) |hello 근본 원인을 hello 다음 중 하나입니다.<ol><li>hello 클러스터가 작동 하지 않습니다.</li><li>수동 컨트롤러 hello hello 활성 컨트롤러와 통신할 수 없습니다 및 수동 컨트롤러에서 hello 명령을 실행 합니다.</li></ol> |Hello 근본 원인에 따라:<ol><li>[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 있는지 toomake 해당 hello 클러스터가 실행 중이 있습니다.</li><li>Hello 활성 컨트롤러에서 hello 명령을 실행 합니다. Tooensure 할 hello 수동 컨트롤러에서 toorun hello 명령을 원하는 경우 해당 hello 수동 컨트롤러가 hello 활성 컨트롤러와 통신할 수 있습니다. 너무 해야[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 이 연결이 끊어진 경우.</li></ol> |
| 3 |Invoke-HcsSetupWizard: RPC 호출 실패함(HRESULT: 0x800706be에서 예외 발생) |클러스터의 작동이 중단되었습니다. |[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 있는지 toomake 해당 hello 클러스터가 실행 중이 있습니다. |
| 4 |Invoke-HcsSetupWizard: 클러스터 리소스를 찾을 수 없음(HRESULT: 0x8007138f에서 예외 발생) |hello 클러스터 리소스를 찾을 수 없습니다. Hello 설치가 정확 하지 않을 때 발생할 수 있습니다. |Tooreset hello 장치 toohello 공장 기본 설정 해야 합니다. [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) toocreate 클러스터 리소스입니다. |
| 5 |Invoke-HcsSetupWizard: 클러스터 리소스가 온라인 상태가 아님(HRESULT: 0x8007138c에서 예외 발생) |클러스터 리소스가 온라인 상태가 아닙니다. |[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요. |

## <a name="errors-related-toodevice-administrator-password"></a>오류 관련된 toodevice 관리자 암호
hello 기본 장치 관리자 암호는 **Password1**합니다. Hello 첫 번째 로그온 후에이 암호 만료 따라서 toouse hello 설치 마법사 toochange 할 것입니다. 처음으로 hello에 대 한 hello 장치를 등록할 때 새 장치 관리자 암호를 제공 해야 합니다. 

암호 요구 사항을 준수 하는 hello를 충족 하는지 확인 합니다.

* 장치 관리자 암호는 8자에서 15자 사이여야 합니다.
* 암호에는 다음 문자 형식 4 hello의 3 가지가 포함 되어야 합니다: 소문자, 대문자, 숫자 및 특수 합니다. 
* 암호는 지난 24 개의 암호 hello와 같을 hello 수 없습니다.

또한 암호 만료, 매년 염두에서에 둬야 및 hello 장치를 성공적으로 등록 한 후에 변경할 수 있습니다. 어떤 이유로 든 hello 등록에 실패 하면 hello 암호는 변경 되지 않습니다.

장치 관리자 암호에 대 한 자세한 내용은 이동 너무[사용 하 여 hello StorSimple 장치 관리자 서비스 toochange StorSimple 암호](storsimple-8000-change-passwords.md)합니다.

Hello hello 장치 관리자 및 StorSimple 스냅숏 관리자 암호를 설정할 때 다음 오류 중 하나 이상을 발생할 수 있습니다.

| 아니요. | 오류 메시지 | 권장 작업 |
| --- | --- | --- |
| 1 |hello 암호 hello 최대 길이 초과 합니다. |장치 관리자 암호는 8자에서 15자 사이여야 합니다. |
| 2 |hello 암호 hello 필요한 길이 충족 하지 않습니다. |장치 관리자 암호는 8자에서 15자 사이여야 합니다.|
| 3 |hello 암호는 소문자를 포함 해야 합니다. |암호에는 3 / 4 문자 유형만 hello 포함 되어야 합니다: 소문자, 대문자, 숫자 및 특수 합니다. 암호가 이 요구 사항을 충족하는지 확인합니다. |
| 4 |hello 암호는 숫자를 포함 해야 합니다. |암호에는 3 / 4 문자 유형만 hello 포함 되어야 합니다: 소문자, 대문자, 숫자 및 특수 합니다. 암호가 이 요구 사항을 충족하는지 확인합니다. |
| 5 |hello 암호는 특수 문자를 포함 해야 합니다. |암호에는 3 / 4 문자 유형만 hello 포함 되어야 합니다: 소문자, 대문자, 숫자 및 특수 합니다. 암호가 이 요구 사항을 충족하는지 확인합니다. |
| 6 |hello 암호 3 개 포함 해야 4 문자 유형만 hello: 대문자, 소문자, 숫자 및 특수 합니다. |사용자 암호 hello 필요한 종류의 문자를 포함 하지 않습니다. 암호가 이 요구 사항을 충족하는지 확인합니다. |
| 7 |매개 변수는 확인과 일치하지 않습니다. |암호 요구 사항을 모두 만족하고 이를 올바르게 입력했는지 확인합니다. |
| 8 |암호는 hello 기본을 일치할 수 없습니다. |hello 기본 암호는 *Password1*합니다. 필요한 toochange이이 암호에 로그인 하면 hello에 대 한 처음으로 합니다. |
| 9 |입력 한 hello 암호가 hello 장치 암호가 일치 하지 않습니다. Hello 암호를 다시 입력 하십시오. |Hello 암호를 확인 하 고 다시 입력 합니다. |

Hello 장치는 등록 되지만 성공적으로 등록 한 후에 적용 되기 전에 암호가 수집 됩니다. hello 암호 복구 워크플로 hello 장치 toobe 등록 필요 합니다.

> [!IMPORTANT]
> 일반적으로 시도 tooapply 암호 실패 성공할 때까지 반복 해 서 hello 소프트웨어 toocollect hello 암호 시도 합니다. 경우에 따라에서 hello 암호를 적용할 수 없습니다. 이 경우 hello 장치를 등록할 수 있으며 계속 있지만 hello 암호는 변경 되지 않습니다 수 있습니다. Hello Azure 포털에서에서 hello 등록 후 hello 장치 관리자 암호를 변경할 수 있습니다.


Hello hello StorSimple 장치 관리자 서비스를 통해 Azure 포털에에서 hello 암호를 재설정할 수 있습니다. 자세한 내용은 이동 너무[hello 장치 관리자 암호 변경](storsimple-8000-change-passwords.md#change-the-device-administrator-password)합니다.

## <a name="errors-during-device-registration"></a>장치 등록 중 오류
Microsoft Azure tooregister hello 장치에서 실행 되는 hello StorSimple 장치 관리자 서비스를 사용 합니다. 하나 이상의 장치를 등록 하는 동안 문제를 수행 하는 hello 발생할 수 있습니다.

| 아니요. | 오류 메시지 | 가능한 원인 | 권장 작업 |
| --- | --- | --- | --- |
| 1 |오류 350027: hello StorSimple 장치 관리자를 사용 하 여 tooregister hello 장치를 실패 했습니다. | |몇 분 정도 기다린 후 hello 작업을 다시 시도 하십시오. Hello 문제가 지속 되 면 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다. |
| 2 |오류 350013: hello 장치를 등록 하는 중에 오류가 발생 했습니다. 이 서비스 등록 키 tooincorrect 원인일 수 있습니다. | |Hello 올바른 서비스 등록 키로 hello 장치를 다시 등록 하세요. 자세한 내용은 참조 [Get hello 서비스 등록 키입니다.](storsimple-8000-manage-service.md#get-the-service-registration-key) |
| 3 |오류 350063: 장치 관리자 서비스 인증 tooStorSimple 전달 되지만 등록 하지 못했습니다. 잠시 후 hello 작업을 다시 시도 하십시오. |이 오류는 ACS 인증 통과 하지만 hello 등록 호출이 toohello 서비스가 실패 했음을 나타냅니다. 간헐적인 네트워크 결함의 결과일 수 있습니다. |Hello 문제가 지속 되 면 하십시오 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다. |
| 4 |오류 350049: 등록 하는 동안 hello 서비스에 연결할 수 없습니다. |Hello 호출 toohello 서비스, 웹 예외가 수신 됩니다. 경우에 따라 hello 나중에 작업을 다시 시도 하 여 해결 될 수 있습니다. |다음 hello 작업을 다시 시도 및 DNS 이름과 IP 주소를 확인 하십시오. Hello 문제가 계속 되 면 [Microsoft 지원에 문의 합니다.](storsimple-8000-contact-microsoft-support.md) |
| 5 |오류 350031: hello 장치는 이미 등록 되었습니다. | |필요한 작업이 없습니다. |
| 6 |오류 350016: 장치 등록에 실패했습니다. | |Hello 등록 키가 올바른지 확인 하십시오. |
| 7 |Invoke-hcssetupwizard:; 장치를 등록 하는 동안 오류가 발생 했습니다. 기한 tooincorrect IP 주소 또는 DNS 이름을 확인할 수 있습니다. 네트워크 설정을 확인하고 다시 시도하세요. Hello 문제가 계속 되 면 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)합니다. (오류 350050) |장치 네트워크 외부 hello를 ping 할 수 있는지 확인 합니다. Toooutside 네트워크 연결이 없는 경우이 오류와 함께 hello 등록 실패할 수 있습니다. 이 오류는 hello 다음 중 하나 이상의 조합일 수 있습니다.<ul><li>잘못된 IP</li><li>잘못된 서브넷</li><li>잘못된 게이트웨이</li><li>잘못된 DNS 설정</li></ul> |Hello hello에서 단계를 참조 하십시오. [단계별 문제 해결 예제](#step-by-step-storsimple-troubleshooting-example)합니다. |
| 8 |Invoke-hcssetupwizard: tooan 내부 서비스 오류 [0x1FBE2] 인해 hello 현재 작업이 실패 했습니다. Hello 작업을 잠시 후 다시 시도 하십시오. Hello 문제가 지속 되 면 Microsoft 지원에 문의 하세요. |모든 사용자가 서비스 또는 에이전트에서 볼 수 없는 오류에 대해 발생한 일반 오류입니다. hello 가장 일반적인 이유는 hello ACS 인증에 실패 될 수 있습니다. Hello 실패에 대 한 가능한 원인은 hello NTP 서버 구성에는 문제가 및 hello 장치의 시간이 올바르게 설정 되지 않았습니다. |(있는 경우 문제) hello 시간을 수정 하 고 hello 등록 작업을 다시 시도 하십시오. Hello 집합 HcsSystem Timezone 명령 tooadjust hello 표준 시간대를 사용 하는 경우 hello 표준 시간대 (예를 들어 "태평양 표준시")의 각 글자를 대문자로 표시 합니다.  이 문제가 지속되면 다음 단계는 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요. |
| 9 |경고: hello 장치를 활성화할 수 없습니다. 장치 관리자 및 StorSimple Snapshot Manager 암호가 변경되지 않습니다. |Hello 등록에 실패 하면 hello 장치 관리자 및 StorSimple 스냅숏 관리자 암호 변경 되지 않습니다. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>StorSimple 배포 문제 해결을 위한 팁
StorSimple에 여러 가지 도구를 사용할 수 있는 tootroubleshoot StorSimple 솔루션에 포함 됩니다. 내용은 다음과 같습니다.

* 지원 패키지 및 장치 로그
* 문제 해결을 위해 특별히 설계된 Cmdlet

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>문제 해결에 사용 가능한 지원 패키지 및 장치 로그
지원 패키지는 hello Microsoft 지원 팀이 장치 문제 해결을 지원할 수 있는 모든 hello 관련 로그를 포함 합니다. StorSimple toogenerate 그러면 지원 담당자와 공유할 수 있는 암호화 된 지원 패키지에 대 한 Windows PowerShell을 사용할 수 있습니다.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>tooview hello 로그 또는 hello hello 지원 패키지 내용의 압축
1. 에 설명 된 대로 StorSimple toogenerate 지원 패키지에 대 한 Windows PowerShell을 사용 하 여 [만들기 지원 패키지를 관리 하 고](storsimple-8000-create-manage-support-package.md)합니다.
2. Hello 다운로드 [암호 해독 스크립트](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 클라이언트 컴퓨터에 로컬로 합니다.
3. 이 사용 하 여 [단계별 절차](storsimple-8000-create-manage-support-package.md#edit-a-support-package) hello 지원 패키지 tooopen 및 암호 해독 합니다.
4. hello 로그는 etw/etvx 형식에서 지원 패키지를 해독 합니다. Windows 이벤트 뷰어에서 hello 단계 tooview 다음 이러한 파일을 수행할 수 있습니다.
   
   1. Hello 실행 **eventvwr** Windows 클라이언트에서 명령을 합니다. 이벤트 뷰어 hello가 시작 됩니다.
   2. Hello에 **동작** 창에서 클릭 **저장 된 로그 열기** 고 etvx/etw 형식의 (hello 지원 패키지)의 지점 toohello 로그 파일입니다. 이제 hello 파일을 볼 수 있습니다. Hello 파일을 연 후 마우스 오른쪽 단추로 클릭 하 고 텍스트로 hello 파일을 저장할 수 있습니다.
      
      > [!IMPORTANT]
      > Hello를 사용할 수도 있습니다 **Get-winevent** cmdlet tooopen Windows PowerShell에서 이러한 파일입니다. 자세한 내용은 참조 [Get-winevent](https://technet.microsoft.com/library/hh849682.aspx) hello Windows PowerShell cmdlet 참조 설명서에에서 있습니다.
     
5. Hello 로그 이벤트 뷰어를 연 다음 문제 관련된 toohello 장치 구성에 포함 된 로그가 hello를 찾습니다.
   
   * hcs_pfconfig/Operational 로그
   * hcs_pfconfig/Config
6. Hello 로그 파일에 hello 설치 마법사를 통해 호출 된 관련된 toohello cmdlet 문자열을 검색 합니다. 이 cmdlet의 목록은 [처음 설치 마법사 프로세스](#first-time-setup-wizard-process)를 참조하세요.
7. Hello 문제의 hello 원인 아웃 수 toofigure 없는 경우 다음을 할 수 있습니다 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 다음 단계에 대 한 합니다. 단계를 사용 하 여 hello [지원 요청](storsimple-8000-contact-microsoft-support.md#create-a-support-request) 경우 Microsoft 지원에 문의 합니다.

## <a name="cmdlets-available-for-troubleshooting"></a>문제 해결에 사용할 수 있는 Cmdlet
다음 Windows PowerShell cmdlet toodetect 연결 오류 hello를 사용 합니다.

* `Get-NetAdapter`:이 cmdlet toodetect hello 네트워크 인터페이스의 상태를 사용 합니다.
* `Test-Connection`:이 cmdlet toocheck hello 네트워크 내부 및 외부 연결 hello 네트워크를 사용 합니다.
* `Test-HcsmConnection`:이 cmdlet toocheck hello 연결 성공적으로 등록 된 장치의 기능을 사용 합니다.
* `Sync-HcsTime`:이 cmdlet toodisplay 장치 시간을 사용 하 고 hello NTP 서버와의 시간 동기화를 강제 합니다.
* `Enable-HcsPing`및 `Disable-HcsPing`: StorSimple 장치에서 이러한 cmdlet tooallow hello 호스트 tooping hello 네트워크 인터페이스를 사용 합니다. 기본적으로 hello StorSimple 네트워크 인터페이스는 tooping 요청 응답 하지 않습니다.
* `Trace-HcsRoute`: 경로 추적 도구로 이 cmdlet을 사용합니다. 패킷을 tooeach 라우터 hello 방식으로 tooa 최종 대상에 시간 기간 동안 보내고 각 홉에서 반환 된 hello 패킷에 기준으로 결과 계산 합니다. 이후 `Trace-HcsRoute` hello 수준의에서 지정 된 라우터나 링크, 패킷이 손실을 표시 하는 라우터를 확인할 수 있습니다 또는 링크 네트워크 문제를 초래할 수 있습니다.
* `Get-HcsRoutingTable`:이 cmdlet toodisplay hello 로컬 IP 라우팅 테이블을 사용 합니다.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Hello Get-netadapter cmdlet으로 문제 해결
처음 장치 배포에 대 한 네트워크 인터페이스를 구성한 경우 hello 하드웨어 상태 hello 장치 hello 서비스와 아직 등록 되지 않았으므로 hello StorSimple 장치 관리자 서비스 UI에서에서 사용할 수 없는 합니다. 또한 hello **하드웨어 상태가** 서비스 동기화에 영향을 주는 문제가 있는 경우에 특히 블레이드 항상 올바르게 hello 장치의 hello 상태를 반영 하지는 않을 수 있습니다. 이러한 상황에서는 hello를 사용할 수 있습니다 `Get-NetAdapter` cmdlet toodetermine hello 상태 및 네트워크 인터페이스의 상태입니다.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>장치에서 모든 hello 네트워크 어댑터 목록이 toosee
1. StorSimple용 Windows PowerShell을 시작한 다음 `Get-NetAdapter`를 입력합니다. 
2. Hello의 hello 출력을 사용 하 여 `Get-NetAdapter` cmdlet 및 지침 toounderstand 다음 hello hello 네트워크 인터페이스의 상태입니다.
   
   * Hello 인터페이스 정상이 고 사용 가능한 경우 hello **ifIndex** 상태가 **를**합니다.
   * Hello 인터페이스 (네트워크 케이블)을 통해 물리적으로 연결 되지 않은 상태가 표시 되지만 hello **ifIndex** 으로 표시 되 고 **비활성화**합니다.
   * Hello 인터페이스 정상 이지만 사용 되지 않는 경우 hello **ifIndex** 상태가 **NotPresent**합니다.
   * Hello 인터페이스가 없는 경우에이 목록에 나타나지 않습니다. StorSimple 장치 관리자 서비스 UI hello 되는 표시 된이 인터페이스 실패 상태에 있습니다.

방법에 대 한 자세한 내용은 toouse이이 cmdlet을 너무 이동[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) hello Windows PowerShell cmdlet 참조에서에서.

hello 다음 섹션에서는 보여 hello의 출력 샘플 `Get-NetAdapter` cmdlet.

 이러한 샘플에서 컨트롤러 0은 hello 수동 컨트롤러 이며과 다음과 같이 구성 되었습니다.

* DATA 0, DATA 1, DATA 2 및 DATA 3 네트워크 인터페이스가 hello 장치에서.
* DATA 4 및 DATA 5 네트워크 인터페이스 카드 없었습니다. 따라서 hello 출력에 나열 되지 됩니다.
* 데이터 0이 활성화되었습니다.

컨트롤러 1은 hello 활성 컨트롤러 이며과 다음과 같이 구성 되었습니다.

* DATA 0, DATA 1, DATA 2, DATA 3, 데이터 4 및 DATA 5 네트워크 hello 장치에 존재 하는 인터페이스
* 데이터 0이 활성화되었습니다.

**샘플 출력 - 컨트롤러 0**

hello 다음은 컨트롤러 0 (수동 컨트롤러 hello) hello 출력 합니다. 데이터 1, 데이터 2 및 데이터 3는 연결되지 않습니다. DATA 4 및 DATA 5 hello 장치에 있는 되지 않기 때문에 나열 되지 않습니다.

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**샘플 출력 - 컨트롤러 1**

hello 다음은 hello 출력 컨트롤러 1 (활성 컨트롤러 hello)입니다. Hello DATA 0 네트워크 인터페이스 hello 장치에 구성 되어 있고 작업에 합니다.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Hello Test-connection cmdlet으로 문제 해결
Hello를 사용할 수 있습니다 `Test-Connection` cmdlet toodetermine StorSimple 장치 toohello 네트워크 외부에 연결할 수 있는지 여부. Hello 네트워킹 매개 변수를 모두 hello DNS를 포함 하 여 hello 설치 마법사에서 올바르게 구성 되는 경우에 hello을 사용할 수 있습니다 `Test-Connection` cmdlet tooping outlook.com 같은 hello 네트워크 외부의 알려진된 주소입니다.

Ping을 사용할 수 없는 경우이 cmdlet과 ping tootroubleshoot 연결 문제를 사용 하도록 설정 해야 합니다.

Hello hello에서 출력의 샘플 다음 참조 `Test-Connection` cmdlet.

> [!NOTE]
> Hello 첫 번째 예제에서 잘못 된 DNS hello 장치 구성 됩니다. 두 번째 샘플 hello hello DNS 올바릅니다.

**샘플 출력 – 잘못된 DNS**

다음 예제는 hello에서 출력은 없습니다 hello IPV4 및 IPV6 주소에 대 한 DNS 해결 되지 않으면 해당 hello를 나타냅니다. 즉, 외부 네트워크에 없는 연결 toohello는 올바른 DNS 필요한 toobe 제공.

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**샘플 출력 – 올바른 DNS**

다음 예제는 hello, hello DNS 반환 IPV4 주소를 나타내는 DNS가 올바르게 구성 하는 hello를 hello 합니다. 이 연결 toohello 네트워크 외부 인지 확인 합니다.

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Hello Test-hcsmconnection cmdlet으로 문제 해결
사용 하 여 hello `Test-HcsmConnection` 이미 있는 장치에 대 한 cmdlet tooand StorSimple 장치 관리자 서비스에 등록 된 연결입니다. 이 cmdlet를 사용 하면 등록된 된 장치 및 StorSimple 장치 관리자 서비스를 해당 하는 hello hello 연결 상태를 확인 합니다. StorSimple용 Windows PowerShell에서 이 명령을 실행할 수 있습니다.

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>toorun hello Test-hcsmconnection cmdlet
1. 해당 hello 장치가 등록 되어 있는지 확인 합니다.
2. Hello 장치 상태를 확인 합니다. 유지 관리 모드 또는 오프 라인으로 hello 장치를 비활성화 하는 경우 hello 다음 오류 중 하나가 표시 될 수 있습니다.
   
   * Errorcode.cisdevicedecommissioned – 해당 hello 장치를 비활성화 합니다.
   * Errorcode.devicenotready – hello 장치가 유지 관리 모드에 해당 합니다.
   * Errorcode.devicenotready – 해당 hello 장치가 온라인 상태가 아닙니다.
3. 해당 hello StorSimple 장치 관리자 서비스가 실행 중인지 확인 하십시오 (hello를 사용 하 여 [Get-clusterresource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet). Hello 서비스를 실행 하지 않는 경우 다음 오류 hello를 나타날 수 있습니다.
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError – Get-ClusterResource를 실행할 때 예외가 있음을 나타냅니다.
4. Hello 액세스 제어 서비스 (ACS) 토큰을 확인 합니다. 웹 예외를 throw 하는 경우 게이트웨이 문제, 누락 된 프록시 인증, 잘못 된 DNS 또는 인증 실패로 hello 결과 수 있습니다. 다음 오류 hello를 표시 될 수 있습니다.
   
   * Errorcode.cisappliancegateway – HttpStatusCode.BadGateway 예외: 이름 확인자 서비스가 hello hello 호스트 이름을 확인할 수 없습니다.
   * Errorcode.cisapplianceproxy – HttpStatusCode.ProxyAuthenticationRequired 예외 (HTTP 상태 코드 407): hello 클라이언트 hello 프록시 서버를 인증할 수 없습니다.
   * ErrorCode.CiSApplianceDNSError – WebExceptionStatus.NameResolutionFailure 예외 나타냅니다: hello 이름 확인자 서비스가 hello 호스트 이름을 확인할 수 없습니다.
   * Errorcode.cisapplianceacserror – hello 서비스에서 인증 오류를 반환 했지만 연결이 되어 있음을 합니다.
     
     웹 예외가 발생하지 않은 경우 ErrorCode.CiSApplianceFailure을 확인하세요. 이 해당 hello 어플라이언스에 실패 나타냅니다.
5. Hello 클라우드 서비스 연결을 확인 합니다. Hello 서비스 웹 예외를 throw 하는 경우 다음 오류 hello를 나타날 수 있습니다.
   
   * Errorcode.cisappliancegateway – HttpStatusCode.BadGateway 예외: 중간 프록시 서버에서 다른 프록시 또는 hello 원래 서버에서 잘못 된 요청을 받았습니다.
   * Errorcode.cisapplianceproxy – HttpStatusCode.ProxyAuthenticationRequired 예외 (HTTP 상태 코드 407): hello 클라이언트 hello 프록시 서버를 인증할 수 없습니다.
   * ErrorCode.CiSApplianceDNSError – WebExceptionStatus.NameResolutionFailure 예외 나타냅니다: hello 이름 확인자 서비스가 hello 호스트 이름을 확인할 수 없습니다.
   * Errorcode.cisapplianceacserror – hello 서비스에서 인증 오류를 반환 했지만 연결이 되어 있음을 합니다.
     
     웹 예외가 발생하지 않은 경우 ErrorCode.CiSApplianceSaasServiceError를 확인하세요. 이 hello StorSimple 장치 관리자 서비스에 문제가 있음을 나타냅니다.
6. Azure Service Bus 연결을 확인합니다. ErrorCode.CiSApplianceServiceBusError는 hello 장치 toohello 서비스 버스를 연결할 수 없음을 나타냅니다.

hello 로그 파일 CiSCommandletLog0Curr.errlog 및 cisagentsvc0curr.errlog에 예외 정보 같은 추가 정보입니다.

너무 toouse cmdlet hello 하는 방법에 대 한 자세한 내용을 보려면 이동[Test-hcsmconnection](https://technet.microsoft.com/library/dn715782.aspx) hello Windows PowerShell 설명서를 참조 합니다.

> [!IMPORTANT]
> 활성 hello 및 hello 수동 컨트롤러 모두에 대해이 cmdlet을 실행할 수 있습니다.

Hello hello에서 출력의 샘플 다음 참조 `Test-HcsmConnection` cmdlet.

**예제 출력 – StorSimple 업데이트 3을 실행하는 성공적으로 등록된 장치**

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**예제 출력 – 오프라인 장치** 

상태를가 하는 장치에서이 샘플은 **오프 라인** hello Azure 포털의에서.

     Checking device registrationstate: Success
     Device is registered successfully
     Checking connectivity from device tooSaaS.. Failure

hello 장치 hello 현재 웹 프록시 구성을 사용 하 여 연결 하지 못했습니다. 이 수는 hello 웹 프록시 구성 문제 또는 네트워크 연결에 문제가 있습니다. 이 경우, 웹 프록시 설정이 올바르며 웹 프록시 서버가 온라인 상태이고 연결할 수 있는지 확인해야 합니다.

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Hello 동기화 HcsTime cmdlet으로 문제 해결
이 cmdlet toodisplay hello 장치 시간을 사용 합니다. 이 cmdlet tooforce를 유도할 수 있습니다 hello 장치 시간을 NTP 서버 hello와 오프셋에 있는 경우-hello 시간을 NTP 서버와 동기화 합니다.
- Hello 장치와 NTP 서버 간의 hello 오프셋은 5 분 보다 큰 경우 경고 메시지가 표시 됩니다. 
- Hello 오프셋 15 분을 초과 하면 hello 장치가 오프 라인 상태가 됩니다. 이 cmdlet tooforce 시간 동기화를 사용할 수 있습니다. 
- 그러나 hello 오프셋 15 시간을 초과 하면 다음 됩니다 수 tooforce 동기화 hello 시간 및 오류 메시지가 표시 됩니다.

**샘플 출력 – Sync-HcsTime을 사용하여 강제 시간 동기화**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Hello HcsPing 사용 및 사용 안 함 HcsPing cmdlet으로 문제 해결
장치에서 네트워크 인터페이스 hello tooICMP ping 요청에 응답 하는 이러한 cmdlet tooensure를 사용 합니다. 기본적으로 hello StorSimple 네트워크 인터페이스는 tooping 요청 응답 하지 않습니다. 이 cmdlet을 사용 하 여 hello 가장 쉬운 방법은 tooknow 경우에 장치가 온라인 상태이 고 연결할 수 있습니다.

**샘플 출력 – HcsPing 사용 및 HcsPing 사용 안함**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Hello 추적 HcsRoute cmdlet으로 문제 해결
경로 추적 도구로 이 cmdlet을 사용합니다. 패킷을 tooeach 라우터 hello 방식으로 tooa 최종 대상에 시간 기간 동안 보내고 각 홉에서 반환 된 hello 패킷에 기준으로 결과 계산 합니다. Hello cmdlet의 주어진된 라우터나 링크에서 패킷 손실 hello 정도 보여 주기 때문에 어떤 라우터를 확인할 수 있습니다 또는 링크 네트워크 문제를 초래할 수 있습니다.

**Tootrace HcsRoute 추적을 사용 하 여 패킷의 경로 hello 하는 방법을 보여 주는 샘플 출력**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Hello Get HcsRoutingTable cmdlet으로 문제 해결
StorSimple 장치에 대 한이 cmdlet tooview hello 라우팅 테이블을 사용 합니다. 라우팅 테이블은 IP (인터넷 프로토콜) 네트워크를 통해 이동하는 데이터 패킷이 어디로 이동하는지 결정하는 데 도움이 되는 규칙 집합입니다.

hello 라우팅 테이블 hello 인터페이스 보여주며, hello 게이트웨이 경로 데이터 toohello hello는 지정 된 네트워크입니다. 또한 hello 경로 tooreach 특정 대상에 대 한 hello 의사 결정자는 hello 라우팅 메트릭을 제공 합니다. hello 낮은 hello 라우팅 메트릭, hello hello 우선 순위가 높은 합니다.

예를 들어, 2의 네트워크 인터페이스, DATA 2 및 DATA 3의 경우 연결 된 toohello 인터넷에 있는 경우. 데이터 2 및 DATA 3에 대 한 hello 라우팅 메트릭을 인 15, 261 각각 hello 낮은 라우팅 메트릭이 데이터 2 tooreach hello 인터넷을 사용 하는 hello 기본 인터페이스는 다음입니다.

StorSimple 장치에서 업데이트 1을 실행 하는 경우에 DATA 0 네트워크 인터페이스 hello 클라우드 트래픽에 대 한 가장 높은 우선 hello에 있습니다. 이 경우에 다른 클라우드 지원 인터페이스, hello 클라우드 트래픽은 DATA 0 통해 라우팅될 수를 의미 합니다.

Hello를 실행 하는 경우 `Get-HcsRoutingTable` hello 예제와 다음), (으로 매개 변수 hello cmdlet을 지정 하지 않고 cmdlet이 모두 IPv4 및 IPv6 라우팅 테이블을 출력 합니다. 지정할 수 있습니다 `Get-HcsRoutingTable -IPv4` 또는 `Get-HcsRoutingTable -IPv6` tooget 관련 라우팅 테이블입니다.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>단계별 StorSimple 문제 해결 예제
hello 다음 예제에서는 StorSimple 배포의 단계별 문제 해결 Hello 예제 시나리오에서는 장치 등록 hello 네트워크 설정이 나 hello DNS 이름이 잘못 되었음을 나타내는 오류 메시지와 함께 실패 합니다.

반환 된 hello 오류 메시지가 표시 됩니다.

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

hello 오류 hello 다음 중 하나로 인해 발생할 수 없습니다.

* 잘못된 하드웨어 설치
* 잘못된 네트워크 인터페이스
* 잘못된 IP 주소, 서브넷 마스크, 게이트웨이, 기본 DNS 서버 또는 웹 프록시
* 잘못된 등록 키
* 잘못된 방화벽 설정

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate 및 수정 프로그램 hello 장치 등록 문제
1. 장치 구성을 확인 하십시오: hello 활성 컨트롤러에서 실행 `Invoke-HcsSetupWizard`합니다.
   
   > [!NOTE]
   > hello 설치 마법사는 hello 활성 컨트롤러에서 실행 해야 합니다. 연결 된 toohello 활성 컨트롤러를 hello 직렬 콘솔에 표시 된 hello 배너에 있는 tooverify 합니다. hello 배너 연결된 toocontroller 0 또는 컨트롤러 1에 요소가 있는지와 hello 컨트롤러가 활성 또는 수동 인지를 나타냅니다. 자세한 내용은 이동 너무[장치에서 활성 컨트롤러 식별](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device)합니다.
   
2. Hello 장치 올바르게 케이블로 연결 되었는지 확인: hello 네트워크 케이블 hello 장치 백플레인에서을 확인 합니다. hello 케이블은 특정 toohello 장치 모델입니다. 자세한 내용은 이동 너무[StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [8600 StorSimple 장치를 설치](storsimple-8600-hardware-installation.md)합니다.
   
   > [!NOTE]
   > 10gbe 네트워크 포트를 사용 하는 경우 toouse hello QSFP-SFP 어댑터와 SFP 케이블을 제공 해야 합니다. 자세한 내용은 참조 hello [케이블, 스위치 및 송수신 장치 hello 10 GbE 포트에 대 한 권장 목록이](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)합니다.
  
3. Hello 네트워크 인터페이스의 hello 상태를 확인 합니다.
   
   * DATA 0에 대 한 hello 네트워크 인터페이스의 hello Get-netadapter cmdlet toodetect hello 상태를 사용 합니다. 
   * Hello 링크가 작동 하지 않을 경우 hello **ifindex** 해당 hello 인터페이스 다운는 상태 표시 됩니다. 그런 다음 hello 포트 toohello 어플라이언스와 toohello 스위치 toocheck hello 네트워크 연결이 필요 합니다. 잘못 된 케이블 아웃 toorule를 해야 합니다. 
   * DATA 0 포트 hello 활성 컨트롤러에 실패 했습니다 해당 hello의 의심 되는 경우 연결 하 여 확인할 수 있습니다 컨트롤러 1 toohello DATA 0 포트입니다. tooconfirm hello 컨트롤러 0에서에서 hello 장치 뒷면에서 hello 네트워크 케이블을 분리이 hello 케이블 toocontroller 1, 연결 및 hello Get-netadapter cmdlet을 다시 실행 하십시오.
     경우 DATA 0 포트는 컨트롤러에 오류가 발생 하면 hello [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 다음 단계에 대 한 합니다. 시스템에서 tooreplace hello 컨트롤러를 할 수 있습니다.
4. Hello 연결 toohello 스위치를 확인 합니다.
   
   * 컨트롤러 0과 컨트롤러 1의 기본 인클로저에 DATA 0 네트워크 인터페이스가 있는 hello에 있는지 확인 동일한 서브넷입니다. 
   * Hello 허브 또는 라우터에서 확인 합니다. 두 컨트롤러 toohello 연결 해야 하는 일반적으로 동일한 허브 또는 라우터에서 합니다. 
   * Hello 연결에 사용 하는 hello 스위치 hello에 있는 두 컨트롤러에 대 한 데이터 0을 갖도록 vLAN이 동일 합니다.
5. 모든 사용자 오류를 제거합니다.
   
   * Hello 설치 마법사를 다시 실행 (실행 **Invoke-hcssetupwizard**)를 입력 하 고 hello 값 오류가 없는지 toomake 다시 합니다. 
   * Hello 등록을 확인 사용 되는 키입니다. 동일한 등록 키를 hello 사용된 tooconnect 여러 장치 tooa StorSimple 장치 관리자 서비스 일 수 있습니다. hello 절차를 사용 하 여 [Get hello 서비스 등록 키](storsimple-8000-manage-service.md#get-the-service-registration-key) 사용 중인 tooensure hello 올바른 등록 키입니다.
     
     > [!IMPORTANT]
     > 실행 되는 여러 서비스를 사용 하도록 설정한 경우 키가 필요 tooensure 해당 hello 등록 hello 적절 한 서비스를 사용 하는 tooregister hello 장치에 대 한 합니다. Hello 잘못 된 StorSimple 장치 관리자 서비스와 장치를 등록 한 할 경우 너무[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 다음 단계에 대 한 합니다. Tooperform hello 장치 (데이터가 손실 될 수 있습니다) 공장 기본 설정으로 할 수 있습니다 toothen toohello 의도 한 서비스 연결 합니다.
     > 
     > 
6. 네트워크 외부 연결 toohello 있다고 hello Test-connection cmdlet tooverify를 사용 합니다. 자세한 내용은 이동 너무[hello Test-connection cmdlet으로 문제를 해결](#troubleshoot-with-the-test-connection-cmdlet)합니다.
7. 방화벽 간섭을 확인합니다. 가상 해당 hello를 확인 한 IP (VIP), 서브넷, 게이트웨이 및 DNS 설정이 모두 올바른지, 연결 문제를 계속 나타나면 경우 방화벽이 장치와 외부 네트워크 hello 간의 통신을 차단 하 고 있습니다. 포트 80 및 443 아웃 바운드 통신에 대 한 StorSimple 장치에서 사용 가능한 지 tooensure가 필요 합니다. 자세한 내용은 [StorSimple 장치에 대한 네트워킹 요구 사항](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)을 참조하세요.
8. Hello 로그를 검토 합니다. 너무 이동[패키지 및 장치 로그를 사용할 수 있는 문제 해결을 위해 지원](#support-packages-and-device-logs-available-for-troubleshooting)합니다.
9. Hello 앞의 단계 해결 되지 않으면 hello 문제 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 도움을 요청 합니다.

## <a name="next-steps"></a>다음 단계
[어떻게 toouse hello 진단 도구 tootroubleshoot StorSimple 장치에 알아봅니다](storsimple-8000-diagnostics.md)합니다.

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
