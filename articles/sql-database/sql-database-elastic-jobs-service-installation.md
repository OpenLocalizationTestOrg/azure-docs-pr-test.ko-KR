---
title: "aaaInstalling 탄력적 데이터베이스 작업 | Microsoft Docs"
description: "Hello 탄력적 작업 기능을 설치 하는 과정을 안내 합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>탄력적 데이터베이스 작업 설치 개요
[**탄력적 데이터베이스 작업** ](sql-database-elastic-jobs-overview.md) PowerShell을 통해 설치할 수 있습니다 또는 Azure 클래식 Portal.You를 얻을 수 hello toocreate 액세스 하는 고 hello PowerShell 패키지를 설치 하는 경우에 hello PowerShell API를 사용 하 여 작업을 관리 합니다. 또한 hello PowerShell Api는이 시점에서 hello 포털 보다 훨씬 더 많은 기능 제공.

이미 설치한 경우 **탄력적 데이터베이스 작업** 기존 hello 포털을 통해 **탄력적 풀**, hello 최신 Powershell 미리 보기 스크립트 tooupgrade 기존 설치를 포함 합니다. 이 뛰어납니다 tooupgrade 설치 toohello 최신 권장 **탄력적 데이터베이스 작업** 순서 tootake 활용을 통해 노출 되는 새로운 기능에 대 한 구성 요소 hello PowerShell Api입니다.

## <a name="prerequisites"></a>필수 조건
* Azure 구독. 무료 평가판에 대해서는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* Azure PowerShell. Hello를 사용 하 여 hello 최신 버전 설치 [웹 플랫폼 설치 관리자](http://go.microsoft.com/fwlink/p/?linkid=320376)합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* [NuGet 명령줄 유틸리티](https://nuget.org/nuget.exe) 사용 되는 tooinstall hello 탄력적 데이터베이스 작업 패키지입니다. 자세한 내용은 http://docs.nuget.org/docs/start-here/installing-nuget을 참조하세요.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>다운로드 하 고 hello 탄력적 데이터베이스 작업 PowerShell 패키지 가져오기
1. Microsoft Azure PowerShell 명령 창을 시작 하 고 다운로드 NuGet 명령줄 유틸리티 (nuget.exe) toohello 디렉터리를 이동 합니다.
2. 다운로드 및 가져오기 **탄력적 데이터베이스 작업** 다음 명령을 hello로 hello 현재 디렉터리에 패키지:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    hello **탄력적 데이터베이스 작업** hello 라는 폴더의 로컬 디렉터리에 파일이 배치 됩니다 **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** 여기서 *x.x.xxxx.x* hello 버전 번호를 반영합니다. hello PowerShell cmdlet (필요한 클라이언트.dll 포함) hello에 살고 있는 **tools\ElasticDatabaseJobs** 하위 디렉터리 및 PowerShell 스크립트 tooinstall hello 업그레이드 및 제거할 수도 hello에  **도구** 하위 디렉터리입니다.
3. 예를 들어 cd 도구를 입력 하 여 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 폴더 toohello tools 하위 디렉터리를 이동 합니다.
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. $Home\Documents\WindowsPowerShell\Modules에 hello.\InstallElasticDatabaseJobsCmdlets.ps1 스크립트 toocopy hello ElasticDatabaseJobs 디렉터리를 실행 합니다. 자동으로 가져옵니다 hello 모듈을 사용에 대 한 예:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Hello 탄력적 데이터베이스 작업 구성 요소를 PowerShell을 사용 하 여 설치
1. Microsoft Azure PowerShell 명령 창을 시작 하 고 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 폴더 toohello \tools 하위 디렉터리를 이동: cd \tools 입력
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Hello.\InstallElasticDatabaseJobs.ps1 PowerShell 스크립트를 실행 하 고 요청 된 해당 변수에 대 한 값을 지정 합니다. 이 스크립트는에 설명 된 hello 구성 요소를 만듭니다 [탄력적 데이터베이스 작업 구성 요소 및 가격](sql-database-elastic-jobs-overview.md#components-and-pricing) tooappropriately hello Azure 클라우드 서비스를 구성 하는 함께 hello 종속 구성 요소를 사용 합니다.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

이 명령을 실행하면 **사용자 이름**과 **암호**를 묻는 창이 열립니다. 이 Azure 자격 증명 hello 사용자 이름 및 hello 관리자 자격 증명 toocreate hello 새 서버에 대 한 원하는 암호를 입력 합니다.

이 샘플 호출에서 제공 하는 hello 매개 변수에 원하는 설정을 수정할 수 있습니다. hello 다음 각 매개 변수에의 hello 동작에 더 많은 정보를 제공합니다.

<table style="width:100%">
  <tr>
    <th>매개 변수</th>
    <th>설명</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Azure 구성 요소를 새로 만든 toocontain hello 만든 hello Azure 리소스 그룹 이름을 제공 합니다. 이 매개 변수의 기본값 너무 "__ElasticDatabaseJob"입니다. 없으면 toochange이이 값을 권장 합니다.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Azure 구성 요소를 새로 만든 hello에 사용 되는 hello Azure 위치 toobe를 제공 합니다. 이 매개 변수 기본값 toohello 중앙 미국 위치입니다.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>서비스 작업 자가 tooinstall hello 수를 제공합니다. 이 매개 변수 기본값 too1입니다. 작업자 수가 높을수록 hello 서비스와 tooprovide 고가용성을 사용 하는 tooscale 수 있습니다. "2" toouse hello 서비스의 고가용성이 필요한 배포를 위한 것이 좋습니다.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Hello 클라우드 서비스 내에서 사용에 대 한 hello v M 크기를 제공합니다. 이 매개 변수 기본값 tooA0입니다. A0/A1/A2/A3의 매개 변수 값은 사용할 수 있는 hello 작업자 역할 toouse ExtraSmall/소규모/보통/큰 크기를 각각. 작업자 역할 크기에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Standard edition에 대 한 hello 서비스 수준 목표를 제공합니다. 이 매개 변수 기본값 tooS0입니다. Hello Azure SQL 데이터베이스 시키는 S0/S1/s 2/s 3의 매개 변수 값 들은 toouse hello 해당 SLO입니다. SQL Database SLO에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>새로 만든 Azure SQL 데이터베이스 서버 hello에 대 한 hello 관리자 사용자 이름을 제공 합니다. 지정 하지 않으면 tooprompt hello 자격 증명에 대 한 PowerShell 자격 증명 창이 열립니다.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>새로 만든 Azure SQL 데이터베이스 서버 hello에 대 한 hello 관리자 암호를 제공 합니다. 제공 되지 tooprompt hello 자격 증명에 대 한 PowerShell 자격 증명 창이 열립니다.</td>
</tr>
</table>

많은 수의 데이터베이스에 대해 동시에 실행 중인 작업 수가 많은 것을 대상으로 하는 시스템에 대 한 것이 좋습니다 toospecify 매개 변수 같은:-ServiceWorkerCount 2-ServiceVmSize a 2-SqlServerDatabaseSlo S2 합니다.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>PowerShell을 사용하여 기존 탄력적 데이터베이스 작업 구성 요소 설치 업데이트
**탄력적 데이터베이스 작업** 을 업데이트할 수 있습니다. 이 프로세스는 toodrop 필요 없이 서비스 코드의 향후 업그레이드에 대 한 허용 하 고 hello 제어 데이터베이스를 다시 만듭니다. Hello 내에서이 프로세스를 사용할 수도 있습니다 동일한 버전 toomodify hello 서비스 VM 크기 또는 hello 서버 작업자 수입니다.

설치 과정의 tooupdate hello VM 크기, 다음 매개 변수를 사용 하 여 스크립트 실행된 hello 업데이트 선택한 toohello 값.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>매개 변수</th>
  <th>설명</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Hello 탄력적 데이터베이스 작업 구성 요소를 처음으로 설치한 경우 사용 하는 hello Azure 리소스 그룹 이름을 식별 합니다. 이 매개 변수의 기본값 너무 "__ElasticDatabaseJob"입니다. 이 아니어서 권장 toochange이이 값이 매개이 변수 toospecify 없을 것입니다.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>서비스 작업 자가 tooinstall hello 수를 제공합니다.  이 매개 변수 기본값 too1입니다.  작업자 수가 높을수록 hello 서비스와 tooprovide 고가용성을 사용 하는 tooscale 수 있습니다.  "2" toouse hello 서비스의 고가용성이 필요한 배포를 위한 것이 좋습니다.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Hello 클라우드 서비스 내에서 사용에 대 한 hello v M 크기를 제공합니다. 이 매개 변수 기본값 tooA0입니다. A0/A1/A2/A3의 매개 변수 값은 사용할 수 있는 hello 작업자 역할 toouse ExtraSmall/소규모/보통/큰 크기를 각각. 작업자 역할 크기에 대한 자세한 내용은 [Elastic Database 작업 구성 요소 및 가격 책정](sql-database-elastic-jobs-overview.md#components-and-pricing)을 참조하세요.</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Hello 탄력적 데이터베이스 작업 구성 요소를 hello 포털을 사용 하 여 설치
설정한 후 [탄력적 풀을 만든](sql-database-elastic-pool-manage-portal.md)를 설치할 수 있습니다 **탄력적 데이터베이스 작업** hello 탄력적인 풀의 각 데이터베이스에 대해 관리 작업의 구성 요소 tooenable 실행 합니다. 사용 하 여 hello 하는 경우와 달리 **탄력적 데이터베이스 작업** PowerShell Api hello 포털 인터페이스는 현재 제한 tooonly 기존 풀에 대해 실행 합니다.

**예상 시간 toocomplete:** 10 분입니다.

1. Hello 통해 hello 탄력적 풀의 hello 대시보드 보기에서 [Azure 포털](https://portal.azure.com/#) , 클릭 **만들기 작업**합니다.
2. Hello에 대 한 작업이 처음으로 만드는 경우를 설치 해야 **탄력적 데이터베이스 작업** 클릭 하 여 **미리 보기 약관**합니다.
3. Hello 용어를 클릭 하 여 hello 확인란을 수락 합니다.
4. 클릭 "설치 서비스" hello 뷰에서 **작업 자격 증명**합니다.
   
    ![Hello 서비스 설치][1]
5. 데이터베이스 관리자의 사용자 이름과 암호를 입력합니다. 새 Azure SQL 데이터베이스 서버는 hello 설치의 일부로 생성 됩니다. 이 새 서버 내에서 hello 제어 데이터베이스 라고 하는 새 데이터베이스를 만들어지고 탄력적 데이터베이스 작업에 대 한 toocontain hello 메타 데이터를 사용 합니다. hello 사용자 이름 및 암호를 여기서 만든 toohello 제어 데이터베이스에서 로깅 hello 목적을 위해 사용 됩니다. 별도 자격 증명 hello 풀 내의 hello 데이터베이스에 대 한 스크립트 실행에 사용 됩니다.
   
    ![사용자 이름 및 암호 만들기][2]
6. Hello 확인 단추를 클릭 합니다. hello 구성 요소가 자동으로 만들어집니다를 새로운 몇 분 안에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다. hello 새 리소스 그룹이 고정 아래와 같이 toohello 보드를 시작 합니다. 일단 만들어지고, 탄력적 데이터베이스 작업 (클라우드 서비스, SQL 데이터베이스, 서비스 버스 및 저장소)은 모두 hello 그룹에 생성 됩니다.
   
    ![시작 보드 내의 리소스 그룹][3]
7. Toocreate 또는 제공 하는 경우 탄력적 데이터베이스 작업 설치 되는 동안 작업을 관리 하는 경우 **자격 증명** hello 메시지의 뒤에 표시 됩니다.
   
    ![배포가 아직 진행 중입니다.][4]

제거에 필요한 경우 hello 리소스 그룹을 삭제 합니다. 참조 [toouninstall hello 탄력적 데이터베이스 구성 요소를 작업 하는 방법을](sql-database-elastic-jobs-uninstall.md)합니다.

## <a name="next-steps"></a>다음 단계
스크립트 실행에 대 한 자세한 내용은 참조 하십시오 hello 그룹의 각 데이터베이스에 만들어집니다. hello 적절 한 권한이 있는 자격 증명 확인 [SQL 데이터베이스를 보호](sql-database-manage-logins.md)합니다.
참조 [만들고 탄력적 데이터베이스 작업 관리](sql-database-elastic-jobs-create-and-manage.md) tooget 시작 합니다.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
