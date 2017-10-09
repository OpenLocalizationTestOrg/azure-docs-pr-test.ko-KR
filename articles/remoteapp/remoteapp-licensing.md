---
title: "aaaAzure RemoteApp 라이선스 | Microsoft Docs"
description: "Azure RemoteApp의 라이선스 작동 방식에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Azure RemoteApp의 라이선스 작동 방식
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

따라서 프로그램 서식 파일을 만든 사용자가 Azure RemoteApp 서비스를 설정 및 준비 toopublish 앱 tooyour 사용자가 합니다. 하지만 여전히 아웃 한 마지막 작업 toofigure: 라이선스입니다. 방금 RemoteApp을 통해 공유 하는 hello 앱에 대 한 RemoteApp에 대 한 라이선스 작업은 어떻게 하나요?

RemoteApp에는 Windows 라이선스 또는 원격 데스크톱 CAL이 필요하지 않습니다. 구독 자체 RemoteApp 쪽 hello 담당합니다. (Hello의 hello 세부 정보를 확인해 보세요 [가격 책정 모델](https://azure.microsoft.com/pricing/details/remoteapp).)

구독에 포함 된 hello 이미지 중 하나를 사용 하는 경우 한 별도 라이선스가 필요 없이 해당 이미지에 설치 하는 hello 앱 중 하나를 공유할 수 있습니다. 예를 들어 hello Windows Server 2012 R2 템플릿 이미지 toobuild 컬렉션을 사용 하면 System Center Endpoint Protection 사용자와 공유할 수 있습니다. hello만 예외 toothis 규칙은 Office 365 ProPlus, 별도 구독을 요구 하 고 Office 2013 프로덕션 컬렉션에서 공유할 수 없습니다.

RemoteApp과 함께 제공 된 toouse hello Office 365 템플릿 이미지를 원하는 경우이 있어야는 *기존* Office 365 ProPlus 계획 합니다. hello 사용자 지정 템플릿을 사용 하 여 게시 하는 모든 Office 365 앱에도 마찬가지입니다. 사용자 고유의 구독과 tooactivate hello 앱 해야합니다. 이 내용은 평가판 및 유료 구독 둘 다에 적용됩니다. Hello 평가판 시 toouse hello Office 365 템플릿 이미지를 원하는 경우 *구독이 아직 없는 및*, 너무 toohello Office 365 페이지로 이동[등록](https://go.microsoft.com/fwlink/p/?LinkID=403802) 평가판 구독에 대 한 합니다. 자세한 내용은 [RemoteApp과 Office가 함께 작동하는 방식](remoteapp-o365.md) 을 참조하세요.

Hello 평가 기간 중 tooget Office 365 평가판 구독을 않도록 하는 경우 RemoteApp과 함께 제공 되는 hello Office 2013 Professional 더하기 템플릿 이미지를 사용 합니다. 이 템플릿 이미지는 30일 동안만 사용할 수 있으며 유료 컬렉션으로 변환할 수 없습니다.

다른 앱에 대 한 toomake hello 라이선스 tooshare hello 앱 한지 확인 해야 합니다.

참 합리적이지 않은가요? Tooshare 자격이 합법적으로 모든 앱을 게시할 수 있습니다. Toomake 실제로 선택 되어 있는지 필요 하 고 권한을 부여 받은 tooshare 프로그램입니다.

클라우드 컬렉션의 CAL 또는 볼륨 라이선스 계약은 사용할 수 없습니다. 하면 *수* 사무실) (제외 하이브리드 컬렉션의 볼륨 라이선스 계약 tooactivate 응용 프로그램을 사용 합니다. Hello 볼륨 라이선스 미디어에서에서 이미지 서식 파일에 해당 하는 tooinstall을 하기만 하면 됩니다. 원격 데스크톱 환경에서 응용 프로그램 공급 업체 tooinstall 라이선스 hello에서에서 hello 정보에 따라 합니다.

