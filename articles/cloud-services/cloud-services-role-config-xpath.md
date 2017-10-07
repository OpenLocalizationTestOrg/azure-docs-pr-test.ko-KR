---
title: "aaaCloud 서비스 역할 구성 XPath 치트 시트 | Microsoft Docs"
description: "안녕 다양 한 XPath 설정이 환경 변수로 hello 클라우드 서비스 역할 구성 tooexpose 설정에서 사용할 수 있습니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>XPath를 사용하여 역할 구성 설정을 환경 변수로 노출
Hello 클라우드 서비스 작업자 또는 웹 역할 서비스 정의 파일에서 환경 변수로 런타임 구성 값을 노출할 수 있습니다. 다음 XPath 값에는 hello (tooAPI 값에 해당)는 사용할 수 있습니다.

이러한 XPath 값은 hello를 통해 사용할 수 또한 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) 라이브러리입니다. 

## <a name="app-running-in-emulator"></a>앱이 에뮬레이터에서 실행 중임
Hello 이러한 앱 hello 에뮬레이터에서 실행 되 고 나타냅니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| 코드 |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>배포 ID
Hello 인스턴스에 대 한 hello 배포 ID를 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| 코드 |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>역할 ID
Hello hello 인스턴스의 현재 역할 ID를 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| 코드 |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>도메인 업데이트
Hello 인스턴스의 hello 업데이트 도메인을 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| 코드 |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>장애 도메인
Hello 인스턴스의 hello 장애 도메인을 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| 코드 |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>역할 이름
Hello 인스턴스의 hello 역할 이름을 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| 코드 |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>구성 설정
Hello 검색 hello 값이 구성 설정을 지정 합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| 코드 |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>로컬 저장소 경로
Hello 인스턴스에 대 한 hello 로컬 저장소 경로 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| 코드 |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>로컬 저장소 크기
Hello hello 인스턴스에 대 한 로컬 저장소의 hello 크기를 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| 코드 |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>끝점 프로토콜
Hello 인스턴스에 대 한 hello 끝점 프로토콜을 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| 코드 |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>끝점 IP
가져옵니다 hello 끝점의 IP 주소를 지정 합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| 코드 |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>끝점 포트
Hello 인스턴스에 대 한 hello 끝점 포트를 검색합니다.

| 형식 | 예 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| 코드 |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>예제
시작 작업 라는 환경 변수를 만드는 작업자 역할의 예로 `TestIsEmulated` toohello 설정 [ @emulated xpath 값](#app-running-in-emulator)합니다. 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) 파일입니다.

[ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) 패키지를 만듭니다.

역할에 대해 [원격 데스크톱](cloud-services-role-enable-remote-desktop.md) 을 사용하도록 설정합니다.

