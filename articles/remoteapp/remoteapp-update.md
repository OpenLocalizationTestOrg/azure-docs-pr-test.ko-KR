---
title: "aaaUpdate Azure RemoteApp 컬렉션 | Microsoft Docs"
description: "자세한 내용은 방법 tooupdate Azure RemoteApp 컬렉션"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Azure RemoteApp에서 컬렉션 업데이트
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

한 번 때을 중지 해야 tooupdate hello 앱 또는 이미지가 Azure RemoteApp 컬렉션에 옵니다. Azure RemoteApp 구독, 클라우드 또는 하이브리드 컬렉션에 포함 된 hello 이미지 중 하나를 사용 하는 경우 쉽게 재설정할 수 있도록 모든 업데이트 자체를 Azure RemoteApp에서 처리 됩니다.

그러나 사용자 지정 이미지 (처음부터 작성 된 또는 우리의 이미지 중 하나를 수정 하 여 만든)을 사용 하는 경우 담당 하는 hello 이미지 및 응용 프로그램 유지 관리 합니다. 이미지 또는 내부 hello 앱 tooupdate를 필요 하면 필요한 toocreate hello 이미지 및 바꾸기 hello 기존 이미지의 업데이트 된 새 버전이이 새로운 업데이트 된 이미지를 사용 하 여 사용자 컬렉션에 있습니다.

그렇다면 컬렉션은 어떻게 업데이트할 수 있을까요? 방법은 상당히 간단합니다.

1. 컬렉션에서 사용한 hello 이미지를 업데이트 합니다. 필요한 모든 패치 또는 업데이트를 적용하고 새 이름으로 저장합니다.
2. [업로드](remoteapp-uploadimage.md) 또는 [가져올](remoteapp-image-on-azurevm.md) 이미지 tooRemoteApp 해당 합니다.
3. 이제 hello 모음 페이지에서 클릭 **업데이트**합니다.
4. Hello에서 hello 새 이미지를 선택 **템플릿 이미지** 목록입니다.
5. Hello 문제가 되는 부분은 다음과 같습니다-toodecide를 어떻게 필요 hello 컬렉션에 응용 프로그램 현재 사용 중인 모든 사용자와 toodeal 합니다. 선택 항목을 다음 hello를 사용할 수 있습니다.
   
   * **사용자에 게 hello 업데이트 후 60 분 제공**합니다. Hello 업데이트가 완료 되는 즉시 Azure RemoteApp의 작업 및 로그 오프 한 후 다시 로그인 toosave 인하 메시지 tooany 활성 사용자 표시 됩니다. 60분이 지난 후에도 로그오프하지 않은 모든 사용자는 자동으로 로그오프됩니다. 사용자는 즉시 다시 로그인할 수 있습니다.
   * **사용자를 즉시 로그아웃**. Hello 업데이트가 완료 되는 즉시 사용자 로그 오프 모든 경고 없이 자동으로 합니다. 이 옵션을 선택하면 사용자가 데이터를 잃을 수 있습니다. 그러나 toohello 앱 즉시 연결할 수 있습니다.
6. Hello, toostart hello 업데이트 확인 표시를 클릭 합니다.

