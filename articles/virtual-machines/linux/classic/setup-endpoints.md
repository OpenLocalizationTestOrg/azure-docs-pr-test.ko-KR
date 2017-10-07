---
title: "클래식 Linux VM에 끝점을 aaaSet | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터를 사용 하 여 hello Azure 클래식 포털 tooallow 통신에서에서 Linux VM에 대 한 끝점을 tooset에 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>어떻게 tooset Azure에서 Linux 클래식 가상 컴퓨터에 끝점을
Hello에 다른 가상 컴퓨터와 개인 네트워크 채널을 통해 hello 클래식 배포 모델을 사용 하 여 Azure에서 만드는 모든 Linux 가상 컴퓨터 자동으로 통신할 수 있습니다이 동일한 클라우드 서비스 또는 가상 네트워크. 그러나 hello 인터넷 또는 다른 가상 네트워크에 있는 컴퓨터에 끝점 toodirect hello 인바운드 네트워크 트래픽을 tooa 가상 컴퓨터가 필요합니다. 이 문서는 [Windows 가상 컴퓨터](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에도 적용됩니다.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

Hello에 **리소스 관리자** 배포 모델을 사용 하 여 끝점이 구성 **(Nsg) 네트워크 보안 그룹**합니다. 자세한 내용은 [포트 및 끝점 열기](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

Hello Azure 포털에서에서 Linux 가상 컴퓨터를 만들 때 끝점에 대 한 SSH (보안 셸) 일반적으로 사용자에 대 한 자동으로 만들어집니다. Hello 가상 컴퓨터를 만드는 동안 또는 나중에 필요에 따라 추가 끝점을 구성할 수 있습니다.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>다음 단계
* Hello를 사용 하 여 VM 끝점을 만들 수도 있습니다 [Azure 명령줄 인터페이스](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다. Hello 실행 **azure vm 끝점 만들기** 명령입니다.
* Hello 리소스 관리자 배포 모델에서 가상 컴퓨터를 만든 경우 리소스 관리자 모드에서 Azure CLI hello을도 사용할 수 있습니다[네트워크 보안 그룹을 만들고](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol 트래픽 toohello VM입니다.
