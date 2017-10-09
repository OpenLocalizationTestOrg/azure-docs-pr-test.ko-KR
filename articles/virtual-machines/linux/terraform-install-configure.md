---
title: "aaaInstall 및 Azure에서 Terraform tooprovision Vm 및 기타 인프라 구성 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall Terraform toocreate Azure 구성 및 리소스"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>설치 하 고 Azure에 Terraform tooprovision Vm 및 기타 인프라 구성 
이 문서 hello 필요한 단계 tooinstall에 설명 하 고 Azure에 가상 컴퓨터와 같은 Terraform tooprovision 리소스를 구성 합니다. 어떻게 toocreate 및 Azure 사용 하 여 자격 증명 tooenable Terraform tooprovision 클라우드 리소스에 안전 하 게 설명 합니다.

HashiCorp Terraform 쉽게 toodefine 제공 하 고 HashiCorp 구성 언어 (HCL) 이라는 사용자 지정 템플릿 언어를 사용 하 여 클라우드 인프라를 배포 합니다. 이 사용자 지정 언어는 [쉽게 toowrite 및 쉽게 toounderstand](terraform-create-complete-vm.md)합니다. 또한 hello를 사용 하 여 `terraform plan` 명령, 커밋하기 전에 hello 변경 tooyour 인프라를 시각화할 수 있습니다. 이러한 단계 toostart Terraform Azure와 함께 사용 하 여 수행 합니다.

## <a name="install-terraform"></a>Terraform 설치
tooinstall Terraform, [다운로드](https://www.terraform.io/downloads.html) hello 패키지 별도 설치 디렉터리에 운영 체제에 적합 합니다. hello 다운로드 전역 경로 정의 해야 하는 단일 실행 파일을 포함 합니다. 에 대 한 tooset Linux 및 Mac에서 경로 hello 하는 방법에 대 한 지침 너무[이 웹 페이지](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux)합니다. 에 대 한 tooset windows에서 경로 hello 하는 방법에 대 한 지침 너무[이 웹 페이지](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)합니다. tooverify hello를 실행 하 여 설치 `terraform` 명령입니다. 출력으로 사용할 수 있는 Terraform 옵션 목록이 표시되어야 합니다.

다음으로, tooallow Terraform 액세스 tooyour Azure 구독 tooperform 인프라 프로 비전 해야 합니다.

## <a name="set-up-terraform-access-tooazure"></a>Terraform 액세스 tooAzure 설정
Azure Active Directory (Azure AD)에 두 개의 엔터티가 toocreate 필요를 Azure로 Terraform tooprovision 리소스 tooenable: Azure AD 응용 프로그램 및 Azure AD 서비스 사용자입니다. 그런 다음 Terraform 스크립트에서 이러한 엔터티의 식별자를 사용합니다. 서비스 주체는 글로벌 Azure AD 응용 프로그램의 로컬 인스턴스입니다. 서비스 사용자는 로컬 세부적인 액세스 제어 tooglobal 리소스 수 있습니다.

Azure AD 응용 프로그램 및 Azure AD 서비스 사용자는 여러 가지 방법으로 toocreate가 있습니다. hello 빠르고 쉬운 방식으로 임 toouse Azure CLI 2.0는 [다운로드 하 여 Windows, Linux 또는 Mac에 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)합니다. PowerShell 또는 Azure CLI 1.0 toocreate hello 필요한 보안 인프라를 사용할 수도 있습니다. 표시 하는 hello 나오는 지침에 따라 모든 이러한 접근 방식을 사용 하 여 Azure에 대 한 Terraform tooconfigure 합니다.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Azure CLI 2.0 사용(Windows, Linux 또는 Mac 사용자의 경우) 
다운로드 하 고 hello를 설치한 후 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), hello 다음 명령을 실행 하 여 Azure 구독을 tooadminister에 로그인 합니다.

```
az login
```

>[!NOTE]
>Toofirst 필요한 hello 중국, Azure 독일 또는 Azure Government 클라우드를 사용 하는 경우 해당 클라우드를 사용 하 여 hello Azure CLI toowork를 구성 합니다. Hello 다음을 실행 하 여이 수행할 수 있습니다.

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

여러 Azure 구독이 있는 경우 해당 세부 정보에 반환한 hello `az login` 명령입니다. 집합 hello `SUBSCRIPTION_ID` hello의 환경 변수 toohold hello 값이 반환 `id` hello 구독에서 필드 toouse 원하는 합니다. 

이 세션에 대 한 toouse 되도록 hello 구독을 설정 합니다.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

Hello 계정 tooget hello 구독 ID를 쿼리 하 한 ID 값을 테 넌 트 키를 누릅니다.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

다음으로 Terraform에 대한 별도의 자격 증명을 만듭니다.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

appId, 암호, sp_name, 및 테넌트가 반환됩니다. Hello appId 및 암호를 기록해 둡니다.

tooconfirm (서비스 사용자) 자격 증명 새 셸을 열고 hello 다음 명령을 실행 합니다. 대체 hello sp_name, 암호 및 테 넌 트에 대 한 값을 반환 합니다.

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>PowerShell 사용(Windows 사용자의 경우) 
toouse Windows toowrite 컴퓨터 및 사용자 Terraform 실행 스크립트 및 구성 작업에 대 한 PowerShell toouse hello 오른쪽 PowerShell 도구와 함께 컴퓨터를 구성 합니다. 

1. hello 단계에 따라 PowerShell 도구 설치 [설치 Azure PowerShell을 구성 하 고](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)합니다. 

2. 다운로드 및 실행 hello [azure setup.ps1 스크립트](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) hello PowerShell 콘솔에서 합니다.

3. toorun hello azure setup.ps1 스크립트를 다운로드 하 여 hello 실행 `./azure-setup.ps1 setup` hello PowerShell 콘솔에서 명령을 합니다. Tooyour 관리자 권한으로 Azure 구독에에서 로그인 합니다.

4. 메시지가 표시되면 응용 프로그램 이름(임의 문자열, 필수)을 제공합니다. 필요에 따라 메시지가 표시되면 강력한 암호를 입력합니다. 암호를 입력하지 않으면 .NET 보안 라이브러리를 사용하여 강력한 암호가 생성됩니다.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Azure CLI 1.0 사용(Linux 또는 Mac 사용자의 경우)
tooget Terraform 설치 컴퓨터에 적절 한 라이브러리 hello Azure CLI 1.0과 함께 Mac 또는 Linux 컴퓨터에서 시작 하세요.  

1. hello 단계에 따라 Azure xPlat CLI 도구 설치 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다. 

2. 다운로드 하 여 JSON 프로세서 hello 지침에 따라 설치 [jq 다운로드](https://stedolan.github.io/jq/download/)합니다.

3. 다운로드 및 실행 hello [azure setup.sh 스크립트](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) hello 콘솔에서 스크립트를 이용한 적입니다.

4. toorun hello azure setup.sh 스크립트를 다운로드 하 여 hello 실행 `./azure-setup setup` hello 콘솔에서 명령을 합니다. Tooyour 관리자 권한으로 Azure 구독에에서 로그인 합니다.
 
5. 메시지가 표시되면 응용 프로그램 이름(임의 문자열, 필수)을 제공합니다. 필요에 따라 메시지가 표시되면 강력한 암호를 입력합니다. 암호를 입력하지 않으면 .NET 보안 라이브러리를 사용하여 강력한 암호가 생성됩니다.

모든 hello 이전 스크립트는 Azure AD 응용 프로그램 및 서비스를 만들 주입니다. hello 서비스 사용자 hello 구독에서 참가자 또는 소유자 수준의 액세스를 가져옵니다. Hello 높은 수준의 액세스 권한을 부여, 인해 항상 해당 스크립트에 의해 생성 된 hello 보안 정보를 보호 해야 합니다. 해당 스크립트에서 제공한 다음 4가지 모든 보안 정보(appId, 암호, subscription_id 및 tenant_id)를 기록해 둡니다.

## <a name="set-environment-variables"></a>환경 변수 설정
Toolet을 만들고 Azure AD 서비스 사용자를 구성한 후 해야 hello 테 넌 트 ID, 구독 ID, 클라이언트 ID 및 클라이언트 비밀 toouse Terraform 알고 있습니다. [Terraform을 사용하여 기본 인프라 만들기](terraform-create-complete-vm.md)에서 설명한 대로 Terraform 스크립트에 해당 값을 포함하면 가능합니다. 또는 다음 환경 변수는 hello (를 실수로 체크 인 또는 사용자의 자격 증명을 공유 되지 않도록):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

이 샘플 셸 스크립트 tooset 해당 변수를 사용할 수 있습니다.

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

또한 Azure Government 중 또는 중국의 Azure 또는 Azure 독일 Terraform를 사용 하는 경우 필요한 tooset hello 환경 변수가 적절 하 게 합니다.

## <a name="next-steps"></a>다음 단계
이제 Terraform을 설치했고 Azure 자격 증명을 구성했으므로 Azure 구독에 인프라를 배포하기 시작할 수 있습니다. 배우는 것이 너무 어떻게[Terraform와 인프라를 만들](terraform-create-complete-vm.md)합니다.
