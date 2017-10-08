---
title: "장애 조치 및 Azure Site Recovery에서 복구에 대 한 복구 계획 aaaCreate | Microsoft Docs"
description: "설명 방법을 toocreate toofail Azure Site Recovery에서 복구 계획을 통해 사용자 지정 하 고 Vm 및 물리적 서버를 복구 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>복구 계획 만들기


이 문서는 [Azure Site Recovery](site-recovery-overview.md)에서 복구 계획을 만들고 사용자 지정하는 정보를 제공합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

 다음 복구 계획 toodo hello를 만듭니다.

* 장애 조치(failover)된 다음 함께 시작하는 컴퓨터의 그룹을 정의합니다.
* 복구 계획 그룹에서 함께 그룹화하여 컴퓨터 간의 종속성을 모델링합니다. 통해 toofail 예를 들어 특정 응용 프로그램 (를) 실행, hello에 해당 응용 프로그램에 대 한 hello Vm의 모든 그룹화 하 고 동일한 복구 계획 그룹입니다.
* 장애 조치(Failover)를 실행합니다. 복구 계획에서 테스트를 실행하고 계획되거나 계획되지 않은 장애 조치를 실행할 수 있습니다.


## <a name="create-a-recovery-plan"></a>복구 계획 만들기

1. **복구 계획** > **복구 계획 만들기**를 클릭합니다.
   Hello 복구 계획 원본 및 대상에 대 한 이름을 지정 합니다. hello 소스 위치 장애 조치 및 복구에 사용할 수 있는 가상 컴퓨터를 포함 해야 합니다.

    - VMM tooVMM 복제에 대 한 선택 **소스 형식** > **VMM**, 원본 및 대상 VMM 서버 hello 및 합니다. 클릭 **Hyper-v** toosee 클라우드에 보호 되는 합니다.
    - VMM tooAzure 선택 **소스 형식** > **VMM**합니다.  선택 hello 원본 VMM 서버 및 **Azure** hello 대상으로 합니다.
    - (VMM 없음) Hyper-v 복제 tooAzure, 선택 **소스 형식** > **Hyper-v 사이트**합니다. Hello 소스로 선택 hello 사이트 및 **Azure** hello 대상으로 합니다.
    - VMware VM 또는 실제 온-프레미스 서버 tooAzure hello 원본으로 구성 서버를 선택 하 고 **Azure** hello 대상으로 합니다.
    - Azure tooAzure 복구 계획에 대 한 hello 소스로 Azure 지역과 보조 Azure 지역 hello 대상으로 선택 합니다. hello 보조 Azure 지역 toowhich 가상 컴퓨터만 보호 됩니다.
2. **가상 컴퓨터를 선택**, hello 가상 컴퓨터 (또는 복제 그룹) 선택 hello 복구 계획에 tooadd toohello 기본 그룹 (그룹 1) 되도록 합니다.

## <a name="customize-and-extend-recovery-plans"></a>복구 계획 사용자 지정 및 확장

복구 계획을 사용자 지정 및 확장할 수 있습니다.

- **새 그룹을 추가**-추가 복구 계획 그룹 (위쪽 tooseven) toohello 기본 그룹을 추가 하 고 더 많은 컴퓨터 또는 복제 그룹 toothose 복구 계획 그룹을 추가 합니다. 그룹에 추가 하는 hello 순서 대로 번호가 매겨집니다. 가상 컴퓨터나 복제 그룹은 1개의 복구 계획 그룹에만 포함할 수 있습니다.
- **수동 작업 추가**—복구 계획 그룹의 앞 또는 뒤에 실행되는 수동 작업을 추가할 수 있습니다. Hello 복구 계획을 실행 하는 경우 hello 수동 작업을 삽입 하는 hello 지점에서 중지 됩니다. 묻는 대화 상자가 toospecify hello 수동 작업이 완료 되도록 합니다.
- **스크립트 추가**—복구 계획 그룹 앞뒤로 실행되는 스크립트를 추가할 수 있습니다. 스크립트를 추가할 때 새 집합 hello 그룹에 대 한 작업을 추가 합니다. 예를 들어 그룹 1에 대 한 사전 단계 집합이 생기 hello 이름의: 그룹 1: 사전 단계입니다. 모든 사전 단계가 이 집합 내에 나열됩니다. 배포 된 VMM 서버가 있는 경우 스크립트 hello 기본 사이트에 추가할 수 있습니다.
- **Azure runbook 추가**—Azure runbook을 사용하여 복구 계획을 확장할 수 있습니다. 예를 들어 tooautomate 작업 또는 toocreate 단일 단계 복구 합니다. [자세히 알아봅니다](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>스크립트 추가

복구 계획에서 PowerShell 스크립트를 사용할 수 있습니다.

 - Hello 예외 정상적으로 처리할 수 있도록 스크립트 try / catch 블록을 사용 하도록 확인 합니다.
    - Hello 스크립트에는 예외가 있는 경우 실행이 중지 되 고 hello 작업에 실패 한 것으로 표시 합니다.
    - 오류가 발생 하면 hello 스크립트의 남은 부분이 실행 되지 않습니다.
    - 오류가 발생할 경우 예기치 않은 장애 조치가 실행 하는 경우, hello 복구 계획이 계속 됩니다.
    - 계획된 된 장애 조치를 실행 하면 오류가 발생 하는 경우 hello 복구 계획을 중지 합니다. Toofix hello 스크립트, 예상 대로 실행 하는 확인 한 다음을 실행 해야 hello 복구 계획 다시 합니다.
- hello Write-host 명령, 복구 계획 스크립트에서 작동 하지 않는 및 hello 스크립트가 실패 합니다. toocreate 출력 하려면 기본 스크립트를 실행 하는 프록시 스크립트를 만듭니다. Hello를 사용 하 여 모든 출력이 파이프 되는지 있는지 확인 >> 명령입니다.
  * hello 스크립트의 시간이 초과 600 초 내에 반환 하지 않습니다.
  * TooSTDERR, 기록 된 내용이 있으면 hello 스크립트는 실패 한 것으로 분류 됩니다. 이 정보는 hello 스크립트 실행 세부 정보에 표시 됩니다.

배포에서 VMM을 사용하는 경우:

* 복구 계획에 스크립트의 hello VMM 서비스 계정 hello 컨텍스트에서 실행 됩니다. 이 계정에 hello 원격 공유에 있는 hello 스크립트에 대 한 읽기 권한이 있는지 확인 합니다. Hello VMM 서비스 계정 권한 수준에서 스크립트 toorun hello를 테스트 합니다.
* VMM cmdlet은 Windows PowerShell 모듈로 배달됩니다. hello 모듈은 hello VMM 콘솔을 설치할 때 설치 됩니다. 다음 hello 스크립트에 명령을 hello를 사용 하 여 스크립트를 로드할 수 있습니다.
   - Import-Module -Name virtualmachinemanager. [자세히 알아보세요](https://technet.microsoft.com/library/hh875013.aspx)을 확인하세요.
* VMM 배포에 최소 1개의 라이브러리 서버가 있는지 확인합니다. 기본적으로 VMM 서버에 대 한 hello 라이브러리 공유 경로 hello MSCVMMLibrary hello 폴더 이름으로 VMM 서버에 로컬로 있는 합니다.
    * 라이브러리 공유 경로가 원격 (또는 로컬 이지만 mscvmmlibrary 공유 안 함) 이면 hello 공유를 다음과 같이 구성 (사용 하 여 \\예를 들어 libserver2.contoso.com\share\):
      * Hello 레지스트리 편집기를 열고 너무 이동**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure 사이트 Recovery\Registration**합니다.
      * Hello 값 편집 **ScriptLibraryPath** 로 넣습니다 \\libserver2.contoso.com\share\. 지정 hello 전체 FQDN입니다. 사용 권한을 toohello 공유 위치를 제공 합니다.
      * 동일한 hello에 있는 사용자 계정 포함 하는 hello 스크립트를 테스트 해야 VMM hello 대로 사용 권한을 서비스 계정입니다. 독립 실행형 확인은 복구 계획에서 방식으로에서 실행 된 테스트 스크립트가 hello 동일 합니다. Hello VMM 서버에서 실행 정책을 toobypass hello를 다음과 같이 설정.
        * 상승 된 권한을 사용 하 여 hello 64 비트 Windows PowerShell 콘솔을 엽니다.
        * 유형: **Set-executionpolicy bypass**. [자세히 알아봅니다](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>스크립트 또는 수동 작업 tooa 계획 추가

Vm 또는 복제 그룹 tooit를 추가 하 고 hello 계획을 만든 후 스크립트 toohello 기본 복구 계획 그룹을 추가할 수 있습니다.

1. 열기 hello 복구 계획 합니다.
2. Hello에서 항목을 클릭 **단계** 목록으로 이동한 다음 클릭 **스크립트** 또는 **수동 작업**합니다.
3. Toowant tooadd hello 스크립트 또는 이전 또는 이후에 hello 작업 항목 선택 여부를 지정 합니다. 사용 하 여 hello **위로 이동** 및 **아래로 이동** 단추, hello 스크립트의 toomove hello 위치 위나 아래로 이동 합니다.
4. VMM 스크립트를 추가 하는 경우 선택 **장애 조치 tooVMM 스크립트**합니다. **스크립트 경로**, 형식 hello 상대 경로 toohello 공유 합니다. 아래 hello VMM 예제에서는 hello 경로 지정 하면: **\RPScripts\RPScript.PS1**합니다.
5. 책을 실행 하는 Azure 자동화를 추가 하는 경우에 runbook은 찾아서 선택 hello Azure runbook을 적절 한 스크립트는 hello에 hello Azure 자동화 계정을 지정 합니다.
6. Hello 복구 계획의 장애 조치 수행, toomake 있는지 hello 스크립트가 예상 대로 작동 합니다.


### <a name="add-a-vmm-script"></a>VMM 스크립트 추가

VMM 원본 사이트가 있는 경우 hello VMM 서버에서 스크립트를 만들고 복구 계획에 포함할 수 있습니다.

1. Hello 라이브러리 공유에 새 폴더를 만듭니다. 예를 들어, \<VMMServerName>\MSSCVMMLibrary\RPScripts.입니다. Hello 소스에 배치 및 대상 VMM 서버입니다.
2. Hello 스크립트 (예: RPScript)를 만들고 예상한 대로 작동 하는지 확인 합니다.
3. Hello 스크립트 hello 위치에 배치 \<VMMServerName > \MSSCVMMLibrary hello 소스 및 대상 VMM 서버에 있습니다.


## <a name="next-steps"></a>다음 단계

장애 조치를 실행하는 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).
