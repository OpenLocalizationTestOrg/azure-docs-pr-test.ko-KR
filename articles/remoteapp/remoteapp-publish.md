---
title: "Azure RemoteApp에 앱 aaaPublish | Microsoft Docs"
description: "자세한 내용은 방법 toopublish 응용 프로그램 및 Azure RemoteApp에서 리소스입니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>어떻게 toopublish RemoteApp에서 응용 프로그램
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

RemoteApp 컬렉션을 만든 후 toopublish hello 앱 이나 사용자를 위해 사용할 수 있는 toomake 되도록 리소스 필요 합니다. hello 구독에서 제공 하는 템플릿 이미지를 하나만 몇 가지 앱-기본적으로 게시 tooshare hello 다른 앱, toopublish 해야 해당 합니다.

> [!NOTE]
> 응용 프로그램 tooupdate 필요 한가요? 너무 해야[업데이트 hello 이미지](remoteapp-update.md) 첫 번째입니다.
> 
> 

Hello에 **게시** hello 포털에서 탭을 클릭 **게시**합니다. 템플릿 이미지의에서 응용 프로그램을 추가 하거나 **시작** 메뉴 하거나 hello 경로 toowhere hello 앱 hello 템플릿 이미지에 설치 되어 제공 합니다. Hello에서 tooadd를 선택 하면 **시작** 메뉴 hello 앱 toopublish hello 목록에서 선택 합니다. Tooprovide hello 경로 toohello 앱을 선택 하면 hello 경로 toohello 앱과 hello 앱에 대 한 이름을 입력 합니다. 대신 hello 경로-예를 들어, "%systemdrive%"의 변수를 사용 하 여 "c:\"합니다.

> [!NOTE]
> Tooadd hello에서 응용 프로그램을 원하는 경우 **시작** 메뉴 toohave 필요 *해당 앱 toohello 추가 **시작** 템플릿 이미지에 대 한 메뉴입니다.* 그렇지 않은 경우 RemoteApp 볼 기능 *은* hello에 **시작** 메뉴 하 고 혼동 됩니다. 
> 
> hello toomake 있는지 앱이 **시작** 메뉴 바로 가기 파일- **.lnk** -hello %systemdrive%\ProgramData\Microsoft\Windows\Start 메뉴 \ 프로그램 폴더입니다.
> 
> Tooadd hello 앱 toohello 잊은 경우 **시작** hello 템플릿을 만들 때 메뉴 tooadd hello 경로 toohello 앱을 선택 합니다. (또는 템플릿 이미지를 다시 만듭니다. 하지만 작업이 훨씬 더 복잡 합니다.)
> 
> 

