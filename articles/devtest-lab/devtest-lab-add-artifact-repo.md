---
title: "Azure DevTest Labs의 랩에 Git 리포지토리 추가 | Microsoft Docs"
description: "Azure DevTest Labs에서 사용자 지정 아티팩트 원본용 GitHub 또는 Visual Studio Team Services Git 리포지토리 추가"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 053f92a65f9ae29154d471fd22ee842620b4f273
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-azure-resource-manager-templates"></a>사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿을 저장할 Git 리포지토리 추가

랩에서 VM의 [사용자 지정 아티팩트를 만들거나](devtest-lab-artifact-author.md) [Azure Resource Manager 템플릿을 사용하여 사용자 지정 테스트 환경을 만들려는](devtest-lab-create-environment-from-arm.md) 경우 팀이 만드는 아티팩트 또는 Azure Resource Manager 템플릿을 포함할 개인 Git 리포지토리도 추가해야 합니다. 리포지토리는 [GitHub](https://github.com) 또는 [VSTS(Visual Studio Team Services)](https://visualstudio.com)에서 호스팅될 수 있습니다.

Microsoft는 그대로 배포하거나 랩에 맞게 사용자 지정할 수 있는 [아티팩트의 Github 리포지토리](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)를 제공했습니다. 아티팩트를 사용자 지정하거나 만들 경우 공용 리포지토리에 저장할 수 없으며 개인 리포지토리를 만들어야 합니다. 

VM을 만들 경우 Azure Resource Manager 템플릿을 저장하고 원할 경우 사용자 지정한 다음 나중에 추가 VM을 손쉽게 만들 수 있습니다. 사용자 지정 Azure Resource Manager 템플릿을 저장할 개인 리포지토리를 만들어야 합니다.  

* GitHub 리포지토리를 만드는 방법을 알아보려면 [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)를 참조하세요.
* Git 리포지토리를 사용하여 Team Services 프로젝트를 만드는 방법을 알아보려면 [Visual Studio Team Services에 연결](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)을 참조하세요.

다음 스크린샷에서는 아티팩트가 포함된 리포지토리가 GitHub에서 어떻게 표시되는지 보여 주는 대한 예입니다.  
![GitHub 아티팩트 리포지토리 샘플](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a>리포지토리 정보 및 자격 증명 가져오기
랩에 리포지토리를 추가하려면 먼저 리포지토리에서 특정 정보를 가져와야 합니다. 다음 섹션에서는 GitHub 및 Visual Studio Team Services에서 호스트되는 리포지토리에 대해 이러한 정보를 가져오는 방법을 안내합니다.

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a>GitHub 리포지토리 복제 URL 및 개인 액세스 토큰 가져오기
GitHub 리포지토리 복제 URL 및 개인 액세스 토큰을 가져오려면 다음 단계를 따르세요.

1. 아티팩트 또는 Azure Resource Manager 템플릿 정의를 포함하는 GitHub 리포지토리의 홈 페이지로 이동합니다.
2. **복제 또는 다운로드**를 선택합니다.
3. 이 단추를 선택하여 **HTTPS 복제 URL** 을 클립보드에 복사하고 나중에 사용할 수 있게 URL을 저장합니다.
4. GitHub의 오른쪽 위에서 프로필 이미지를 탭하고 **설정**을 선택합니다.
5. 왼쪽의 **개인 설정** 메뉴에서 **개인 액세스 토큰**을 선택합니다.
6. **Generate new token**(새 토큰 생성)을 탭합니다.
7. **새 개인 액세스 토큰** 페이지에서 **토큰 설명**을 입력하고 **범위 선택**에서 기본 항목을 수락한 다음 **토큰 생성**을 선택합니다.
8. 나중에 필요하므로 생성한 토큰을 저장합니다.
9. 이제 GitHub를 닫아도 됩니다.   
10. [리포지토리에 랩 연결](#connect-your-lab-to-the-repository) 섹션을 계속 진행합니다.

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Visual Studio Team Services 리포지토리 복제 URL 및 개인 액세스 토큰 가져오기
Visual Studio Team Services 리포지토리 복제 URL 및 개인 액세스 토큰을 가져오려면 다음 단계를 따르세요.

1. 팀 컬렉션의 홈페이지(예: `https://contoso-web-team.visualstudio.com`)를 연 다음 프로젝트를 선택합니다.
2. 프로젝트 홈 페이지에서 선택 **코드**합니다.
3. 복제 URL을 보려면 프로젝트 **코드** 페이지에서 **복제**를 선택합니다.
4. 이 자습서의 뒷부분에서 필요하므로 URL을 저장합니다.
5. 개인 액세스 토큰을 만들려면 사용자 계정 드롭다운 메뉴에서 **내 프로필** 을 탭합니다.
6. 프로필 정보 페이지에서 **보안**을 탭합니다.
7. **보안** 탭에서 **추가**를 선택합니다.
8. **개인 액세스 토큰 만들기** 페이지에서

   * 토큰에 대한 **설명** 을 입력합니다.
   * **다음 기간 내에 만료** 목록에서 **180일**을 선택합니다.
   * **계정** 목록에서 **액세스 가능한 모든 계정**을 선택합니다.
   * **모든 범위** 옵션을 선택합니다.
   * **토큰 만들기**를 선택합니다.
9. 완료되면 새 토큰이 **개인 액세스 토큰** 목록에 표시됩니다. **토큰 복사**를 선택하고 나중에 사용할 수 있게 토큰 값을 저장합니다.
10. [리포지토리에 랩 연결](#connect-your-lab-to-the-repository) 섹션을 계속 진행합니다.

## <a name="connect-your-lab-to-the-repository"></a>랩을 리포지토리에 연결
1. [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.
2. **추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.
3. 랩 목록에서 원하는 랩을 탭합니다.   
4. 왼쪽 패널에서 **구성 및 정책**을 선택합니다.
5. 랩의 **구성 및 정책** 영역에서 **리포지토리**를 선택합니다.
6. **리포지토리** 영역에서 **+ 추가**를 선택합니다.

    ![리포지토리 추가 버튼](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. 두 번째 **리포지토리** 페이지에서 다음 정보를 지정합니다.

   * **이름** - 리포지토리의 이름을 입력합니다.
   * **Git 복제 URL** - 이전에 GitHub 또는 Visual Studio Team Services에서 복사한 Git HTTPS 복제 URL을 입력합니다.
   * **분기** - 정의를 가져올 분기를 입력합니다.
   * **개인 액세스 토큰** - 이전에 GitHub 또는 Visual Studio Team Services에서 가져온 개인 액세스 토큰을 입력합니다.
   * **폴더 경로** - 아티팩트 또는 Azure Resource Manager 템플릿 정의가 포함된 복제 URL에 상대적인 폴더 경로를 하나 이상 입력합니다. 하위 디렉터리를 지정하는 경우 폴더 경로에 슬래시를 포함해야 합니다.

     ![리포지토리 영역](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계
개인 Git 리포지토리를 만든 후 필요에 따라 다음 중 하나 또는 둘 다를 수행할 수 있습니다.
* [사용자 지정 아티팩트](devtest-lab-artifact-author.md)를 저장합니다. 저장한 아티팩트는 나중에 새 VM을 만드는 데 사용할 수 있습니다.
* [Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스를 만든](devtest-lab-create-environment-from-arm.md) 다음 개인 리포지토리에 템플릿을 저장합니다.

VM을 만드는 경우 Git 리포지토리에 아티팩트 또는 템플릿이 추가되었는지 확인할 수 있습니다. 추가된 아티팩트 또는 템플릿은 목록에서 즉시 사용할 수 있으며 원본이 지정된 열에 개인 리포지토리의 이름이 표시됩니다. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>관련 블로그 게시물
* [Azure DevTest Labs에서 실패한 아티팩트 문제를 해결하는 방법](devtest-lab-troubleshoot-artifact-failure.md)
* [Azure DevTest Labs에서 리소스 관리자 템플릿을 사용하여 기존 AD 도메인에 VM 가입](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
