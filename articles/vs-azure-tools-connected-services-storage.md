---
title: "Visual Studio에서 연결 된 서비스를 사용 하 여 Azure 저장소 aaaAdd | Microsoft Docs"
description: "Hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 Azure 저장소 tooyour 앱 추가"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Visual Studio 연결 서비스를 사용하여 Azure 저장소 추가
Visual Studio와 함께 hello tooAzure 저장소 hello를 사용 하 여 다음 중 하나 연결할 수 있습니다 **연결 된 서비스 추가** 대화 상자:

- C# 클라우드 서비스
- .NET 백 엔드 모바일 서비스
- ASP.NET 웹 사이트 또는 서비스
- ASP.NET Core 서비스
- Azure WebJob 서비스 

hello 연결된 서비스 기능 모든 필요한 hello 참조와 연결 코드 tooyour 프로젝트를 추가 및 구성 파일을 적절 하 게 수정 합니다. 

작업이 완료 되 면 hello **연결 된 서비스 추가** 설명서 hello 단계 필요한 toostart blob 저장소, 큐 및 테이블 사용을 자세히 보여 주는 대화 상자에 자동으로 표시 됩니다.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>TooAzure hello 연결 된 서비스를 사용 하 여 저장소 연결 대화 상자
1. Visual Studio에서 프로젝트 열기

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **연결 된 서비스** 노드를 선택 하 고 hello 상황에 맞는 메뉴에서 **연결 된 서비스 추가**합니다.
   
    ![Azure 연결된 서비스 추가](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. Hello에 **연결 된 서비스** 페이지에서 **Azure 저장소와 클라우드 저장소**합니다.
   
    ![Azure Storage 추가](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. Hello에 **Azure 저장소** 대화 상자, 기존 저장소 계정 선택 및 선택 **추가**합니다.
   
    저장소 계정 toocreate 해야 할 경우 toohello 다음 단계로 이동 합니다. 그렇지 않은 경우 6 toostep를 건너뜁니다.
    
    ![기존 저장소 계정 tooproject 추가](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate 저장소 계정: 
   
   1. 선택 **새 저장소 계정 만들기** hello hello 대화 상자 맨 아래에 있습니다.

   1. Hello 채울 **저장소 계정 만들기** 대화 상자를 닫고 선택 **만들기**합니다.
      
       ![새 Azure Storage 계정](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Hello 때 **Azure 저장소** 대화 상자가 표시 됩니다, 새 저장소 계정 hello hello 목록에 나타납니다. Hello 목록의 hello 새 저장소 계정을 선택 하 고 선택 **추가**합니다.

1. 저장소 연결된 서비스 hello 아래에 나타납니다. hello **서비스 참조** 프로젝트의 노드.
   
## <a name="how-your-project-is-modified"></a>프로젝트를 수정하는 방법
Hello 대화를 완료 하면 Visual Studio는 참조를 추가 하 고 특정 구성 파일을 수정 합니다. 그러면 특정 변경 내용이 hello hello 프로젝트 형식에 따라 달라 집니다. 

- ASP.NET 프로젝트 - [변경된 내용 – ASP.NET 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- ASP.NET Core 프로젝트 - [변경된 내용 – ASP.NET 5 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- 클라우드 서비스 프로젝트(웹 역할 및 작업자 역할) - [변경된 내용 – 클라우드 서비스 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- WebJob 프로젝트 - [변경된 내용 -WebJob 프로젝트](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>다음 단계
- [MSDN 포럼: Azure 저장소](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Microsoft Azure Storage 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)
- [Azure 저장소 설명서](https://docs.microsoft.com/azure/storage/)
