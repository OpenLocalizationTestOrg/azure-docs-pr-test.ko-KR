---
title: "aaaPublish-WebApplicationWebSite (Windows PowerShell 스크립트) | Microsoft Docs"
description: "웹 toopublish tooan Azure 웹 사이트 프로젝트 하는 방법에 대해 알아봅니다. 이 스크립트는 없는 경우 Azure 구독에서 hello 필요한 리소스를 만듭니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (Windows PowerShell 스크립트)
## <a name="syntax"></a>구문
웹 프로젝트 tooan Azure 웹 사이트를 게시합니다. hello 스크립트 없는 경우 Azure 구독에 필요한 hello 리소스를 만듭니다.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>구성
hello 경로 toohello는 JSON 구성 파일 hello 배포의 hello 세부 사항을 설명 합니다.

| 매개 변수 | 기본값 |
| --- | --- |
| Aliases |없음 |
| Required? |true |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

## <a name="subscriptionname"></a>SubscriptionName
hello toocreate hello 웹 사이트에 원하는 구독을 Azure의 hello 이름입니다.

| 매개 변수 | 기본값 |
| --- | --- |
| Aliases |없음 |
| Required? |false |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
hello 경로 toohello 웹 배포 패키지 toopublish toohello 웹 사이트입니다. Visual Studio에서 hello 웹 게시 마법사를 사용 하 여이 패키지를 만들 수 있습니다. 자세한 내용은 [Azure 클라우드 서비스 및 ASP.NET으로 시작하기](http://go.microsoft.com/fwlink/p/?LinkID=623089)를 참조하세요.

| 매개 변수 | 기본값 |
| --- | --- |
| Aliases |없음 |
| Required? |false |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
hello 사용자 이름 및 Azure의 hello SQL 데이터베이스에 대 한 암호입니다.

| 매개 변수 | 기본값 |
| --- | --- |
| Aliases |없음 |
| Required? |false |
| Position |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
True 이면 hello 스크립트 toohello에서 메시지를 인쇄 출력 스트림에입니다.

| 매개 변수 | 기본값 |
| --- | --- |
| Aliases |없음 |
| Required? |false |
| Position |named |
| 기본값 |false |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

## <a name="remarks"></a>설명
자세한 설명은 toouse hello 스크립트 toocreate 개발 및 테스트 환경을 참조 하는 방법에 대 한 [Windows PowerShell 스크립트를 사용 하 여 tooPublish tooDev 및 시험 환경](vs-azure-tools-publishing-using-powershell-scripts.md)합니다.

hello JSON 구성 파일의 배포 toobe 이란 hello 세부 정보를 지정 합니다. Hello 이름과 hello 웹 사이트에 대 한 사용자 이름 등의 hello 프로젝트를 만들 때 지정한 hello 정보가 포함 됩니다. 있는 경우 hello 데이터베이스 tooprovision도를 있습니다. hello 코드 다음 JSON 구성 파일을 예를 보여 줍니다.

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

배포 된 hello JSON 구성 파일 toochange를 편집할 수 있습니다. 웹 사이트 섹션은 필수 이지만 hello 데이터베이스 섹션은 선택 사항입니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 [Publish-WebApplicationVM(Windows PowerShell 스크립트)](vs-azure-tools-publish-webapplicationvm.md)

