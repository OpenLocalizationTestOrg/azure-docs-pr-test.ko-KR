---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: "자세한 내용은 방법 toodeploy 웹 응용 프로그램 tooa 가상 컴퓨터. 이 스크립트는 없는 경우 Azure 구독에서 hello 필요한 리소스를 만듭니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (Windows PowerShell 스크립트)
웹 응용 프로그램 tooa 가상 컴퓨터를 배포합니다. hello 스크립트 없는 경우 Azure 구독에 필요한 hello 리소스를 만듭니다.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>구성
hello 경로 toohello는 JSON 구성 파일 hello 배포의 hello 세부 사항을 설명 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

### <a name="subscriptionname"></a>SubscriptionName
hello 이름 hello toocreate hello 가상 컴퓨터를 원하는 Azure 구독.

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position |named |
| 기본값 |Hello 구독 파일의 첫 번째 구독 hello를 사용 하 여 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
hello 경로 toohello 웹 배포 패키지 toopublish toohello 가상 컴퓨터가 있습니다. Visual Studio에서 hello 웹 게시 마법사를 사용 하 여이 패키지를 만들 수 있습니다. [방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx)를 참조하세요.

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
True 인 경우에 신뢰할 수 있는 루트 인증 기관에서 서명 하지 않은 인증서 hello 사용할을 수 있습니다.

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position |named |
| 기본값 |false |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

### <a name="vmpassword"></a>VMPassword
hello 가상 컴퓨터 계정에 대 한 hello 자격 증명입니다. 예: VMPassword @{Name = "admin"; 암호 = "password"}

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
Azure의 hello SQL 데이터베이스에 대 한 hello 자격 증명입니다. 예: DatabaseServerPassword @{Name = "admin"; 암호 = "password"}

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
True 이면 hello 스크립트 toohello에서 메시지를 인쇄 출력 스트림에입니다.

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position |named |
| 기본값 |false |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

## <a name="remarks"></a>설명
자세한 설명은 toouse hello 스크립트 toocreate 개발 및 테스트 환경을 참조 하는 방법에 대 한 [Windows PowerShell 스크립트를 사용 하 여 tooPublish tooDev 및 시험 환경](vs-azure-tools-publishing-using-powershell-scripts.md)합니다.

hello JSON 구성 파일의 배포 toobe 이란 hello 세부 정보를 지정 합니다. Hello 이름, 선호도 그룹, VHD 이미지 및 hello 가상 컴퓨터의 크기와 같은 hello 프로젝트를 만들 때 지정한 hello 정보가 포함 됩니다. 도 있는 경우 hello 끝점 hello 데이터베이스 tooprovision hello 가상 컴퓨터를 포함 하 고 웹 배포 매개 변수입니다. hello 코드 다음 JSON 구성 파일을 예를 보여 줍니다.

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

프로 비전 된 hello JSON 구성 파일 toochange를 편집할 수 있습니다. 가상 컴퓨터 및 클라우드 서비스 필요 하지만 hello 데이터베이스 섹션은 선택 사항입니다.

