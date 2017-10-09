---
title: "Visual Studio에서 Azure 클라우드 서비스 프로젝트 aaaConfigure | Microsoft Docs"
description: "어떻게 tooconfigure Azure 클라우드 해당 프로젝트에 대 한 요구 사항에 따라 Visual Studio에서 서비스 프로젝트에 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Visual Studio에서 Azure 클라우드 서비스 프로젝트 구성
프로젝트 요구 사항에 따라 Azure 클라우드 서비스 프로젝트를 구성할 수 있습니다. 다음 범주 hello에 대 한 hello 프로젝트에 대 한 속성을 설정할 수 있습니다.

- **클라우드 서비스 tooAzure 게시** -기존 클라우드 서비스 배포 tooAzure 실수로 삭제 되지 않도록 하는 속성 toomake를 설정할 수 있습니다.
- **Hello 로컬 컴퓨터에서 클라우드 서비스 실행 또는 디버그할** -서비스 구성 toouse를 선택할 수 있으며 toostart hello Azure 저장소 에뮬레이터를 표시할지 여부를 지정 합니다.
- **만들 때 클라우드 서비스 패키지의 유효성을 검사** -아무 문제 없이 배포 해당 hello 클라우드 서비스 패키지를 확인할 수 있도록 모든 경고를 오류로 tootreat를 결정할 수 있습니다. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>단계 tooconfigure Azure 클라우드 서비스 프로젝트
1. Visual Studio에서 클라우드 서비스 프로젝트 열기 또는 만들기

1. **솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.
   
1. Hello 프로젝트의 속성 페이지에서 선택 hello **개발** 탭 합니다.

    ![프로젝트 속성 메뉴](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. 설정 **기존 배포를 삭제 하기 전에 확인** 너무**True**합니다. 이 설정을 통해 Azure의 기존 배포가 실수로 삭제 하지 않으면 tooensure

1. 원하는 선택 hello **서비스 구성** tooindicate 서비스 구성을 원하는 toouse 실행 하거나 클라우드 서비스를 로컬로 디버깅할 때. 방법에 대 한 자세한 내용은 toomodify는 역할에 대 한 서비스 구성을 참조 [어떻게 Azure에 대 한 tooconfigure hello 역할 클라우드 Visual Studio와 함께 서비스](./vs-azure-tools-configure-roles-for-cloud-service.md)합니다.

1. 설정 **Azure 저장소 에뮬레이터 시작** 너무**True** toostart hello Azure 저장소 에뮬레이터를 실행 하거나 클라우드 서비스를 로컬로 디버깅할 때.

1. 설정 **경고를 오류로 처리** 너무**True** toomake 있는지 패키지 유효성 검사 오류가 있는 경우 게시할 수 없습니다.

1. 설정 **웹 프로젝트 포트 사용** 너무**True** IIS Express에서 로컬로 시작할 때마다 웹 역할이 동일한 포트 각각 hello를 사용 하는지 toomake 합니다.

1. Visual Studio 도구 모음 hello **저장**합니다.

## <a name="next-steps"></a>다음 단계
- [여러 서비스 구성을 사용하여 Azure 프로젝트 구성](vs-azure-tools-multiple-services-project-configurations.md)

