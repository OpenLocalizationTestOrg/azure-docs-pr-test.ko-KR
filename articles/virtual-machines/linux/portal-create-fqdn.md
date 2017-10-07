---
title: "hello Azure 포털에서에서 Linux VM에 대 한 FQDN aaaCreate | Microsoft Docs"
description: "정규화 된 도메인 이름, 또는 리소스 관리자에 대 한 FQDN toocreate hello Azure 포털에서에서 가상 컴퓨터를 기반 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Linux VM에 대 한 hello Azure 포털에서에서 정규화 된 도메인 이름 만들기

Hello에 가상 컴퓨터 (VM)를 만들 때 [Azure 포털](https://portal.azure.com), hello 가상 컴퓨터에 대 한 공용 IP 리소스를 자동으로 생성 됩니다. VM이 IP 주소 tooremotely 액세스 hello를 사용 합니다. Hello 포털을 만들지 않고 있지만 [정규화 된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), 또는 FQDN으로 추가할 수 있습니다 하나 만들어지면 hello VM입니다. 이 문서에서는 hello 단계 toocreate DNS 이름 또는 FQDN을 보여줍니다.

## <a name="create-a-fqdn"></a>FQDN 만들기
이 문서에서는 사용자가 VM을 이미 만들었다고 가정합니다. 필요한 경우 다음을 할 수 있습니다 [hello 포털에서 VM을 만듭니다](quick-create-portal.md) 또는 [hello Azure CLI로](quick-create-cli.md)합니다. VM이 실행되면 다음 단계를 따릅니다.

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

연결할 수 있습니다. 원격으로 VM이이 DNS를 사용 하 여와 같은 이름을 toohello `ssh azureuser@mydns.westus.cloudapp.azure.com`합니다.

## <a name="next-steps"></a>다음 단계
VM에는 공용 IP 및 DNS 이름이 있으므로 nginx, MongoDB, Docker와 같은 일반적인 응용 프로그램 프레임워크 또는 서비스를 배포할 수 있습니다.

또한 Azure 배포 구축에 대한 팁은 [Resource Manager 사용](../../azure-resource-manager/resource-group-overview.md)에서 자세히 읽어볼 수 있습니다.

