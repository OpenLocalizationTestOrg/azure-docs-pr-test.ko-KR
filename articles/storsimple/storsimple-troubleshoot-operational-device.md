---
title: "배포 된 StorSimple 장치 aaaTroubleshoot | Microsoft Docs"
description: "설명 방법을 현재 배포 되 고 작동 하는 StorSimple 장치에서 발생 하는 오류 toodiagnose 및 수정 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>작동 StorSimple 장치 문제 해결
## <a name="overview"></a>개요
이 문서에서는 StorSimple 장치가 배포되고 작동된 후 발생할 수 있는 구성 문제를 해결하기 위한 유용한 문제 해결 지침을 제공합니다. 일반적인 문제, 가능한 원인 및 Microsoft Azure StorSimple을 실행 하는 경우 발생할 수 있는 문제를 해결 하는 권장된 단계 toohelp를 설명 합니다. 이 정보는 tooboth hello StorSimple 온-프레미스 물리적 장치 및 hello StorSimple 가상 장치에 적용합니다.

단계 뿐만 아니라 Microsoft Azure StorSimple 작업 중 발생할 수 있는 오류 코드의 목록을 찾을 수 있습니다이 문서의 hello 끝 tooresolve hello 오류 취할 수 있습니다. 

## <a name="setup-wizard-process-for-operational-devices"></a>운영 장치에 대한 설치 마법사 프로세스
Hello 설치 마법사를 사용 하 여 ([Invoke-hcssetupwizard][1]) toocheck 장치 구성을 hello 및 필요에 따라 수정 조치를 수행 합니다.

이전에 구성 및 작동 장치에서 hello 설치 마법사를 실행 하는 경우에 hello 프로세스 흐름 다릅니다. 유일한 hello 다음 항목을 변경할 수 있습니다.

* IP 주소, 서브넷 마스크 및 게이트웨이
* 기본 DNS 서버
* 기본 NTP 서버
* 선택적 웹 프록시 구성

hello 작업 관련된 toopassword 컬렉션 및 장치 등록 hello 설치 마법사를 수행 하지 않습니다.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Hello 설치 마법사의 후속 실행 하는 동안 발생 하는 오류
hello 오류 및 권장된 조치 tooresolve에 대 한 가능한 원인으로, 다음 표에 hello 작동 하는 장치에서 hello 설치 마법사를 실행할 때 발생할 수 있는 hello 오류를 설명 합니다. 

| 아니요. | 오류 메시지 또는 조건 | 가능한 원인 | 권장 작업 |
|:--- |:--- |:--- |:--- |
| 1 |오류 350032: 이 장치는 이미 비활성화되었습니다. |비활성화 된 장치에서 hello 설치 마법사를 실행 하는 경우이 오류가 나타납니다. |[Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요. 비활성화된 장치를 제공할 수 없습니다. 공장 재설정 hello 장치를 다시 활성화할 수 있습니다 필요할 수 있습니다. |
| 2 |Invoke-HcsSetupWizard : ERROR_INVALID_FUNCTION(HRESULT: 0x80070001에서 예외 발생) |hello DNS 서버 업데이트가 실패 했습니다. DNS 설정은 전역 설정 되며 모든 hello 사용 네트워크 인터페이스를 통해 적용 됩니다. |Hello 인터페이스를 사용 하도록 설정 하 고 hello DNS 설정을 다시 적용 합니다. 이러한 설정은 전역 설정 때문에 설정된 된 다른 인터페이스에 대 한 hello 네트워크를 방해할 수 있습니다.이 있습니다. |
| 3 |hello 장치 hello StorSimple Manager 서비스 포털의 온라인 toobe 나타나지만 hello 작업이 실패 하면 toocomplete hello 최소 설치를 시도 하 고 hello 구성을 저장 합니다. |초기 설치 작업 동안 hello 웹 프록시 구성 하지 않은 위치에 실제 프록시 서버가 불구 합니다. |사용 하 여 hello [Test-hcsmconnection cmdlet] [ 2] toolocate hello 오류입니다. [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 없습니다 toocorrect hello 문제가 있다면 합니다. |
| 4 |Invoke-hcssetupwizard: 값이 예상 hello 범위에 속하지 않습니다. |잘못된 서브넷 마스크 때문에 이 오류가 발생합니다. 가능한 원인:  <ul><li> hello 서브넷 마스크 누락 되었거나 비어 있습니다.</li><li>hello Ipv6 접두사 형식이 올바르지 않습니다.</li><li>hello 인터페이스는 클라우드를 지원 하지만 hello 게이트웨이가 누락 되었거나 잘못 되었습니다.</li></ul>0 데이터를 자동으로 hello 설치 마법사를 통해 구성 된 경우 클라우드 사용 note 합니다. |toodetermine hello 문제 서브넷 0.0.0.0 또는 256.256.256.256을 사용 하 고 hello 출력 한 다음 확인 합니다. 필요에 따라 hello 서브넷 마스크, 게이트웨이 및 Ipv6 접두사에 대 한 올바른 값을 입력 합니다. |

## <a name="error-codes"></a>오류 코드
오류는 숫자 순서로 나열됩니다.

| 오류 번호 | 오류 텍스트 또는 설명 | 권장되는 사용자 작업 |
|:--- |:--- |:--- |
| 10502 |저장소 계정에 액세스하는 동안 오류가 발생했습니다. |몇 분간 기다린 다음 작업을 다시 시도하세요. Hello 오류가 계속 되 면 다음 단계에 대 한 Microsoft 지원에 문의 하세요. |
| 40017 |hello 백업 정책에 지정 된 볼륨 hello 장치에서 찾을 수 없습니다으로 hello 백업 작업이 실패 했습니다. |Hello 백업 작업을 다시 시도, hello 오류가 계속 되 면 Microsoft 지원에 문의 합니다. 다음 단계를 문의하세요. |
| 40018 |hello 장치에서 발견 된 hello 백업 정책에 지정 된 hello 볼륨 중 hello 백업 작업이 실패 했습니다. |Hello 백업 작업을 다시 시도, hello 오류가 계속 되 면 Microsoft 지원에 문의 합니다. 다음 단계를 문의하세요. |
| 390061 |hello 시스템은 사용 중 또는 사용할 수 없습니다. |몇 분간 기다린 다음 작업을 다시 시도하세요. Hello 오류가 계속 되 면 다음 단계에 대 한 Microsoft 지원에 문의 하세요. |
| 390143 |오류 코드가 390143인 오류가 발생했습니다. (알 수 없는 오류.) |Hello 오류가 계속 되 면 Microsoft 지원에 다음 단계에 문의 하세요. |

## <a name="next-steps"></a>다음 단계
없습니다 tooresolve hello 문제가 있다면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 도움을 요청 합니다. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
