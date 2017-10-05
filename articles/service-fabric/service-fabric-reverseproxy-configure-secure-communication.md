---
title: "Azure Service Fabric 역방향 프록시 보안 통신 | Microsoft Docs"
description: "안전한 종단 간 통신을 사용하려면 역방향 프록시를 구성합니다."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="3d625-103">역방향 프록시를 사용하여 보안 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="3d625-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="3d625-104">이 문서에서는 역방향 프록시와 서비스 간에 보안 연결을 설정하여 종단 간 보안 채널을 사용하도록 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="3d625-105">보안 서비스에 연결하는 것은 역방향 프록시가 HTTPS에서 수신하도록 구성된 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="3d625-106">이 문서의 나머지 부분에서는 이 구성을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="3d625-107">Service Fabric에서 역방향 프록시를 구성하려면 [Azure Service Fabric의 역방향 프록시](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d625-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="3d625-108">역방향 프록시와 서비스 간의 안전한 연결 설정</span><span class="sxs-lookup"><span data-stu-id="3d625-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="3d625-109">서비스를 인증하는 역방향 프록시:</span><span class="sxs-lookup"><span data-stu-id="3d625-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="3d625-110">역방향 프록시는 해당 인증서를 사용하여 자체적으로 서비스를 식별하며 **클러스터** [리소스 종류 섹션](../azure-resource-manager/resource-group-authoring-templates.md)의 ***reverseProxyCertificate*** 속성에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="3d625-111">서비스는 역방향 프록시에서 제공한 인증서를 확인하기 위한 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="3d625-112">이 서비스는 허용된 클라이언트 인증서 세부 정보를 구성 패키지의 구성 설정으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="3d625-113">이는 런타임 시 읽을 수 있으며 역방향 프록시에서 제공한 인증서의 유효성을 검사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="3d625-114">구성 설정을 추가하려면 [응용 프로그램 매개 변수 관리](service-fabric-manage-multiple-environment-app-configuration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d625-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="3d625-115">서비스에서 제공한 인증서를 통해 서비스의 ID를 확인하는 역방향 프록시:</span><span class="sxs-lookup"><span data-stu-id="3d625-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="3d625-116">역방향 프록시는 서비스에서 제공하는 인증서의 서버 인증서 유효성 검사를 수행하기 위해 None, ServiceCommonNameAndIssuer 및 ServiceCertificateThumbprints 옵션 중 하나를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="3d625-117">이러한 세 가지 옵션 중 하나를 선택하려면 [fabricSettings](service-fabric-cluster-fabric-settings.md) 아래에 있는 ApplicationGateway/Http 요소의 parameters 섹션에서 **ApplicationCertificateValidationPolicy**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="3d625-118">이러한 각 옵션의 추가 구성에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d625-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="3d625-119">서비스 인증서 유효성 검사 옵션</span><span class="sxs-lookup"><span data-stu-id="3d625-119">Service certificate validation options</span></span> 

- <span data-ttu-id="3d625-120">**None**: 역방향 프록시가 프록시 설정된 서비스 인증서의 확인을 건너뛰고 보안 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="3d625-121">기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-121">This is the default behavior.</span></span>
<span data-ttu-id="3d625-122">ApplicationGateway/Http 요소의 parameters 섹션에서 값이 **None**인 **ApplicationCertificateValidationPolicy**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="3d625-123">**ServiceCommonNameAndIssuer**: 역방향 프록시가 인증서의 일반 이름과 직접 발급자의 지문을 기반으로 서비스에서 제공하는 인증서를 확인합니다. ApplicationGateway/Http 요소의 parameters 섹션에서 값이 **ServiceCommonNameAndIssuer**인 **ApplicationCertificateValidationPolicy**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="3d625-124">서비스 일반 이름 및 발급자 지문 목록을 지정하려면 아래 표시된 것처럼 fabricSettings 아래에 **ApplicationGateway/Http/ServiceCommonNameAndIssuer** 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="3d625-125">여러 인증서 일반 이름 및 발급자 지문 쌍을 매개 변수 배열 요소에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="3d625-126">끝점 역방향 프록시가 연결되어 일반 이름과 발급자 지문이 여기에 지정된 값과 일치하는 인증서가 제시되면 SSL 채널이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="3d625-127">인증서 세부 정보가 일치하지 않으면 502(잘못된 게이트웨이) 상태 코드와 함께 역방향 프록시가 클라이언트 요청에 대해 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="3d625-128">HTTP 상태 줄에 "잘못된 SSL 인증서"라는 구문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- <span data-ttu-id="3d625-129">**ServiceCertificateThumbprints**: 역방향 프록시가 지문을 기반으로 프록시 설정된 서비스 인증서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="3d625-130">서비스가 자체 서명된 인증서로 구성될 때 이 경로를 선택할 수 있습니다. ApplicationGateway/Http 요소의 parameters 섹션에서 값이 **ServiceCertificateThumbprints**인 **ApplicationCertificateValidationPolicy**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="3d625-131">또한 ApplicationGateway/Http 요소의 parameters 섹션에서 **ServiceCertificateThumbprints** 항목이 있는 지문을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="3d625-132">값 필드에서 여러 개의 지문을 쉼표로 구분된 목록으로 지정할 수 있습니다(아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="3d625-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="3d625-133">이 구성 항목 목록에 서버 인증서의 지문이 있으면 역방향 프록시가 SSL 연결에 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="3d625-134">그렇지 않으면 연결을 종료하고 502(잘못된 게이트웨이)와 함께 클라이언트의 요청에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="3d625-135">HTTP 상태 줄에 "잘못된 SSL 인증서"라는 구문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="3d625-136">서비스가 보안 끝점과 비보안 끝점을 노출할 때 끝점 선택 논리</span><span class="sxs-lookup"><span data-stu-id="3d625-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="3d625-137">Service Fabric은 서비스에 대한 다중 끝점 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="3d625-138">
          [서비스 매니페스트에서 리소스 지정](service-fabric-service-manifest-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d625-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="3d625-139">역방향 프록시는 **ListenerName** 쿼리 매개 변수를 기반으로 요청을 전달할 끝점 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="3d625-140">이 값이 지정되지 않은 경우 끝점 목록에서 아무 끝점이나 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="3d625-141">이제 HTTP 또는 HTTPS 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="3d625-142">역방향 프록시가 “보안 전용 모드”로 작동하게 하려는 시나리오/요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="3d625-143">즉, 보안 역방향 프록시가 비보안 끝점으로 요청을 전달하지 않도록 하고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="3d625-144">이렇게 하려면 ApplicationGateway/Http 요소의 parameters 섹션에서 값이 **true**인 **SecureOnlyMode** 구성 항목을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> <span data-ttu-id="3d625-145">**SecureOnlyMode**에서 작동할 때 클라이언트가 HTTP(비보안) 끝점에 해당하는 **ListenerName**을 지정한 경우 역방향 프록시는 404(찾을 수 없음) HTTP 상태 코드와 함께 요청에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="3d625-146">역방향 프록시를 통한 클라이언트 인증서 인증 설정</span><span class="sxs-lookup"><span data-stu-id="3d625-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="3d625-147">SSL 종료는 역방향 프록시에서 발생하며 모든 클라이언트 인증서 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="3d625-148">서비스가 클라이언트 인증서 인증을 수행하려면 ApplicationGateway/Http 요소의 parameters 섹션에서 **ForwardClientCertificate** 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="3d625-149">**ForwardClientCertificate**가 **false**로 설정되면 역방향 프록시가 클라이언트와의 SSL 핸드셰이크 중 클라이언트 인증서를 요청하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="3d625-150">기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-150">This is the default behavior.</span></span>

2. <span data-ttu-id="3d625-151">**ForwardClientCertificate**가 **true**로 설정되면 역방향 프록시가 클라이언트와의 SSL 핸드셰이크 중 클라이언트 인증서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="3d625-152">그런 다음 **X-Client-Certificate**라는 사용자 지정 HTTP 헤더에 클라이언트 인증서 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="3d625-153">헤더 값은 클라이언트 인증서의 base64로 인코딩된 PEM 형식의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="3d625-154">서비스는 인증서 데이터를 검사한 후 요청에 성공하거나/적절한 상태 코드와 함께 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="3d625-155">클라이언트가 인증서를 제시하지 않으면 역방향 프록시는 빈 헤더를 전달하고 서비스에서 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="3d625-156">역방향 프록시는 단지 전달자일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="3d625-157">클라이언트 인증서의 유효성 검사를 수행하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d625-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3d625-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d625-158">Next steps</span></span>
* <span data-ttu-id="3d625-159">다른 서비스 인증서 유효성 검사 옵션을 사용하여 보안 역방향 프록시를 구성하려면 [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)(보안 서비스에 연결하도록 역방향 프록시 구성)에서 Azure Resource Manager 템플릿 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d625-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="3d625-160">[GitHub의 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)에서 서비스 간 HTTP 통신의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d625-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="3d625-161">Reliable Services 원격을 사용하여 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="3d625-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="3d625-162">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="3d625-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="3d625-163">클러스터 인증서 관리</span><span class="sxs-lookup"><span data-stu-id="3d625-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
