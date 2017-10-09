---
title: "Azure Active Directory와 클러스터 aaaHPC 팩 | Microsoft Docs"
description: "Azure Active Directory와 Azure에서 HPC 팩 2016 toointegrate 클러스터링 하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Azure Active Directory를 사용하여 Azure에서 HPC 팩 클러스터 관리
[Microsoft HPC 팩 2016](https://technet.microsoft.com/library/cc514029)은 Azure에서 HPC 팩 클러스터를 배포하는 관리자에 대해 Azure AD([Azure Active Directory](../../active-directory/index.md))와의 통합을 지원합니다.



상위 수준의 작업을 수행 하는 hello에 대 한이 문서의 hello 단계를 수행 합니다. 
* 수동으로 HPC 팩 클러스터를 Azure AD 테넌트와 통합
* Azure의 HPC 팩 클러스터에서 작업 관리 및 예약 

HPC Pack 클러스터 솔루션을 Azure AD와 통합 다른 응용 프로그램과 서비스 toointegrate 표준 단계를 따릅니다. 이 문서에서는 Azure AD의 기본 사용자 관리에 익숙하다고 가정합니다. 자세한 내용 및 배경 참조 hello [Azure Active Directory 설명서](../../active-directory/index.md) hello 섹션에 따라 합니다.

## <a name="benefits-of-integration"></a>통합의 이점


Azure Active Directory (Azure AD)는 다중 테 넌 트 클라우드 기반 디렉터리 및 id 관리 하는 서비스 toocloud 솔루션 single sign-on (SSO) 액세스를 제공 합니다.

HPC Pack 클러스터를 Azure AD와의 통합 hello는 다음과 같은 목표가 달성 데 도움이 됩니다.

* Active Directory 도메인 컨트롤러를 기존의 hello hello HPC Pack 클러스터에서 제거 합니다. 이 비즈니스 및 속도 높이고 hello 배포 프로세스에 대 한 필요가 없는 경우에 hello 클러스터를 유지 관리의 hello 비용을 줄일 수 있습니다.
* 다음 Azure AD에 의해 표시 되는 이점을 활용 하 여 hello:
    *   SSO(Single sign-on) 
    *   Azure의 hello HPC Pack 클러스터에 대 한 로컬 AD id를 사용 하 여 

    ![Azure Active Directory 환경](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>필수 조건
* **Azure 가상 컴퓨터에 배포된 HPC 팩 2016 클러스터** - 단계는 [Azure에서 HPC 팩 2016 클러스터 배포](hpcpack-2016-cluster.md)를 참조하세요. Hello 헤드 노드의 hello DNS 이름 및 hello이이 문서의 단계를 완료 하려면 클러스터 관리자의 hello 자격 증명 필요.

  > [!NOTE]
  > Azure Active Directory 통합은 HPC 팩 2016 이전에 HPC 팩의 버전에서 지원되지 않습니다.



* **클라이언트 컴퓨터** -는 Windows 또는 Windows Server 클라이언트 컴퓨터 실행 너무 HPC Pack 클라이언트 유틸리티를 해야 합니다. Toouse hello HPC Pack 웹 포털 또는 REST API toosubmit 작업을만 하려는 경우에 사용자가 선택한 모든 클라이언트 컴퓨터를 사용할 수 있습니다.

* **HPC Pack 클라이언트 유틸리티** -hello Microsoft 다운로드 센터에서에서 사용할 수 있는 hello 무료 설치 패키지를 사용 하 여 hello 클라이언트 컴퓨터에 hello HPC Pack 클라이언트 유틸리티를 설치 합니다.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>1 단계: Azure AD 테 넌 트와 hello HPC 클러스터 서버 등록
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 클릭 **Active Directory** 왼쪽된 메뉴 hello와 구독에서 hello 원하는 디렉터리를 클릭 합니다. 사용 권한 tooaccess 리소스 hello 디렉터리에 있어야 합니다.
3. **사용자**를 클릭하고 사용자 계정이 이미 만든 또는 구성되어 있는지 확인합니다.
4. **응용 프로그램** > **추가**를 클릭하고 **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다. Hello 정보 hello 마법사에서 다음을 입력 합니다.
    * **이름** - HPCPackClusterServer
    * **유형**: **웹 응용 프로그램 및/또는 Web API**를 선택합니다.
    * **로그온 URL**-hello는 기본적으로 hello 샘플에 대 한 기본 URL`https://hpcserver`
    * **앱 ID URI** - `https://<Directory_name>/<application_name>`. 대체 `<Directory_name`> Azure AD 테 넌 트 예를 들어, 전체 이름 hello로 `hpclocal.onmicrosoft.com`, 대체 `<application_name>` 이전에 선택한 hello 이름의 합니다.

5. Hello 앱을 추가한 후 클릭 **구성**합니다. Hello 다음과 같은 속성을 구성 합니다.
    * **응용 프로그램은 다중 테넌트**에서 **예**를 선택합니다.
    * 선택 **예** 에 대 한 **사용자 할당 필요 tooaccess 앱**합니다.

6. **Save**를 클릭합니다. 저장이 완료되면 **매니페스트 관리**를 클릭합니다. 이 작업은 응용 프로그램의 매니페스트 JavaScript 개체 표기법(JSON) 파일을 다운로드합니다. Hello를 배치 하 여 다운로드 한 hello 매니페스트 편집 `appRoles` 설정 하 고 추가한 응용 프로그램 역할을 수행 하는 hello:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Hello 파일을 저장 합니다. Hello 포털에서 클릭 **매니페스트 관리** > **매니페스트 업로드**합니다. 그런 다음 hello 편집 된 매니페스트를 업로드할 수 있습니다.
8. **사용자**를 클릭하고 사용자를 선택한 다음 **할당**을 클릭합니다. Hello 사용 가능한 역할 (HpcUsers 또는 HpcAdminMirror) toohello 사용자 중 하나를 할당 합니다. Hello 디렉터리에 추가 사용자와이 단계를 반복 합니다. 클러스터 사용자에 대한 배경 정보는 [클러스터 사용자 관리](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx)를 참조하세요.

   > [!NOTE] 
   > toomanage 사용자가 사용할 수 있는 권장 hello Azure Active Directory 미리 보기 블레이드에서 hello에 [Azure 포털](https://portal.azure.com)합니다.
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>2 단계: Azure AD 테 넌 트와 hello HPC 클러스터 클라이언트 등록

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 클릭 **Active Directory** 왼쪽된 메뉴 hello와 구독에서 hello 원하는 디렉터리를 클릭 합니다. 사용 권한 tooaccess 리소스 hello 디렉터리에 있어야 합니다.
3. **응용 프로그램** > **추가**를 클릭하고 **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다. Hello 정보 hello 마법사에서 다음을 입력 합니다.

    * **이름** - HPCPackClusterClient
    * **형식** - **네이티브 클라이언트 응용 프로그램**을 선택합니다.
    * **URI 리디렉션** - `http://hpcclient`

4. Hello 앱을 추가한 후 클릭 **구성**합니다. 복사 hello **클라이언트 ID** 값을 저장 합니다. 나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.

5. **tooother 응용 프로그램 사용 권한**, 클릭 **응용 프로그램 추가**합니다. 검색 하 고 hello HpcPackClusterServer 응용 프로그램 (1 단계에서에서 만든)을 추가 합니다.

6. Hello에 **위임 된 권한** 드롭다운 **액세스 HpcClusterServer**합니다. 그런 다음 **Save**를 클릭합니다.


## <a name="step-3-configure-hello-hpc-cluster"></a>3 단계: hello HPC 클러스터를 구성 합니다.

1. Azure에서 헤드 노드에 HPC 팩 2016 toohello를 연결 합니다.

2. HPC PowerShell을 시작합니다.

3. Hello 다음 명령을 실행 합니다.

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    여기서,

    * `AADTenant`같은 hello Azure AD 테 넌 트 이름 지정`hpclocal.onmicrosoft.com`
    * `AADClientAppId`2 단계에서에서 만든 hello 앱에 대 한 hello 클라이언트 ID를 지정 합니다.

4. Hello HpcSchedulerStateful 서비스를 다시 시작 합니다.

    여러 헤드 노드를 클러스터에서 PowerShell 명령을 hello 헤드 노드 tooswitch hello 주 복제본에서 hello HpcSchedulerStateful 서비스에 대 한 다음 hello를 실행할 수 있습니다.

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>4 단계: 관리 하 고 hello 클라이언트에서 작업 제출

컴퓨터에 tooinstall hello HPC Pack 클라이언트 유틸리티 hello Microsoft 다운로드 센터에서에서 HPC 팩 2016 설치 파일 (전체 설치)를 다운로드 합니다. Hello 설치를 시작할 때 hello에 대 한 hello 설치 옵션을 선택 합니다. **HPC Pack 클라이언트 유틸리티**합니다.

tooprepare hello 클라이언트 컴퓨터 설치 중에 사용 하는 hello 인증서 [HPC 클러스터 설정](hpcpack-2016-cluster.md) hello 클라이언트 컴퓨터에 있습니다. 표준 Windows를 사용 하 여 인증서 관리 프로시저 tooinstall hello 공용 인증서 toohello **인증서 – 현재 사용자** > **신뢰할 수 있는 루트 인증 기관** 저장 합니다. 

이제 hello HPC Pack 명령을 실행 하거나 toosubmit hello HPC 팩 작업 관리자 GUI 사용 하 여 있고 hello Azure AD 계정을 사용 하 여 클러스터 작업을 관리 합니다. 작업 전송 옵션을 참조 하십시오. [Azure에서 HPC 제출 작업 tooan HPC 팩 클러스터](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster)합니다.

> [!NOTE]
> Hello에 대 한 tooconnect toohello HPC Pack 클러스터에서 Azure 처음으로 시도 하면 팝업 창이 나타납니다. 에 Azure AD 자격 증명 toolog에를 입력 합니다. hello 토큰이 다음 캐시 됩니다. 이후 연결 toohello 클러스터 hello Azure 사용에에서 인증 변경 또는 hello 캐시의 선택을 취소 하면 않는 경우 토큰을 캐시 합니다.
>
  
예를 들어 hello 이전 단계를 완료 한 후 쿼리할 수 있습니다는 온-프레미스 클라이언트에서 작업에 대 한 다음과 같습니다.

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Azure AD 통합을 사용하는 작업 제출에 유용한 cmdlet 

### <a name="manage-hello-local-token-cache"></a>Hello 로컬 토큰 캐시를 관리 합니다.

HPC 팩 2016 두 개의 새로운 HPC PowerShell cmdlet toomanage hello 로컬 토큰 캐시를 제공합니다. 이러한 cmdlet은 비대화형으로 작업을 제출하는 데 유용합니다. 다음 예제는 hello를 참조 하십시오.

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Hello Azure AD 계정을 사용 하 여 작업을 제출 하기 위한 hello 자격 증명 설정 

따라, (도메인에 가입 된 HPC 클러스터의 경우 한 도메인 사용자 계정으로 실행, 도메인 가입 된 HPC 클러스터의 경우 hello 헤드 노드에 대 한 로컬 사용자로 실행) hello HPC 클러스터 사용자 toorun hello 작업을 할 수도 있습니다.

1. 사용 하 여 hello 다음 명령 tooset hello 자격 증명:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. 그런 다음 다음과 같이 hello 작업을 제출 합니다. hello 계산 노드에서 hello 작업/태스크 실행 $localUser 아래에서 합니다.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   경우 `–Credential` 으로 지정 하지 않으면 `Submit-HpcJob`, Azure AD 계정을 hello 처럼 hello 작업 또는 작업 로컬 매핑된 사용자 실행 합니다. (hello HPC 클러스터는 로컬 사용자를 만듭니다 hello Azure AD 계정 toorun hello 작업 이름이 hello.)
    
3. Azure AD 계정 hello에 대 한 확장된 데이터를 설정 합니다. Hello Azure AD 계정을 사용 하 여 Linux 노드에서 MPI 작업을 실행 하는 경우에 유용 합니다.

   * Azure AD 계정 자체 hello에 대 한 확장된 데이터를 설정 합니다.

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * 확장된 데이터를 설정하고 HPC 클러스터 사용자로 실행합니다.
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

