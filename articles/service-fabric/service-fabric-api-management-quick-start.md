---
title: "API 관리 빠른 시작 되 면 서비스 패브릭 aaaAzure | Microsoft Docs"
description: "이 가이드에서는 Azure API 관리 및 서비스 패브릭 tooquickly 시작 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Service Fabric 및 Azure API Management 빠른 시작

이 가이드에서는 알아봅니다 tooset Azure API 관리 서비스 패브릭를 하 고 서비스 패브릭에서 첫 번째 API 작업 toosend 트래픽 tooback 간 서비스를 구성 하는 방법입니다. 서비스 패브릭 Azure API 관리 시나리오에 대해 자세히 toolearn 참조 hello [개요](service-fabric-api-management-overview.md) 문서. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>API 관리 및 서비스 패브릭 tooAzure 배포

hello 첫 번째 단계는 toodeploy API 관리 및 공유 가상 네트워크에서 서비스 패브릭 클러스터 tooAzure 것입니다. 따라서 tooany 백 엔드 서비스 서비스 패브릭에서 직접 서비스 검색과 서비스 파티션 확인 트래픽을 전달을 수행할 수 있도록 서비스 패브릭와 직접 API 관리 toocommunicate를 수 있습니다.

### <a name="topology"></a>토폴로지

이 가이드는 hello 다음 배포 토폴로지 tooAzure API 관리 및 서비스 패브릭의 서브넷에는 hello 동일한 가상 네트워크:

 ![그림 캡션][sf-apim-topology-overview]

리소스 관리자 템플릿은 tooget 신속 하 게 시작 각 배포 단계에 제공 됩니다.

 - 네트워크 토폴로지:
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Service Fabric 클러스터:
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - API Management:
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>TooAzure에 로그인 하 고 구독을 선택 합니다.

이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다. 새 PowerShell 세션을 시작할 때 tooyour Azure 계정에에서 로그인 하 고 Azure 명령을 실행 하기 전에 구독을 선택 합니다.
 
Azure 계정 tooyour에 로그인 합니다.

```powershell
PS > Login-AzureRmAccount
```

구독을 선택합니다.

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

배포에 대해 새 리소스 그룹을 만듭니다. 이름 및 위치를 지정합니다.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Hello 네트워크 토폴로지를 배포 합니다.

hello 첫 번째 단계는 hello 네트워크 토폴로지 toowhich API 관리를 tooset 및 hello 서비스 패브릭 클러스터를 배포 됩니다. hello [network.json] [ network-arm] 리소스 관리자 서식 파일은 구성 된 toocreate 두 서브넷과 가상 네트워크 (VNET) 및 두 개의 보안 그룹 NSG (네트워크). 

hello [network.parameters.json] [ network-parameters-arm] 매개 변수 파일 hello 서브넷 및 API 관리 및 서비스 패브릭에 배포 될 Nsg의 hello 이름을 포함 합니다. 이 가이드에 대 한 hello 매개 변수 값 변경 toobe가 필요 하지 않습니다. 이러한 값을 사용 하는 hello API 관리 및 서비스 패브릭 리소스 관리자 템플릿, 그에 따라에 다른 리소스 관리자 템플릿을 hello 여기를 수정 하는 경우 수정 해야 하도록 합니다. 

 1. Hello 다음 리소스 관리자 템플릿 및 매개 변수 파일을 다운로드 합니다.

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. 다음 PowerShell 명령을 toodeploy hello 리소스 관리자 템플릿 및 매개 변수 파일이 hello 네트워크 설정에 대 한 hello를 사용 합니다.

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Hello 서비스 패브릭 클러스터를 배포 합니다.

Hello 네트워크 리소스 배포를 완료 되 고 나면 hello 다음 단계 toodeploy hello 서브넷에 있는 서비스 패브릭 클러스터 toohello VNET 되며 NSG hello 서비스 패브릭 클러스터에 대 한 지정 합니다. 이 자습서에 대 한 hello 서비스 패브릭 리소스 관리자 템플릿은 hello VNET, 서브넷 및 hello 이전 단계에서 설정한 NSG의 미리 구성 된 toouse hello 이름입니다. 

hello 서비스 패브릭 클러스터 리소스 관리자 템플릿 구성된 toocreate 인증서 보안을 사용 하 여 보안 클러스터입니다. hello 인증서가 클러스터 및 toomanage 사용자 액세스 tooyour 서비스 패브릭 클러스터에 사용 되는 toosecure 노드 통신 합니다. API 관리 서비스 검색에 대 한이 인증서 tooaccess hello 서비스 패브릭 명명 서비스를 사용합니다.

이 단계에서는 클러스터 보안을 위해 Key Vault에 인증서가 있어야 합니다. Key Vault를 사용하여 보안 클러스터를 설정하는 작업에 대한 자세한 내용은 [Resource Manager를 사용하여 Azure에서 클러스터를 만드는 방법에 대한 가이드](service-fabric-cluster-creation-via-arm.md)를 참조하세요.

> [!NOTE]
> Azure Active Directory 인증 클러스터 액세스에 사용 되는 추가 toohello 인증서에 추가할 수 있습니다. Azure Active Directory 방식으로 toomanage 사용자 액세스 tooyour 서비스 패브릭 클러스터를 권장 하는 hello 이지만이 자습서 toocomplete 필요 하지 않습니다. 인증서는 클러스터 노드 간 보안에도 필요하고 Azure API Management 인증에도 필요하지만 Service Fabric 백 엔드에 대해 Azure Active Directory를 사용하는 인증은 현재 지원되지 않습니다.

 1. Hello 다음 리소스 관리자 템플릿 및 매개 변수 파일을 다운로드 합니다.
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. Hello hello에 빈 매개 변수를 입력 `cluster.parameters.json` hello 등 배포에 대 한 파일 [키 자격 증명 모음 정보가](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) 클러스터 인증서에 대 한 합니다.

 3. 다음 PowerShell 명령을 toodeploy hello 리소스 관리자 템플릿 및 매개 변수 파일 toocreate hello 서비스 패브릭 클러스터 hello를 사용 합니다.

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>API Management 배포

API 관리 toohello VNET 서브넷 hello 및 API 관리에 대 한 지정 된 NSG에 마지막으로 배포 합니다. 않아도 toowait 서비스 패브릭 클러스터 배포 toofinish hello에 대 한 API 관리를 배포 하기 전에. 

이 자습서에 대 한 hello API 관리 리소스 관리자 템플릿은 hello VNET, 서브넷 및 hello 이전 단계에서 설정한 NSG의 미리 구성 된 toouse hello 이름입니다. 

 1. Hello 다음 리소스 관리자 템플릿 및 매개 변수 파일을 다운로드 합니다.
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. Hello hello에 빈 매개 변수를 입력 `apim.parameters.json` 배포에 대 한 합니다.

 3. 다음 PowerShell 명령을 toodeploy hello 리소스 관리자 템플릿 및 매개 변수 파일이 API 관리에 대 한 hello를 사용 합니다.

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>API Management 구성

API Management 및 Service Fabric 클러스터가 배포되면 API Management에서 Service Fabric 백 엔드를 구성할 수 있습니다. 이렇게 하면 toocreate 트래픽 tooyour 서비스 패브릭 클러스터를 보내는 백 엔드 서비스 정책은 있습니다.

### <a name="api-management-security"></a>API Management 보안

tooconfigure hello 서비스 패브릭 백 엔드 먼저 tooconfigure API 관리의 보안 설정 합니다. tooconfigure 보안 설정을 hello Azure 포털의에서 tooyour API 관리 서비스를 이동 합니다.

#### <a name="enable-hello-api-management-rest-api"></a>Hello API 관리 REST API를 사용 하도록 설정

hello API 관리 REST API는 현재 hello 유일한 방법은 tooconfigure 백 엔드 서비스입니다. hello 첫 번째 단계는 tooenable hello API 관리 REST API 및 보안을 설정 합니다.

 1. API 관리 서비스 hello 선택 **관리 API-미리 보기** 아래 **보안**합니다.
 2. Hello 확인 **API 관리 REST API 사용** 확인란을 선택 합니다.
 3. 관리 API URL hello-이후 tooset hello 서비스 패브릭 백 엔드를 사용 하는 hello URL입니다.
 4. 생성 된 **액세스 토큰** 만료 날짜와 키를 선택 하 여 hello를 클릭 한 다음 **생성** hello 페이지의 hello 아래쪽으로 단추입니다.
 5. 복사 hello **액세스 토큰** 및 저장-단계를 수행 하는 hello이 사용 해야 합니다. Note hello 기본 키와 보조 키와 다릅니다.

#### <a name="upload-a-service-fabric-client-certificate"></a>Service Fabric 클라이언트 인증서 업로드

API 관리 액세스 tooyour 클러스터를 포함 하는 클라이언트 인증서를 사용 하 여 서비스 검색에 대 한 서비스 패브릭 클러스터도 인증 해야 합니다. 간단한 설명을 위해이 자습서에서는 클러스터에 동일한 인증서는 기본적으로 사용 되는 tooaccess 수 hello 서비스 패브릭 클러스터를 만들 때 지정한을 hello 합니다.

 1. API 관리 서비스 hello 선택 **클라이언트 인증서-미리 보기** 아래 **보안**합니다.
 2. Hello 클릭 **+ 추가** 단추
 2. Hello 개인 키 (.pfx) 인증서의 파일 hello 클러스터 서비스 패브릭 클러스터를 만들 때 지정한 선택한 이름을, hello 개인 키 암호를 제공 합니다.

> [!NOTE]
> 이 자습서에서는 클라이언트 인증 및 클러스터 노드를 보안에 대 한 hello 동일한 인증서를 사용 합니다. 구성 된 하나의 tooaccess 서비스 패브릭 클러스터를 설정한 경우 별도 클라이언트 인증서를 사용할 수 있습니다.

### <a name="configure-hello-backend"></a>Hello 백 엔드를 구성 합니다.

API 관리 보안을 구성 했으므로 hello 서비스 패브릭 백 엔드를 구성할 수 있습니다. 서비스 패브릭 백 엔드에 대 한 hello 서비스 패브릭 클러스터에는 특정 서비스 패브릭 서비스 아니라 hello 백 엔드입니다. 그러면 hello 클러스터를 하나의 서비스 보다 단일 정책 tooroute toomore 있습니다.

이 단계는 앞에서 생성 하는 hello 액세스 토큰이 필요 하 고 hello tooAPI 관리 hello 이전 단계에서 업로드 한 클러스터 인증서에 대 한 지문입니다.

> [!NOTE]
> Hello 이전 단계에서 별도 클라이언트 인증서를 사용 하는 API 관리에 대 한 경우이 단계에서는 추가 toohello 클러스터 인증서 지문에 클라이언트 인증서 hello hello 지문이 필요 합니다.

HTTP PUT 요청 toohello API 관리 API URL hello API 관리 REST API tooconfigure hello 서비스 패브릭 백 엔드 서비스를 사용 하도록 설정할 때 앞에서 기록한 다음 hello를 보냅니다. 표시 됩니다는 `HTTP 201 Created` hello 명령 성공할 때 응답 합니다. 각 필드에 대 한 자세한 내용은 참조 hello API 관리 [백 엔드 API 참조 설명서](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)합니다.

HTTP 명령 및 URL:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

헤더 요청:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

본문 요청:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

hello **url** 여기에서 매개 변수는 모든 요청을 하는 클러스터에서 서비스의 정규화 된 서비스 이름을 라우팅할 tooby 기본 백 엔드 정책에 지정 되는 서비스 이름이 없는 경우. 와 같은 가짜 서비스 이름을 사용할 수 있습니다 "fabric: / 가짜/서비스" toohave 대체 서비스 수행 하려는 경우.

API 관리 toohello 참조 [백 엔드 API 참조 설명서](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) 각 필드에 대 한 자세한 내용은 합니다.

#### <a name="example"></a>예제

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Service Fabric 백 엔드 서비스 배포

서비스 패브릭 백 엔드 tooAPI 관리로 구성 하는 hello를가지고 tooyour 서비스 패브릭 서비스 트래픽을 전송 하는 Api에 대 한 백 엔드 정책을 작성할 수 있습니다. 그러나 먼저 서비스 패브릭 tooaccept 요청에서 실행 되는 서비스를 필요 합니다.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>HTTP 끝점이 있는 Service Fabric 서비스 만들기

이 자습서에 대 한 기본 상태 비저장 ASP.NET Core 신뢰할 수 있는 서비스 hello 기본 웹 API 프로젝트 템플릿을 사용 하 여 만들겠습니다. 이렇게 하면 서비스의 HTTP 끝점을 Azure API Management를 통해 노출합니다.

```
/api/values
```

[ASP.NET Core 개발에 대한 개발 환경을 설정](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core)하는 것으로 시작합니다.

개발 환경이 설정되면 Visual Studio를 관리자 권한으로 시작하고 ASP.NET Core 서비스를 만듭니다.

 1. Visual Studio에서 파일 -> 새 프로젝트를 선택합니다.
 2. 클라우드에 hello 서비스 패브릭 응용 프로그램 템플릿을 선택 하 고 이름을 **"ApiApplication"**합니다.
 3. Hello ASP.NET Core 서비스 템플릿 선택한 이름 hello 프로젝트 **"WebApiService"**합니다.
 4. Web API ASP.NET Core 1.1 hello 프로젝트 템플릿을 선택 합니다.
 5. Hello 프로젝트를 만든 후 엽니다 `PackageRoot\ServiceManifest.xml` hello를 제거 하 고 `Port` hello 끝점 리소스 구성에서 특성:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    이렇게 하면 서비스 패브릭 toospecify API 관리에서 트래픽 tooflow tooit 허용 hello 클러스터 리소스 관리자 템플릿에 hello 네트워크 보안 그룹을 통해 열에서는 있는 hello 응용 프로그램 포트 범위에서 동적으로 포트.
 
 6. Visual Studio tooverify hello web API에서에서 F5 키를 눌러를 로컬로 사용할 수 있습니다. 

    서비스 패브릭 탐색기를 열고 드릴 다운 tooa 특정 인스턴스의 hello ASP.NET Core 서비스 toosee hello 기준 주소 hello 서비스에서 수신 대기 합니다. 추가 `/api/values` toohello 기준 주소와 브라우저에서 엽니다. Hello hello Web API 템플릿에 ValuesController hello에서 Get 메서드를 호출합니다. 두 문자열을 포함 하는 JSON 배열 hello 템플릿에서 제공 되는 hello 기본 응답을 반환 합니다.

    ```json
    ["value1", "value2"]`
    ```

    Azure에서 API 관리를 통해 노출할 수 있는 hello 끝점입니다.

 7. 마지막으로, Azure의 hello 응용 프로그램 tooyour 클러스터를 배포 합니다. [Visual Studio를 사용 하 여](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. 클러스터 끝점을 제공 (예를 들어 `mycluster.westus.cloudapp.azure.com:19000`) Azure에 있는 toodeploy hello 응용 프로그램 tooyour 서비스 패브릭 클러스터입니다.

`fabric:/ApiApplication/WebApiService`로 명명된 ASP.NET Core 상태 비저장 서비스는 이제 Azure의 Service Fabric 클러스터에서 실행되어야 합니다.

## <a name="create-an-api-operation"></a>API 작업 만들기

이제 우리 준비 toocreate API 관리에서 작업으로 해당 외부 클라이언트가 사용 하 여 toocommunicate hello ASP.NET Core hello 서비스 패브릭 클러스터에서 실행 되는 상태 비저장 서비스입니다.

 1. Azure 포털 toohello을 고 tooyour API 관리 서비스 배포를 이동 합니다.
 2. Hello API 관리 서비스 블레이드에서 선택 **Api-미리 보기**
 3. Hello를 클릭 하 여 새로운 API 추가 **빈 API** 상자와 hello 대화 상자를 입력 합니다.

     - **웹 서비스 URL**: Service Fabric 백 엔드에는 이 URL 값이 사용되지 않습니다. 여기에 임의의 값을 입력할 수 있습니다. 이 자습서에서는 `http://servicefabric`을 사용합니다.
     - **이름**: API 이름을 제공합니다. 이 자습서에서는 `Service Fabric App`을 사용합니다.
     - **URL 구성표**: HTTP, HTTPS 또는 둘 다 선택합니다. 이 자습서에서는 `both`를 사용합니다.
     - **API URL 접미사**: API의 접미사를 제공합니다. 이 자습서에서는 `myapp`를 사용합니다.
 
 4. Hello API를 만든 후 클릭 **추가 작업이 +** tooadd 프런트 엔드 API 작업 합니다. Hello 값을 입력 합니다.
    
     - **URL**: 선택 `GET` hello API에 대 한 URL 경로 제공 합니다. 이 자습서에서는 `/api/values`를 사용합니다.
     
       기본적으로 hello URL 경로입니다. 여기에 지정 된 URL 경로 hello toohello 백 엔드 서비스 패브릭 서비스 보내집니다. Hello를 사용 하는 경우 동일한 URL 경로 여기에 경우 해당 서비스 사용 `/api/values`, 추가 수정 없이 hello 작업 작동 합니다. 이 경우는 또한 필요 toospecify 경로 다시 작성 작업이 정책에 나중에 백 엔드 서비스 패브릭 서비스에서 사용 하는 hello URL 경로와 다른 URL 경로 여기 지정할 수도 있습니다.
     - **표시 이름**: hello API에 대 한 모든 이름을 제공 합니다. 이 자습서에서는 `Values`를 사용합니다.

## <a name="configure-a-backend-policy"></a>백 엔드 정책 구성

hello 백 엔드 정책 모든 항목이 함께 연결합니다. 이 hello 백 엔드 서비스 패브릭 서비스 toowhich 요청 라우팅됩니다 구성한입니다. 이 정책 tooany API 작업을 적용할 수 있습니다. hello [서비스 패브릭 용 백 엔드 구성이](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) hello 다음 요청 라우팅 컨트롤을 제공 합니다. 
 - 인스턴스 선택 하거나 하드 코드 된 서비스 패브릭 서비스 인스턴스 이름을 지정 하 여 서비스 (예를 들어 `"fabric:/myapp/myservice"`) 또는 hello HTTP 요청에서 생성 된 (예를 들어 `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Service Fabric 분할 체계를 통해 파티션 키를 생성하여 파티션 확인
 - 상태 저장 서비스 복제본 선택
 - 확인 조건을 다시 서비스 위치를 확인 하 고 요청을 보내거나 toospecify hello 조건을 사용할 수 있는 다시 시도 하십시오.

이 자습서에 대 한 요청을 라우팅하 직접 toohello 이전에 배포한 ASP.NET Core 상태 비저장 서비스 백 엔드 정책을 만듭니다.

 1. 선택 하 고 hello 편집 **정책 인바운드** hello에 대 한 `Values` hello 편집 아이콘을 클릭 하 고 다음을 선택 하 여 작업 **코드 보기**합니다.
 2. Hello 정책 코드 편집기에서 추가 된 `set-backend-service` 아래에서 다음과 같이 정책 인바운드 정책과 hello 클릭 **저장** 단추:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

모든 서비스 패브릭 백 엔드 정책 특성 집합에 대 한 참조 toohello [API 관리 백 엔드 설명서](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Hello API tooa 제품을 추가 합니다. 

Hello API를 호출할 수 있습니다, 전에 tooa 제품 toousers 액세스 권한을 부여할 수 있는 추가 되어야 합니다. 

 1. API 관리 서비스 hello 선택 **제품-미리 보기**합니다.
 2. 기본적으로 API Management는 스타터와 무제한의 두 가지 제품을 제공합니다. Hello 무제한 제품을 선택 합니다.
 3. API를 선택합니다.
 4. Hello 클릭 **+ 추가** 단추입니다.
 5. 선택 hello `Service Fabric App` API hello 누르고 hello 이전 단계에서 만든 **선택** 단추입니다.

### <a name="test-it"></a>테스트

이제 hello Azure 포털에서 직접 요청 tooyour 백 엔드 서비스 관리 API를 통해 서비스 패브릭에서 보내는 시도할 수 있습니다.

 1. API 관리 서비스 hello 선택 **API-미리 보기**합니다.
 2. Hello에 `Service Fabric App` hello 이전 단계에서 만든 API 선택 hello **테스트** 탭 합니다.
 3. Hello 클릭 **보낼** 단추 toosend 테스트 요청 toohello 백 엔드 서비스입니다.

## <a name="next-steps"></a>다음 단계

이제 기본 설정의 Service Fabric 및 API Management가 있습니다.

이 자습서를 신속 하 게 설정 하 여 서비스 패브릭 클러스터 tooget에 대 한 기본 인증서 기반 사용자 인증을 사용 합니다. Service Fabric 클러스터에 대한 보다 고급의 사용자 인증은 [Azure Active Directory 인증](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication)과 함께 사용하는 것이 좋습니다. 

그런 다음, [만들고 Azure API 관리에서 고급 제품 설정을 구성](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare 현실 세계 트래픽에 대 한 응용 프로그램입니다.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
