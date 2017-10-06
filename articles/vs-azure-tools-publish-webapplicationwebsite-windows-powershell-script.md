---
title: "aaaPublish-WebApplicationWebSite (Windows PowerShell 스크립트) | Microsoft Docs"
description: "웹 toopublish tooan Azure 웹 사이트 프로젝트 하는 방법에 대해 알아봅니다. 이 스크립트는 없는 경우 Azure 구독에서 hello 필요한 리소스를 만듭니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="e6534-104">Publish-WebApplicationWebSite (Windows PowerShell 스크립트)</span><span class="sxs-lookup"><span data-stu-id="e6534-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="e6534-105">구문</span><span class="sxs-lookup"><span data-stu-id="e6534-105">Syntax</span></span>
<span data-ttu-id="e6534-106">웹 프로젝트 tooan Azure 웹 사이트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="e6534-107">hello 스크립트 없는 경우 Azure 구독에 필요한 hello 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="e6534-108">구성</span><span class="sxs-lookup"><span data-stu-id="e6534-108">Configuration</span></span>
<span data-ttu-id="e6534-109">hello 경로 toohello는 JSON 구성 파일 hello 배포의 hello 세부 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="e6534-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e6534-110">Parameter</span></span> | <span data-ttu-id="e6534-111">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e6534-112">Aliases</span><span class="sxs-lookup"><span data-stu-id="e6534-112">Aliases</span></span> |<span data-ttu-id="e6534-113">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-113">none</span></span> |
| <span data-ttu-id="e6534-114">Required?</span><span class="sxs-lookup"><span data-stu-id="e6534-114">Required?</span></span> |<span data-ttu-id="e6534-115">true</span><span class="sxs-lookup"><span data-stu-id="e6534-115">true</span></span> |
| <span data-ttu-id="e6534-116">Position</span><span class="sxs-lookup"><span data-stu-id="e6534-116">Position</span></span> |<span data-ttu-id="e6534-117">named</span><span class="sxs-lookup"><span data-stu-id="e6534-117">named</span></span> |
| <span data-ttu-id="e6534-118">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-118">Default value</span></span> |<span data-ttu-id="e6534-119">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-119">none</span></span> |
| <span data-ttu-id="e6534-120">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="e6534-120">Accept pipeline input?</span></span> |<span data-ttu-id="e6534-121">false</span><span class="sxs-lookup"><span data-stu-id="e6534-121">false</span></span> |
| <span data-ttu-id="e6534-122">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="e6534-122">Accept wildcard characters?</span></span> |<span data-ttu-id="e6534-123">false</span><span class="sxs-lookup"><span data-stu-id="e6534-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="e6534-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="e6534-124">SubscriptionName</span></span>
<span data-ttu-id="e6534-125">hello toocreate hello 웹 사이트에 원하는 구독을 Azure의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="e6534-126">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e6534-126">Parameter</span></span> | <span data-ttu-id="e6534-127">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e6534-128">Aliases</span><span class="sxs-lookup"><span data-stu-id="e6534-128">Aliases</span></span> |<span data-ttu-id="e6534-129">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-129">none</span></span> |
| <span data-ttu-id="e6534-130">Required?</span><span class="sxs-lookup"><span data-stu-id="e6534-130">Required?</span></span> |<span data-ttu-id="e6534-131">false</span><span class="sxs-lookup"><span data-stu-id="e6534-131">false</span></span> |
| <span data-ttu-id="e6534-132">Position</span><span class="sxs-lookup"><span data-stu-id="e6534-132">Position</span></span> |<span data-ttu-id="e6534-133">named</span><span class="sxs-lookup"><span data-stu-id="e6534-133">named</span></span> |
| <span data-ttu-id="e6534-134">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-134">Default value</span></span> |<span data-ttu-id="e6534-135">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-135">none</span></span> |
| <span data-ttu-id="e6534-136">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="e6534-136">Accept pipeline input?</span></span> |<span data-ttu-id="e6534-137">false</span><span class="sxs-lookup"><span data-stu-id="e6534-137">false</span></span> |
| <span data-ttu-id="e6534-138">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="e6534-138">Accept wildcard characters?</span></span> |<span data-ttu-id="e6534-139">false</span><span class="sxs-lookup"><span data-stu-id="e6534-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="e6534-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="e6534-140">WebDeployPackage</span></span>
<span data-ttu-id="e6534-141">hello 경로 toohello 웹 배포 패키지 toopublish toohello 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="e6534-142">Visual Studio에서 hello 웹 게시 마법사를 사용 하 여이 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="e6534-143">자세한 내용은 [Azure 클라우드 서비스 및 ASP.NET으로 시작하기](http://go.microsoft.com/fwlink/p/?LinkID=623089)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6534-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="e6534-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e6534-144">Parameter</span></span> | <span data-ttu-id="e6534-145">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e6534-146">Aliases</span><span class="sxs-lookup"><span data-stu-id="e6534-146">Aliases</span></span> |<span data-ttu-id="e6534-147">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-147">none</span></span> |
| <span data-ttu-id="e6534-148">Required?</span><span class="sxs-lookup"><span data-stu-id="e6534-148">Required?</span></span> |<span data-ttu-id="e6534-149">false</span><span class="sxs-lookup"><span data-stu-id="e6534-149">false</span></span> |
| <span data-ttu-id="e6534-150">Position</span><span class="sxs-lookup"><span data-stu-id="e6534-150">Position</span></span> |<span data-ttu-id="e6534-151">named</span><span class="sxs-lookup"><span data-stu-id="e6534-151">named</span></span> |
| <span data-ttu-id="e6534-152">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-152">Default value</span></span> |<span data-ttu-id="e6534-153">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-153">none</span></span> |
| <span data-ttu-id="e6534-154">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="e6534-154">Accept pipeline input?</span></span> |<span data-ttu-id="e6534-155">false</span><span class="sxs-lookup"><span data-stu-id="e6534-155">false</span></span> |
| <span data-ttu-id="e6534-156">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="e6534-156">Accept wildcard characters?</span></span> |<span data-ttu-id="e6534-157">false</span><span class="sxs-lookup"><span data-stu-id="e6534-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="e6534-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="e6534-158">DatabaseServerPassword</span></span>
<span data-ttu-id="e6534-159">hello 사용자 이름 및 Azure의 hello SQL 데이터베이스에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="e6534-160">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e6534-160">Parameter</span></span> | <span data-ttu-id="e6534-161">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e6534-162">Aliases</span><span class="sxs-lookup"><span data-stu-id="e6534-162">Aliases</span></span> |<span data-ttu-id="e6534-163">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-163">none</span></span> |
| <span data-ttu-id="e6534-164">Required?</span><span class="sxs-lookup"><span data-stu-id="e6534-164">Required?</span></span> |<span data-ttu-id="e6534-165">false</span><span class="sxs-lookup"><span data-stu-id="e6534-165">false</span></span> |
| <span data-ttu-id="e6534-166">Position</span><span class="sxs-lookup"><span data-stu-id="e6534-166">Position</span></span> |<span data-ttu-id="e6534-167">named</span><span class="sxs-lookup"><span data-stu-id="e6534-167">named</span></span> |
| <span data-ttu-id="e6534-168">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-168">Default value</span></span> |<span data-ttu-id="e6534-169">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-169">none</span></span> |
| <span data-ttu-id="e6534-170">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="e6534-170">Accept pipeline input?</span></span> |<span data-ttu-id="e6534-171">false</span><span class="sxs-lookup"><span data-stu-id="e6534-171">false</span></span> |
| <span data-ttu-id="e6534-172">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="e6534-172">Accept wildcard characters?</span></span> |<span data-ttu-id="e6534-173">false</span><span class="sxs-lookup"><span data-stu-id="e6534-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="e6534-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="e6534-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="e6534-175">True 이면 hello 스크립트 toohello에서 메시지를 인쇄 출력 스트림에입니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="e6534-176">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e6534-176">Parameter</span></span> | <span data-ttu-id="e6534-177">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e6534-178">Aliases</span><span class="sxs-lookup"><span data-stu-id="e6534-178">Aliases</span></span> |<span data-ttu-id="e6534-179">없음</span><span class="sxs-lookup"><span data-stu-id="e6534-179">none</span></span> |
| <span data-ttu-id="e6534-180">Required?</span><span class="sxs-lookup"><span data-stu-id="e6534-180">Required?</span></span> |<span data-ttu-id="e6534-181">false</span><span class="sxs-lookup"><span data-stu-id="e6534-181">false</span></span> |
| <span data-ttu-id="e6534-182">Position</span><span class="sxs-lookup"><span data-stu-id="e6534-182">Position</span></span> |<span data-ttu-id="e6534-183">named</span><span class="sxs-lookup"><span data-stu-id="e6534-183">named</span></span> |
| <span data-ttu-id="e6534-184">기본값</span><span class="sxs-lookup"><span data-stu-id="e6534-184">Default value</span></span> |<span data-ttu-id="e6534-185">false</span><span class="sxs-lookup"><span data-stu-id="e6534-185">false</span></span> |
| <span data-ttu-id="e6534-186">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="e6534-186">Accept pipeline input?</span></span> |<span data-ttu-id="e6534-187">false</span><span class="sxs-lookup"><span data-stu-id="e6534-187">false</span></span> |
| <span data-ttu-id="e6534-188">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="e6534-188">Accept wildcard characters?</span></span> |<span data-ttu-id="e6534-189">false</span><span class="sxs-lookup"><span data-stu-id="e6534-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="e6534-190">설명</span><span class="sxs-lookup"><span data-stu-id="e6534-190">Remarks</span></span>
<span data-ttu-id="e6534-191">자세한 설명은 toouse hello 스크립트 toocreate 개발 및 테스트 환경을 참조 하는 방법에 대 한 [Windows PowerShell 스크립트를 사용 하 여 tooPublish tooDev 및 시험 환경](vs-azure-tools-publishing-using-powershell-scripts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="e6534-192">hello JSON 구성 파일의 배포 toobe 이란 hello 세부 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="e6534-193">Hello 이름과 hello 웹 사이트에 대 한 사용자 이름 등의 hello 프로젝트를 만들 때 지정한 hello 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="e6534-194">있는 경우 hello 데이터베이스 tooprovision도를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="e6534-195">hello 코드 다음 JSON 구성 파일을 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="e6534-196">배포 된 hello JSON 구성 파일 toochange를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="e6534-197">웹 사이트 섹션은 필수 이지만 hello 데이터베이스 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e6534-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6534-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6534-198">Next steps</span></span>
<span data-ttu-id="e6534-199">자세한 내용은 [Publish-WebApplicationVM(Windows PowerShell 스크립트)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="e6534-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

