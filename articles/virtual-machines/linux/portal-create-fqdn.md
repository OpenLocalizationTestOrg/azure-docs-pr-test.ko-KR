---
title: "Azure Portal에서 Linux VM에 대한 FQDN 만들기 | Microsoft Docs"
description: "Azure Portal에서 가상 컴퓨터를 기반으로 한 Resource Manager에 대한 정규화된 도메인 이름 또는 FQDN을 만드는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 49bfec791fcca3feabc4eb280cefd7faada0ea31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a>Linux VM용 Azure Portal에서 정규화된 도메인 이름 만들기

[Azure Portal](https://portal.azure.com)에서 VM(가상 컴퓨터)을 만들 때, 가상 컴퓨터의 공용 IP 리소스가 자동으로 만들어집니다. 이 IP 주소를 사용하여 VM에 원격으로 액세스합니다. 포털에서 [정규화된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) 또는 FQDN을 만들지는 않지만 VM을 만들면 이름을 추가할 수 있습니다. 이 문서에서는 DNS 이름 또는 FQDN을 만드는 단계를 보여 줍니다.

## <a name="create-a-fqdn"></a>FQDN 만들기
이 문서에서는 사용자가 VM을 이미 만들었다고 가정합니다. 필요한 경우 [포털에서](quick-create-portal.md) 또는 [Azure CLI를 사용하여](quick-create-cli.md) VM을 만들 수 있습니다. VM이 실행되면 다음 단계를 따릅니다.

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

이제 `ssh azureuser@mydns.westus.cloudapp.azure.com`을 사용하는 경우처럼 이 DNS 이름을 사용하여 원격으로 VM에 연결할 수 있습니다.

## <a name="next-steps"></a>다음 단계
VM에는 공용 IP 및 DNS 이름이 있으므로 nginx, MongoDB, Docker와 같은 일반적인 응용 프로그램 프레임워크 또는 서비스를 배포할 수 있습니다.

또한 Azure 배포 구축에 대한 팁은 [Resource Manager 사용](../../azure-resource-manager/resource-group-overview.md)에서 자세히 읽어볼 수 있습니다.

