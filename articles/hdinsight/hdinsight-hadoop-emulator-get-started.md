---
title: "-에뮬레이터-Azure HDInsight Hadoop 샌드박스를 사용 하 여 aaaLearn | Microsoft Docs"
description: "사용에 대 한 학습 toostart hello Hadoop 에코 시스템, Azure 가상 컴퓨터에서 Hortonwork에서 Hadoop 샌드박스를 설정할 수 있습니다. "
keywords: "Hadoop 에뮬레이터, Hadoop 샌드박스"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="d792f-104">가상 컴퓨터의 에뮬레이터인 Hadoop 샌드박스 시작</span><span class="sxs-lookup"><span data-stu-id="d792f-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="d792f-105">Tooinstall hello Hadoop 에코 시스템에 대 한 가상 컴퓨터 toolearn에서 Hortonworks에서 Hadoop 샌드박스 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="d792f-106">hello 샌드박스 Hadoop, Hadoop 분산 파일 시스템 (HDFS), 및 작업 제출 하는 방법에 대 한 로컬 개발 환경 toolearn를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="d792f-107">Hadoop에 익숙해졌으면 HDInsight 클러스터를 만들어 Azure에서 Hadoop 사용을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="d792f-108">Tooget 시작 하는 방법에 대 한 자세한 내용은 참조 하십시오. [HDInsight의 Hadoop 시작](hdinsight-hadoop-linux-tutorial-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d792f-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d792f-109">Prerequisites</span></span>
* <span data-ttu-id="d792f-110">[Oracle VirtualBox](https://www.virtualbox.org/)</span><span class="sxs-lookup"><span data-stu-id="d792f-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="d792f-111">[여기](https://www.virtualbox.org/wiki/Downloads)에서 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="d792f-112">다운로드 하 여 hello 가상 컴퓨터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="d792f-113">Toohello 찾아보기 [Hortonworks 다운로드](http://hortonworks.com/downloads/#sandbox)합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="d792f-114">클릭 **VIRTUALBOX에 대 한 다운로드** toodownload hello VM에서 최신 Hortonworks 샌드박스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="d792f-115">Hello 다운로드가 시작 되기 전에 Hortonworks와 증명된 tooregister 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="d792f-116">네트워크 속도 따라 하나의 tootwo 시간 toodownload이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![VirtualBox에 대한 Hortonworks Sandbox를 다운로드용 링크 이미지](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="d792f-118">같은 웹 페이지 hello를 hello 클릭 **Virtual Box에서 가져오기** toodownload hello 가상 컴퓨터에 대 한 설치 지침을 포함 하는 PDF를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="d792f-119">이전 HDP 버전 샌드박스 toodownload hello 아카이브를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Hortonworks 샌드박스 보관](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="d792f-121">Hello 가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="d792f-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="d792f-122">Open Oracle VM VirtualBox를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="d792f-123">Hello에서 **파일** 메뉴를 클릭 하 여 **가져오기 기기**, hello Hortonworks 샌드박스 이미지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="d792f-124">선택 hello Hortonworks 샌드박스 클릭 **시작**, 차례로 **보통 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="d792f-125">Hello 가상 컴퓨터는 hello 부팅 프로세스를 완료 되 면 로그인 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![일반 시작](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="d792f-127">웹 브라우저를 열고 표시 된 toohello URL (일반적으로 http://127.0.0.1:8888) 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="d792f-128">샌드박스 암호 설정</span><span class="sxs-lookup"><span data-stu-id="d792f-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="d792f-129">Hello에서 **시작** hello Hortonworks 샌드박스 페이지의 단계 **보기 고급 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="d792f-130">이 페이지 toolog SSH를 사용 하 여 toohello 샌드박스에서 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="d792f-131">제공한 hello 이름 및 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d792f-132">웹 기반 SSH에 hello 가상 컴퓨터에서 제공 하는 hello SSH 클라이언트를 설치 하는 경우 사용할 수 있습니다 **http://localhost:4200 /**합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="d792f-133">hello 처음 SSH를 사용 하 여 연결 하는 hello 루트 계정에 대 한 증명된 toochange hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="d792f-134">새 암호를 입력합니다. 이 암호는 SSH를 사용하여 로그인할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="d792f-135">로그인 한 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="d792f-136">메시지가 표시 되 면 hello Ambari 관리자 계정에 대 한 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="d792f-137">이 hello Ambari 웹 UI에 액세스할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="d792f-138">Hive 명령 사용</span><span class="sxs-lookup"><span data-stu-id="d792f-138">Use Hive commands</span></span>

1. <span data-ttu-id="d792f-139">SSH 연결 toohello 샌드박스에서 hello 명령 toostart hello 하이브 셸에 다음을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d792f-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="d792f-140">Hello 셸이 시작 되 면 다음 tooview hello 표 hello 샌드박스 함께 제공 되는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d792f-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="d792f-141">다음 tooretrieve 10 행 hello에서 사용 하 여 hello `sample_07` 테이블:</span><span class="sxs-lookup"><span data-stu-id="d792f-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="d792f-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d792f-142">Next steps</span></span>
* [<span data-ttu-id="d792f-143">자세한 내용은 방법 Hortonworks 샌드박스 hello로 toouse Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d792f-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="d792f-144">Hello Hortonworks 샌드박스의 hello ropes 학습</span><span class="sxs-lookup"><span data-stu-id="d792f-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="d792f-145">Hadoop 자습서 - HDP 시작</span><span class="sxs-lookup"><span data-stu-id="d792f-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

