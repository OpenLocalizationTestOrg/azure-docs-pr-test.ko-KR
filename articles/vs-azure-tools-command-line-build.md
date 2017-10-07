---
title: "Azure에 대 한 빌드 aaaCommand 줄 | Microsoft Docs"
description: "Azure에 대한 명령줄 빌드"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Hello 명령줄에서 Azure 프로젝트 빌드
Microsoft Build Engine (MSBuild) hello를 사용 하 여 Visual Studio가 설치 되지 않은 빌드 랩 환경에서 제품을 빌드할 수 있습니다. MSBuild는 Microsoft에서 확장 가능하고 완전히 지원되는 프로젝트 파일에 대한 XML 형식을 사용합니다. Hello MSBuild 파일 형식을 사용 하 여 설명할 수 있습니다 항목 하나 이상의 플랫폼 및 구성에 대해 작성 합니다.

이 항목에서는 그 방법을 설명 하 고 hello 명령줄에서 MSBuild를 실행할 수도 있습니다. Hello 명령줄에서 속성을 설정 하면 프로젝트의 특정 구성을 빌드할 수 있습니다. 마찬가지로, MSBuild에서 작성 하는 hello 대상을 정의할 수 있습니다. 명령줄 매개 변수 및 MSBuild에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)를 참조하세요.

## <a name="msbuild-parameters"></a>MSBuild 매개 변수
hello 가장 간단한 방법은 toocreate 패키지는 hello로 MSBuild toorun `/t:Publish` 옵션입니다. 기본적으로이 명령은 디렉터리에에서 만듭니다 hello 프로젝트에 대 한 관계 toohello 루트 폴더와 같은 `<ProjectDirectory>\bin\Configuration\app.publish\`합니다. Azure 프로젝트를 빌드할 때 두 파일이 생성 됩니다: 패키지 파일 자체와 해당 구성 파일 hello hello:

* 패키지 파일(`project.cspkg`)
* 구성 파일(`ServiceConfiguration.TargetProfile.cscfg`)

기본적으로 각 Azure 프로젝트에는 로컬(디버깅) 빌드용 서비스 구성 파일 하나와 클라우드(스테이징 또는 프로덕션) 빌드용 서비스 구성 파일 하나가 포함되지만 필요에 따라 서비스 구성 파일을 추가하거나 제거할 수 있습니다. Visual Studio 내에서 패키지를 빌드할 때 hello 패키지와 함께 어떤 서비스 구성 파일 tooinclude를 묻습니다. MSBuild를 사용 하 여 패키지를 빌드할 때 hello 로컬 서비스 구성 파일은 기본적으로 포함 됩니다. tooinclude 서로 다른 서비스 구성 파일을 집합 hello `TargetProfile` hello MSBuild 명령의 속성 (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

패키지 및 구성 파일을 hello를 사용 하 여 hello 경로 설정 hello에 대 한 다른 디렉터리에 저장 된 toouse 하려는 경우 `/p:PublishDir=Directory\` hello 후행 백슬래시 구분 기호를 포함 하 여 옵션입니다.

## <a name="next-steps"></a>다음 단계
Hello 패키지를 만든 후 tooAzure 배포할 수 있습니다. 설명 하는 자습서에 대 한 tooautomate 처리 하는 참조 [Azure에서 클라우드 서비스에 대 한 지속적인 업데이트](./cloud-services/cloud-services-dotnet-continuous-delivery.md)합니다.

