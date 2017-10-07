---
title: "aaaPublish 응용 프로그램 tooindividual 사용자에 게는 Azure RemoteApp 컬렉션 (미리 보기) | Microsoft Docs"
description: "Azure RemoteApp에서 그룹에 따라 대신 앱 tooindividual 사용자를 게시할 수는 방법에 대해 알아봅니다."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Azure RemoteApp 컬렉션 (미리 보기)에 tooindividual 사용자가 응용 프로그램 게시
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

이 문서에서는 설명 어떻게 toopublish 응용 프로그램 tooindividual 사용자는 Azure RemoteApp 컬렉션에 있습니다. 이것이 Azure RemoteApp에서, 현재 비공개 미리 보기 및 사용 가능한 유일한 tooselect 조기 채택자 평가 목적에서 새로운 기능입니다.

Azure RemoteApp만 한 가지 방법은 응용 프로그램 게시를 사용 하는 원래: 관리자에 게 게시할 앱 hello 이미지에서 표시 tooall 사용자 hello 컬렉션에 예상 되 고 있습니다.

일반적인 시나리오는 tooinclude 단일에서 많은 응용 프로그램 이미지 및 순서 tooreduce 관리 비용이 증가 한 컬렉션을 배포 합니다. 종종 일부 응용 프로그램 관련 tooall 사용자-관리자 toopublish 앱 tooindividual 사용자 피드 해당 응용 프로그램에서 불필요 한 응용 프로그램 볼 하지 않는 방법을 합니다.

이제 Azure RemoteApp에서 현재 제한된 미리 보기 기능으로 가능합니다. 다음은 hello 새로운 기능에 대 한 간단한 요약이입니다.

1. 컬렉션은 두 가지 모드 중 하나로 설정할 수 있습니다.
   
   * hello 원래 컬렉션 모드에서는 컬렉션의 모든 사용자가 볼 수 있는 모든 게시 된 응용 프로그램입니다. 이 hello 기본 모드입니다.
   * hello 새 응용 프로그램 모드를 toothem 명시적으로 할당 된 응용 프로그램에 사용자만 볼
2. Hello 순간에 hello 적용 모드에만 사용할 수 있으며 Azure RemoteApp PowerShell cmdlet을 사용 합니다.
   
   * 때 hello 컬렉션에 사용자 할당 tooapplication 모드 설정 hello Azure 포털을 통해 관리할 수 없습니다. 사용자 할당은 toobe PowerShell cmdlet을 통해 관리 합니다.
3. 사용자는 데이터만 볼 hello 응용 프로그램은 toothem 직접 게시 합니다. 그러나 수 가능한 사용자 toolaunch hello 운영 체제에 직접 액세스 하 여 hello 이미지에서 사용할 수 있는 다른 응용 프로그램을 hello에 대 한 합니다.
   
   * 이 기능은 응용 프로그램의 보안 잠금 기능을 제공 하지 않습니다. 피드 hello 응용 프로그램의 표시 여부를 제한 하기만 합니다.
   * 응용 프로그램에서 tooisolate 사용자가 필요한 경우 toouse 분리 된 컬렉션에 대 한 해야 합니다.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>어떻게 tooget Azure RemoteApp PowerShell cmdlet
tootry hello 새 미리 보기 기능 toouse Azure PowerShell cmdlet을 필요 합니다. 현재 하지 가능한 toouse hello Azure 관리 포털 tooenable hello 새 응용 프로그램 게시 모드입니다.

첫째, 있어야 hello [Azure PowerShell 모듈](/powershell/azure/overview) 설치 합니다.

그런 다음 관리자 모드와 실행된 hello cmdlet을 다음의 hello PowerShell 콘솔을 시작 합니다.

        Add-AzureAccount

Azure 사용자 이름 및 암호를 묻는 메시지가 나타납니다. 로그인 한 후 Azure 구독에 대 한 Azure RemoteApp cmdlet 수 toorun 됩니다.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>어떻게 toocheck 모드는 컬렉션은
Hello 다음 cmdlet을 실행 합니다.

        Get-AzureRemoteAppCollection <collectionName>

![Hello 컬렉션 모드를 확인 합니다.](./media/remoteapp-perapp/araacllelvel.png)

hello AclLevel 속성 hello 다음 값을 가질 수 있습니다.

* 컬렉션: hello 원래 게시 모드입니다. 모든 사용자는 게시된 앱을 모두 볼 수 있습니다.
* 응용 프로그램: hello 새 게시 모드입니다. 사용자는 hello 앱만 게시 toothem 직접 표시 됩니다.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>어떻게 tooswitch tooapplication 게시 모드
Hello 다음 cmdlet을 실행 합니다.

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

응용 프로그램 게시 상태를 유지 됩니다: 처음에 모든 사용자는 hello 원래 게시 된 앱을 모두 표시 됩니다.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>어떻게 toolist 사용자가 특정 응용 프로그램을 볼 수 있는 사용자
Hello 다음 cmdlet을 실행 합니다.

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Hello 응용 프로그램을 볼 수 있는 모든 사용자를 나열 합니다.

참고: Get AzureRemoteAppProgram CollectionName를 실행 하 여 hello 응용 프로그램 별칭 (위의 hello 구문에서 "응용 프로그램 별칭" 라고 함)를 볼 수 <collectionName>합니다.

## <a name="how-tooassign-an-application-tooa-user"></a>어떻게 tooassign 응용 프로그램 tooa 사용자
Hello 다음 cmdlet을 실행 합니다.

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

hello 사용자는 이제 hello Azure RemoteApp 클라이언트에서 hello 응용 프로그램에 표시 하 고 수 tooconnect tooit 됩니다.

## <a name="how-tooremove-an-application-from-a-user"></a>어떻게 tooremove 사용자 로부터 응용 프로그램
Hello 다음 cmdlet을 실행 합니다.

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>사용자 의견 제공
이 미리 보기 기능에 대한 제안과 의견에 감사합니다. Hello 정보를 입력 하세요 [설문 조사](http://www.instant.ly/s/FDdrb) toolet 어떻게 생각 알려주세요.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>기회 tootry hello 미리 보기 기능이 없 었?
경우 있습니다 하지 참여 hello 미리 보기에 아직를 사용 하 여이 [설문 조사](http://www.instant.ly/s/AY83p) toorequest 액세스 합니다.

