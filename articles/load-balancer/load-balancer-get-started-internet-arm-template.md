---
title: "aaaCreate 인터넷 연결 부하 분산 장치-Azure 템플릿 | Microsoft Docs"
description: "어떻게 toocreate 인터넷 연결 부하 분산 장치 템플릿을 사용 하는 리소스 관리자에 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>템플릿을 사용하여 인터넷 연결 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [포털](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [toocreate 인터넷 연결 부하 분산 장치 클래식 배포 모델을 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Hello 템플릿을 사용 하 여 배포 toodeploy 클릭

hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다. toodeploy toodeploy, 클릭 하 여 사용 하 여이 서식 파일에 따라 [이 링크](http://go.microsoft.com/fwlink/?LinkId=544801), 클릭 **tooAzure 배포**hello 기본 매개 변수 값, 필요한 경우 바꾼 hello 포털의 hello 지침을 따릅니다.

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.

PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.

1. Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.
2. Hello 실행 **새로 AzureRmResourceGroupDeployment** 사용 하 여 리소스 그룹 cmdlet toocreate hello 템플릿.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 서식 파일을 배포 합니다.

hello Azure CLI를 사용 하 여 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.

    ```azurecli
    azure config mode arm
    ```

    다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.

        info:    New mode is arm

3. 브라우저에서 이동 너무[퀵 스타트 템플릿 hello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)hello json 파일의 내용을 hello 복사한 컴퓨터에서 새 파일에 붙여 넣습니다. 이 시나리오에서는 있습니다 것 수 값을 복사할 hello 라는 tooa 파일 아래 **c:\lb\azuredeploy.parameters.json**합니다.
4. Hello 실행 **으로 azure 그룹 배포 만들기** cmdlet toodeploy hello 새 부하 분산 장치 hello 템플릿 및 매개 변수를 사용 하 여 파일을 다운로드 하 고 위에서 수정할 수 있습니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
