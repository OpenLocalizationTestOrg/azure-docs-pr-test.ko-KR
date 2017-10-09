---
title: "Azure 가상 컴퓨터 템플릿 aaaMultiple IP 주소 | Microsoft Docs"
description: "어떻게 tooassign 여러 IP 주소에 대해 알아봅니다 tooa 가상 컴퓨터는 Azure 리소스 관리자 템플릿을 사용 하 여 합니다."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Toovirtual 컴퓨터는 Azure 리소스 관리자 템플릿을 사용 하 여 여러 IP 주소를 할당 합니다.

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

이 문서에서는 리소스 관리자 템플릿을 사용 하 여 toocreate hello Azure 리소스 관리자 배포를 통해 가상 컴퓨터 (VM)을 모델링 하는 방법을 설명 합니다. 여러 공용 및 개인 IP 주소를 할당할 수 없습니다 toohello hello 클래식 배포 모델을 통해 VM을 배포 하는 경우 동일한 NIC입니다. Azure 배포 모델을 읽을 hello에 대 한 자세한 toolearn [배포 모델을 이해](../resource-manager-deployment-model.md) 문서.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>템플릿 설명

서식 파일 배포 tooquickly 있으며 다른 구성 값으로 Azure 리소스를 만들고 일관 되 게 합니다. 읽기 hello [리소스 관리자 템플릿 연습](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure 리소스 관리자 템플릿으로 모르는 경우 문서. hello [여러 IP 주소를 사용 하 여 VM 배포](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) 템플릿을 사용 하는이 문서의 내용입니다.

<a name="resources"></a>배포 hello 템플릿은 hello 다음 리소스를 만듭니다.

|리소스|이름|설명|
|---|---|---|
|네트워크 인터페이스|*myNic1*|hello 세 가지 IP 구성은이 문서의 hello 시나리오 섹션에 설명 된 생성 되 고 toothis NIC. 할당|
|공용 IP 주소 리소스|2개 *myPublicIP* 및 *myPublicIP2*가 만들어집니다.|이러한 리소스 고정 공용 IP 주소 할당 및 toohello 할당 *IPConfig-1* 및 *IPConfig-2* hello 시나리오에 설명 된 IP 구성 합니다.|
|VM|*myVM1*|표준 DS3 VM|
|가상 네트워크|*myVNet1*|*mySubnet*라는 단일 서브넷이 있는 가상 네트워크|
|저장소 계정|고유 toohello 배포|저장소 계정|

<a name="parameters"></a>Hello 서식 파일을 배포할 때는 hello 매개 변수 뒤에 대 한 값을 지정 해야 합니다.

|이름|설명|
|---|---|
|adminUsername|관리자 사용자 이름. hello 사용자 이름을 사용 하 여 따라야 [Azure 사용자 이름 요구 사항을](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.|
|adminPassword|관리자 암호 hello 암호 따라야 [Azure 암호 요구 사항을](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm)합니다.|
|dnsLabelPrefix|PublicIPAddressName1에 대한 DNS 이름. hello DNS 이름에는 hello 공용 할당 된 IP 주소의 toohello VM tooone를 해결 됩니다. hello 이름은 고유 해야 hello Azure 내에서 만들어야 하는 지역 (위치)에서 VM hello 합니다.|
|dnsLabelPrefix1|PublicIPAddressName2에 대한 DNS 이름. hello DNS 이름에는 hello 공용 할당 된 IP 주소의 toohello VM tooone를 해결 됩니다. hello 이름은 고유 해야 hello Azure 내에서 만들어야 하는 지역 (위치)에서 VM hello 합니다.|
|OSVersion|hello hello VM에 대 한 Windows/Linux 버전입니다. hello 운영 체제가 지정 된 Windows/Linux 버전을 선택 하는 hello의 완전 하 게 패치가 적용 된 이미지입니다.|
|imagePublisher|hello Windows/Linux 이미지 게시자 hello에 대 한 VM을 선택 합니다.|
|imageOffer|hello에 대 한 hello Windows/Linux 이미지 VM을 선택 합니다.|

Hello 서식 파일에서 배포 된 hello 리소스의 각 작업은 몇 가지 기본 설정으로 구성 됩니다. Hello 메서드를 다음 중 하나를 통해 이러한 설정을 볼 수 있습니다.

- **GitHub의 hello 템플릿 보기:** 서식 파일에 익숙한 경우 hello 내에서 hello 설정을 볼 수 있습니다 [템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json)합니다.
- **배포한 후 hello 설정을 보려면:** 템플릿으로 잘 모르는 경우 hello 다음 섹션 중 하나에 단계를 사용 하 여 hello 템플릿을 배포 하 고 다음 배포 후 hello 설정을 볼 수 있습니다.

Hello Azure 포털, PowerShell 또는 hello Azure CLI (명령줄 인터페이스) toodeploy hello 서식 파일을 사용할 수 있습니다. 모든 생성 되는 hello 결과가 동일 합니다. toodeploy hello 템플릿 hello 다음 섹션 중 하나에 단계를 완료 hello 합니다.

## <a name="deploy-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 배포

단계를 수행 하는 전체 hello hello Azure 포털을 사용 하 여 toodeploy hello 템플릿을 합니다.

1. 필요한 경우 hello 서식 파일을 수정 합니다. hello에 나열 된 설정과 hello 리소스를 배포 하는 hello 템플릿 [리소스](#resources) 이 문서의 섹션. toolearn 템플릿에 대 한 자세한 방법과 tooauthor를 읽기 hello [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)문서.
2. Hello 메서드를 다음 중 하나가 지정 된 hello 서식 파일을 배포 합니다.
    - **Hello 포털에서 템플릿을 선택 hello:** hello에서 단계를 완료 하는 hello [사용자 지정 서식 파일에서 리소스를 배포](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) 문서. 명명 된 hello 기존 템플릿을 선택 *101 vm-다중 ipconfig*합니다.
    - **직접:** hello hello 포털에서 직접 단추 tooopen hello 템플릿을 다음를 클릭 합니다.<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Hello 방법에 관계 없이 선택 하면 toosupply 값 hello에 필요한 [매개 변수](#parameters) 이전에이 문서에 나와 있습니다. Hello VM 배포 된 후 toohello VM을 연결 하 고 hello 개인 IP 주소 toohello 운영 체제 hello를 완료 하 여 배포 된 hello에 단계 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

## <a name="deploy-using-powershell"></a>PowerShell을 사용하여 배포

PowerShell에서 다음 단계 완료 hello를 사용 하 여 toodeploy hello 템플릿:

1. Hello의 hello 단계를 완료 하 여 배포 hello 템플릿을 [PowerShell과 함께 서식 파일을 배포](../azure-resource-manager/resource-group-template-deploy-cli.md) 문서. hello 문서 서식 파일을 배포 하기 위한 여러 옵션을 설명 합니다. Toodeploy hello를 사용 하 여 선택 하는 경우 `-TemplateUri parameter`,이 서식 파일에 대 한 URI를 hello *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*합니다. Toodeploy hello를 사용 하 여 선택 하는 경우 `-TemplateFile` 매개 변수를 복사 hello 내용의 hello [템플릿 파일](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) 컴퓨터에 새 파일에는 GitHub에서 합니다. 필요한 경우 hello 템플릿 내용을 수정 합니다. hello에 나열 된 설정과 hello 리소스를 배포 하는 hello 템플릿 [리소스](#resources) 이 문서의 섹션. toolearn 템플릿에 대 한 자세한 방법과 tooauthor를 읽기 hello [제작 Azure 리소스 관리자 템플릿을 ](../azure-resource-manager/resource-group-authoring-templates.md)문서.

    Hello에 나열 된 hello 매개 변수 값에 대 한 값을 제공 해야 hello 옵션을 선택 된 toodeploy hello 서식 파일에 관계 없이 [매개 변수](#parameters) 이 문서의 섹션. Hello의 hello 내용을 복사 하는 매개 변수 파일을 사용 하 여 toosupply 매개 변수를 선택 하면 [매개 변수 파일](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) 컴퓨터에 새 파일에는 GitHub에서 합니다. Hello 파일의 hello 값을 수정 합니다. Hello에 대 한 hello 값으로 생성 하는 hello 파일 사용 `-TemplateParameterFile` 매개 변수입니다.

    hello OSVersion, ImagePublisher, imageOffer 매개 변수에 대 한 유효한 값 toodetermine hello의 단계를 완료 hello [탐색 및 선택 Windows VM 이미지 문서](../virtual-machines/windows/cli-ps-findimage.md) 문서.

    >[!TIP]
    >dnslabelprefix를 사용할 수 있는지 확실 하지 않은 경우 입력 hello `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` 아웃 toofind 명령입니다. 경우에 사용할 수 있는, hello 명령이 반환 합니다 `True`합니다.

2. Hello VM 배포 된 후 toohello VM을 연결 하 고 hello 개인 IP 주소 toohello 운영 체제 hello를 완료 하 여 배포 된 hello에 단계 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

## <a name="deploy-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 배포

다음 단계 완료 hello Azure CLI 1.0 hello를 사용 하 여 toodeploy hello 템플릿:

1. Hello의 hello 단계를 완료 하 여 배포 hello 템플릿을 [hello Azure CLI로 템플릿을 배포](../azure-resource-manager/resource-group-template-deploy-cli.md) 문서. hello 문서 hello 서식 파일을 배포 하기 위한 여러 옵션을 설명 합니다. Toodeploy hello를 사용 하 여 선택 하는 경우 `--template-uri` (-f),이 서식 파일에 대 한 URI를 hello *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*합니다. Toodeploy hello를 사용 하 여 선택 하는 경우 `--template-file` (-f) 매개 변수를 복사 hello 내용의 hello [템플릿 파일](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) 컴퓨터에 새 파일에는 GitHub에서 합니다. 필요한 경우 hello 템플릿 내용을 수정 합니다. hello에 나열 된 설정과 hello 리소스를 배포 하는 hello 템플릿 [리소스](#resources) 이 문서의 섹션. toolearn 템플릿에 대 한 자세한 방법과 tooauthor를 읽기 hello [제작 Azure 리소스 관리자 템플릿을 ](../azure-resource-manager/resource-group-authoring-templates.md)문서.

    Hello에 나열 된 hello 매개 변수 값에 대 한 값을 제공 해야 hello 옵션을 선택 된 toodeploy hello 서식 파일에 관계 없이 [매개 변수](#parameters) 이 문서의 섹션. Hello의 hello 내용을 복사 하는 매개 변수 파일을 사용 하 여 toosupply 매개 변수를 선택 하면 [매개 변수 파일](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) 컴퓨터에 새 파일에는 GitHub에서 합니다. Hello 파일의 hello 값을 수정 합니다. Hello에 대 한 hello 값으로 생성 하는 hello 파일 사용 `--parameters-file` (-e) 매개 변수입니다.

    hello OSVersion, ImagePublisher, imageOffer 매개 변수에 대 한 유효한 값 toodetermine hello의 단계를 완료 hello [탐색 및 선택 Windows VM 이미지 문서](../virtual-machines/windows/cli-ps-findimage.md) 문서.

2. Hello VM 배포 된 후 toohello VM을 연결 하 고 hello 개인 IP 주소 toohello 운영 체제 hello를 완료 하 여 배포 된 hello에 단계 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
