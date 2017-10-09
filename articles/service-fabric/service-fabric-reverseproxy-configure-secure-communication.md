---
title: "서비스 패브릭 aaaAzure 역방향 프록시 보안 통신 | Microsoft Docs"
description: "역방향 프록시 tooenable 보안 종단 간 통신을 구성 합니다."
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
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>보안 서비스 tooa hello 역방향 프록시를 사용 하 여 연결

이 문서에서는 tooestablish hello 역방향 프록시 및 서비스를 최종 tooend 보안 채널을 사용할 수 있게 간의 연결을 보호 하는 방법을 설명 합니다.

Toosecure 서비스를 연결 하면 역방향 프록시 구성된 toolisten HTTPS에는 하는 경우에 지원 됩니다. Hello 문서의 나머지 부분에서는 hello 좋다고 가정 합니다.
너무 참조[역방향 프록시 Azure 서비스 패브릭에서](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello 서비스 패브릭에서 역방향 프록시입니다.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>역방향 프록시 hello와 서비스 간의 보안 연결 설정 

### <a name="reverse-proxy-authenticating-tooservices"></a>역방향 프록시 tooservices 인증:
hello 역방향 프록시 구분 정보를 지정 된 해당 인증서를 사용 하 여 tooservices ***reverseProxyCertificate*** hello에 대 한 속성 **클러스터** [리소스 유형 섹션](../azure-resource-manager/resource-group-authoring-templates.md). 서비스는 hello 역방향 프록시에서 제공 하는 hello 논리 tooverify hello 인증서를 구현할 수 있습니다. hello 서비스는 hello 구성 패키지의 구성 설정으로 허용 하는 hello 클라이언트 인증서 세부 정보를 지정할 수 있습니다. 이 런타임에 읽을 수 및 hello 역방향 프록시를 제공한 toovalidate hello 인증서를 사용 합니다. 너무 참조[매개 변수를 응용 프로그램 관리](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello 구성 설정입니다. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>역방향 프록시 hello 서비스에서 제공 하는 hello 인증서를 통해 hello 서비스 id를 확인 하는 중:
hello 다음 옵션 중 하나 tooperform 서버 인증서 유효성 검사의 hello 서비스에서 제공 하는 hello 인증서를 역방향 프록시 지원: None, ServiceCommonNameAndIssuer, 및 ServiceCertificateThumbprints 합니다.
이러한 세 가지 옵션 중 하나는 tooselect 지정 hello **ApplicationCertificateValidationPolicy** 에서 ApplicationGateway/Http 요소의 hello 매개 변수 섹션에서 [fabricSettings](service-fabric-cluster-fabric-settings.md)합니다.

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

이러한 각 옵션에 대 한 추가 구성에 대 한 내용은 toohello 다음 섹션을 참조 하십시오.

### <a name="service-certificate-validation-options"></a>서비스 인증서 유효성 검사 옵션 

- **None**: 역방향 프록시 hello 프록시 서비스 인증서의 확인을 건너뛰고 hello 보안 연결을 설정 합니다. 이 hello 기본 동작입니다.
Hello 지정 **ApplicationCertificateValidationPolicy** 값을 가진 **None** ApplicationGateway/Http 요소의 hello 매개 변수 섹션에서.

- **ServiceCommonNameAndIssuer**: 역방향 프록시 hello 인증서 hello 서비스 인증서의 일반 이름 및 즉시 발급자 지문에 따라 제시 확인: hello 지정 **ApplicationCertificateValidationPolicy**  값을 가진 **ServiceCommonNameAndIssuer** ApplicationGateway/Http 요소의 hello 매개 변수 섹션에서.

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

일반 서비스 이름 및 발급자 지문 toospecify hello 목록을 추가 **ApplicationGateway/Http/ServiceCommonNameAndIssuer** fabricSettings, 아래와 같이 요소입니다. Hello 매개 변수 배열 요소에 여러 인증서 일반 이름 및 발급자 지문 쌍을 추가할 수 있습니다. 

Toopresents 일반적인 인 인증서를 연결 하는 hello 끝점에 대 한 역방향 프록시 이름 및 발급자 지문 중 하 나와 일치 여기에서 지정 된 hello 값, SSL 채널이 설정 합니다. 실패 toomatch hello 인증서 세부 정보에 역방향 프록시 502 (잘못 된 게이트웨이) 상태 코드와 함께 hello 클라이언트의 요청에 실패 합니다. HTTP 상태 줄 hello hello 구 "잘못 된 SSL 인증서"도 포함 됩니다. 

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


- **ServiceCertificateThumbprints**: 역방향 프록시는 해당 지문에 기반한 hello 프록시 서비스 인증서를 확인 합니다. 선택할 수 있습니다 toogo이이 경로 hello 서비스는 자체 서명 된 인증서로 구성 된 경우: hello 지정 **ApplicationCertificateValidationPolicy** 값을 가진 **ServiceCertificateThumbprints**ApplicationGateway/Http 요소의 hello 매개 변수 섹션에서.

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

와 hello 지문을 지정는 **ServiceCertificateThumbprints** ApplicationGateway/Http 요소의 매개 변수 섹션 아래 항목을 입력 합니다. 아래와 같이 여러 지문이 hello 값 필드에 쉼표로 구분 된 목록으로 지정할 수 있습니다.

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

Hello 서버 인증서의 지문 안녕하세요가 구성 항목에 표시 되 면 역방향 프록시 hello SSL 연결에 성공 합니다. 그렇지 않으면 hello 연결을 종료 하 고 실패 hello 502 (잘못 된 게이트웨이)와 클라이언트의 요청 합니다. HTTP 상태 줄 hello hello 구 "잘못 된 SSL 인증서"도 포함 됩니다.

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>서비스가 보안 끝점과 비보안 끝점을 노출할 때 끝점 선택 논리
Service Fabric은 서비스에 대한 다중 끝점 구성을 지원합니다. 
          [서비스 매니페스트에서 리소스 지정](service-fabric-service-manifest-resources.md)을 참조하세요.

역방향 프록시 hello에 따라 hello 끝점 tooforward hello 요청 중 하나를 선택 합니다. **ListenerName** 쿼리 매개 변수입니다. 지정 하지 않으면 모든 끝점 hello 끝점 목록에서 선택할 수 있습니다. 이제 HTTP 또는 HTTPS 끝점을 선택할 수 있습니다. 있을 수 있습니다 시나리오/요구 사항 "보안 유일한 모드 에서는" hello 역방향 프록시 toooperate 저장할 즉, hello 보안 역방향 프록시 tooforward 요청 toounsecured 끝점 되기를 원하지 않습니다. Hello를 지정 하 여 이렇게 할 **SecureOnlyMode** 값을 가진 구성 항목 **true** ApplicationGateway/Http 요소의 hello 매개 변수 섹션에서.   

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
> 작업할 경우 **SecureOnlyMode**클라이언트에서 지정 하는 경우, 한 **ListenerName** tooan HTTP(unsecured) 끝점, 해당 역방향 프록시 404 (찾을 수 없음) HTTP 상태 코드로 hello 요청에 실패 합니다.

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Hello 역방향 프록시를 통해 클라이언트 인증서 인증을 설정
SSL 종료 hello 역방향 프록시에서 발생 하 고 모든 hello 클라이언트 인증서 데이터 손실 됩니다. Hello 서비스 tooperform 클라이언트 인증서 인증에 대 한 hello 설정 **ForwardClientCertificate** ApplicationGateway/Http 요소의 hello 매개 변수 섹션에서 설정 합니다.

1. 때 **ForwardClientCertificate** 너무 설정**false**역방향 프록시 요청 하지 것입니다 hello 클라이언트 인증서는 SSL 핸드셰이크 중 hello 클라이언트와 함께 합니다.
이 hello 기본 동작입니다.

2. 때 **ForwardClientCertificate** 너무 설정**true**, hello 클라이언트와의 SSL 핸드셰이크 중 hello 클라이언트의 인증서에 대 한 프록시 요청을 반전 합니다.
그런 다음 보냅니다 hello 클라이언트 인증서 데이터 라는 사용자 지정 HTTP 헤더를 **X 클라이언트 인증서**합니다. hello 헤더 값이 hello hello 클라이언트 인증서의 base64 인코딩 PEM 형식 문자열입니다. hello 서비스 수 성공/실패 적절 한 상태 코드를 사용 하 여 hello 요청 hello 인증서 데이터를 검사 한 후 합니다.
Hello 클라이언트 인증서를 제공 하지 않으면 역방향 프록시 헤더가 비어 있으면를 전달 하 고 hello 서비스 핸들 hello 대/소문자를 사용 합니다.

> 역방향 프록시는 단지 전달자일 뿐입니다. Hello 클라이언트 인증서의 유효성 검사를 수행 하지 않습니다.


## <a name="next-steps"></a>다음 단계
* 너무 참조[역방향 프록시 tooconnect toosecure 서비스 구성](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) Azure 리소스 관리자에 대 한 서식 파일을 tooconfigure 보안 역방향 프록시 hello 다양 한 서비스 인증서 유효성 검사 옵션으로 샘플링 합니다.
* [GitHub의 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)에서 서비스 간 HTTP 통신의 예제를 참조하세요.
* [Reliable Services 원격을 사용하여 원격 프로시저 호출](service-fabric-reliable-services-communication-remoting.md)
* [Reliable Services에서 OWIN을 사용하는 Web API](service-fabric-reliable-services-communication-webapi.md)
* [클러스터 인증서 관리](service-fabric-cluster-security-update-certs-azure.md)
