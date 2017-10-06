---
title: "내부 부하 분산 장치-Azure 템플릿 aaaCreate | Microsoft Docs"
description: "내부 프로그램 toocreate 리소스 관리자에서 서식 파일을 사용 하 여 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a>템플릿을 사용하여 내부 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Hello 템플릿을 사용 하 여 배포 toodeploy 클릭

hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다. toodeploy toodeploy, 클릭 하 여 사용 하 여이 서식 파일에 따라 [이 링크](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), 클릭 **tooAzure 배포**hello 기본 매개 변수 값, 필요한 경우 바꾼 hello 포털의 hello 지침을 따릅니다.

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.

PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.

1. Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.
2. Hello 매개 변수 파일 tooyour 로컬 디스크를 다운로드 합니다.
3. Hello 파일을 편집 하 고 저장 합니다.
4. Hello 실행 **새로 AzureRmResourceGroupDeployment** 사용 하 여 리소스 그룹 cmdlet toocreate hello 템플릿.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
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

3. Hello 매개 변수 파일을 열고 해당 내용을 선택한 컴퓨터에 tooa 파일을 저장 합니다. 이 예에서는 저장 hello 매개 변수 파일 너무*parameters.json*합니다.
4. Hello 실행 **으로 azure 그룹 배포 만들기** toodeploy hello 템플릿 및 매개 변수를 사용 하 여 새로운 내부 부하 분산 장치를 hello 명령 파일을 다운로드 하 고 위에서 수정할 수 있습니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>다음 단계

[원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)

