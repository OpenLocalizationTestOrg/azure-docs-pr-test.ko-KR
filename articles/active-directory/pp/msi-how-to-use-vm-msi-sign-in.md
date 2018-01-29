---
title: "로그인에 Azure VM 관리 서비스 ID를 사용하는 방법"
description: "스크립트 클라이언트 로그인 및 리소스 액세스에 Azure VM MSI 서비스 주체를 사용하는 단계별 지침 및 예제입니다."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/05/2018
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: c5f71d27a9e07cc6d6a260b809e91aaa2a50270c
ms.sourcegitcommit: 1d423a8954731b0f318240f2fa0262934ff04bd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="sign-in-using-a-vm-user-assigned-managed-service-identity-msi"></a>VM 사용자 할당 MSI(관리 서비스 ID)를 사용하여 로그인

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]이 문서에서는 사용자 할당 MSI 서비스 주체를 사용한 로그인에 대한 CLI 스크립트 예제 및 오류 처리와 같은 중요한 항목에 대한 지침을 제공합니다.

## <a name="prerequisites"></a>필수 구성 요소

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

이 문서에서 Azure CLI 예제를 사용하기 위해 최신 버전의 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)을 설치해야 합니다. 

> [!IMPORTANT]
> - 이 문서의 모든 샘플 스크립트에서는 MSI 사용 Virtual Machine에서 명령줄 클라이언트를 실행한다고 가정합니다. Azure Portal에서 VM "연결" 기능을 사용하여 VM에 원격으로 연결합니다. VM에서 MSI 사용에 대한 자세한 내용은 [Azure CLI를 사용하여 VM MSI(관리 서비스 ID) 구성](msi-qs-configure-cli-windows-vm.md) 또는 (PowerShell, 포털, 템플릿 또는 Azure SDK를 사용하는) 변형 문서 중 하나를 참조하세요. 
> - 로그인 및 리소스 액세스 중에 오류를 방지하려면 적절한 범위(VM 이상)에서 최소한 "읽기 권한자" 액세스 권한을 MSI를 제공하여 VM에 Azure Resource Manager 작업을 허용해야 합니다. 자세한 내용은 [Azure CLI를 사용하여 MSI(관리 서비스 ID)에 리소스 액세스 권한 할당](msi-howto-assign-access-cli.md)을 참조하세요.

## <a name="overview"></a>개요

MSI는 VM에서 [MSI를 활성화하여 만든](msi-overview.md#how-does-it-work) [서비스 주체](~/articles/active-directory/develop/active-directory-dev-glossary.md#service-principal-object)를 제공합니다. 서비스 주체는 Azure 리소스에 액세스 권한을 부여하고 로그인 및 리소스 액세스를 위한 스크립트/명령줄에 의한 ID로 사용될 수 있습니다. 일반적으로 고유한 ID 하에서 보호된 리소스에 액세스하기 위해 스크립트 클라이언트는 다음을 수행해야 합니다.  

   - Azure AD에서 기밀/웹 클라이언트 응용 프로그램으로 등록하고 동의합니다.
   - 앱의 자격 증명(스크립트에 포함됨)을 사용하여 해당 서비스 주체 하에 로그인합니다.

MSI를 사용하는 경우 MSI 서비스 주체 하에서 로그인할 수 있으므로 스크립트 클라이언트는 더 이상 수행하지 않아도 됩니다. 

## <a name="azure-cli"></a>Azure CLI

다음 스크립트에서는 다음과 같은 방법을 설명합니다.

1. 사용자 할당 MSI 서비스 주체 하의 Azure AD에 로그인합니다.  
2. Azure Resource Manager를 호출하고 VM의 Azure 지역 위치를 가져옵니다. CLI에서는 자동으로 토큰 획득/사용을 관리합니다. `<VM NAME>`에 대한 VM 이름 및 `<MSI ID>`에 대한 사용자 할당 MSI 리소스 ID를 대체해야 합니다. 사용자 할당 MSI를 만드는 동안 `id` 속성에서 MSI 리소스 ID가 반환됩니다(`az identity create` 명령의 예제는 [Azure CLI를 사용하여 VM에 사용자 할당 MSI(관리 서비스 ID) 구성](msi-qs-configure-cli-windows-vm.md) 참조).

    ```azurecli
    az login --msi –u <MSI ID>
   
    vmLocation=$(az resource list -n <VM NAME> --query [*].location --out tsv)
    echo The VM region location is $vmLocation
    ```

    예제 응답:
   
    ```bash
    user@vmLinux:~$ az login --msi -u /subscriptions/80c696ff-5efa-4909-a64d-z1b616f423bl/resourcegroups/rgName/providers/Microsoft.ManagedIdentity/userAssignedIdentities/msiName
    [
      {
        "environmentName": "AzureCloud",
        "id": "90c696ff-5efa-4909-a64d-z1b616f423bl",
        "isDefault": true,
        "name": "MSIResource-/subscriptions/90c696ff-5efa-4909-a64d-z1b616f423bl/resourcegroups/rgName/providers/Microsoft.ManagedIdentity/userAssignedIdentities/msiName@50342",
        "state": "Enabled",
        "tenantId": "933a8f0e-ec41-4e69-8ad8-971zc4b533ll",
        "user": {
          "name": "userAssignedIdentity",
          "type": "servicePrincipal"
        }
      }
    ]  
    user@vmLinux:~$ vmLocation=$(az resource list -n vmLinux --query [*].location --out tsv)
    user@vmLinux:~$ echo The VM region location is $vmLocation
    The VM region location is westcentralus
    ```

## <a name="resource-ids-for-azure-services"></a>Azure 서비스의 리소스 ID

Azure AD를 지원하고 MSI 및 해당하는 리소스 ID를 사용하여 테스트된 리소스의 목록은 [Azure AD 인증을 지원하는 Azure 서비스](msi-overview.md#azure-services-that-support-azure-ad-authentication)를 참조하세요.

## <a name="error-handling-guidance"></a>오류 처리 지침 

다음과 같은 응답은 MSI가 올바르게 구성되지 않았음을 나타낼 수 있습니다.

- CLI: *MSI: 'HTTPConnectionPool(host='localhost', port=50342) 오류를 표시하여 'http://localhost:50342/oauth2/token'에서 토큰을 검색하지 못했습니다.* 

이러한 오류 중 하나를 수신하면 [Azure Portal](https://portal.azure.com)에서 Azure VM에 반환됩니다.

- **구성** 페이지로 이동하여 "관리 서비스 ID"를 "예"로 설정했는지 확인합니다.
- **확장** 페이지로 이동하여 MSI 확장이 올바르게 배포되었는지 확인합니다.

이 두 항목 중 하나가 올바르지 않으면 리소스에서 MSI를 다시 할당하거나 배포 오류 관련 문제를 해결해야 할 수 있습니다. VM을 구성하는 데 도움이 필요한 경우 [Azure CLI를 사용하여 VM MSI(관리 서비스 ID) 구성](msi-qs-configure-cli-windows-vm.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

- Azure VM에서 MSI를 사용하도록 설정하려면 [Azure CLI를 사용하여 VM MSI(관리 서비스 ID) 구성](msi-qs-configure-cli-windows-vm.md)을 참조하세요.

다음 설명 섹션을 사용하여 피드백을 제공하고 콘텐츠를 구체화하고 모양을 갖출 수 있습니다.








