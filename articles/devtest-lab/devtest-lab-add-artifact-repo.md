---
title: "Azure DevTest Labs에서 Git 리포지토리 tooa 랩 aaaAdd | Microsoft Docs"
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
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Git 리포지토리 toostore 사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿 추가

너무 하려는 경우[사용자 지정 아티팩트를 만들](devtest-lab-artifact-author.md) 랩에서 Vm hello에 대 한 또는 [Azure 리소스 관리자 템플릿 toocreate 사용자 지정 테스트 환경을 사용 하 여](devtest-lab-create-environment-from-arm.md), 개인 Git 리포지토리에 tooinclude도 추가 해야 hello 아티팩트 또는 팀에서 Azure 리소스 관리자 템플릿을 합니다. hello 저장소에 호스팅될 수 [GitHub](https://github.com) 또는 [VSTS Visual Studio Team Services ()](https://visualstudio.com)합니다.

Microsoft는 그대로 배포하거나 랩에 맞게 사용자 지정할 수 있는 [아티팩트의 Github 리포지토리](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)를 제공했습니다. 를 사용자 지정 하거나 아티팩트를 만들 때 hello 공용 저장소에 저장할 수 없습니다-개인 리포지토리에 직접 만들어야 합니다. 

Hello Azure 리소스 관리자 템플릿을 저장, 한 다음 사용 하 여 사용자 지정할 수는 VM을 만들 때 나중 tooeasily 더 많은 Vm을 만듭니다. 사용자 고유의 개인 리포지토리에 toostore 지정 Azure 리소스 관리자 템플릿을 만들어야 합니다.  

* toocreate GitHub 리포지토리를 확인 하려면 어떻게 toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)합니다.
* toocreate Git 리포지토리를 포함 하는 Team Services 프로젝트를 확인 하려면 어떻게 toolearn [tooVisual Studio Team Services 연결](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)합니다.

hello 다음 스크린 샷에서의 예가 나와 아티팩트가 포함 된 저장소 GitHub에서 표시 되는 방식을:  
![GitHub 아티팩트 리포지토리 샘플](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Hello 저장소 정보 및 자격 증명 가져오기
리포지토리 tooyour 랩 tooadd 먼저 가져와야 특정 정보 리포지토리에서 합니다. 다음 섹션 hello GitHub 및 Visual Studio Team Services에서 호스트 되는 저장소에 대 한이 정보를 가져오는 과정을 안내 합니다.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Hello GitHub 리포지토리 복제 URL 및 개인용 액세스 토큰 가져오기
tooget hello GitHub 리포지토리 복제 URL 및 개인 액세스 토큰에는 다음이 단계를 따르십시오.

1. Hello 아티팩트 또는 Azure 리소스 관리자 템플릿 정의 포함 하는 hello GitHub 리포지토리의 toohello 홈 페이지를 찾습니다.
2. **복제 또는 다운로드**를 선택합니다.
3. 선택 hello 단추 toocopy hello **복제 url을 HTTPS** toohello 클립보드 하 고 나중에 사용할 hello URL을 저장 합니다.
4. GitHub의 hello 오른쪽 위 모서리에 hello 프로필 이미지를 선택 하 고 선택 **설정을**합니다.
5. Hello에 **개인 설정** 메뉴 hello 왼쪽에서 선택 **개인용 액세스 토큰**합니다.
6. **Generate new token**(새 토큰 생성)을 탭합니다.
7. Hello에 **새 개인용 액세스 토큰** 페이지에서 입력 한 **설명 토큰**, hello에서 hello 기본 항목을 수락 **범위를 선택**, 선택한 후 **생성 토큰**합니다.
8. 나중에 필요에 따라 생성 된 hello 토큰을 저장 합니다.
9. 이제 GitHub를 닫아도 됩니다.   
10. Toohello 계속 [랩 toohello 리포지토리에 연결](#connect-your-lab-to-the-repository) 섹션.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Hello Visual Studio Team Services 리포지토리 복제 URL 및 개인용 액세스 토큰 가져오기
tooget hello Visual Studio Team Services 리포지토리 복제 URL 및 개인 액세스 토큰에는 다음이 단계를 따르십시오.

1. 열기 hello 홈 페이지의 팀 컬렉션 (예를 들어 `https://contoso-web-team.visualstudio.com`)을 선택한 다음 프로젝트를 선택 합니다.
2. Hello 프로젝트 홈 페이지에서 선택 **코드**합니다.
3. hello 프로젝트, tooview hello 클론 URL **코드** 페이지에서 **복제**합니다.
4. 이 자습서의 뒷부분에 나오는 필요에 따라 hello URL을 저장 합니다.
5. 개인 액세스 토큰 toocreate 선택 **내 프로필** hello 사용자 계정 드롭 다운 메뉴에서 합니다.
6. Hello 프로필 정보 페이지에서 선택 **보안**합니다.
7. Hello에 **보안** 탭에서 **추가**합니다.
8. Hello에 **개인용 액세스 토큰을 만듭니다.** 페이지:

   * 입력 한 **설명** hello 토큰에 대 한 합니다.
   * 선택 **180 일** hello에서 **만료에** 목록입니다.
   * 선택 **액세스할 수 있는 모든 계정을** hello에서 **계정** 목록입니다.
   * Hello 선택 **모든 범위** 옵션입니다.
   * **토큰 만들기**를 선택합니다.
9. 완료 되 면 hello 새 토큰 나타납니다 hello **개인 액세스 토큰** 목록입니다. 선택 **토큰 복사**, 한 다음 나중에 사용할 hello 토큰 값을 저장 합니다.
10. Toohello 계속 [랩 toohello 리포지토리에 연결](#connect-your-lab-to-the-repository) 섹션.

## <a name="connect-your-lab-toohello-repository"></a>랩 toohello 리포지토리에 연결
1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.   
4. 왼쪽된 패널의 hello 선택 **구성 및 정책**합니다.
5. Hello 랩에 **구성 및 정책** 영역에서 **저장소**합니다.
6. Hello에 **저장소** 영역에서 **+ 추가**합니다.

    ![리포지토리 추가 버튼](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. Hello에 두 번째 **저장소** 페이지 hello 다음 정보를 지정 합니다.

   * **이름** -hello 저장소에 대 한 이름을 입력 합니다.
   * **Git 복제 Url** -GitHub 또는 Visual Studio Team Services에서 앞에서 복사한 hello Git HTTPS 클론 URL을 입력 합니다.
   * **분기** -hello 분기 tooget 정의를 입력 합니다.
   * **개인용 액세스 토큰** -GitHub 또는 Visual Studio Team Services에서 이전에 얻은 hello 개인용 액세스 토큰을 입력 합니다.
   * **폴더 경로** -프로그램 아티팩트 또는 Azure 리소스 관리자 템플릿 정의가 포함 된 하나 이상의 폴더에 경로 상대 toohello 클론 URL을 입력 합니다. 하위 디렉터리를 지정할 때는 hello 폴더 경로에 있는지 tooinclude hello 슬래시를 확인 합니다.

     ![리포지토리 영역](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계
개인 Git 리포지토리를 만든 후 필요에 따라 hello 다음 중 하나 또는 모두를 수행할 수 있습니다.
* 저장소 프로그램 [사용자 지정 아티팩트](devtest-lab-artifact-author.md)이며 이후 toocreate를 사용할 수 있습니다 새 Vm입니다.
* [Azure 리소스 관리자 템플릿으로 환경 다중 VM 및 PaaS 리소스 만들기](devtest-lab-create-environment-from-arm.md) 다음 개인 리 포에 hello 서식 파일을 보관 합니다.

VM을 만들 때 hello 아티팩트 또는 템플릿 / tooyour Git 리포지토리에 추가 된 것을 확인할 수 있습니다. 즉시 hello 또는 목록에서 아티팩트 템플릿 hello 소스를 지정 하는 hello 열에 표시 된 사용자의 개인 리포지토리의 hello 이름으로 사용할 수 있습니다. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>관련 블로그 게시물
* [어떻게 tootroubleshoot Azure DevTest Labs의 아티팩트를 실패](devtest-lab-troubleshoot-artifact-failure.md)
* [VM tooexisting Azure DevTest Labs에서 리소스 관리자 템플릿을 사용 하는 AD 도메인 가입](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
