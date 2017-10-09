---
title: "Visual Studio와 함께 사설 Azure 클라우드에 aaaAccessing | Microsoft Docs"
description: "Tooaccess 사설 Visual Studio를 사용 하 여 리소스를 클라우드 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="ddc2f-103">Visual Studio로 사설 Azure 클라우드에 액세스</span><span class="sxs-lookup"><span data-stu-id="ddc2f-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="ddc2f-104">기본적으로 Visual Studio는 공용 Azure 클라우드 REST 끝점을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="ddc2f-105">이 항목에서는 방법을 toouse 개인 클라우드 설명의 인증서 tooaccess-및 상호 작용-Visual Studio에서 사설 클라우드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="ddc2f-106">Visual Studio에서 tooaccess 사설 Azure 클라우드</span><span class="sxs-lookup"><span data-stu-id="ddc2f-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="ddc2f-107">Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885) hello 사설 클라우드에 대 한 게시 설정 파일을 다운로드 하거나 게시 설정 파일에 대 한 관리자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="ddc2f-108">공용 버전 Azure의 hello에서 이것이 링크 toodownload hello [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="ddc2f-109">(hello 다운로드 한 파일의 확장명이 해야 `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="ddc2f-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="ddc2f-110">Visual Studio 열기</span><span class="sxs-lookup"><span data-stu-id="ddc2f-110">Open Visual Studio</span></span>

1. <span data-ttu-id="ddc2f-111">**서버 탐색기**를 마우스 오른쪽 단추로 클릭 hello **Azure** 노드 hello 상황에 맞는 메뉴에서 **구독 관리 및 필터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![구독 명령 관리](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="ddc2f-113">Hello에 **Microsoft Azure 구독 관리** 대화 상자에서 선택 hello **인증서** 탭을 선택한 다음 선택 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Azure 인증서 가져오기](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="ddc2f-115">Hello에 **Microsoft Azure 구독 가져오기** 대화 상자에서 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![찾아보기 단추 hello Microsoft Azure 구독 가져오기 대화 상자에서](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="ddc2f-117">Hello에 **열려** 대화 상자에서 디렉터리 위치 하면 저장 된 hello 게시 설정 파일 선택 hello 파일을 선택한 다음 찾아보기 toohello **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Hello 게시 설정 파일 선택](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="ddc2f-119">때 toohello 반환 **Microsoft Azure 구독 가져오기** 대화 상자에서 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Hello 게시 설정 파일 가져오기](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="ddc2f-121">hello 인증서 hello 게시 설정 파일에서 Visual Studio로 가져오며 이제 사설 클라우드 리소스 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="ddc2f-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddc2f-122">Next steps</span></span>
- [<span data-ttu-id="ddc2f-123">게시 tooan Visual Studio에서 Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="ddc2f-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="ddc2f-124">[방법: 게시 설정 및 구독 정보를 다운로드 및 가져오기](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="ddc2f-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
