---
title: "저장소 계정 목록을 aaaAzure"
description: "저장소 계정 설정을 Eclipse 용 Azure 도구 키트 hello를 사용 하 여 관리"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Azure 저장소 계정 목록
Azure 저장소 계정을 사용 하는 JDK, 응용 프로그램 서버 및 임의 구성 요소는 물론 캐싱을 사용할 때 상태를 저장 하는 데 사용 되는 위치 toobe를 다운로드 합니다. Eclipse는 Eclipse 작업 영역에서 사용할 수 있는 tooyour 프로젝트는 알려진된 저장소 계정 목록을 유지 관리 합니다. tooopen hello **저장소 계정은** 대화 상자를 사용 하는 toomanage Eclipse 내에서 나열 하는 클릭 **창**, 클릭 **기본 설정**, 확장 **Azure** , 클릭 하 고 **저장소 계정은**합니다.

hello 다음 표시 되어 hello **저장소 계정은** 대화 상자.

![][ic719496]

이 대화 상자에서 열 수도 있습니다는 **계정** hello 다음과 같은 저장소 계정을 사용 하는 대화 상자에서 링크:

* hello **JDK** hello 탭 **서버 구성** 대화 상자.
* hello **서버** hello 탭 **서버 구성** 대화 상자.
* hello **구성 요소 추가** 대화 상자.
* hello **캐싱** 속성 대화 상자.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>저장소를 사용 하 여 계정을 tooimport 게시 설정 파일
1. Hello 내 **저장소 계정은** 대화 상자에서 클릭 **게시 설정 파일에서 가져오기**합니다.

2. (이 단계는 이미 게시 설정 파일 tooyour 로컬 컴퓨터를 저장 하는 경우.) Hello에 **구독 정보 가져오기** 대화 상자를 클릭 하 여 **게시 설정 파일 다운로드**합니다. 아직 Azure 계정에 로그인 하지 않은 경우에 증명된 toolog 됩니다. 다음 메시지가 표시 됩니다 toosave Azure 게시 설정 파일입니다. (Hello hello 로그온 페이지에 표시 되는 결과 지침을 무시할 수 hello Azure 포털에서 제공 하며 Visual Studio 사용자를 대상으로 합니다.) Tooyour 로컬 시스템으로 저장 합니다.

3. Hello에 여전히 **구독 정보 가져오기** 대화 상자에서 hello 클릭 **찾아보기** 단추, 선택 hello 설정을 저장 한 파일을 로컬에서 이전에 게시 하 고 클릭 **열**.

4. 클릭 **확인** tooclose hello **구독 정보 가져오기** 대화 상자.

## <a name="toocreate-a-new-storage-account"></a>toocreate 새 저장소 계정
1. Hello 내 **저장소 계정은** 대화 상자에서 클릭 **추가**합니다.

2. Hello 내 **저장소 계정 추가** 대화 상자를 클릭 하 여 **새로**합니다.

3. Hello 내 **새 저장소 계정** 대화 상자에서 다음 hello에 대 한 값을 지정 합니다.

   * 저장소 계정 이름

   * Hello 저장소 계정의 위치입니다.

   * Hello 저장소 계정에 대 한 설명입니다.

   * hello 구독 toowhich hello 저장소 계정에 속해 있습니다.

4. 클릭 **확인** tooclose hello **새 저장소 계정** 대화 상자.

만든 저장소 계정 toobe 프로그램에 대 일 분 정도 걸릴 수 있습니다. 를 만든 후 클릭 **확인** tooclose hello **저장소 계정 추가** 대화 상자에서 및 새로운 저장소 계정이 사용 가능한 저장소 계정 목록이 toohello 추가 될 합니다.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>기존 저장소 계정 toohello 목록 tooadd
1. Hello에 나열 된 hello 단계를 수행 하면 아직 없는 Azure 저장소 계정, 만들 경우 **toocreate 새 저장소 계정 섹션** 위에 있습니다. (새 저장소 계정을 hello에서 만들 수 있습니다 또는 [Azure 관리 포털][Azure Management Portal].)

2. Hello 내 **저장소 계정은** 대화 상자에서 클릭 **추가**합니다.

3. Hello 내 **저장소 계정 추가** 대화 상자에서 값을 입력 **이름** 및 **선택 키**합니다. 기존 Azure 저장소 계정에 대 한 hello 계정 이름과 액세스 키 여야 합니다. 사용 하 여 hello **저장소** hello 섹션 [Azure 관리 포털] [ Azure Management Portal] tooview 저장소 계정의 이름을 지정 하 고 키입니다. 프로그램 **저장소 계정 추가** 대화 상자가 유사 toohello 다음에 표시 됩니다.
   
   ![][ic719497]

4. 클릭 **확인** tooclose hello **저장소 계정 추가** 대화 상자.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify 저장소 계정 toouse 새 액세스 키
1. Hello 내 **저장소 계정은** 대화 상자에서 tooedit 원하고 클릭 hello 저장소 계정을 클릭 **편집**합니다.

2. Hello 내 **저장소 계정 액세스 키 편집** 대화 상자에서 hello 수정 **선택 키** 값입니다.

3. 클릭 **확인** tooclose hello **저장소 계정 액세스 키 편집** 대화 상자.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove hello 목록에서 저장소 계정을 Eclipse에서 유지 관리
1. Hello 내 **저장소 계정은** 대화 상자에서 tooedit 원하고 클릭 hello 저장소 계정을 클릭 **제거**합니다.

2. 클릭 **확인** 때 메시지 표시 tooremove hello 저장소 계정입니다.

> [!NOTE]
> Hello 통해 hello 저장소 계정을 제거 하는 **저장소 계정은** 대화만이 목록에서 제거 hello Eclipse 내에서 볼 수 있는 저장소 계정입니다. Azure 구독에서 저장소 계정을 hello를 제거 하지 않습니다. 또한 hello 저장소 계정 수 다시 목록에 표시 Eclipse 구독 hello 세부 정보를 다시 로드 한 후 합니다.
> 
> 

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse] 

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
