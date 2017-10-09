---
title: "Azure RemoteApp 이미지 aaaCreate | Microsoft Docs"
description: "Azure RemoteApp에 대 한 이미지를 만드는 데 사용할 수 있는 hello 옵션에 알아보기"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Azure RemoteApp 이미지 만들기
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp 사용자와 공유 하는 이미지 toohold hello 앱을 사용 합니다. (म 이미지 걸리고 hello 사용자 Azure RemoteApp에 로그인 할 때 액세스의 toocreate Vm-를 사용 합니다.) 응용 프로그램을 선택 하 여 Azure RemoteApp 컬렉션 toocreate 클라우드 또는 하이브리드, 먼저 설치 된 해당 응용 프로그램을 사용 하 여 이미지 만들기 합니다. 그런 다음 해당 이미지를 사용 하는 컬렉션을 만듭니다, 그리고 toohello 컬렉션, 사용자를 할당 및 toothose 사용자가 앱을 게시 합니다.

이미지를 만들거나 사용하기 위한 다양한 옵션이 있습니다. 기본 hello [요구 사항](remoteapp-imagereqs.md) 이미지는 Windows Server 2012 r 2를 실행 hello RDSH 원격 데스크톱 세션 호스트 () 역할이 설치 되어 있고 하 합니다. 이미지를 얻는 방법이 흥미롭습니다.

Hello tooimages 상태가 되 면 다음 옵션을 사용할 수 있습니다.

* [Azure 가상 컴퓨터를 기반으로 이미지](remoteapp-image-on-azurevm.md)를 가져와서 사용할 수 있습니다. 이 방법은 사용자 지정 설정이 필요한 LOB(기간 업무) 앱에 적합합니다. Hello 앱에 대 한 이미지 toowork hello를 사용자 지정할 수 있습니다.
* [사용자 지정 이미지를 만든 후 업로드](remoteapp-create-custom-image.md)할 수 있습니다. 이 방법은 온-프레미스 원격 데스크톱 서비스 배포에 사용할 이미지가 이미 있는 경우에 유용합니다.
* Hello 중 하나를 사용 [템플릿 이미지](remoteapp-images.md) RemoteApp 구독에 포함 합니다. 이러한 이미지를 만든 및 hello a p p 팀에서 유지 관리을 일부 표준 응용 프로그램 (예: hello Office 제품군) tooyour 사용할 수 있는 사용자를 만들 수 있는지를 포함 합니다. Note 프로덕션 설정에서 해당만 hello Office 365 Pro Plus 이미지를 사용할 수 있습니다.

이미지를 가져오는 위치 또는 만드는 방법에 관계 없이 toomake hello 이해 해도 됩니다 [응용 프로그램 요구 사항](remoteapp-appreqs.md) tooensure 앱 RemoteApp에서 잘 작동 합니다. 그렇다면 hello 다음 단계는 toocreate는 [클라우드](remoteapp-create-cloud-deployment.md) 또는 [하이브리드](remoteapp-create-hybrid-deployment.md) 컬렉션입니다.

