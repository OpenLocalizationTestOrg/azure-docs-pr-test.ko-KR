---
title: "aaaAzure 백업 에이전트 FAQ | Microsoft Docs"
description: "에 대 한 toocommon 질문에 답변: Azure 백업 에이전트 작업, 백업 및 보존 제한 어떻게 hello 합니다."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "백업 및 재해 복구; 백업 서비스"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Hello Azure 백업 에이전트에 대 한 질문
이 기술 자료이 문서에 대 한 답변 toocommon 질문 toohelp hello Azure 백업 에이전트 구성 요소를 신속 하 게 이해 합니다. 일부 hello 대답의 링크 toohello 문서 포괄적인 정보가 포함 되어 있습니다. Hello에 hello Azure 백업 서비스에 대 한 질문을 게시할 수도 있습니다 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)합니다.

## <a name="configure-backup"></a>백업 구성
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Hello 최신 Azure 백업 에이전트는 어디서 다운로드할 수 있습니까? <br/>
Windows Server, System Center DPM 또는 Windows 클라이언트에서 백업에 대 한 hello 최신 에이전트를 다운로드할 수 있습니다 [여기](http://aka.ms/azurebackup_agent)합니다. 가상 컴퓨터를 tooback hello VM 에이전트 (hello 적절 한 확장명을 자동으로 설치)을 사용 합니다. VM 에이전트 hello hello Azure 갤러리에서에서 만든 가상 컴퓨터에 이미 있습니다.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Hello Azure 백업 에이전트를 구성할 때 저는 증명된 tooenter hello에 대 한 자격 증명 모음 자격 증명입니다. 저장소 자격 증명은 만료되나요?
예, 자격 증명 모음 hello 48 시간 후 만료 됩니다. Hello 파일 만료 되 면 toohello Azure 포털 및 다운로드 hello 자격 증명 모음 자격 증명 파일에서에서 로그인 자격 증명 모음 합니다.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>어떤 드라이브 유형의 파일 및 폴더를 백업할 수 있나요? <br/>
드라이브/볼륨 다음 hello를 백업할 수 없습니다.

* 이동식 미디어: 모든 백업 항목 원본은 고정된 것으로 보고되어야 합니다.
* 읽기 전용 볼륨: hello 볼륨 hello 볼륨 섀도 복사본 서비스 (VSS) toofunction 쓰기 가능 해야 합니다.
* 오프 라인 볼륨: hello 볼륨 VSS toofunction 온라인 상태 여야 합니다.
* 네트워크 공유: hello 볼륨 로컬 toohello 서버 toobe 온라인 백업을 사용 하 여 백업 이어야 합니다.
* Bitlocker로 보호 된 볼륨: hello 볼륨 잠금을 해제 해야 hello 백업이 발생할 수 있습니다.
* 파일 시스템 식별: NTFS는 hello 지원 되는 유일한 파일 시스템입니다.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>내 서버에서 어떤 파일 및 폴더 형식을 백업할 수 있나요?<br/>
hello 유형만 지원 됩니다.

* 암호화
* 압축
* 스파스
* 압축 + 스파스
* 하드 링크: 지원되지 않음, 건너뜀
* 재분석 지점: 지원되지 않음, 건너뜀
* 암호화 + 스파스: 지원되지 않음, 건너뜀
* 압축 스트림: 지원되지 않음, 건너뜀
* 스파스 스트림: 지원되지 않음, 건너뜀

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Hello VM 확장을 사용 하 여 hello Azure 백업 서비스에서 이미 지 원하는 Azure VM에서 hello Azure 백업 에이전트를 설치할 수 있습니까? <br/>
그렇습니다. Azure 백업 기능은 hello VM 확장을 사용 하 여 Azure Vm에 대 한 VM 수준 백업. tooprotect 파일 및 폴더 hello 게스트 Windows 운영 체제에 hello 게스트 Windows 운영 체제에 hello Azure 백업 에이전트를 설치 합니다.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>파일과 폴더 hello Azure VM에서 제공 하는 임시 저장소에는 Azure VM tooback에 hello Azure 백업 에이전트를 설치할 수 있습니까? <br/>
예. Hello 게스트 Windows 운영 체제에 hello Azure 백업 에이전트를 설치 하 고 파일 및 폴더 tootemporary 저장소를 백업 합니다. 임시 저장소 데이터가 초기화된 후에는 백업 작업이 실패합니다. 또한 hello 임시 저장 데이터 삭제 되었지만 toonon 비휘발성 저장소만 복원할 수 있습니다.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Hello 캐시 폴더에 대 한 hello 최소 크기 요구 사항은 무엇입니까? <br/>
hello 캐시 폴더의 hello 크기 hello를 백업 하는 데이터 양을 결정 합니다. 캐시 폴더의 데이터 저장소에 필요한 hello 공간이 5% 이어야 합니다.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>내 서버 tooanother 데이터 센터를 등록 하는 방법<br/>
백업 데이터의 등록 된 hello 자격 증명 모음 toowhich toohello 데이터 센터에 전송 됩니다. hello 가장 쉬운 방법은 toochange hello datacenter는 toouninstall hello 에이전트 hello 에이전트를 다시 설치 하 고 tooa 새 자격 증명 모음 toodesired 데이터 센터에 속해 있는 등록 합니다.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Hello Azure 백업 에이전트는 Windows Server 2012 중복 제거를 사용 하는 서버에서 작동 합니까? <br/>
예. hello 에이전트 서비스는 hello 백업 작업을 준비할 때 중복 제거 된 hello 데이터 toonormal 데이터를 변환 합니다. 그런 다음 백업에 대 한 hello 데이터를 최적화, hello 데이터를 암호화 및 암호화 hello 데이터 toohello 온라인 백업 서비스를 전송 합니다.

## <a name="backup"></a>백업
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Hello Azure 백업 에이전트에 대 한 지정 된 hello 캐시 위치를 변경 하려면 어떻게 해야 합니까?<br/>
다음 목록 toochange hello 캐시 위치 hello를 사용 합니다.

1. Hello 다음 관리자 권한 명령 프롬프트에서 명령을 실행 하 여 hello 백업 엔진을 중지 합니다.

    ```PS C:\> Net stop obengine``` 
  
2. Hello 파일을 이동 하지 마십시오. 대신, 복사 hello 캐시 공간 폴더 tooa 다른 드라이브 공간이 충분 합니다. 백업을 hello 새 캐시 공간 사용 하는 hello를 확인 한 후 hello 원래 캐시 공간을 제거할 수 있습니다.
3. 다음 레지스트리 항목 hello 경로 toohello 새 캐시 공간 폴더와 hello를 업데이트 합니다.<br/>

    | 레지스트리 경로 | 레지스트리 키 | 값 |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*새 캐시 폴더 위치* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*새 캐시 폴더 위치* |

4. Hello 다음 관리자 권한 명령 프롬프트에서 명령을 실행 하 여 hello 백업 엔진을 다시 시작 합니다.

    ```PS C:\> Net start obengine```

Hello 백업 생성 hello 새 캐시 위치에 성공적으로 완료 되 면 hello 원래 캐시 폴더를 제거할 수 있습니다.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>예상 대로 hello Azure 백업 에이전트 toowork hello 캐시 폴더가 넣기<br/>
hello hello 캐시 폴더에 대 한 다음 위치 권장 되지 않습니다.

* 네트워크 공유 또는 이동식 미디어: hello 캐시 폴더에는 온라인 백업을 사용 하 여 백업 해야 하는 로컬 toohello 서버 여야 합니다. 네트워크 위치 또는 USB 드라이브 같은 이동식 미디어는 지원되지 않습니다.
* 오프 라인 볼륨: hello 캐시 폴더를 Azure 백업 에이전트를 사용 하 여 예상된 백업에 대 한 온라인 상태 여야 합니다.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>지원 되지 않는 hello 캐시 폴더의 특성 있습니까?<br/>
hello 다음 특성 또는 바로 조합이 지원 되지 않습니다 hello 캐시 폴더:

* 암호화
* 중복 제거
* 압축
* 스파스
* 재분석 지점

hello 캐시 폴더와 hello 메타 데이터 VHD hello Azure 백업 에이전트에 대 한 hello 필요한 특성을 갖지 않습니다.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>이 방식으로 tooadjust hello 양의 hello 백업 서비스에서 사용 되는 대역폭 있습니까?<br/>
  예 hello를 사용 하 여 **속성 변경** hello 백업 에이전트 tooadjust 대역폭의 옵션입니다. 대역폭을 사용 하는 경우 대역폭 및 hello 횟수 hello 크기를 조정할 수 있습니다. 단계별 지침은 **[네트워크 제한 사용](backup-configure-vault.md#enable-network-throttling)**을 참조하세요.

## <a name="manage-backups"></a>백업 관리
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>이 데이터 tooAzure 백업 하는 Windows server를 바꾸면 어떻게 되나요?<br/>
서버 이름을 바꾸면 현재 구성된 모든 백업이 중지됩니다.
Hello 서버 hello 새 이름을 hello 백업 자격 증명 모음에 등록 합니다. Hello 첫 번째 백업 작업은 새 이름을 hello hello 자격 증명 모음을 등록 하면는 *전체* 백업 합니다. Hello를 사용 하 여 toorecover 데이터 hello 이전 서버 이름으로 자격 증명 모음 toohello 백업 해야 할 경우 [ **다른 서버** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) hello에 대 한 옵션 **데이터 복구** 마법사.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Azure 백업 에이전트를 사용 하 여 백업 정책에 지정 될 수 있는 hello 최대 파일 경로 길이 무엇입니까? <br/>
Azure Backup 에이전트는 NTFS에 의존합니다. hello [파일 경로 길이 지정 hello Windows API에 의해 제한 됩니다](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths)합니다. Tooprotect 원하는 hello 파일의 파일 경로 길이 hello Windows API에서 허용 하는 보다 긴 경우 hello 부모 폴더 또는 hello 디스크 드라이브를 백업 합니다.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Azure Backup 에이전트를 사용하는 Azure Backup 정책의 파일 경로에 어떤 문자가 허용되나요? <br>
 Azure Backup 에이전트는 NTFS에 의존합니다. 파일 사양의 일부분으로 [NTFS 지원 문자](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) 를 사용할 수 있습니다. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>백업 정책을 구성 하려면 경우에 hello 경고, "Azure 백업 구성 되지 않은이 서버에 대 한" 나타남 <br/>
이 경고는 hello 로컬 서버에 저장 된 hello 백업 일정 설정 hello 백업 자격 증명 모음에 저장 된 설정을 hello 동일 hello 없을 때 발생 합니다. Hello 서버 또는 hello 설정을 복구 된 tooa 알려진 좋은 상태 에서도 있었지만 hello 백업 일정 수 동기화를 손실 됩니다. 이 경고가 표시 되 면 [hello 백업 정책을 다시 구성할](backup-azure-manage-windows-server.md) 차례로 **지금 백업 실행** tooresynchronize hello 로컬 서버를 Azure입니다.
