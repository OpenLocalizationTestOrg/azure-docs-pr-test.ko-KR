---
title: "Azure에서 Jenkins 서버 aaaCreate"
description: "Jenkins hello Jenkins 솔루션 템플릿에서 Azure Linux 가상 컴퓨터에 설치 하 고 샘플 Java 응용 프로그램을 빌드하십시오."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="334ab-103">Jenkins 서버 hello Azure 포털에서에서 Azure Linux VM에서 만들기</span><span class="sxs-lookup"><span data-stu-id="334ab-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="334ab-104">이 퀵 스타트의 표시 방법을 tooinstall [Jenkins](https://jenkins.io) azure hello 도구와 구성 된 플러그 인 toowork Ubuntu Linux VM에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="334ab-105">작업을 완료하면 Azure에서 실행되는 Jenkins 서버가 [GitHub](https://github.com)에서 샘플 Java 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="334ab-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="334ab-106">Prerequisites</span></span>

* <span data-ttu-id="334ab-107">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="334ab-107">An Azure subscription</span></span>
* <span data-ttu-id="334ab-108">컴퓨터의 명령줄에 대 한 액세스 tooSSH (hello 예: Bash 셸은 또는 [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="334ab-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="334ab-109">Hello 솔루션 템플릿에서 hello Jenkins VM 만들기</span><span class="sxs-lookup"><span data-stu-id="334ab-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="334ab-110">열기 hello [마켓플레이스 이미지를 Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) 에서 웹 브라우저를 선택 **GET IT 이제** hello hello 페이지의 왼쪽에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="334ab-111">가격 책정 세부 정보 및 선택 검토 hello **계속**을 선택한 후 **만들기** tooconfigure hello Jenkins 서버 hello Azure 포털에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Azure Portal 대화 상자](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="334ab-113">Hello에 **기본 설정을 구성** 탭 hello 필드 뒤에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![기본 설정 구성](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="334ab-115">**이름**에 **Jenkins**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="334ab-116">**사용자 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-116">Enter a **User name**.</span></span> <span data-ttu-id="334ab-117">사용자 이름은 hello 만족 해야 합니다 [특정 요구 사항](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="334ab-118">선택 **암호** hello로 **인증 유형을** 고 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="334ab-119">hello 암호는 대문자, 숫자 및 특수 문자를 하나 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="334ab-120">사용 하 여 **myJenkinsResourceGroup** hello에 대 한 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="334ab-121">Hello 선택 **미국 동부** [Azure 지역](https://azure.microsoft.com/regions/) hello에서 **위치** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="334ab-122">선택 **확인** tooproceed toohello **추가 옵션을 구성** 탭 합니다. 고유한 도메인 이름을 tooidentify hello Jenkins 서버를 입력 하 고 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![추가 옵션 설정](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="334ab-124">유효성 검사에 통과 되 면 선택 **확인** hello에서 다시 **요약** 탭 합니다. 마지막으로 선택 **구매** toocreate hello Jenkins VM입니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="334ab-125">서버에 준비 되 면 알림을 받게 hello Azure 포털에서:</span><span class="sxs-lookup"><span data-stu-id="334ab-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Jenkins는 준비 알림임](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="334ab-127">TooJenkins 연결</span><span class="sxs-lookup"><span data-stu-id="334ab-127">Connect tooJenkins</span></span>

<span data-ttu-id="334ab-128">웹 브라우저에서 tooyour 가상 컴퓨터 (예를 들어 http://jenkins2517454.eastus.cloudapp.azure.com/)를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="334ab-129">SSH 터널을 사용 하 여 컴퓨터에서 안전 하 게 hello 페이지 tooaccess hello Jenkins 콘솔에 설명 되어 있으므로 hello Jenkins 콘솔을 보안 되지 않은 HTTP를 통해 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Jenkins 잠금 해제](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="334ab-131">Hello를 사용 하 여 hello 터널 설정 `ssh` hello 페이지 hello 명령줄에서 명령을 교체 `username` hello 솔루션 템플릿에서 hello 가상 컴퓨터를 설정 하는 경우 이전에 선택한 hello 가상 컴퓨터 관리자 사용자의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="334ab-132">Hello 터널 시작 된 후 이동 toohttp://localhost:8080 / 로컬 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="334ab-133">Hello 다음 SSH toohello Jenkins VM을 통해 연결 되어 있는 동안 hello 명령줄에서 명령을 실행 하 여 hello 초기 암호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="334ab-134">이 초기 암호를 사용 하 여 처음 hello에 대 한 hello Jenkins 대시보드를 잠금 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Jenkins 잠금 해제](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="334ab-136">선택 **제안 된 플러그 인 설치** hello에서 다음 페이지 하 고 다음 Jenkins 관리자 사용 되는 사용자 tooaccess hello Jenkins 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins가 준비되었습니다.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="334ab-138">Jenkins 서버 hello 준비 toobuild 코드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="334ab-139">첫 번째 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="334ab-139">Create your first job</span></span>

<span data-ttu-id="334ab-140">선택 **새 작업을 만들** hello Jenkins 콘솔에서 다음 이름을 **mySampleApp** 선택 **Freestyle 프로젝트**을 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![새 작업 만들기](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="334ab-142">선택 hello **소스 코드 관리** 탭을 사용 하도록 설정 **Git**, hello에 대 한 url을 입력 하 고 **리포지토리 URL** 필드:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="334ab-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Hello Git 리포지토리를 정의 합니다.](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="334ab-144">선택 hello **빌드** 탭 한 다음 선택 **추가 빌드 단계**, **호출 Gradle 스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="334ab-145">**Gradle 래퍼 사용**을 선택한 후 **래퍼 위치**에 `complete`를 입력하고 **작업**에 `build`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Gradle 래퍼 toobuild hello를 사용 하 여](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="334ab-147">**고급..**을 선택하고</span><span class="sxs-lookup"><span data-stu-id="334ab-147">Select **Advanced..**</span></span> <span data-ttu-id="334ab-148">다음을 입력 하 고 `complete` hello에 **루트 빌드 스크립트** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="334ab-149">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-149">Select **Save**.</span></span>

![Hello Gradle 래퍼 빌드 단계에서 설정을 고급 설정](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="334ab-151">Hello 코드 작성</span><span class="sxs-lookup"><span data-stu-id="334ab-151">Build hello code</span></span>

<span data-ttu-id="334ab-152">선택 **이제 빌드** toocompile hello 코드와 패키지 hello 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="334ab-153">빌드가 완료 되 면 선택 hello **작업 영역** hello 프로젝트에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Hello 빌드에서 toohello 작업 영역 tooget hello JAR 파일 찾아보기](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="334ab-155">너무 이동`complete/build/libs` hello를 확인 하 고 `gs-spring-boot-0.1.0.jar` 거기 tooverify 프로그램 빌드에 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="334ab-156">서버는 이제 프로그램 Jenkins toobuild Azure에서 사용자의 프로젝트를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="334ab-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="334ab-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="334ab-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="334ab-158">Jenkins 에이전트로 Azure VM 추가</span><span class="sxs-lookup"><span data-stu-id="334ab-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
