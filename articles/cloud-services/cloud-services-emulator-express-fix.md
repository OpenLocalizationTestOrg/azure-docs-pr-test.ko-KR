---
title: "aaaSetup emulator express는 Visual Studio에서 클라우드 서비스 응용 프로그램을 toodebug | Microsoft Docs"
description: "Tooinstall Visual Studio에서 Emulator Express는 c + + 재배포 가능 tooenable hello 하는 방법을 설명 합니다."
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="00fba-103">Emulator Express toodebug 클라우드 서비스 응용 프로그램을 사용 하 여 VS 2017에</span><span class="sxs-lookup"><span data-stu-id="00fba-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="00fba-104">이 문서에서는 설명 어떻게 toouse Emulator Express toodebug 클라우드 서비스에서에서 응용 프로그램 VS 2017 합니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="00fba-105">배경 상황</span><span class="sxs-lookup"><span data-stu-id="00fba-105">Background context</span></span>
<span data-ttu-id="00fba-106">Emulator Express는 Visual Studio에서 클라우드 서비스 웹 및 작업자 역할을 디버그하는 데 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="00fba-107">이 설정은 hello 클라우드 서비스 프로젝트 속성 페이지에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![프로젝트 속성 열기][0]

![Emulator Express는 기본으로 선택되어 있습니다.][1]

<span data-ttu-id="00fba-110">hello [Visual c + + 재배포 가능 패키지] [ Visual C++ Redistributable] express 에뮬레이터에서 Visual Studio는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="00fba-111">현재 hello Azure 워크 로드로 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="00fba-112">F5 시 제스처 toodebug 클라우드 서비스 응용 프로그램, Visual Studio는 tooinstall이 구성이 요소 확인 및 디버깅을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![C++ 재배포 가능 패키지 설치 프롬프트][2]

<span data-ttu-id="00fba-114">예 tooinstall c + + 재배포 가능 패키지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-114">Click Yes tooinstall C++ Redistributable.</span></span>

![C++ 재배포 가능 패키지 설치][3]

<span data-ttu-id="00fba-116">Toolaunch 디버깅 세션 다시 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-116">Press F5 again toolaunch debugging sessions.</span></span>

![디버그 시작][4]

![디버그 성공][5]

> <span data-ttu-id="00fba-119">참고: C++ 재배포 가능 패키지는 한 번만 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="00fba-120">이전 버전의 Azure SDK에서 업그레이드했으며 Emulator Express를 설치한 경우이 문제가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="00fba-121">수동 해결</span><span class="sxs-lookup"><span data-stu-id="00fba-121">Manual workaround</span></span>
<span data-ttu-id="00fba-122">Hello를 설치할 수도 있습니다 [Visual c + + 재배포 가능 패키지] [ Visual C++ Redistributable] 수동으로 방법 Visual Studio에 설치 되어 시스템 때 동일한 효과 적용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00fba-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="00fba-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="00fba-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="00fba-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="00fba-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="00fba-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00fba-125">Next Steps</span></span>
<span data-ttu-id="00fba-126">에 대 한 자세한 toodebug Azure 계산 에뮬레이터를 사용 하 여 Visual Studio에서 클라우드 서비스 응용 프로그램: [toorun Emulator Express를 사용 하 고 로컬 컴퓨터에서 클라우드 서비스 디버그][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="00fba-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
