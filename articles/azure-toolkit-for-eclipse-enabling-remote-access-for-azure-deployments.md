---
title: "aaaEnabling Eclipse에서 Azure 배포에 대 한 원격 액세스"
description: "Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Azure 배포에 대 한 tooenable 원격 액세스 하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Eclipse에서 Azure 배포에 대한 원격 액세스를 사용하도록 설정
toohelp 배포 문제 해결, 사용 하도록 설정 하 고 배포를 호스트 하는 원격 액세스 tooconnect toohello 가상 컴퓨터를 사용할 수 있습니다. 원격 액세스 기능 hello hello 프로토콜 RDP (원격 데스크톱)에 의존합니다. TooAzure를 게시 하기 전에 원격 액세스를 구성할 수 Eclipse와 Windows 운영 체제를 사용 하는 경우 또는 tooAzure, 게시 한 후 배포에 대 한 원격 액세스를 구성할 수 있습니다. 참고가 Azure에서 순서 tooconnect tooyour 배포의 가상 컴퓨터의 운영 체제와 호환 되는 원격 데스크톱 클라이언트 필요 합니다.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>원격 액세스 하기 전에 tooenable tooAzure를 배포 하는 방법
> [!NOTE]
> 응용 프로그램 tooAzure를 배포 하기 전에 원격 액세스 tooenable toobe Windows에서 Eclipse를 실행 해야 합니다.
> 
> 

hello 다음 그림에 나와 hello **원격 액세스** 속성 대화 상자 tooenable 원격 액세스를 사용 합니다.

![][ic719494]

두 가지 방법으로 toodisplay hello **원격 액세스** 속성 대화 상자:

* Hello 클릭 **고급** hello에 대 한 링크 **원격 액세스** hello 섹션 **tooAzure 게시** 대화 상자.

* 열기 hello **속성** Azure 프로젝트의 대화 상자.

새 Azure 배포 프로젝트를 만들면 hello 프로젝트는 기본적으로 사용 하는 원격 액세스 않아도 됩니다. 그러나 있습니다 사용 하 여 쉽게 원격 액세스 hello에 hello 사용자 이름 및 암호를 지정 하 여 **tooAzure 게시** 대화 상자. hello 원격 액세스 암호는 X.509 인증서를 사용 하 여 암호화 됩니다. 사용 하지 않는 경우, 사용자 고유의 인증서를 제공 hello 암호화는 hello Eclipse 용 Azure 플러그 인과 함께 제공 된 자체 서명 된 인증서를 사용 합니다. Hello에이 자체 서명 된 인증서가 **cert** Azure 프로젝트의 폴더를 저장 된 공용 인증서 파일 (SampleRemoteAccessPublic.cer)로 모두 및 개인 정보 교환 (PFX)으로 인증서 파일 ( SampleRemoteAccessPrivate.pfx)입니다. 후자의 hello hello hello 인증서에 대 한 개인 키가 포함 되어 있고 기본 암호 인 **Password1**합니다. 그러나이 암호는 누구나 알 이후 학습 목적으로 프로덕션 배포에 대 한 하지에 대해서만 hello 기본 인증서를 사용 해야 합니다. 따라서 이외의 학습 목적으로 배포를 위한 tooenabled 원격 세션을 원하는 경우 클릭 하 여 해야 hello **고급** hello에 대 한 링크 **tooAzure 게시** 대화 toospecify 직접 인증서입니다. 해당 Azure hello 사용자 암호를 해독할 수 있으므로 hello Azure 관리 포털 내에서 서비스를 호스트 하는 참고 hello 인증서 tooyour tooupload hello PFX 버전이 필요 합니다.

hello 자습서의 나머지 부분에서는 hello tooenable 원격 사용 하지 않도록 설정 하는 원격 액세스를 사용 하 여 처음에 만든 Azure 배포 프로젝트에 대 한 액세스 하는 방법을 보여 줍니다. 이 자습서의 목적을 위해 새 자체 서명된 인증서를 만들 예정이며 해당 .pfx 파일은 사용자가 선택한 암호를 갖게 됩니다. 인증 기관에서 발급 한 인증서를 사용 하 여 hello 옵션이 있습니다.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>원격 액세스 한 후 tooenable tooAzure 구축 하는 방법을
tooenable 원격 액세스 배포 tooAzure를 사용 하 여 hello 단계를 수행 하면:

1. Azure 계정을 사용 하 여 hello Azure 관리 포털에 로그인

2. **클라우드 서비스**목록에서 배포된 클라우드 서비스를 선택합니다.

3. Hello 클라우드 서비스 웹 페이지에서 클릭 hello **구성** 링크

4. Hello 구성 페이지의 아래쪽 hello 클릭 hello **원격** 링크

5. Hello 팝업 대화 상자가 나타나는 경우:
   
   * Hello 역할을 지정 하면 tooenable 원격 액세스 하려는

   * Tooselect hello 클릭 **원격 데스크톱 사용** 확인란
   
   * 사용자 이름 및 원격 액세스를 위한 toouse 원하는 암호를 지정 합니다.
   
   * Hello 인증서 toouse 선택

6. **확인** 

구성 변경 진행 중 몇 분 toocomplete 소요 될 수 있는 않다는 메시지가 표시 됩니다. Hello 구성 변경이 완료 되 면에서 다음과 같이 hello hello **toolog에 원격으로** 이 문서의 뒷부분에 나오는 섹션.

## <a name="how-tooenable-remote-access-in-your-package"></a>Tooenable 원격 패키지에 액세스 하는 방법
1. Eclipse의 Project Explorer 창에서 Azure 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Properties**를 클릭합니다.

2. Hello에 **속성** 대화 상자를 확장 하 고 **Azure** hello 왼쪽 창에서 **원격 액세스**합니다.

3. Hello에 **원격 액세스** 대화 상자에서 확인 **이 로그인 자격 증명으로 모든 역할 tooaccept 원격 데스크톱 연결을 사용 하도록 설정** 을 선택 합니다.

4. Hello 원격 데스크톱 연결에 대 한 사용자 이름을 지정 합니다.

5. 지정 하 고 hello 사용자에 대 한 hello 암호를 확인 합니다. hello 사용자 이름 및 암호 설정 된 값이 대화이 상자에 원격 데스크톱 연결을 설정할 때 사용 됩니다. (이것은 PFX 암호와 다른 별도 암호입니다.)

6. Hello 사용자 계정에 대 한 hello 만료 날짜를 지정 합니다.

7. 클릭 **새로** toocreate 새 자체 서명 된 인증서입니다. (또는 hello 통해 작업 영역이 나 파일 시스템에서 인증서를 선택할 수 **작업 영역** 또는 **FileSystem** 각각 하지만이 자습서에서는 새 만듭니다 단추 인증서입니다.)

   * Hello에 **새 인증서** 대화 상자에서 지정 하 고 PFX 파일을 사용 하는 hello 암호를 확인 합니다.

   * 에 대해 제공 된 값과 hello 허용 **이름 (CN)**, 하거나 사용자 지정 이름을 사용 합니다.

   * Hello 새 인증서를.cer 형식으로 저장 될 hello 경로 파일 이름을 지정 합니다. 이 단계와 hello 다음 단계에 대 한 hello를 사용할 수 있습니다 **cert** 수 있지만 Azure 프로젝트의 폴더는 무료 toochoose 다른 위치입니다. 이 자습서의 목적을 위해 **c:\mycert\mycert.cer**을 사용합니다. (Hello 만들 **c:\mycert** 폴더 이전 tooproceeding 또는 원하는 경우 기존 폴더를 사용 합니다.)

   * Hello 새 인증서와 개인 키를.pfx 형식으로 저장할 수 hello 경로 파일 이름을 지정 합니다. 이 자습서의 목적을 위해 **c:\mycert\mycert.pfx**를 사용합니다. 프로그램 **새 인증서** 대화 비슷한 toohello 다음과 같아야 합니다. (사용 하지 않은 경우 hello 폴더 경로 업데이트 **c:\mycert**):
     
      ![][ic712275]

   * 클릭 **확인** tooclose hello **새 인증서** 대화 상자.

8. 프로그램 **원격 액세스** 대화 비슷한 toohello 다음과 같아야 합니다.</p>
   
   ![][ic719495]

9. 클릭 **확인** tooclose hello **원격 액세스** 대화 상자.

응용 프로그램을 다시 작성, hello로 toocloud 배포에 대 한 집합을 작성 합니다.

## <a name="toolog-in-remotely"></a>toolog에 원격으로
역할 인스턴스가 준비 되 면 원격 응용 프로그램을 호스팅하는 toohello 가상 컴퓨터에 로그온 할 수 있습니다.

* Windows 및 선택한 hello에서 Eclipse를 사용 하는 경우 **배포 시 원격 데스크톱 시작** 옵션 중에 배포 tooAzure 나타납니다 원격 데스크톱 연결 로그온 화면이 배포를 시작할 때입니다. Hello 사용자 이름 및 암호를 묻는 메시지가 나타나면 hello 원격 사용자에 대해 지정한 hello 값을 입력 하 고에 수 toolog 됩니다.

* 또 다른 방법은 toolog hello를 통해 원격으로 <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure 관리 포털</a>:
  
  * Hello 내 **클라우드 서비스** hello Azure 관리 포털의 보기 클라우드 서비스를 클릭 하 고 **인스턴스**, 특정 인스턴스를 클릭 하 고 클릭 다음 hello **연결**단추입니다. hello **연결** 단추가 hello 명령 모음에서 hello 다음과 같이 나타납니다.
    
      ![][ic659273]

  * Hello를 클릭 한 후 **연결** 단추를 증명된 tooopen RDP 파일을 사용할 수 있습니다. Hello 파일을 열고 hello 프롬프트를 따릅니다. (있습니다 수이 파일 tooyour 로컬 컴퓨터를 저장할 수도 한 다음 hello 파일 두 번 클릭 하 여 tooremote 로그에서에서 실행 tooyour toofirst 필요 없이 가상 컴퓨터 이동 hello 관리 포털.)

  * Hello 사용자 이름 및 암호를 묻는 메시지가 나타나면 hello 원격 사용자에 대해 지정한 hello 값을 입력 하 고에 수 toolog 됩니다.

> [!NOTE]
> Windows 이외의 운영 체제에 있는 toouse 운영 체제와 호환 되는 원격 데스크톱 클라이언트를 해야 hello 단계 tooconfigure hello 다운로드 한 RDP 파일의 hello 설정 사용 하 여 해당 클라이언트를 수행 합니다.
> 
> 

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse] 

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
