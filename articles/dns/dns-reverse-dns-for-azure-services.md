---
title: "Azure 서비스에 대 한 DNS aaaReverse | Microsoft Docs"
description: "Tooconfigure Azure에서 호스팅된 서비스에 대 한 DNS 조회를 반대로 하는 방법에 대해 알아봅니다"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Azure에서 호스트되는 서비스에 대해 역방향 DNS 구성

이 문서에서는 tooconfigure Azure에서 호스팅된 서비스에 대 한 DNS 조회를 반대로 하는 방법을 설명 합니다.

Azure의 서비스는 Azure에서 할당하고 Microsoft가 소유하는 IP 주소를 사용합니다. 영역에 있는 hello 해당 Microsoft 소유 역방향 DNS 조회 (PTR 레코드)이 역방향 DNS 레코드를 만들어야 합니다. 이 문서에서는 설명 어떻게 toodo이 있습니다.

이 시나리오 혼동 해서는 안 hello 기능과 함께 너무[Azure DNS에서 할당 된 IP 범위에 대 한 hello 역방향 DNS 조회 영역을 호스팅하려](dns-reverse-dns-hosting.md)합니다. 이 경우 hello 역방향 조회 영역을 나타내는 hello IP 범위 할당 해야 tooyour 조직 일반적으로 ISP가 있습니다.

이 문서를 읽기 전에 이 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)에 익숙해지는 것이 좋습니다.

Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.
* Hello 리소스 관리자 배포 모델에서 계산 리소스 (예: 가상 컴퓨터, 가상 컴퓨터 크기 집합 또는 서비스 패브릭 클러스터) PublicIpAddress 리소스를 통해 노출 됩니다. DNS 역방향 조회는 hello 'ReverseFqdn' hello PublicIpAddress 속성을 사용 하 여 구성 됩니다.
* Hello 클래식 배포 모델에서는 계산 리소스는 클라우드 서비스를 사용 하 여 노출 됩니다. DNS 역방향 조회는 hello 클라우드 서비스의 hello 'ReverseDnsFqdn' 속성을 사용 하 여 구성 됩니다.

역방향 DNS hello Azure 앱 서비스에 대 한 현재 지원 되지 않습니다.

## <a name="validation-of-reverse-dns-records"></a>역방향 DNS 레코드의 유효성 검사

제 3 자가 자신의 Azure 서비스 매핑 tooyour DNS 도메인에 대 한 역방향 DNS 레코드 수 toocreate 되지 않아야 합니다. tooprevent이 Azure hello 여기서 hello 역방향 DNS 레코드에 지정 된 도메인 이름과 hello와 동일 또는 동일 hello에 DNS 이름 또는 IP 주소 PublicIpAddress 또는 클라우드 hello로 확인 되 면 서비스를 사용 하는 역방향 DNS 레코드 만들기가 하나만 허용 Azure 구독.

이 유효성 검사는 hello 역방향 DNS 레코드를 설정 하거나 수정할 때만 수행 됩니다. 유효성 재검사는 정기적으로 수행되지 않습니다.

예를 들어: hello PublicIpAddress 리소스 hello DNS 이름 contosoapp1.northus.cloudapp.azure.com 및 IP 주소 23.96.52.53 가정해 보겠습니다. ReverseFqdn PublicIpAddress로 지정할 수 있으며 hello에 대 한 hello:
* PublicIpAddress hello에 대 한 hello DNS 이름, contosoapp1.northus.cloudapp.azure.com
* hello DNS 이름에서 다른 PublicIpAddress hello에 대 한 동일한 contosoapp2.westus.cloudapp.azure.com 같은 구독을
* 베 니 티 DNS 이름, app1.contoso.com, 등으로이 이름은 *첫 번째* CNAME toocontosoapp1.northus.cloudapp.azure.com 또는 구성 tooa 다른 PublicIpAddress hello에 동일한 구독 합니다.
* 베 니 티 DNS 이름, app1.contoso.com, 등으로이 이름은 *첫 번째* hello에 A 레코드 toohello IP 주소로 23.96.52.53, 또는 다른 PublicIpAddress의 toohello IP 주소 구성 동일한 구독 합니다.

hello 동일한 제약 조건을 적용 tooreverse DNS 클라우드 서비스에 대 한 합니다.


## <a name="reverse-dns-for-publicipaddress-resources"></a>PublicIpAddress 리소스에 대한 역방향 DNS

이 섹션에서는 tooconfigure Azure PowerShell, Azure CLI 1.0 또는 Azure CLI 2.0을 사용 하 여 hello 리소스 관리자 배포 모델의 PublicIpAddress 리소스에 대 한 DNS를 반대로 하는 방법에 대 한 자세한 지침을 제공 합니다. 현재 hello Azure 포털을 통해 PublicIpAddress 리소스에 대 한 역방향 DNS 구성 지원 되지 않습니다.

Azure는 현재 IPv4 PublicIpAddress 리소스에 대해서만 역방향 DNS를 지원합니다. IPv6에 대해서는 지원되지 않습니다.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>역방향 DNS tooan PublicIpAddresses 기존 추가

#### <a name="powershell"></a>PowerShell

tooadd 역방향 DNS tooan PublicIpAddress 기존:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd 역방향 DNS 이름에 아직 PublicIpAddress 기존 DNS tooan, DNS 이름을 지정 해야 합니다.

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

tooadd 역방향 DNS tooan PublicIpAddress 기존:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd 역방향 DNS 이름에 아직 PublicIpAddress 기존 DNS tooan, DNS 이름을 지정 해야 합니다.

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

tooadd 역방향 DNS tooan PublicIpAddress 기존:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd 역방향 DNS 이름에 아직 PublicIpAddress 기존 DNS tooan, DNS 이름을 지정 해야 합니다.

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>역방향 DNS를 사용하여 공용 IP 주소 만들기

hello 역방향 DNS 속성이 이미 지정 된 새 PublicIpAddress toocreate:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>기존 PublicIpAddresses의 역방향 DNS 보기

tooview hello 기존 PublicIpAddress에 대 한 값을 구성 합니다.

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>기존 공용 IP 주소에서 역방향 DNS 제거

tooremove 기존 PublicIpAddress에서 역방향 DNS 속성:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Cloud Services에 대한 역방향 DNS 구성

이 섹션에서는 어떻게 tooconfigure 역방향 DNS 클라우드 서비스에 대 한 Azure PowerShell을 사용 하 여 hello 클래식 배포 모델에 대 한 자세한 지침을 제공 합니다. 클라우드 서비스에 대 한 역방향 DNS 구성 Azure CLI 1.0 또는 Azure CLI 2.0 hello Azure 포털을 통해 지원 되지 않습니다.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>역방향 DNS tooexisting 클라우드 서비스를 추가 합니다.

기존 클라우드 서비스는 역방향 DNS 레코드 tooan tooadd:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>역방향 DNS를 사용하여 클라우드 서비스 만들기

toocreate hello 역방향 DNS 속성이 이미 지정 된 새 클라우드 서비스:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>기존 클라우드 서비스에 대한 역방향 DNS 보기

tooview hello 기존 클라우드 서비스에 대 한 DNS 속성 역방향:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>기존 클라우드 서비스에서 역방향 DNS 제거

기존 클라우드 서비스에서 역방향 DNS 속성 tooremove:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>FAQ

### <a name="how-much-do-reverse-dns-records-cost"></a>역방향 DNS 레코드의 비용은 얼마인가요?

무료입니다.  역방향 DNS 레코드 또는 쿼리에 대한 추가 비용은 없습니다.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>내 역방향 DNS 레코드 확인은 인터넷을 hello?

예. Azure 서비스에 대 한 hello 역방향 DNS 속성을 설정 하면 모든 hello DNS 위임이 Azure가 관리 하 고 DNS 영역 모든 인터넷 사용자가 확인 하는 역방향 DNS 레코드 tooensure 필요한.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>내 Azure 서비스에 대해 기본 역방향 DNS 레코드가 생성되나요?

안 됩니다. 역방향 DNS는 옵트인(opt in) 기능입니다. 기본값은 없습니다 tooconfigure 하지 않으려는 경우 역방향 DNS 레코드가 만들어집니다. 해당 합니다.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Hello 정규화 된 도메인 이름 (FQDN)에 대 한 hello 형식은 무엇입니까?

FQDN은 정방향 순서로 지정되고 점으로 끝나야 합니다(예: "app1.contoso.com.").

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Hello에 대 한 유효성 검사 hello 역방향 DNS 필자가 지정한 경우 실패 하면 어떻게 되나요?

Hello 역방향 DNS 유효성 검사에 실패 하는 경우 hello 작업 tooconfigure hello 역방향 DNS 레코드는 실패 합니다. 필요에 따라 hello 역방향 DNS 값을 수정 하 고 다시 시도 하십시오.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Azure App Service에 대한 역방향 DNS를 구성할 수 있나요?

아니요. 역방향 DNS hello Azure 앱 서비스에 대 한 지원 되지 않습니다.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>내 Azure 대해 다중 역방향 DNS 레코드를 구성할 수 있나요?

안 됩니다. Azure는 각 Azure Cloud Service 또는 PublicIpAddress에 대해 단일 역방향 DNS 레코드를 지원합니다.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>IPv6 PublicIpAddress 리소스에 대한 역방향 DNS를 구성할 수 있나요?

안 됩니다. Azure는 현재 IPv4 PublicIpAddress 리소스 및 Cloud Services에 대해서만 역방향 DNS를 지원합니다.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>보내기 메일 tooexternal 도메인 내 Azure 계산 서비스에서

아니요. [Azure 계산 서비스 보내는 전자 메일 tooexternal 도메인을 지원 하지 않습니다.](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>다음 단계

역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.
<br>
너무 방법에 대해 알아봅니다[Azure dns에서 ISP에 할당 된 IP 범위에 대 한 호스트 hello 역방향 조회 영역](dns-reverse-dns-for-azure-services.md)합니다.

