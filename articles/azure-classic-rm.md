---
title: "aaaResource 관리자 및 서비스 관리 (클래식) 배포 모드 | Microsoft Docs"
description: "리소스 관리자 및 클래식 배포 모델 간의 hello 차이점에 알아봅니다."
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Azure 배포 모델
Azure 플랫폼 hello 전환입니다.  새 tooAzure 이거나 사용 되 고 그 년, 인지 toounderstand 중요 한 몇 가지 주요 변경 내용 hello 하는 중 toohello 플랫폼이이 전환 중입니다.

모든 Azure 리소스 배포 모델을 따르는 hello 중 하나 또는 모두를 지원 합니다.

* **리소스 관리자:** hello Azure 리소스에 대 한 최신 배포 모델입니다. 대부분의 최신 리소스는 이미 이 배포 모델을 지원하고 결국 모든 리소스도 지원할 것입니다.   
* **클래식:** 이 모델은 현재 대부분의 기존 Azure 리소스에 의해 지원됩니다. 새 리소스 추가 tooAzure이이 모델을 지원 하지 않습니다.

각 Azure 리소스 세부 정보를 해당 되는 서비스 모델에 대 한 hello 설명서 만들 수 있습니다.

## <a name="why-does-this-matter"></a>이것이 왜 문제가 될까요?
다음 이유로 hello에 대 한 중요 한:

* 사용 중인 hello Azure 플랫폼 기능은 이러한 두 모델에서 서로 다릅니다.  예를 들어 있는 hello 리소스 관리자 배포 모델 (또는 리소스 관리자만)를 사용 하 여 만든 리소스를 만들 수 있습니다 [Azure 리소스 관리자 템플릿을](azure-resource-manager/resource-group-overview.md#template-deployment)반면 hello 클래식 배포 모델을 사용 하 여 만든 리소스 수 없습니다.
* 개별 Azure 리소스 기능 hello 또는 동작 hello 두 개의 모델을 다를 수 있습니다 한 모델이 나 다른 hello에만 존재 됩니다.  예를 들어 hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터 간에 분산 트래픽 부하가 *암시적* 가상 컴퓨터는 Azure 클라우드 서비스의 멤버 이며 가상 간에 부하 균형 자동으로 하기 때문에 클라우드 서비스 내의 컴퓨터입니다. 리소스 관리자를 사용 하 여 만든 가상 컴퓨터 클라우드 서비스의 구성원이 아닌 및 별도 Azure 부하 분산 장치 리소스 해야 *명시적으로* 여러 가상 컴퓨터에서 트래픽을 분산 tooload 생성 합니다.  
* Azure 리소스의 생성, 구성 및 관리는 이 두 모델 간에 차이가 있습니다.
* 하나의 배포 모델을 사용하여 생성된 리소스와 다른 배포 모델을 사용하여 생성된 리소스가 반드시 상호 운영 가능한 것은 아닙니다. 예를 들어 한 배포 모델을 사용 하 여 만든 Azure 가상 컴퓨터만 수 hello를 사용 하 여 만든 가상 네트워크를 연결 된 tooAzure 배포 모델이 동일 합니다.    

기본 각각 hello 배포 모델의 각 리소스에 대 한 응용 프로그램 프로그래밍 인터페이스 (API)입니다.  한 [리소스 관리자 API](https://msdn.microsoft.com/library/azure/dn948464.aspx) hello 리소스 관리자 배포 모델에 대 한 및 [서비스 관리 API](https://msdn.microsoft.com/library/azure/ee460799.aspx) hello 클래식 배포 모델에 대 한 합니다. 개발자는 이러한 Api와 toointeract 코드를 작성할 수 있습니다 *직접*합니다.  

하지만 IT 전문가 일반적으로 상호 작용 이러한 Api *간접적으로* 그래픽 포털을 웹 브라우저에서 사용 하 여 Azure PowerShell을 사용 하 여 cmdlet를 사용 하 여 Windows 컴퓨터를 켜거나 hello Azure 명령줄 인터페이스 (CLI)에 Windows, OS X 또는 Linux 컴퓨터입니다. IT 전문가 hello에서 사용 하는 간접 이러한 메서드의 모든 세 hello Api와 직접 상호 작용 합니다. 즉, 새 기능을 도입된 toohello Azure 플랫폼 또는 리소스는 항상 직접 사용할 수 있게 hello API 통해 먼저 hello 간접 방법은 hello에 대 한 지원 새 리소스 및 hello API 사용 가능 후 기능입니다.  

아래 섹션에서는 hello 어떻게 Azure 리소스에 설명 hello 다양 한 배포 모델을 사용 하 여 hello 3 간접 메서드를 통해 구성 됩니다.

## <a name="portals"></a>포털
Azure에는 다음 두 포털이 있습니다.

* **[Azure Portal](https://manage.windowsazure.com):** Azure를 어느 정도 사용했다면 이 포털을 사용한 것입니다. 사용 되는 toocreate 사용 되며 hello 클래식 배포 모델을 지 원하는 이전 Azure 리소스를 구성 합니다. Toocreate 사용 하거나만 지 원하는 리소스 관리자 리소스를 구성할 수 없습니다. 
* **[Azure Preview 포털](https://azure.microsoft.com/overview/preview-portal/):** 최신 Azure 리소스를 사용하는 경우 이 포털을 사용해봤을 것입니다. 일부 Azure 리소스를 구성 하 고 사용 되는 toocreate 수 있습니다. 결국 수 toocreate 수 하 고 모든 Azure 리소스를 구성 합니다. 지 원하는 두 가지 경우 모두 일부 리소스에 대 한이 포털 사용된 toocreate 수 있고 배포 모델 중 하나를 사용 하 여 리소스를 구성 합니다. 

일부 리소스 및 기능만 만들고 사용할 수 있는 한 포털 이나 다른 hello에 구성 합니다. 일부 리소스 또는 기능 만들 수 없습니다 (아직) 또는 각 포털에 구성 된 및 PowerShell로만 구성할 수 있습니다, 그리고 CLI 또는 둘 다 hello 합니다. 각 Azure 리소스에 대 한 hello 설명서를 만들 수 있습니다 방법을 자세히 설명 합니다. 

## <a name="powershell"></a>PowerShell
와 [PowerShell](/powershell/azureps-cmdlets-docs) 명령줄 또는 만든 스크립트 toocreate를 사용 하 고 Windows 컴퓨터에서 Azure 리소스를 구성할 수 있습니다.  개별 Azure 리소스에는 [Resource Manager cmdlet](/powershell/azure/overview), [서비스 관리 cmdlet](/powershell/azure/overview?view=azuresmps-3.7.0) 또는 두 가지 모두가 있을 수 있습니다.  일부 리소스 및 기능 에서만 만들 수 있습니다 및/또는 PowerShell 또는 CLI hello를 사용 하 여 구성 합니다. 리소스 관리자 PowerShell cmdlet을 사용 하는 경우 hello 리소스에 따라 만들고 Azure 리소스를 구성 하기 위한 두 가지 옵션을 할 수 있습니다.

* **PowerShell cmdlet에만:** 만들고 개별적으로 hello cmdlet을 사용 하 여 각 리소스에 대 한 각 Azure 리소스를 구성할 수 있습니다. 이 작업은 명령줄에서 또는 저장할 수 있는 PowerShell 스크립트 및 버전으로 여러 명령을 포함하여 수행할 수 있습니다.
* **Azure 리소스 관리자 템플릿 사용 하 여 PowerShell cmdlet:** PowerShell toocreate Azure에서는 Azure 리소스 관리자 템플릿을 사용 하 여 리소스입니다. 템플릿을 저장하고 버전을 지정할 수 있습니다. 에 대 한 자세한 hello 읽어 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md) 문서. 다운로드하고 수정할 수 있는 일반 솔루션에 대해 몇 가지 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 도 지원됩니다.

## <a name="cli"></a>CLI
만들 수 있으며 hello CLI를 사용 하 여 Windows, OS X 또는 Linux 컴퓨터에서 Azure 리소스를 구성할 수 없습니다.  읽기 hello [설치 hello Azure CLI](cli-install-nodejs.md) 선택한 운영 체제에 문서 tooinstall hello CLI 합니다. PowerShell 등는 리소스를 사용 하 여 만드는 여부에 따라 사용 해야 하는 다양 한 명령이 [리소스 관리자](xplat-cli-azure-resource-manager.md) 또는 hello [클래식 (서비스 관리)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 배포 모델입니다.

## <a name="next-steps"></a>다음 단계
* [Resource Manager](azure-resource-manager/resource-group-overview.md)에 대해 알아봅니다.
* 너무 방법을 이해[템플릿 디자인](best-practices-resource-manager-design-templates.md)합니다.

