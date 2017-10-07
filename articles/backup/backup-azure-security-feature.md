---
title: "aaaSecurity 기능 toohelp Azure 백업을 사용 하는 하이브리드 백업은 보호 | Microsoft Docs"
description: "Azure 백업 toomake 백업 보다 안전한에 toouse 보안 기능이 하는 방법에 대해 알아봅니다"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>보안 기능 toohelp Azure 백업을 사용 하는 하이브리드 백업 보호
맬웨어, 랜섬웨어 및 침입과 같은 보안 문제에 대한 우려는 증가하고 있습니다. 이러한 보안 문제는 돈과 데이터 측면 모두에서 비용이 많이 들 수 있습니다. 보안을 제공 하는 Azure 백업에 이제 이러한 공격은 tooguard 기능 toohelp 하이브리드 백업 보호 합니다. 이 문서에서는 어떻게 tooenable 및 사용 하 여 이러한 기능에 Azure 복구 서비스 에이전트 및 Azure 백업 서버를 사용 하 여 설명 합니다. 이러한 기능으로는 다음이 포함됩니다.

- **방지**. 암호 변경과 같은 중요한 작업이 수행될 때마다 추가적인 인증 계층이 제공됩니다. 이 유효성 검사는 tooensure 등의 작업이 될 수 있는 올바른 Azure 자격 증명이 있는 사용자가 수행 합니다.
- **경고**. Toohello 구독 관리자 때마다 백업 데이터 삭제와 같은 중요 한 작업을 수행 하는 전자 메일 알림이 전송 됩니다. 이 전자 메일을 통해 해당 hello 사용자 등의 작업에 대 한 신속 하 게 알려집니다.
- **복구**. 삭제 된 백업 데이터 추가 대 한 hello 삭제의 hello 날짜에서 14 일 동안 유지 됩니다. 이렇게 하면 hello 데이터를 복구할 특정된 기간 내에서 되므로 공격이 발생 하는 경우에 데이터가 손실 되지 않습니다. 또한 최소 복구 지점의 더 많은 수 tooguard 손상 데이터에 대 한 유지 관리 됩니다.

> [!NOTE]
> IaaS(Infrastructure as a Service) VM 백업으로 인프라를 사용하는 경우 보안 기능은 사용하지 말아야 합니다. 이러한 기능은 아직 IaaS VM 백업에 사용할 수 없으므로 사용하도록 설정해도 영향을 미치지 않습니다. 다음을 사용하는 경우에만 보안 기능을 사용하도록 설정해야 합니다. <br/>
>  * **Azure Backup 에이전트**. 최소 에이전트 버전 2.0.9052. 이러한 기능을 사용 하도록 설정한 후 toothis tooperform 중요 한 작업 에이전트 버전을 업그레이드 해야 합니다. <br/>
>  * **Azure Backup Server**. Azure Backup Server 업데이트 1을 포함한 최소 Azure Backup 에이전트 버전 2.0.9052. <br/>
>  * **System Center Data Protection Manager**. Data Protection Manager 2012 R2 UR12 또는 Data Protection Manager 2016 UR2를 포함한 최소 Azure Backup 에이전트 버전 2.0.9052. <br/> 


> [!NOTE]
> 이러한 기능은 Recovery Services 자격 증명 모음에만 사용할 수 있습니다. 복구 서비스 자격 증명 모음을 새로 만든 모든 hello는 이러한 기능이 기본적으로 활성화 되어 있습니다. 기존 복구 서비스 자격 증명 모음에 대 한 사용자가 hello 다음 섹션에에서 언급 된 hello 단계를 사용 하 여 로그온이 기능을 사용 합니다. 기능을 사용 하는 hello, 후 tooall hello 복구 서비스 에이전트 컴퓨터, Azure 백업 서버 인스턴스 및 Data Protection Manager 서버 hello 모음에 등록도 적용 됩니다. 이 기능의 설정은 일회성 작업이며 사용하도록 설정한 후에는 사용하지 않도록 설정할 수 없습니다.
>

## <a name="enable-security-features"></a>보안 기능 사용
복구 서비스 자격 증명 모음을 만드는 경우 모든 hello 보안 기능을 사용할 수 있습니다. 기존 자격 증명 모음으로 작업하는 경우 다음 단계를 수행하여 보안 기능을 사용하도록 설정합니다.

1. Azure 자격 증명을 사용 하 여 Azure 포털 toohello에 로그인 합니다.
2. **찾아보기**를 선택하고 **Recovery Services**를 입력합니다.

    ![Azure Portal의 찾아보기 옵션의 스크린샷](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다. 이 목록에서 자격 증명 모음을 선택합니다. hello 선택한 자격 증명 모음 대시보드를 엽니다.
3. 아래에서 hello 자격 증명 모음에 나타나는 항목의 hello 목록 **설정**, 클릭 **속성**합니다.

    ![Recovery Services 자격 증명 모음 옵션의 스크린샷](./media/backup-azure-security-feature/vault-list-properties.png)
4. **보안 설정**에서 **업데이트**를 클릭합니다.

    ![Recovery Services 자격 증명 모음 속성의 스크린샷](./media/backup-azure-security-feature/security-settings-update.png)

    hello 업데이트 링크 엽니다 hello **보안 설정** 블레이드를 hello 기능에 대해 간략하게 설명 하 고 할 수 있습니다.
5. Hello 드롭 다운 목록에서 **Azure Multi-factor Authentication 구성 했습니까?**를 사용 하는 경우 값 tooconfirm 선택 [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)합니다. 사용 하는 경우 다른 장치 (예: 휴대폰)에서 tooauthenticate toohello Azure 포털에에서 서명 하는 동안 묻습니다.

   백업에 중요 한 작업을 수행 하는 경우 보안 PIN을 hello Azure 포털에서 사용할 수 있는 tooenter 수 있습니다. Azure Multi-Factor Authentication을 사용하도록 설정하면 보안 계층이 추가됩니다. 유효한 Azure 자격 증명이 있는 사용자 권한을 부여 하 고 두 번째 장치에서 인증에 hello Azure 포털에 액세스할 수 있습니다.
6. 선택한 toosave 보안 설정 **사용** 클릭 **저장**합니다. 선택할 수 있습니다 **사용** hello에서 값을 선택한 후에 **Azure Multi-factor Authentication 구성 했습니까?** hello 이전 단계에서 목록입니다.

    ![보안 설정의 스크린샷](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>삭제된 백업 데이터 복구
백업 추가 14 일 동안 삭제 된 백업 데이터를 유지 하며 삭제 되지는 않습니다 경우 즉시 hello **delete 백업 데이터와 함께 백업 중지** 작업이 수행 됩니다. toorestore hello 14 일 동안에서이 데이터는 hello 사용 하는지에 따라 단계를 수행 합니다.

**Azure Recovery Services 에이전트** 사용자의 경우:

1. 백업이 수행 된 hello 컴퓨터를 계속 사용할 수 있는 경우 사용 하 여 [데이터 toohello 복구 동일한 컴퓨터](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) Azure 복구 서비스에서는 모든 hello 이전 복구 지점에서 toorecover 합니다.
2. 이 컴퓨터를 사용할 수 없는 경우 사용 하 여 [복구 tooan 대체 컴퓨터](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse 다른 Azure 복구 서비스 컴퓨터 tooget이이 데이터입니다.

**Azure Backup Server** 사용자:

1. 백업이 수행 된 hello 서버 계속 사용할 수 없으면 삭제 hello 데이터 원본을 다시 보호 하 고 hello를 사용 하 여 **데이터 복구** 모든 hello 이전 복구 지점에서 toorecover 기능입니다.
2. 이 서버를 사용할 수 없는 경우 사용 하 여 [다른 Azure 백업 서버에서 데이터를 복구할](backup-azure-alternate-dpm-server.md) toouse 다른 Azure 백업 서버 인스턴스 tooget이이 데이터입니다.

**Data Protection Manager** 사용자의 경우:

1. 백업이 수행 된 hello 서버 계속 사용할 수 없으면 삭제 hello 데이터 원본을 다시 보호 하 고 hello를 사용 하 여 **데이터 복구** 모든 hello 이전 복구 지점에서 toorecover 기능입니다.
2. 이 서버를 사용할 수 없는 경우 사용 하 여 [외부 DPM 추가](backup-azure-alternate-dpm-server.md) toouse 다른 Data Protection Manager 서버 tooget이이 데이터입니다.

## <a name="prevent-attacks"></a>공격을 방지
유효한 사용자만 다양 한 작업을 수행할 수 있는지 toomake 검사가 추가 되었습니다. 여기에는 추가적인 인증 계층 제공 및 복구를 위한 최소 보존 범위 유지 관리가 포함됩니다.

### <a name="authentication-tooperform-critical-operations"></a>인증 tooperform 중요 한 작업
추가 계층을 추가 하면 중요 한 작업에 대 한 인증의 일부로 보안 PIN 프롬프트 tooenter 수행할 때 **Delete 데이터로 보호 중지** 및 **변경 암호** 작업 .

tooreceive이이 핀:

1. Azure 포털 toohello에 로그인 합니다.
2. 너무 찾아보기**복구 서비스 자격 증명 모음** > **설정** > **속성**합니다.
3. **보안 PIN** 아래에서 **생성**을 클릭합니다. Hello PIN toobe hello Azure 복구 서비스 에이전트 사용자 인터페이스에 입력 한 포함 된 블레이드가 열립니다.
    이 PIN은 5분 동안만 유효하며 해당 시간이 지나면 자동으로 생성됩니다.

### <a name="maintain-a-minimum-retention-range"></a>최소 보존 범위 유지 관리
복구의 올바른 숫자 항상 있는지 tooensure 지점을 사용할 수 있는, 검사를 수행 하는 hello 추가 되었습니다.

- 일일 보존의 경우 최소 **7**일 보존이 수행되어야 합니다.
- 주간 보존의 경우 최소 **4**주 보존이 수행되어야 합니다.
- 월간 보존의 경우 최소 **3**개월 보존이 수행되어야 합니다.
- 연간 보존의 경우 최소 **1**년 보존이 수행되어야 합니다.

## <a name="notifications-for-critical-operations"></a>중요한 작업에 대한 알림
일반적으로 중요 한 작업을 수행 하면 구독 admin 님 안녕하세요 hello 작업에 대 한 세부 정보와 함께 전자 메일 알림이 전송 됩니다. Hello Azure 포털을 사용 하 여 이러한 알림 추가 전자 메일 받는 사람을 구성할 수 있습니다.

이 문서에 언급 된 hello 보안 기능 대상된 공격에 대 한 철저 한 방어 메커니즘을 제공 합니다. 무엇 보다도 하는 경우 발생 하는 공격 이러한 기능 제공 hello 기능 toorecover 데이터입니다.

## <a name="troubleshooting-errors"></a>문제 해결 오류
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 정책 변경 |hello 백업 정책을 수정할 수 없습니다. 오류: tooan 내부 서비스 오류 [0x29834] 인해 hello 현재 작업이 실패 했습니다. Hello 작업을 잠시 후 다시 시도 하십시오. Hello 문제가 지속 되 면 Microsoft 지원에 문의 하세요. |**원인:**<br/>이 오류는 보안 설정 사용 hello 최소 값 위에 지정 된 아래의 tooreduce 보존 범위를 시도 하 고 지원 되지 않는 버전에 있는 (지원 되는 버전은이 문서의 첫 번째 참고에 지정 됨). <br/>**권장 작업:**<br/> Hello 최소 보존 지정 된 기간 (3 주 매주, 매월 또는 매년에 대 한 1 년 동안 매일, 4 개의 주에 대 한 일) 위에 보존 기간을 설정 해야이 경우 tooproceed 정책과 관련 업데이트 합니다. 필요에 따라 선호 되는 방법은 tooupdate 백업 에이전트가 있는 경우, Azure 백업 서버 및/또는 DPM UR tooleverage 모든 hello 보안 업데이트입니다. |
| 암호 변경 |입력한 보안 PIN이 잘못되었습니다. (ID: 100130) 올바른 보안 PIN toocomplete hello이이 작업을 제공 합니다. |**원인:**<br/> 이 오류는 중요한 작업(예: 암호 변경)을 수행하는 동안 잘못되거나 만료된 보안 PIN을 입력하는 경우 발생합니다. <br/>**권장 작업:**<br/> toocomplete hello 작업 유효한 보안 PIN을 입력 해야 합니다. tooget hello PIN tooAzure 포털에 로그인 하 고 탐색 tooRecovery 서비스 자격 증명 모음 > 설정 > 속성 > 보안 PIN을 생성 합니다. 이 PIN toochange 암호를 사용 합니다. |
| 암호 변경 |작업이 실패했습니다. ID: 120002 |**원인:**<br/>이 오류에는 보안 설정 사용, toochange 암호 시도 및 지원 되지 않는 버전 (이 문서의 첫 번째 참고에 지정 된 유효 버전)에 있는 경우 제공 됩니다.<br/>**권장 작업:**<br/> toochange 암호 백업 에이전트 toominimum 버전 최소 2.0.9052, Azure 백업 서버 toominimum 업데이트 1, 및/또는 DPM 2012 R2 UR12 또는 DPM 2016 UR2 (다운로드 링크 아래) 유효한 보안 PIN을 입력 한 다음 DPM toominimum 먼저 업데이트 해야 있습니다. tooget hello PIN tooAzure 포털에 로그인 하 고 탐색 tooRecovery 서비스 자격 증명 모음 > 설정 > 속성 > 보안 PIN을 생성 합니다. 이 PIN toochange 암호를 사용 합니다. |

## <a name="next-steps"></a>다음 단계
* [Azure 복구 서비스 자격 증명 모음 시작](backup-azure-vms-first-look-arm.md) tooenable 이러한 기능입니다.
* [Hello 최신 Azure 복구 서비스 에이전트 다운로드](http://aka.ms/azurebackup_agent) toohelp Windows 컴퓨터를 보호 하 고 공격에 대 한 백업 데이터를 보호 합니다.
* [다운로드는 최신 Azure 백업 서버 hello](https://aka.ms/latest_azurebackupserver) toohelp 작업 부하를 보호 하 고 공격에 대 한 백업 데이터를 보호 합니다.
* [System Center 2012 R2 Data Protection Manager에 대 한 UR12 다운로드](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) 또는 [UR2 System Center 2016 Data Protection Manager에 대 한 다운로드](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp 작업 부하를 보호 하 고 공격에 대 한 백업 데이터를 보호 합니다.
