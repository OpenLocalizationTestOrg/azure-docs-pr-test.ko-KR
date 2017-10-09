---
title: "Visual Studio에서 Azure 클라우드 서비스 프로젝트 aaaCreating | Microsoft Docs"
description: "이제 toocreate Visual Studio에서 Azure 클라우드 서비스 프로젝트에 알아봅니다"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Visual Studio에서 Azure 클라우드 서비스 프로젝트 만들기
Azure Tools for Visual Studio hello Azure 클라우드 서비스를 만들 수 있는 프로젝트 템플릿을 제공 합니다. Visual Studio tooconfigure hello 프로젝트를 만든 후 하면, 디버깅 및 hello 클라우드 서비스 tooAzure를 배포 합니다.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>단계 toocreate Visual Studio에서 Azure 클라우드 서비스 프로젝트
이 섹션에서는 하나 이상의 웹 역할을 사용하여 Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만드는 과정을 안내합니다.  

1. 관리자 권한으로 Visual Studio를 시작합니다.

1. Hello 주 메뉴에서 선택 **파일** > **새로** > **프로젝트**합니다.

1. 선택 **클라우드** hello Visual C# 또는 Visual Basic에서 프로젝트 템플릿 노드에서 선택한 **Azure 클라우드 서비스** hello 템플릿 목록에서.

    ![새 Azure 클라우드 서비스](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Hello toouse toodevelop 프로젝트를 원하는.NET Framework의 버전을 지정 합니다.

1. 이름 및 프로젝트에 대 한 위치와 hello 솔루션에 대 한 이름을 입력 합니다. 

1. **확인**을 선택합니다.

1. Hello에 **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 선택 hello 역할 tooadd, 원하고 hello 오른쪽 화살표 단추 tooadd 선택으로 tooyour 솔루션입니다.

    ![새 Azure 클라우드 서비스 역할 선택](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. hover hello hello 역할에서 역할을 추가한 toorename **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 hello 상황에 맞는 메뉴에서 **이름 바꾸기**합니다. 솔루션 내에서 역할 이름을 변경할 수 있습니다 (hello에 **솔루션 탐색기**)에 추가 된 후입니다.

    ![Azure 클라우드 서비스 역할 이름 바꾸기](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Visual Studio Azure 프로젝트 hello hello 솔루션에 연결 toohello 역할 프로젝트에 있습니다. hello 프로젝트도 hello *서비스 정의 파일* 및 *서비스 구성 파일*:

- **서비스 정의 파일** -은 필요한 역할을 포함 하는 응용 프로그램, 끝점 및 가상 컴퓨터 크기에 대 한 hello 런타임 설정을 정의 합니다. 
- **서비스 구성 파일** -역할의 인스턴스 개수 실행 되 고 hello 역할에 대해 정의 된 hello 설정의 값을 구성 합니다. 

이러한 파일에 대 한 자세한 내용은 참조 [Visual Studio에서 Azure 클라우드 서비스에 대 한 hello 역할 구성](vs-azure-tools-configure-roles-for-cloud-service.md)합니다.

## <a name="next-steps"></a>다음 단계
- [Visual Studio에서 Azure 클라우드 서비스 프로젝트의 역할 관리](./vs-azure-tools-cloud-service-project-managing-roles.md)
