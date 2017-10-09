---
title: "aaaHow toomanage 구성 및 프로필 서비스 | Microsoft Docs"
description: "자세한 방법을 서비스 구성 및 프로필 구성 파일이 있는 toowork | hello 배포 환경에 대 한 설정을 저장 하 고 클라우드 서비스에 대 한 설정을 게시 합니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>구성 및 프로필 toomanage 서비스 하는 방법
## <a name="overview"></a>개요
클라우드 서비스를 게시하면 Visual Studio는 두 종류의 구성 파일, 서비스 구성 및 프로필에 구성 정보를 저장합니다. 서비스 구성 (파일.cscfg)에 Azure 클라우드 서비스에 대 한 hello 배포 환경에 대 한 설정을 저장 합니다. Azure는 클라우드 서비스를 관리하는 경우 이 구성 파일을 사용합니다. Hello 반면에, 게시 설정이 클라우드 서비스에 대 한 프로필 (파일.azurePubxml) 저장 합니다. 이러한 설정에는 hello를 사용 하면 선택한 항목에 대 한 기록을 게시 마법사, 및 Visual Studio에서 로컬로 사용 됩니다. 이 항목에서는 설명 방법을 두 가지 유형의 구성 파일을 toowork 합니다.

## <a name="service-configurations"></a>서비스 구성
각 배포 환경에 대 한 여러 서비스 구성을 toouse를 만들 수 있습니다. 예를 들어 hello toorun를 사용 하 고 프로덕션 환경에 대 한 Azure 응용 프로그램 및 다른 서비스 구성을 테스트 하는 로컬 환경에 대 한 서비스 구성을 만들 수 있습니다.

요구 사항에 따라 이 서비스 구성을 추가, 삭제, 이름 변경 및 수정할 수 있습니다. Hello 다음 그림에에서 나와 있는 것 처럼 Visual Studio에서 이러한 서비스 구성을 관리할 수 있습니다.

![서비스 구성 관리](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

Hello를 열 수도 있습니다 **구성 관리** hello 역할의 속성 페이지에서 대화 상자. Azure 프로젝트에서 역할에 대 한 tooopen hello 속성 해당 역할에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **속성**합니다. Hello에 **설정** 탭에서 확장 hello **서비스 구성** 목록에서 선택한 후 **관리** tooopen hello **구성 관리**대화 상자.

### <a name="tooadd-a-service-configuration"></a>tooadd 서비스 구성
1. 솔루션 탐색기에서 Azure 프로젝트 hello에 대 한 hello 바로 가기 메뉴를 열고 선택한 후 **구성 관리**합니다.
   
    hello **서비스 구성 관리** 대화 상자가 나타납니다.
2. 서비스 구성을 tooadd 기존 구성의 복사본을 만들어야 합니다. toodo이 원하는 toocopy hello 이름 목록에서 다음을 선택 하는 hello 구성을 선택 **복사본 만들기**합니다.
3. (선택 사항) toogive hello 서비스 구성 다른 이름으로 hello 이름 목록에서 hello 새 서비스 구성을 선택한 다음 선택 **이름 바꾸기**합니다. Hello에 **이름** 텍스트 상자는 toouse이 서비스 구성에 대 한 한 다음 선택 hello 이름을 입력 합니다 **확인**합니다.
   
    새 서비스 구성 파일을 ServiceConfiguration 라고 합니다. [새 Name].cscfg toohello Azure 프로젝트를 솔루션 탐색기에서 추가 됩니다.

### <a name="toodelete-a-service-configuration"></a>toodelete 서비스 구성
1. 솔루션 탐색기에서 Azure 프로젝트 hello에 대 한 hello 바로 가기 메뉴를 열고 선택한 후 **구성 관리**합니다.
   
    hello **서비스 구성 관리** 대화 상자가 나타납니다.
2. 서비스 구성 toodelete hello 구성을 선택 toodelete hello에서 원하는 **이름** 나열 하 고 다음 선택 **제거**합니다. 대화 상자가 되도록 toodelete이이 구성을 tooverify 나타납니다.
3. **삭제**를 선택합니다.
   
     hello 서비스 구성 파일은 hello 솔루션 탐색기에서 Azure 프로젝트에서에서 제거 됩니다.

### <a name="toorename-a-service-configuration"></a>toorename 서비스 구성
1. 솔루션 탐색기에서 Azure 프로젝트 hello에 대 한 hello 바로 가기 메뉴를 열고 선택한 후 **구성 관리**합니다.
   
    hello **서비스 구성 관리** 대화 상자가 나타납니다.
2. 서비스 구성 toorename hello에서 hello 새 서비스 구성을 선택 **이름** 목록에서 선택한 후 **이름 바꾸기**합니다. Hello에 **이름** 텍스트 상자는 toouse이 서비스 구성에 대 한 한 다음 선택 hello 이름을 입력 합니다 **확인**합니다.
   
    hello 이름이 hello 서비스 구성 파일의 솔루션 탐색기에서 Azure 프로젝트 hello에 변경 됩니다.

### <a name="toochange-a-service-configuration"></a>toochange 서비스 구성
* Toochange 서비스 구성을 원한다 면 hello Azure 프로젝트에서에서 toochange 한 다음 선택 hello 특정 역할에 대 한 hello 바로 가기 메뉴를 열고 **속성**합니다. 참조 [하는 방법: Visual Studio와 함께 Azure 클라우드 서비스에 대 한 hello 역할 구성](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) 자세한 정보에 대 한 합니다.

## <a name="make-different-setting-combinations-by-using-profiles"></a>프로필을 사용하여 여러 다른 설정 조합 만들기
프로필을 사용 하 여 자동으로 채울 있습니다 hello **게시 마법사** 다양 한 용도 대 한 설정의 다양 한 조합을 사용 합니다. 예를 들어, 디버깅용으로 하나의 프로필이 있고 릴리스 빌드용으로 다른 프로필이 있을 수 있습니다. 이 경우 프로그램 **디버그** 프로필 갖기 **IntelliTrace** 사용 하도록 설정 하 고 hello **디버그** 구성을 선택 하며, 사용자 및 **릴리스** 프로필 갖기 **IntelliTrace** 사용 안 함 및 hello **릴리스** 구성을 선택 합니다. 다른 저장소 계정을 사용 하는 서비스 toodeploy 서로 다른 프로필을 사용할 수도 있습니다.

Hello에 대 한 hello 마법사를 처음으로 실행 하면 기본 프로필이 만들어집니다. Visual Studio tooyour hello에서 Azure 프로젝트에 추가 되는.azurePubXml 확장명을 가진 파일에 hello 프로필 저장 **프로필** 폴더입니다. 나중에 hello 마법사를 실행할 때 수동으로 다른 프로필을 지정, hello 파일 자동으로 업데이트 합니다. 절차를 수행 하는 hello를 실행 하기 전에 해야 이미 게시 클라우드 서비스가 한 번 이상.

### <a name="tooadd-a-profile"></a>tooadd 프로필
1. Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **게시**합니다.
2. 다음 toohello **profile을 대상** 목록, 선택 hello **프로필 저장** 다음 그림에 표시 하는 hello로 단추입니다. 이렇게 하면 프로필이 만들어 집니다.
   
    ![새 프로필 만들기](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Hello 프로필을 만든 후에 선택 **< 관리... >** hello에 **profile을 대상** 목록입니다.
   
    hello **프로필 관리** 다음 그림에 표시 하는 hello로 대화 상자가 나타납니다.
   
    ![프로필 관리 대화 상자](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. Hello에 **이름** 목록에서 프로필을 선택한 다음 선택 **복사본 만들기**합니다.
5. Hello 선택 **닫기** 단추입니다.
   
    새 프로필 hello hello 대상 프로필 목록에 나타납니다.
6. Hello에 **profile을 대상** 목록에서 방금 만든 선택 hello 프로필. hello 게시 마법사 설정이 선택한 hello 프로필 hello 선택 항목으로 채웁니다.
7. 선택 hello **이전** 및 **다음** toodisplay hello 게시 마법사의 각 페이지 단추 하 고이 프로필에 대 한 hello 설정을 사용자 지정 합니다. 자세한 내용은 [Azure 응용 프로그램 게시 마법사](http://go.microsoft.com/fwlink/p/?LinkID=623085) 를 참조하세요.
8. Hello 설정 사용자 지정을 완료 한 후 선택 **다음** toogo 백 toohello 설정 페이지. 이러한 설정을 사용 하 여 hello 서비스를 게시할 때 또는 선택 하는 경우 hello 프로필은 저장 **저장** 프로필 다음 toohello 목록입니다.

### <a name="toorename-or-delete-a-profile"></a>toorename 또는 프로 파일 삭제
1. Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **게시**합니다.
2. Hello에 **profile을 대상** 목록에서 **관리**합니다.
3. Hello에 **프로필 관리** 대화 상자, 선택 hello 프로필 toodelete를 원하고 다음 선택 **제거**합니다.
4. 나타나는 hello 확인 대화 상자에서 선택 **확인**합니다.
5. **닫기**를 선택합니다.

### <a name="toochange-a-profile"></a>toochange 프로필
1. Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 연 다음 선택 **게시**합니다.
2. Hello에 **profile을 대상** toochange 선택 hello 프로필을 나열 합니다.
3. 선택 hello **이전** 및 **다음** 단추 toodisplay의 각 페이지 hello 게시 마법사 및 원하는 hello 설정 변경 합니다. 자세한 내용은 [Azure 응용 프로그램 게시 마법사](http://go.microsoft.com/fwlink/p/?LinkID=623085) 를 참조하세요.
4. Hello 설정을 변경에서는 완료 된 후 선택 **다음** toogo 백 toohello **설정을** 페이지.
5. (선택 사항) 선택 **게시** hello 새 설정을 사용 하 여 toopublish hello 클라우드 서비스입니다. 이 시간에 클라우드 서비스를 닫습니다 toopublish 않으려면 hello 게시 마법사, Visual Studio 묻는 경우 toosave hello 변경 toohello 프로필입니다.

## <a name="next-steps"></a>다음 단계
Visual Studio에서 Azure 프로젝트의 다른 부분 구성에 대 한 toolearn 참조 [Azure 프로젝트 구성](http://go.microsoft.com/fwlink/p/?LinkID=623075)

