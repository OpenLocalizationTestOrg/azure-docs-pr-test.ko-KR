---
title: "Azure 스택에 대 한 서비스 사용자를 만들 | Microsoft Docs"
description: "Azure 리소스 관리자의 역할 기반 액세스 제어를 사용한 리소스에 대 한 액세스 관리를 사용할 수 있는 새 서비스 사용자를 만드는 방법을 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/25/2017
ms.author: helaw
ms.openlocfilehash: 058b01a37e2858801895fd22cf73dd6bd342ca04
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="provide-applications-access-to-azure-stack"></a>Azure 스택에 응용 프로그램 액세스 권한을 제공합니다

*적용 대상: Azure 스택 통합 시스템과 Azure 스택 개발 키트*

응용 프로그램에 배포 하거나 Azure 스택에서 Azure 리소스 관리자를 통해 리소스를 구성에 액세스 하면 응용 프로그램에 대 한 자격 증명 인 서비스 사용자를 만듭니다.  그런 다음 해당 서비스 보안 주체에만 필요한 권한을 위임할 수 있습니다.  

예를 들어 Azure 리소스 관리자를 사용 하 여 Azure 리소스를 인벤토리 하는 구성 관리 도구를 할 수 있습니다.  이 시나리오에서는 서비스 사용자를 만들, 읽기 역할 해당 서비스 사용자에 부여 하거나 구성 관리 도구 읽기 전용 액세스를 제한할 수 있습니다. 

서비스 보안 주체는 때문에 사용자 고유의 자격 증명으로 응용 프로그램을 실행 하는 것이 좋습니다.

* 서비스 계정 사용 권한을 보다 다른 사용자에 권한을 할당할 수 있습니다. 일반적으로 이러한 권한은 정확히 앱 실행에 필요한 것으로 제한됩니다.
* 책임이 변경되면 앱의 자격 증명을 변경할 필요가 없습니다.
* 무인 스크립트를 실행할 때 인증서를 사용하여 인증을 자동화할 수 있습니다.  

## <a name="getting-started"></a>시작

Azure 스택, 배포 방법에 따라 사용자는 서비스를 만들어 시작 합니다.  이 문서 만드는 과정을 안내 모두에 대 한 서비스 사용자 [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) 및 [Active Directory 페더레이션 Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs)합니다.  서비스 사용자를 만든 후에 일련의 AD FS와 Azure Active Directory에 공통 되는 단계에 사용 되는 [권한을 위임할](azure-stack-create-service-principals.md#assign-role-to-service-principal) 역할을 합니다.     

## <a name="create-service-principal-for-azure-ad"></a>Azure AD에 대 한 서비스 사용자 만들기

Azure AD id 저장소로 사용 하 여 Azure 스택을 배포한 경우에 Azure에 대해 수행 하는 것 처럼 서비스 사용자를 만들 수 있습니다.  이 여기서 포털을 통해 단계를 수행 하는 방법을 보여 줍니다.  확인 해야 하는 [필요한 Azure AD 권한](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) 시작 하기 전에.

### <a name="create-service-principal"></a>서비스 주체 만들기
이 섹션에서는 Azure ad 응용 프로그램을 나타내는 응용 프로그램 (서비스 주체)을 만듭니다.

1. [Azure Portal](https://portal.azure.com)을 통해 Azure 계정에 로그인합니다.
2. 선택 **Azure Active Directory** > **앱 등록** > **추가**   
3. 응용 프로그램에 대한 이름 및 URL을 제공합니다. 만들려는 응용 프로그램 유형으로 **웹앱/API** 또는 **네이티브**를 선택합니다. 값을 설정한 후 **만들기**를 선택합니다.

응용 프로그램에 대 한 서비스 사용자를 만들었습니다.

### <a name="get-credentials"></a>자격 증명 가져오기
프로그래밍 방식으로 로그인 할 때에 응용 프로그램 및 인증 키에 대 한 ID를 사용 합니다. 이러한 값을 가져오려면 다음 단계를 사용합니다.

1. Active Directory의 **앱 등록**에서 응용 프로그램을 선택합니다.

2. **응용 프로그램 ID**를 복사하고 응용 프로그램 코드에 저장합니다. [샘플 응용 프로그램](#sample-applications) 섹션의 응용 프로그램은 이 값을 클라이언트 ID로 참조합니다.

     ![클라이언트 ID](./media/azure-stack-create-service-principal/image12.png)
3. 인증 키를 생성하려면 **키**를 선택합니다.

4. 키에 대한 설명 및 키의 기간을 제공합니다. 완료되면 **저장**을 선택합니다.

키를 저장하면 키 값이 표시됩니다. 나중에 키를 검색할 수 없으므로 이 값을 복사해둡니다. 응용 프로그램으로 등록 하도록 응용 프로그램 ID와 키 값을 제공 합니다. 응용 프로그램에서 검색할 수 있는 위치에 키 값을 저장합니다.

![공유 키](./media/azure-stack-create-service-principal/image15.png)


완료 되 면 진행 [응용 프로그램 역할을 할당](azure-stack-create-service-principals.md#assign-role-to-service-principal)합니다.

## <a name="create-service-principal-for-ad-fs"></a>AD FS에 대 한 서비스 사용자 만들기
AD FS와 Azure 스택을 배포한 경우에 서비스 사용자를 만들고 액세스에 대 한 역할 할당에 해당 id를 사용 하 여 PowerShell에서 로그인 PowerShell을 사용할 수 있습니다.

### <a name="before-you-begin"></a>시작하기 전에

[Azure 스택 로컬 컴퓨터에 사용 하는 데 필요한 도구를 다운로드 합니다.](azure-stack-powershell-download.md)

### <a name="import-the-identity-powershell-module"></a>Identity PowerShell 모듈을 가져옵니다
도구를 다운로드 한 후 다운로드 한 폴더로 이동 하 고 다음 명령을 사용 하 여 Identity PowerShell 모듈을 가져옵니다.

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

모듈을 가져올 "AzureStack.Connect.psm1 디지털 서명 되지 않은 라는 오류가 나타날 수 있습니다. 스크립트가 실행 되지 않습니다는 시스템에서 ". 이 문제를 해결 하려면 관리자 권한 PowerShell 세션에서에서 다음 명령을 사용 하 여 스크립트 실행을 허용 하도록 실행 정책을 설정할 수 있습니다.

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-the-service-principal"></a>서비스 주체 만들기
업데이트를 확인 하 여 다음 명령을 실행 하 여 서비스 사용자를 만들 수 있습니다는 *DisplayName* 매개 변수:
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a>역할 할당
서비스 사용자를 만든 후 해야 [역할 할당](azure-stack-create-service-principals.md#assign-role-to-service-principal)

### <a name="sign-in-through-powershell"></a>PowerShell을 통해 로그인
역할에 할당 한 후 다음 명령을 사용 하 여 서비스 사용자를 사용 하 여 Azure 스택에 서명할 수 있습니다.

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-to-service-principal"></a>서비스 사용자 역할을 할당 합니다.
구독의 리소스에 액세스하려면 역할에 응용 프로그램을 할당해야 합니다. 응용 프로그램에 적합한 사용 권한을 나타내는 역할을 결정합니다. 사용 가능한 역할에 대해 알아보려면 [RBAC: 기본 제공 역할](../../active-directory/role-based-access-built-in-roles.md)을 참조하세요.

구독, 리소스 그룹 또는 리소스 수준에서 범위를 설정할 수 있습니다. 권한은 하위 수준의 범위로 상속됩니다. 예를 들어 응용 프로그램에 리소스 그룹에 대한 읽기 권한자 역할을 추가하면 응용 프로그램이 리소스 그룹과 그 안에 포함된 모든 리소스를 읽을 수 있습니다.

1. Azure 스택 포털에서 응용 프로그램을 할당 하려는 범위 수준으로 이동 합니다. 예를 들어 구독 범위에서 역할을 할당하려면 **구독**을 선택합니다. 대신 리소스 그룹 또는 리소스를 선택할 수 있습니다.

2. 응용 프로그램을 할당할 특정 구독(리소스 그룹 또는 리소스)을 선택합니다.

     ![할당을 위한 구독 선택](./media/azure-stack-create-service-principal/image16.png)

3. **Access Control(IAM)**을 선택합니다.

     ![액세스 선택](./media/azure-stack-create-service-principal/image17.png)

4. **추가**를 선택합니다.

5. 응용 프로그램에 할당할 역할을 선택합니다.

6. 응용 프로그램을 검색하고 선택합니다.

7. **확인**을 선택하여 역할 할당을 완료합니다. 목록에서 해당 범위에 대한 역할에 할당된 사용자 목록에 응용 프로그램이 표시될 것입니다.

서비스 사용자를 만들고 역할에 할당 했을 했으므로이 사용 하 여 응용 프로그램 내에서 Azure 스택 리소스에 액세스할 수를 시작할 수 있습니다.  

## <a name="next-steps"></a>다음 단계

[사용자 권한 관리](azure-stack-manage-permissions.md)