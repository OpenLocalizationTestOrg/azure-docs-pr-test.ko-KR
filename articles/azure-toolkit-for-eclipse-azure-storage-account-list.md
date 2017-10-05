---
title: "Azure 저장소 계정 목록"
description: "Eclipse용 Azure 도구 키트를 사용하여 저장소 계정 설정 관리"
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a>Azure 저장소 계정 목록
Azure 저장소 계정은 JDK, 응용 프로그램 서버, 임의 구성 요소뿐만 아니라 캐싱을 사용하는 경우 상태 저장을 위해 다운로드 위치를 사용할 수 있도록 합니다. Eclipse는 프로젝트에 사용할 수 있는 알려진 저장소 계정 목록을 사용자의 Eclipse 작업 공간에 유지 관리합니다. 목록을 관리하는 데 사용되는 **저장소 계정** 대화 상자를 열려면, Eclipse에서 **창**, **기본 설정**을 차례로 클릭하고 **Azure**를 확장한 다음 **저장소 계정**을 클릭합니다.

다음은 **Storage Accounts** 대화 상자입니다.

![][ic719496]

이 대화 상자는 다음과 같이 저장소 계정을 사용하는 대화 상자의 **Accounts** 링크를 통해 열 수도 있습니다.

* **서버 구성** 대화 상자의 **JDK** 탭
* **서버 구성** 대화 상자의 **서버** 탭
* **Add Component** 대화 상자
* **Caching** 속성 대화 상자

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>게시 설정 파일을 사용하여 저장소 계정 가져오기
1. **저장소 계정** 대화 상자에서 **PUBLISH-SETTINGS 파일에서 가져오기**을 클릭합니다.

2. (게시 설정 파일을 로컬 컴퓨터에 이미 저장한 경우에는 이 단계를 건너뜁니다.) **구독 정보 가져오기** 대화 상자에서 **PUBLISH-SETTINGS 파일 다운로드**을 클릭합니다. Azure 계정에 로그인하지 않은 경우에는 로그인을 요청하는 메시지가 표시됩니다. 그 후 Azure 게시 설정 파일을 저장하도록 요청하는 메시지가 표시됩니다. (로그인 페이지에 이렇게 표시되는 지침은 무시할 수 있습니다. 이러한 지침은 Azure 포털에 의해 제공되며 Visual Studio 사용자를 위한 것입니다.) 로컬 컴퓨터에 저장합니다.

3. **구독 정보 가져오기** 대화 상자에서 **찾아보기** 단추를 클릭하고 이전에 로컬에 저장해 놓은 게시 설정 파일을 선택한 다음 **열기**를 클릭합니다.

4. **확인**을 클릭하여 **구독 정보 가져오기** 대화 상자를 닫습니다.

## <a name="to-create-a-new-storage-account"></a>새 저장소 계정 만들기
1. **저장소 계정** 대화 상자에서 **추가**를 클릭합니다.

2. **저장소 계정 추가** 대화 상자에서 **새로 만들기**를 클릭합니다.

3. **New Storage Account** 대화 상자에서 다음 항목에 대한 값을 지정합니다.

   * 저장소 계정 이름

   * 저장소 계정의 위치

   * 저장소 계정에 대한 설명

   * 저장소 계정이 속해 있는 구독

4. **확인**를 클릭하여 **새 저장소 계정** 대화 상자를 닫습니다.

저장소 계정을 만드는 데 몇 분 정도 걸릴 수 있습니다. 계정이 생성된 후에 **확인**를 클릭하여 **저장소 계정 추가** 대화 상자를 닫으면, 새 저장소 계정이 사용 가능한 저장소 계정 목록에 추가됩니다.

## <a name="to-add-an-existing-storage-account-to-the-list"></a>기존 저장소 계정을 목록에 추가
1. Azure 저장소 계정이 없는 경우에는 위의 **새 저장소 계정 만들기 섹션** 에 나열된 단계에 따라서 계정을 만듭니다. (또는 [Azure Management Portal][Azure Management Portal]에서 새 저장소 계정을 만들 수 있습니다.)

2. **저장소 계정** 대화 상자에서 **추가**를 클릭합니다.

3. **저장소 계정 추가** 대화 상자에서 **이름** 및 **선택키**의 값을 입력합니다. 계정 이름 및 액세스 키는 기존 Azure 저장소 계정에 대한 값이어야 합니다. 저장소 계정 이름 및 키를 보려면 [Azure Management Portal][Azure Management Portal]의 **저장소** 섹션을 사용합니다. **Add Storage Account** 대화 상자는 다음과 유사한 모양입니다.
   
   ![][ic719497]

4. **확인**을 클릭하여 **저장소 계정 추가** 대화 상자를 닫습니다.

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>새 액세스 키를 사용하도록 저장소 계정 수정
1. **저장소 계정** 대화 상자에서 편집할 저장소 계정을 클릭한 후 **편집**을 클릭합니다.

2. **저장소 계정 선택기 편집** 대화 상자에서 **선택키** 값을 수정합니다.

3. **확인**을 클릭하고 **저장소 계정 선택기 편집** 대화 상자를 닫습니다.

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>Eclipse에 유지 관리되는 목록에서 저장소 계정 제거
1. **저장소 계정** 대화 상자에서 편집할 저장소 계정을 클릭한 후 **제거**를 클릭합니다.

2. 저장소 계정을 제거한다는 메시지가 표시되면 **OK** 를 클릭합니다.

> [!NOTE]
> **Storage Accounts** 대화 상자를 통해 저장소 계정을 제거하면, 계정은 Eclipse 내에서 볼 수 있는 저장소 계정 목록에서만 제거됩니다. Azure 구독에서 저장소 계정을 제거하는 것은 아닙니다. 아울러 Eclipse에서 구독 세부 정보를 다시 로드한 후에 저장소 계정이 다시 표시될 수 있습니다.
> 
> 

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse] 

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
