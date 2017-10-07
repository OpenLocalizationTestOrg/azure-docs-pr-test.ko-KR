---
title: "GitHub 엔터프라이즈와 소스 제어 통합을 자동화 aaaAzure | Microsoft Docs"
description: "Hello 방법 자세히 설명 합니다. 자동화 runbook의 소스 제어에 대 한 GitHub 엔터프라이즈와 tooconfigure 통합 합니다."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Azure Automation 시나리오 - GitHub Enterprise와 Automation 소스 제어 통합

자동화는 현재 자동화 계정 tooa GitHub 소스 제어 리포지토리에 tooassociate runbook 수 있는 소스 제어 통합을 지원 합니다.  그러나 배포한 고객의 [GitHub Enterprise](https://enterprise.github.com/home) toosupport 자신의 DevOps 사례, toouse 할 것은 runbook의 toomanage hello 수명 주기 개발 tooautomate 비즈니스 프로세스 및 서비스 관리 작업입니다.  

이 시나리오에서는 hello Azure 리소스 관리자 모듈 및 Git 도구가 설치 된 Hybrid Runbook Worker로 구성 된 데이터 센터의 Windows 컴퓨터를가지고 있습니다.  hello 하이브리드 작업자 컴퓨터의 hello 로컬 Git 리포지토리를 복제를 있습니다.  Hello runbook hello 하이브리드 작업자에서 실행 될 때 hello Git 디렉터리 동기화 되 고 hello 자동화 계정으로 hello runbook 파일 내용을 가져옵니다.

이 문서에서는 설명 어떻게 Azure 자동화 환경에서이 구성을 tooset 합니다. 자동화 hello 보안 자격 증명으로 구성 하 여 시작, runbook 필요한 toosupport이이 시나리오에서는 및의 데이터에서 Hybrid Runbook Worker 배포 toorun hello runbook 가운데 맞춤 및 GitHub Enterprise 리포지토리 toosynchronize 액세스 자동화 계정 사용 하 여 runbook입니다.  


## <a name="getting-hello-scenario"></a>Hello 시나리오를 가져오기

이 시나리오 hello에서 직접 가져올 수 있는 두 개의 PowerShell runbook 이루어져 [Runbook 갤러리](automation-runbook-gallery.md) hello Azure 포털 또는 hello에서 다운로드 [PowerShell 갤러리](https://www.powershellgallery.com)합니다.

### <a name="runbooks"></a>Runbook

Runbook | 설명| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook은 hello worker에서 runbook hello 자동화 계정에 순서 tooimport runbook에서 Azure로 인증할 수 있도록 자동화 계정 tooa 하이브리드 작업자에서 RunAs 인증서를 내보냅니다.| 
Sync-LocalGitFolderToAutomationAccount | Runbook 동기화 hello 하이브리드 컴퓨터의 로컬 Git 폴더 hello 한 다음 hello 자동화 계정으로 hello runbook 파일 (*.ps1)를 가져옵니다.|

### <a name="credentials"></a>자격 증명

자격 증명 | 설명|
-----------|------------|
GitHRWCredential | 자격 증명 자산 권한 toohello 하이브리드 작업자와 toocontain hello 사용자 이름 및 사용자의 암호를 만듭니다.|

## <a name="installing-and-configuring-this-scenario"></a>이 시나리오 설치 및 구성

### <a name="prerequisites"></a>필수 조건

1. hello 동기화 LocalGitFolderToAutomationAccount runbook hello를 사용 하 여 인증 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)합니다. 

2. Microsoft Operations Management Suite (OMS) 작업 영역 설정 하 고 구성 하는 Azure 자동화 솔루션 hello로은 필요 합니다.  생성 되 고 hello를 실행할 때를 구성 하지 않은 경우이 시나리오를 구성 하 고 hello 자동화 사용 되는 계정 tooinstall와 관련이 있는, **새로 OnPremiseHybridWorker.ps1** hello 하이브리드에서 스크립트 runbook worker입니다.        

    > [!NOTE]
    > 현재 hello 다음 지역만 자동화 통합을 지 원하는 OMS- **오스트레일리아 남동부**, **미국 동부 2**, **동남 아시아**, 및 **서 부 유럽**합니다. 

3. 컴퓨터를 호스트 하는 또한 hello GitHub 소프트웨어 hello runbook 파일을 유지 하 여 전용된 하이브리드 Runbook 작업자로 사용 될 수 있습니다 (*runbook*.ps1) hello 파일 시스템 toosynchronize GitHub 사이 있는 원본 디렉터리에 사용자 및 자동화 계정입니다.

### <a name="import-and-publish-hello-runbooks"></a>가져오기 및 hello runbook 게시

tooimport hello *내보내기 RunAsCertificateToHybridWorker* 및 *동기화 LocalGitFolderToAutomationAccount* hello Azure 포털에서에서 자동화 계정의 hello Runbook 갤러리에서에서 runbook hello 절차에 따라 [hello Runbook 갤러리에서에서 Runbook 가져오기](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal)합니다. 성공적으로 가져온 자동화 계정으로 후 hello runbook을 게시 합니다.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Hybrid Runbook Worker 배포 및 구성

Hello 요구 사항을 검토 하 고의 hello 절차를 사용 하 여 hello 자동화 된 설치 단계를 수행 해야 데이터 센터에 이미 배포 된 Hybrid Runbook Worker가 [Azure 자동화 Hybrid Runbook Worker-설치 자동화 구성과](automation-hybrid-runbook-worker.md#automated-deployment)합니다.  컴퓨터에 hello 하이브리드 작업자를 성공적으로 설치한 후 수행 하는 구성 toosupport이이 시나리오 단계 toocomplete 다음 hello 합니다.

1. Toohello 컴퓨터 호스팅 hello 하이브리드 Runbook 작업자 역할에 로컬 관리자 권한이 있는 계정으로 서명과 디렉터리 toohold hello Git runbook 파일을 만듭니다.  Hello 내부 Git 리포지토리 toohello 디렉터리를 복제 합니다.
2. 이미 않아도 만든 실행 계정 또는 toocreate 한 새 이러한 용도로 전용를 원하는 경우 hello Azure 포털에서에서 탐색 tooAutomation 계정을 자동화 계정을 선택한 만들기는 [자격 증명 자산](automation-credentials.md) 입니다 hello 사용자 이름 및 사용자 권한 toohello 하이브리드 작업자에 대 한 암호를 포함합니다.  
3. 자동화 계정에서 [hello runbook 편집](automation-edit-textual-runbook.md)**내보내기 RunAsCertificateToHybridWorker** hello hello 변수 값을 수정 하 고 *$Password* 강력한와 암호입니다.    Hello 값을 수정한 후 클릭 **게시** toohave hello runbook의 초안 버전을 hello 게시 합니다. 
5. Hello runbook을 시작 **내보내기 RunAsCertificateToHybridWorker**, 및 hello **Runbook 시작** 블레이드 hello 옵션 아래에서 **실행 설정** hello옵션을선택**Hybrid Worker** 및이 시나리오에 대해 이전에 만든 hello 드롭다운 목록에서 선택 hello Hybrid worker 그룹입니다.  

    이 runbook hello 작업자의 % (이 시나리오-가져오기 runbook toohello 자동화 계정에 대 한 특정)에 Azure 리소스가 순서 toomanage의 연결 계정으로 실행 hello를 사용 하 여 Azure로 인증할 수 있도록 인증서 toohello 하이브리드 작업자를 내보냅니다.

4. 자동화 계정에서 선택 hello Hybrid worker 그룹 앞에서 만든 및 [RunAs 계정을 지정](automation-hrw-run-runbooks.md#runas-account) hello Hybrid worker 그룹 및 선택한 hello 자격 증명 자산 방금 또는 이미 만들었습니다.  이렇게 하면 해당 hello 동기화 runbook Git 명령을 실행할 수 있습니다. 
5. Hello runbook을 시작 **동기화 LocalGitFolderToAutomationAccount**, hello 다음과 같은 필수 입력된 매개 변수 값을 제공 및 hello **Runbook 시작** 블레이드 hello 옵션 아래에서 **실행 설정** hello 옵션을 선택 **Hybrid Worker** 및이 시나리오에 대해 이전에 만든 hello 드롭다운 목록에서 선택 hello Hybrid worker 그룹:
    * *ResourceGroup* -hello 자동화 계정에 연결 된 리소스 그룹의 이름
    * *AutomationAccountName* -hello 자동화 계정 이름
    * *GitPath* -hello 로컬 폴더 또는 파일 크기가 hello Hybrid Runbook Worker에 toopull 최신 변경 내용을 Git가 설정

    Hello 하이브리드 작업자 컴퓨터의 로컬 Git 폴더 hello 동기화 되 고 hello 소스 디렉터리 toohello 자동화 계정에서에서 hello.ps1 파일을 가져옵니다.

    ![Sync-LocalGitFolderToAutomationAccount Runbook 시작](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Hello에서 선택 하 여 hello runbook에 대 한 작업 요약 정보를 볼 **Runbook** 자동화 계정 및 선택 hello 블레이드 **작업** 바둑판식으로 배열입니다.  Hello를 선택 하 여 성공적으로 완료 확인 **모든 로그** 타일 및 hello 자세한 로그 스트림 검토 합니다.  

## <a name="next-steps"></a>다음 단계

-  runbook 형식이, 장점 및 제한 사항에 대해 자세히 tooknow 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)
-  PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
