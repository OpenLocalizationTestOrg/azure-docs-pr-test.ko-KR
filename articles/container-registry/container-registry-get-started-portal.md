---
title: "aaaCreate 개인 Docker 레지스트리-Azure 포털 | Microsoft Docs"
description: "만들기 및 관리 사설 Docker 컨테이너 레지스트리 Azure 포털 hello로 시작."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 개인 Docker 컨테이너 등록 만들기
Azure 포털 toocreate 컨테이너 레지스트리 hello를 사용 하 하 고 해당 설정을 관리 키를 누릅니다. 또한 생성 하 고 컨테이너 레지스트리에 hello를 사용 하 여 관리 수 [Azure CLI 2.0 명령은](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) 또는 프로그래밍 방식으로 컨테이너 레지스트리 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).

배경 및 개념에 대 한 참조 [개요 hello](container-registry-intro.md)합니다.

## <a name="create-a-container-registry"></a>컨테이너 레지스트리 만들기
1. Hello에 [Azure 포털](https://portal.azure.com), 클릭 **+ 새로 만들기**합니다.
2. 에 대 한 검색 hello 마켓플레이스 **Azure 컨테이너 레지스트리**합니다.
3. 게시자가 **Microsoft**인 **Azure 컨테이너 레지스트리**를 선택합니다.
    ![Azure Marketplace의 컨테이너 레지스트리 서비스](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. **만들기**를 클릭합니다. hello **Azure 컨테이너 레지스트리** 블레이드 나타납니다.

    ![컨테이너 레지스트리 설정](./media/container-registry-get-started-portal/container-registry-settings.png)
5. Hello에 **Azure 컨테이너 레지스트리** 블레이드에서 hello 다음 정보를 입력 합니다. 완료하면 **만들기**를 클릭합니다.

    a. **레지스트리 이름**: 특정 레지스트리에 대한 전역적으로 고유한 최상위 도메인 이름입니다. 이 예제에서는 hello 레지스트리 이름이 *myRegistry01*, 되지만 대신 사용자 고유의의 고유 이름입니다. hello 이름에는 문자와 숫자만 포함할 수 있습니다.

    b. **리소스 그룹**: 기존 선택 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다.

    c. **위치**: 여기서 hello 서비스는 Azure 데이터 센터 위치를 선택 [사용 가능한](https://azure.microsoft.com/regions/services/)와 같은 **미국 중남부**합니다.

    d. **관리: 사용자**:는 관리자 사용자 tooaccess hello 레지스트리를 사용 하도록 설정 합니다. Hello 레지스트리를 만든 후이 설정을 변경할 수 있습니다.

      > [!IMPORTANT]
      > 또한 tooproviding에 admin 사용자 계정을 통해 액세스할 컨테이너 레지스트리에 Azure Active Directory 서비스 사용자에 의해 지원 되는 인증을 지원 합니다. 자세한 내용 및 고려 사항은 [컨테이너 레지스트리로 인증](container-registry-authentication.md)을 참조하세요.
      >

    e. **저장소 계정**: 기본 설정 toocreate hello를 사용 하 여 한 [저장소 계정](../storage/common/storage-introduction.md), hello에서 기존 저장소 계정을 선택 하거나 동일한 위치입니다. Premium Storage는 현재 지원되지 않습니다.

## <a name="manage-registry-settings"></a>레지스트리 설정 관리
Hello 레지스트리를 만든 후 hello 레지스트리 설정의 찾을 hello부터 시작 하 여 **컨테이너 레지스트리에** 블레이드 hello 포털에서입니다. 예를 들어 hello 설정을 toolog tooyour 레지스트리에 할 수 있습니다 또는 tooenable 하거나 hello 관리: 사용자를 사용 하지 않도록 설정할 수 있습니다.

1. Hello에 **컨테이너 레지스트리에** 블레이드에서 레지스트리 hello 이름을 클릭 합니다.

    ![컨테이너 레지스트리 블레이드](./media/container-registry-get-started-portal/container-registry-blade.png)
2. toomanage 액세스 설정을 클릭 **선택 키**합니다.

    ![컨테이너 레지스트리 액세스](./media/container-registry-get-started-portal/container-registry-access.png)
3. 다음 설정을 참고 hello:

   * **로그인 서버** -toolog를 사용 하 여 toohello 레지스트리에 hello 정규화 된 이름입니다. 이 예제에서는 `myregistry01.azurecr.io`입니다.
   * **관리: 사용자** -tooenable 설정/해제 하거나 hello 레지스트리 관리자 사용자 계정을 사용 하지 않도록 설정 합니다.
   * **사용자 이름** 및 **암호** -(설정 된 경우) hello admin 사용자 계정의 자격 증명을 hello toohello 레지스트리에 toolog를 사용할 수 있습니다. 필요에 따라 hello 암호를 다시 생성할 수 있습니다. 다른 암호 hello를 다시 생성 하는 동안에 하나의 암호를 사용 하 여 연결 toohello 레지스트리 유지 관리할 수 있도록 두 개의 암호가 생성 됩니다. 서비스 사용자와 tooauthenticate 대신 참조 [개인 Docker 컨테이너 레지스트리로 인증](container-registry-authentication.md)합니다.

## <a name="next-steps"></a>다음 단계
* [Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제](container-registry-get-started-docker-cli.md)
