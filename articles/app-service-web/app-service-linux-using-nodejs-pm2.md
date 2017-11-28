---
title: "Linux에서 Azure 웹 앱에서 Node.js 용 aaaUsing 오후 2 구성 | Microsoft Docs"
description: "Linux의 Azure Web App에서 Node.js용 PM2 구성 사용"
keywords: "azure app service, 웹앱, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="2b762-104">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="2b762-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="2b762-105">Linux에서 Azure 웹 앱에 대 한 응용 프로그램 스택 tooNode.js hello로 설정 하면 메시지가 hello 옵션 tooset Node.js 시작 파일 hello 다음 이미지에에서 나와 있는 것 처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Node.js 시작 파일 설정][1]

<span data-ttu-id="2b762-107">이 작업을 수행 하는 hello의 하나 옵션 toodo를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="2b762-108">Node.js 앱에 대 한 시작 스크립트 hello 지정 (예: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="2b762-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="2b762-109">Node.js 앱에 대 한 hello 오후 2 구성 파일 toouse 지정 (예: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="2b762-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2b762-110">특정 파일이 수정 되 면 자동으로 Node.js 프로세스 toorestart 하려면 hello 오후 2 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="2b762-111">그러지 않으면 응용 프로그램은 변경 알림의 받을 때(예: 응용 프로그램 코드가 변경될 때) 다시 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="2b762-112">Node.js hello를 확인할 수 있습니다 [파일 문서](http://pm2.keymetrics.io/docs/usage/application-declaration/) 옵션 hello 모든 되지만 process.json 파일로 사용의 예:</span><span class="sxs-lookup"><span data-stu-id="2b762-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="2b762-113">이 구성에서 중요 한 사항이 toonote가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="2b762-114">hello "스크립트" 속성 응용 프로그램의 시작 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="2b762-115">hello "인스턴스" 속성 hello 노드 프로세스 toolaunch의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="2b762-116">것이 좋습니다 toomaximize 여러 개의 코어가 있는 대규모 Vm에서 응용 프로그램을 실행 하는 경우 여기에 값을 높게 설정 하 여 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="2b762-117">변경 될 때 원하는 toorestart hello 노드 프로세스에 대 한 모든 파일을 지정 하는 배열 "감시" hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="2b762-118">"Watch_options" hello, 현재 해야 "usePolling" toospecify true로 응용 프로그램 콘텐츠 탑재 된 hello 방식 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2b762-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b762-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b762-119">Next steps</span></span>
* [<span data-ttu-id="2b762-120">Linux에서 Azure Web App이란?</span><span class="sxs-lookup"><span data-stu-id="2b762-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="2b762-121">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="2b762-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
