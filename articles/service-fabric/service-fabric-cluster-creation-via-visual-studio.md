---
title: "Visual Studio를 사용 하 여 서비스 패브릭 클러스터를 aaaSetting | Microsoft Docs"
description: "Visual Studio에서 Azure 리소스 그룹 프로젝트에서 만든 Azure 리소스 관리자 템플릿을 사용 하 여 서비스 패브릭을 tooset 클러스터링 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Visual Studio를 사용하여 서비스 패브릭 클러스터 설정
이 문서에서는 Visual Studio 및 Azure 리소스 관리자 템플릿을 사용 하 여 Azure 서비스 패브릭을 tooset 클러스터링 하는 방법을 설명 합니다. Visual Studio Azure 리소스 그룹 프로젝트 toocreate hello 템플릿을 사용 합니다. 배포할 수 hello 서식 파일을 만든 후 Visual Studio에서 직접 tooAzure 합니다. 스크립트에서 또는 CI(연속 통합) 기능의 일부로 사용할 수도 있습니다.

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Azure 리소스 그룹 프로젝트를 사용하여 서비스 패브릭 클러스터 템플릿 만들기
tooget 시작, Visual Studio를 열고 Azure 리소스 그룹 프로젝트를 만듭니다 (hello에서 사용할 수 **클라우드** 폴더):

![선택한 Azure 리소스 그룹 프로젝트를 사용하는 새 프로젝트 대화 상자][1]

이 프로젝트에 대 한 새 Visual Studio 솔루션을 만들거나 tooan 기존 솔루션에 추가할 수 있습니다.

> [!NOTE]
> Hello Azure 리소스 그룹 프로젝트 hello 클라우드 노드 아래에 표시 되지 않으면, 않아도 hello Azure SDK가 설치 되어 있습니다. 웹 플랫폼 설치 관리자를 시작 ([지금 설치](http://www.microsoft.com/web/downloads/platform.aspx) 설치 하지 않은 경우), "Azure SDK에 대 한.NET" 및 Visual Studio 버전에 호환 되는 hello 버전 설치에 대 한 다음 검색 하 고 있습니다.
> 
> 

Hello 확인 단추를 맞추면 Visual Studio에서 묻는 tooselect hello 리소스 관리자 템플릿을 toocreate:

![선택한 서비스 패브릭 클러스터 템플릿을 사용하여 Azure 템플릿 대화 상자를 선택합니다.][2]

Hello 서비스 패브릭 클러스터 템플릿과 적중된 hello 확인 단추를 다시 선택 합니다. hello 프로젝트 및 hello 리소스 관리자 템플릿 이제 만들었습니다.

## <a name="prepare-hello-template-for-deployment"></a>배포에 대 한 hello 템플릿 준비
Hello 템플릿이 있으면 배포 toocreate hello 클러스터 전에 hello 필요한 템플릿 매개 변수 값을 제공 해야 합니다. 이러한 매개 변수 값 hello에서 읽혀집니다 `ServiceFabricCluster.parameters.json` hello에 있는 파일 `Templates` hello 리소스 그룹 프로젝트의 폴더입니다. Hello 파일을 열고 hello 다음 값을 제공 합니다.

| 매개 변수 이름 | 설명 |
| --- | --- |
| adminUserName |서비스 패브릭 컴퓨터 (노드)에 대 한 hello 관리자 계정의 hello 이름입니다. |
| certificateThumbprint |hello 클러스터를 보호 하는 hello 인증서의 지문 안녕하세요입니다. |
| sourceVaultResourceId |hello *리소스 ID* hello 키 자격 증명 모음의 hello 클러스터를 보호 하는 hello 인증서 저장 됩니다. |
| certificateUrlValue |hello 클러스터 보안 인증서의 hello URL입니다. |

Visual Studio 서비스 패브릭 리소스 관리자 템플릿 hello 인증서로 보호 되는 보안 클러스터를 만듭니다. 이 인증서는 hello로 식별 되 마지막 세 개의 템플릿 매개 변수 (`certificateThumbprint`, `sourceVaultValue`, 및 `certificateUrlValue`)에 있어야 하 고는 **Azure 키 자격 증명 모음**합니다. 어떻게 toocreate hello 클러스터 보안 인증서에 대 한 자세한 내용은 참조 하십시오. [서비스 패브릭 클러스터 보안 시나리오](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) 문서.

## <a name="optional-change-hello-cluster-name"></a>선택 사항: hello 클러스터 이름 변경
모든 서비스 패브릭 클러스터에는 이름이 있습니다. 클러스터 이름 ("hello Azure 지역) 함께 개인 Azure에서 패브릭 클러스터를 만들면 hello 클러스터에 대 한 hello 도메인 이름 (DNS System) 이름입니다. 예를 들어, 클러스터 이름을 `myBigCluster`, hello 새 클러스터를 호스트 하는 hello 리소스 그룹의 hello 위치 (Azure 지역)는 미국 동부를 hello 클러스터의 DNS 이름을 hello 됩니다 `myBigCluster.eastus.cloudapp.azure.com`합니다.

기본적으로 hello 클러스터 이름은 자동으로 생성 이며 임의 접미사 tooa "클러스터" 접두사를 연결 하 여 고유 하 게 합니다. 이렇게 하면 매우 쉽게 toouse hello 서식 파일의 일부로 **연속 통합** (CI) 시스템입니다. Toouse 의미 있는 tooyou 있는 클러스터에 대해 특정 이름을 설정의 hello hello 값 `clusterName` hello 리소스 관리자 템플릿 파일에 변수 (`ServiceFabricCluster.json`) tooyour 선택한 이름입니다. 변수는 해당 파일에 정의 된 hello 첫 번째 변수입니다.

## <a name="optional-add-public-application-ports"></a>옵션: 공용 응용 프로그램 포트 추가
배포 하기 전에 hello 클러스터에 대 한 toochange hello 공용 응용 프로그램이 포트를 할 수 있습니다. 기본적으로 두 개의 공용 TCP 포트 (80 및 8081) hello 템플릿을 엽니다. 응용 프로그램에 대 한 추가 해야 할 경우 hello 템플릿에서 hello Azure 부하 분산 장치 정의 수정 합니다. hello 정의 hello 주 템플릿 파일에 저장 됩니다 (`ServiceFabricCluster.json`). 해당 파일을 열고 `loadBalancedAppPort`를 검색합니다. 각 포트는 세 개의 아티팩트에 연결됩니다.

1. Hello 포트에 대 한 hello TCP 포트 값을 정의 하는 템플릿 변수:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *프로브* Azure 부하 분산 장치가 하나 tooanother 통해 toouse 실패 하기 전에 특정 서비스 패브릭 노드 하려고 시도 빈도 및 기간 hello에 대 한 정의입니다. hello 프로브는 hello 부하 분산 장치 리소스의 일부입니다. 첫 번째 기본 응용 프로그램 포트 hello에 대 한 hello 프로브 정의 다음과 같습니다.
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. A *부하 분산 규칙* hello 포트 및 부하 분산 서비스 패브릭 클러스터 노드 집합을 사용 하는 hello 프로브 함께 연결입니다.
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Toodeploy toohello 클러스터를 계획 하는 hello 응용 프로그램에서 더 많은 포트를 필요 만드는 추가 검색 및 부하 분산 규칙 정의 하 여 추가할 수 있습니다. 방법에 대 한 자세한 내용은 Azure 부하 분산 장치를 리소스 관리자 템플릿을 통해 toowork 참조 [템플릿을 사용 하는 내부 부하 분산 장치를 만들기 전에](../load-balancer/load-balancer-get-started-ilb-arm-template.md)합니다.

## <a name="deploy-hello-template-by-using-visual-studio"></a>Visual Studio를 사용 하 여 hello 서식 파일을 배포 합니다.
모든 hello에 필요한 매개 변수 값 저장 한 후의`ServiceFabricCluster.param.dev.json` 파일을 준비 toodeploy hello 템플릿을 있고 서비스 패브릭 클러스터를 만듭니다. Visual Studio 솔루션 탐색기에서 hello 리소스 그룹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포 | 새 배포...** . 필요한 경우 Visual Studio hello 표시 됩니다 **tooResource 그룹 배포** tooauthenticate tooAzure 묻는 대화 상자:

![배포 tooResource 그룹 대화 상자][3]

hello 대화 상자에는 hello 클러스터와 새 옵션 toocreate을 hello 제공에 대 한 기존 리소스 관리자 리소스 그룹을 선택할 수 있습니다. 일반적으로 이렇게 하면 의미 toouse 서비스 패브릭 클러스터에 대 한 별도 리소스 그룹 있습니다.

Hello 배포 단추 맞추면 tooconfirm hello 템플릿 매개 변수 값 Visual Studio에 요청 합니다. 적중된 hello **저장** 단추입니다. 매개 변수가 하나 지속형된 값이 없는: hello 클러스터에 대 한 hello 관리 계정 암호입니다. Visual Studio 하나에 대 한 메시지에 따라 tooprovide 암호 값을 해야 합니다.

> [!NOTE]
> Azure SDK 2.9부터는 Visual Studio에서 배포 중에 **Azure 주요 자격 증명 모음**에서 암호를 읽도록 지원합니다. Hello 템플릿 매개 변수 대화 상자에서 해당 hello 확인 `adminPassword` 매개 변수 입력란 오른쪽 hello에 대 한 작은 "키" 아이콘입니다. 이 아이콘으로 hello hello 클러스터에 대 한 관리자 암호는 기존 키 자격 증명 모음 암호 tooselect이 있습니다. 단지 있는지 toofirst을 주요 자격 증명 모음의 hello 고급 액세스 정책에서 템플릿 배포에 대 한 Azure 리소스 관리자 액세스를 사용 하도록 설정 합니다. 
> 
> 

Hello Visual Studio 출력 창에 hello 배포 프로세스의 hello 진행률을 모니터링할 수 있습니다. Hello 템플릿 배포가 완료 되 면 새 클러스터가 준비 toouse 되었습니다!

> [!NOTE]
> PowerShell이 현재 사용 중인 hello 컴퓨터에서 사용 되는 tooadminister Azure 않은 경우 toodo 약간 정리 작업 필요.
> 
> 1. PowerShell 스크립팅 hello를 실행 하 여 사용 하도록 설정 [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) 명령입니다. 개발 컴퓨터인 경우 "제한 없음" 정책이 일반적으로 허용됩니다.
> 2. 결정 여부 Azure PowerShell 명령 및 실행에서 진단 데이터 수집 tooallow [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) 또는 [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) 필요에 따라 합니다. 이렇게 하면 템플릿 배포 중 발생하는 불필요한 프롬프트를 줄일 수 있습니다.
> 
> 

오류가 있는 경우 이동 toohello [Azure 포털](https://portal.azure.com/) 및 열기 hello 리소스 그룹에 배포 합니다. 클릭 **모든 설정을**, 클릭 **배포** hello 설정 블레이드에서 합니다. 리소스 그룹 배포에 오류가 발생한 경우 여기에 자세한 진단 정보를 남깁니다.

> [!NOTE]
> 서비스 패브릭 클러스터 특정 개수의 toomaintain 가용성을 노드 toobe 필요 하 고 상태-"쿼럼을 유지 관리 합니다." 참조 tooas 유지 따라서,는 것은 안전 tooshut hello 클러스터의 hello 시스템의 모든 작동 중지 처음 수행 하지 않는 한는 [시/도의 전체 백업](service-fabric-reliable-services-backup-restore.md)합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [Hello Azure 포털을 사용 하 여 서비스 패브릭 클러스터를 설정 하는 방법에 대 한 자세한 내용은](service-fabric-cluster-creation-via-portal.md)
* [자세한 내용은 방법 toomanage Visual Studio를 사용 하 여 서비스 패브릭 응용 프로그램 및 배포](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
