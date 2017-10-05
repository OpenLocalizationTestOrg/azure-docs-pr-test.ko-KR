---
title: "Publish-WebApplicationWebSite(Windows PowerShell 스크립트) | Microsoft Docs"
description: "Azure 웹 사이트에 웹 프로젝트를 게시하는 방법에 대해 알아봅니다. 없는 경우 이 스크립트는 Azure 구독에 필요한 리소스를 만듭니다."
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
ms.openlocfilehash: 07d21b7ce6cd8aee1cff704d316e7a2ca8c00437
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="55867-104">Publish-WebApplicationWebSite (Windows PowerShell 스크립트)</span><span class="sxs-lookup"><span data-stu-id="55867-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="55867-105">구문</span><span class="sxs-lookup"><span data-stu-id="55867-105">Syntax</span></span>
<span data-ttu-id="55867-106">Azure 웹 사이트에 웹 프로젝트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="55867-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="55867-107">없는 경우 스크립트는 Azure 구독에 필요한 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55867-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="55867-108">구성</span><span class="sxs-lookup"><span data-stu-id="55867-108">Configuration</span></span>
<span data-ttu-id="55867-109">배포의 세부 정보를 설명하는 JSON 구성 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="55867-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="55867-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="55867-110">Parameter</span></span> | <span data-ttu-id="55867-111">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="55867-112">Aliases</span><span class="sxs-lookup"><span data-stu-id="55867-112">Aliases</span></span> |<span data-ttu-id="55867-113">없음</span><span class="sxs-lookup"><span data-stu-id="55867-113">none</span></span> |
| <span data-ttu-id="55867-114">Required?</span><span class="sxs-lookup"><span data-stu-id="55867-114">Required?</span></span> |<span data-ttu-id="55867-115">true</span><span class="sxs-lookup"><span data-stu-id="55867-115">true</span></span> |
| <span data-ttu-id="55867-116">Position</span><span class="sxs-lookup"><span data-stu-id="55867-116">Position</span></span> |<span data-ttu-id="55867-117">named</span><span class="sxs-lookup"><span data-stu-id="55867-117">named</span></span> |
| <span data-ttu-id="55867-118">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-118">Default value</span></span> |<span data-ttu-id="55867-119">없음</span><span class="sxs-lookup"><span data-stu-id="55867-119">none</span></span> |
| <span data-ttu-id="55867-120">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="55867-120">Accept pipeline input?</span></span> |<span data-ttu-id="55867-121">false</span><span class="sxs-lookup"><span data-stu-id="55867-121">false</span></span> |
| <span data-ttu-id="55867-122">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="55867-122">Accept wildcard characters?</span></span> |<span data-ttu-id="55867-123">false</span><span class="sxs-lookup"><span data-stu-id="55867-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="55867-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="55867-124">SubscriptionName</span></span>
<span data-ttu-id="55867-125">웹사이트를 만들려는 Azure 구독의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="55867-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="55867-126">매개 변수</span><span class="sxs-lookup"><span data-stu-id="55867-126">Parameter</span></span> | <span data-ttu-id="55867-127">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="55867-128">Aliases</span><span class="sxs-lookup"><span data-stu-id="55867-128">Aliases</span></span> |<span data-ttu-id="55867-129">없음</span><span class="sxs-lookup"><span data-stu-id="55867-129">none</span></span> |
| <span data-ttu-id="55867-130">Required?</span><span class="sxs-lookup"><span data-stu-id="55867-130">Required?</span></span> |<span data-ttu-id="55867-131">false</span><span class="sxs-lookup"><span data-stu-id="55867-131">false</span></span> |
| <span data-ttu-id="55867-132">Position</span><span class="sxs-lookup"><span data-stu-id="55867-132">Position</span></span> |<span data-ttu-id="55867-133">named</span><span class="sxs-lookup"><span data-stu-id="55867-133">named</span></span> |
| <span data-ttu-id="55867-134">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-134">Default value</span></span> |<span data-ttu-id="55867-135">없음</span><span class="sxs-lookup"><span data-stu-id="55867-135">none</span></span> |
| <span data-ttu-id="55867-136">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="55867-136">Accept pipeline input?</span></span> |<span data-ttu-id="55867-137">false</span><span class="sxs-lookup"><span data-stu-id="55867-137">false</span></span> |
| <span data-ttu-id="55867-138">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="55867-138">Accept wildcard characters?</span></span> |<span data-ttu-id="55867-139">false</span><span class="sxs-lookup"><span data-stu-id="55867-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="55867-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="55867-140">WebDeployPackage</span></span>
<span data-ttu-id="55867-141">웹 사이트에 게시하는 웹 배포 패키지에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="55867-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="55867-142">Visual Studio에서 웹 게시 마법사를 사용하여 이 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55867-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="55867-143">자세한 내용은 [Azure 클라우드 서비스 및 ASP.NET으로 시작하기](http://go.microsoft.com/fwlink/p/?LinkID=623089)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55867-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="55867-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="55867-144">Parameter</span></span> | <span data-ttu-id="55867-145">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="55867-146">Aliases</span><span class="sxs-lookup"><span data-stu-id="55867-146">Aliases</span></span> |<span data-ttu-id="55867-147">없음</span><span class="sxs-lookup"><span data-stu-id="55867-147">none</span></span> |
| <span data-ttu-id="55867-148">Required?</span><span class="sxs-lookup"><span data-stu-id="55867-148">Required?</span></span> |<span data-ttu-id="55867-149">false</span><span class="sxs-lookup"><span data-stu-id="55867-149">false</span></span> |
| <span data-ttu-id="55867-150">Position</span><span class="sxs-lookup"><span data-stu-id="55867-150">Position</span></span> |<span data-ttu-id="55867-151">named</span><span class="sxs-lookup"><span data-stu-id="55867-151">named</span></span> |
| <span data-ttu-id="55867-152">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-152">Default value</span></span> |<span data-ttu-id="55867-153">없음</span><span class="sxs-lookup"><span data-stu-id="55867-153">none</span></span> |
| <span data-ttu-id="55867-154">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="55867-154">Accept pipeline input?</span></span> |<span data-ttu-id="55867-155">false</span><span class="sxs-lookup"><span data-stu-id="55867-155">false</span></span> |
| <span data-ttu-id="55867-156">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="55867-156">Accept wildcard characters?</span></span> |<span data-ttu-id="55867-157">false</span><span class="sxs-lookup"><span data-stu-id="55867-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="55867-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="55867-158">DatabaseServerPassword</span></span>
<span data-ttu-id="55867-159">Azure에서 SQL 데이터베이스의 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="55867-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="55867-160">매개 변수</span><span class="sxs-lookup"><span data-stu-id="55867-160">Parameter</span></span> | <span data-ttu-id="55867-161">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="55867-162">Aliases</span><span class="sxs-lookup"><span data-stu-id="55867-162">Aliases</span></span> |<span data-ttu-id="55867-163">없음</span><span class="sxs-lookup"><span data-stu-id="55867-163">none</span></span> |
| <span data-ttu-id="55867-164">Required?</span><span class="sxs-lookup"><span data-stu-id="55867-164">Required?</span></span> |<span data-ttu-id="55867-165">false</span><span class="sxs-lookup"><span data-stu-id="55867-165">false</span></span> |
| <span data-ttu-id="55867-166">Position</span><span class="sxs-lookup"><span data-stu-id="55867-166">Position</span></span> |<span data-ttu-id="55867-167">named</span><span class="sxs-lookup"><span data-stu-id="55867-167">named</span></span> |
| <span data-ttu-id="55867-168">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-168">Default value</span></span> |<span data-ttu-id="55867-169">없음</span><span class="sxs-lookup"><span data-stu-id="55867-169">none</span></span> |
| <span data-ttu-id="55867-170">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="55867-170">Accept pipeline input?</span></span> |<span data-ttu-id="55867-171">false</span><span class="sxs-lookup"><span data-stu-id="55867-171">false</span></span> |
| <span data-ttu-id="55867-172">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="55867-172">Accept wildcard characters?</span></span> |<span data-ttu-id="55867-173">false</span><span class="sxs-lookup"><span data-stu-id="55867-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="55867-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="55867-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="55867-175">True이면 스크립트에서 출력 스트림으로 메시지를 프린트합니다.</span><span class="sxs-lookup"><span data-stu-id="55867-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="55867-176">매개 변수</span><span class="sxs-lookup"><span data-stu-id="55867-176">Parameter</span></span> | <span data-ttu-id="55867-177">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="55867-178">Aliases</span><span class="sxs-lookup"><span data-stu-id="55867-178">Aliases</span></span> |<span data-ttu-id="55867-179">없음</span><span class="sxs-lookup"><span data-stu-id="55867-179">none</span></span> |
| <span data-ttu-id="55867-180">Required?</span><span class="sxs-lookup"><span data-stu-id="55867-180">Required?</span></span> |<span data-ttu-id="55867-181">false</span><span class="sxs-lookup"><span data-stu-id="55867-181">false</span></span> |
| <span data-ttu-id="55867-182">Position</span><span class="sxs-lookup"><span data-stu-id="55867-182">Position</span></span> |<span data-ttu-id="55867-183">named</span><span class="sxs-lookup"><span data-stu-id="55867-183">named</span></span> |
| <span data-ttu-id="55867-184">기본값</span><span class="sxs-lookup"><span data-stu-id="55867-184">Default value</span></span> |<span data-ttu-id="55867-185">false</span><span class="sxs-lookup"><span data-stu-id="55867-185">false</span></span> |
| <span data-ttu-id="55867-186">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="55867-186">Accept pipeline input?</span></span> |<span data-ttu-id="55867-187">false</span><span class="sxs-lookup"><span data-stu-id="55867-187">false</span></span> |
| <span data-ttu-id="55867-188">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="55867-188">Accept wildcard characters?</span></span> |<span data-ttu-id="55867-189">false</span><span class="sxs-lookup"><span data-stu-id="55867-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="55867-190">설명</span><span class="sxs-lookup"><span data-stu-id="55867-190">Remarks</span></span>
<span data-ttu-id="55867-191">스크립트를 사용하여 개발 및 테스트 환경을 만드는 방법에 대한 전체 설명은 [Windows PowerShell 스크립트를 사용하여 개발 및 테스트 환경에 게시](vs-azure-tools-publishing-using-powershell-scripts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55867-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="55867-192">JSON 구성 파일은 배포될 내용의 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55867-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="55867-193">해당 웹 사이트의 이름 및 사용자 이름과 같은 프로젝트를 만들 때 지정된 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="55867-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="55867-194">있는 경우 프로비전할 새 데이터베이스도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="55867-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="55867-195">다음 코드에서는 JSON 구성 파일을 예로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="55867-195">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="55867-196">배포된 내용을 변경하도록 JSON 구성 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55867-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="55867-197">웹 사이트 섹션은 필수이지만 데이터 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="55867-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55867-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55867-198">Next steps</span></span>
<span data-ttu-id="55867-199">자세한 내용은 [Publish-WebApplicationVM(Windows PowerShell 스크립트)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="55867-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

