---
title: "Azure에서 방화벽 aaaUse FreeBSD 패킷 필터 toocreate | Microsoft Docs"
description: "자세한 내용은 방법 toodeploy NAT FreeBSD의를 사용 하 여 방화벽 PF Azure에서."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>어떻게 toouse FreeBSD 패킷 필터 toocreate Azure의 보안 방화벽
이 문서에서는 소개 어떻게 toodeploy 일반적인 웹 서버 시나리오에 대 한 Azure 리소스 관리자 템플릿을 통해 FreeBSD의 Packer 필터를 사용 하는 NAT 방화벽입니다.

## <a name="what-is-pf"></a>PF란?
PF(패킷 필터 또는 pf)는 BSD에서 사용이 허가된 상태 저장 패킷 필터로, 방화벽을 위한 소프트웨어의 핵심 부분입니다. PF는 빠르게 발전해 왔으며 현재 사용 가능한 다른 방화벽에 비해 여러 가지 이점을 제공합니다. 네트워크 주소 변환 (NAT) PF 첫 날 패킷 스케줄러 다음 이후 이며 활성 큐 관리 hello ALTQ 통합를 PF의 구성을 통해 구성 가능 하 여 PF에 통합 되었습니다. 장애 조치 및 중복성, 세션 인증 및 ftp 프록시 tooease 게이트웨이나 hello 어려운 FTP 프로토콜을 authpf pfsync CARP 등의 기능 PF. 확장도 한 즉, PF는 강력하고 풍부한 기능을 갖춘 방화벽입니다. 

## <a name="get-started"></a>시작
Hello 클라우드에서 사용자 웹 서버에 대 한 보안 방화벽 설정에 관심이 다시 시작 하겠습니다. 이 Azure 리소스 관리자 템플릿 tooset 네트워킹 토폴로지를 사용 하는 hello 스크립트를 적용할 수 있습니다.
PF 및 FreeBSD 가상 컴퓨터를 두 개를 사용 하 여 hello Nginx 웹 서버 설치 하 고 구성 하는 NAT /redirection을 수행 하 hello Azure 리소스 관리자 템플릿 FreeBSD 가상 컴퓨터를 설정 합니다. 또한 두 명의 웹 서버 hello에 대 한 NAT tooperforming 송신 트래픽, hello NAT/리디렉션 가상 컴퓨터 HTTP 요청을 차단 하 고 라운드 로빈 방식으로 두 명의 웹 서버 toohello 리디렉션됩니다. hello VNet hello 개인 라우팅할 수 없는 IP 주소 공간 10.0.0.2/24 사용 하 고 hello 템플릿의 hello 매개 변수를 수정할 수 있습니다. 또한 hello Azure 리소스 관리자 템플릿 hello 대상 IP 주소에 따라 toooverride Azure 기본 경로 사용 하는 전체 VNet의 개별 경로 컬렉션인 hello에 대 한 경로 테이블을 정의 합니다. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Azure CLI를 통해 배포
최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다. [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 `myResourceGroup` hello에 `West US` 위치 합니다.

```azurecli
az group create --name myResourceGroup --location westus
```

다음으로 hello 템플릿을 배포 [pf freebsd 설정](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) 와 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다. 다운로드 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) 아래에서 동일한 경로 hello 및 리소스 값을 사용 하 여 자체와 같은 정의 `adminPassword`, `networkPrefix`, 및 `domainNamePrefix`합니다. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

약 5 분 후의 hello 정보 받아볼 `"provisioningState": "Succeeded"`합니다. 수 있습니다 ssh toohello 프런트 엔드 VM (NAT) 또는 hello 공용 IP 주소 또는 FQDN hello 프런트 엔드 VM (NAT)을 사용 하 여 브라우저에서 Nginx 웹 서버에 액세스 합니다. hello 다음 예에서는 나열 FQDN과 hello에 toohello 프런트 엔드 VM (NAT) 할당 된 공용 IP 주소 `myResourceGroup` 리소스 그룹입니다. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>다음 단계
Azure에서 사용자 고유의 NAT를 tooset 시겠습니까? 무료 오픈 소스면서 강력한 기능을 원하시나요? 그렇다면 PF가 적격입니다. Hello 템플릿을 사용 하 여 [pf freebsd 설정](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), 라운드 로빈 부하 분산 FreeBSD의를 사용 하 여 NAT 방화벽을 5 분 tooset만 하면 일반적인 웹 서버 시나리오에 대 한 Azure에서 PF 합니다. 

Azure에서 FreeBSD의 toolearn hello 제공 하려는 경우 너무 참조[Azure에서 소개 tooFreeBSD](freebsd-intro-on-azure.md)합니다.

PF에 대 한 자세한 tooknow를 원하는 경우 너무 참조[FreeBSD 지침 서](https://www.freebsd.org/doc/handbook/firewalls-pf.html) 또는 [PF-사용자 설명서](https://www.freebsd.org/doc/handbook/firewalls-pf.html)합니다.
