---
title: "Azure Cosmos db aaaPython 플라스 웹 응용 프로그램 자습서 | Microsoft Docs"
description: "Azure에서 호스팅되는 Python 플라스 웹 응용 프로그램에서 Azure Cosmos DB toostore 및 액세스 데이터를 사용 하 여에 대 한 데이터베이스 자습서를 검토 합니다. 응용 프로그램 개발 솔루션을 찾습니다."
keywords: "응용 프로그램 개발, Python flask, Python 웹 응용 프로그램, Python 웹 개발"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="2ff98-105">Azure Cosmos DB를 사용하여 Python Flask 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="2ff98-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ff98-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2ff98-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="2ff98-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2ff98-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="2ff98-108">Java</span><span class="sxs-lookup"><span data-stu-id="2ff98-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="2ff98-109">Python</span><span class="sxs-lookup"><span data-stu-id="2ff98-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="2ff98-110">이 자습서 toouse Azure Cosmos DB toostore 데이터에 액세스 하는 Python에서 웹 응용 프로그램을 Azure에서 호스트 하 고 일부 이전에 Python 및 Azure 웹 사이트를 사용 하 여 경험이 있다고 가정 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="2ff98-111">이 데이터베이스 자습서에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="2ff98-112">Cosmos DB 계정 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="2ff98-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="2ff98-113">Python Flask 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2ff98-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="2ff98-114">Cosmos DB를 사용 하 여 웹 응용 프로그램에서 tooand를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="2ff98-115">웹 응용 프로그램 tooAzure hello를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="2ff98-116">이 자습서를 따라 설문 조사에 대 한 toovote 수 있는 간단한 투표 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![이 데이터베이스 자습서에서 만든 hello 투표 응용 프로그램의 스크린 샷](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="2ff98-118">데이터베이스 자습서 필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ff98-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="2ff98-119">이 문서의 지침 hello를 수행 하기 전에 hello 다음이 설치 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="2ff98-120">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="2ff98-120">An active Azure account.</span></span> <span data-ttu-id="2ff98-121">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ff98-122">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ff98-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="2ff98-123">또는</span><span class="sxs-lookup"><span data-stu-id="2ff98-123">OR</span></span> 

    <span data-ttu-id="2ff98-124">Hello의 로컬 설치 [Azure Cosmos DB 에뮬레이터](local-emulator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="2ff98-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="2ff98-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="2ff98-126">[Visual Studio용 Python 도구](https://github.com/Microsoft/PTVS/)</span><span class="sxs-lookup"><span data-stu-id="2ff98-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="2ff98-127">[Python 2.7용 Microsoft Azure SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="2ff98-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="2ff98-128">[Python 2.7.13](https://www.python.org/downloads/windows/)</span><span class="sxs-lookup"><span data-stu-id="2ff98-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2ff98-129">를 설치 하는 Python 2.7 hello에 대 한 처음으로 하는 경우 hello 사용자 지정 Python 2.7.13 화면에서 선택 했는지 확인 **python.exe tooPath 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Tooselect 추가 python.exe tooPath 해야 하는 hello 사용자 지정 Python 2.7.11 화면의 스크린 샷](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="2ff98-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)</span><span class="sxs-lookup"><span data-stu-id="2ff98-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="2ff98-132">1단계: Azure Cosmos DB 데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2ff98-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="2ff98-133">Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="2ff98-134">계정이 이미 없거나 사용 중인 경우이 자습서에 대 한 Azure Cosmos DB 에뮬레이터 hello 건너뛰어도 너무[2 단계: 새 Python 플라스 웹 응용 프로그램 만들기](#step-2-create-a-new-python-flask-web-application)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="2ff98-135">이제 toocreate hello에서 새 Python 플라스 웹 응용 프로그램 접지 하는 방법을 단계별로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="2ff98-136">2단계: 새 Python Flask 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2ff98-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="2ff98-137">Hello에 Visual Studio에서 **파일** 메뉴 너무 가리킨**새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="2ff98-138">hello **새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="2ff98-139">Hello 왼쪽된 창에서 **템플릿** 차례로 **Python**, 클릭 하 고 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="2ff98-140">선택 **플라스 웹 프로젝트** hello 가운데 창에서 다음 hello에서 **이름** 상자에 입력 **자습서**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="2ff98-141">Hello에 설명 된 대로 Python 패키지 이름을 해야 모두 소문자 여야 기억 [Python 코드에 대 한 스타일 가이드](https://www.python.org/dev/peps/pep-0008/#package-and-module-names)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="2ff98-142">이러한 새 tooPython 플라스, Python에서 웹 응용 프로그램을 더 빠르게 빌드할 수 있는 웹 응용 프로그램 개발 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Python 왼쪽, Python 플라스 웹 프로젝트를 hello 중간 및 hello 이름 자습서 hello 이름 상자에 선택 하는 hello에 강조 표시 된 Visual Studio에서 새 프로젝트 창 hello의 스크린샷](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="2ff98-144">Hello에 **Python Tools for Visual Studio** 창 클릭 **가상 환경에 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Hello 데이터베이스 자습서-Python Tools for Visual Studio 창 스크린 샷](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="2ff98-146">Hello에 **가상 환경 추가** 창 hello 기본값을 적용 하 고 PyDocumentDB Python을 현재 지원 하지 않으므로 Python 2.7 hello 기본 환경으로 사용할 수 있습니다, 3.x 및 클릭 한 다음 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="2ff98-147">이 프로젝트에 대 한 필요한 hello Python 가상 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Hello 데이터베이스 자습서-Python Tools for Visual Studio 창 스크린 샷](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="2ff98-149">hello 출력 창 표시 `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` hello 환경이 성공적으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="2ff98-150">3 단계: hello Python 플라스 웹 응용 프로그램 수정</span><span class="sxs-lookup"><span data-stu-id="2ff98-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="2ff98-151">Hello Python 플라스 패키지 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="2ff98-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="2ff98-152">프로젝트를 설정한 후 tooadd 필요한 hello 플라스 패키지 tooyour를 포함 하 여 프로젝트 pydocumentdb, documentdb Python 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="2ff98-153">솔루션 탐색기에서 라는 hello 파일을 열고 **requirements.txt** hello 내용을 hello 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="2ff98-154">Hello 저장 **requirements.txt** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="2ff98-155">솔루션 탐색기에서 **환경**을 마우스 오른쪽 단추로 클릭하고 **requirements.txt에서 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![스크린 샷 requirements.txt hello 목록에서 강조 표시에서 선택한 설치를 보여 주는 env (Python 2.7)](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="2ff98-157">설치 후 hello 출력 창에는 hello 다음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="2ff98-158">드문 경우 지만 hello 출력 창에 오류가 표시 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="2ff98-159">이 경우 hello 오류 관련된 toocleanup 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="2ff98-160">경우에 따라 hello 정리 하지 못했으나 hello 설치 여전히 성공적으로 수행 됩니다 (에서 위로 스크롤 hello 출력 창 tooverify이).</span><span class="sxs-lookup"><span data-stu-id="2ff98-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="2ff98-161">설치 하 여 확인할 수 있습니다 [모으기 hello 가상 환경](#verify-the-virtual-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="2ff98-162">Hello 설치에 실패 했습니다. hello 유효성 확인이 성공 되지만 경우 확인 toocontinue입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="2ff98-163">Hello 가상 환경 확인</span><span class="sxs-lookup"><span data-stu-id="2ff98-163">Verify hello virtual environment</span></span>
<span data-ttu-id="2ff98-164">모두 올바르게 설치되었는지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="2ff98-165">키를 눌러 hello 솔루션을 구축 **Ctrl**+**Shift**+**B**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="2ff98-166">Hello 빌드에 성공 hello 웹 사이트를 눌러 시작 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="2ff98-167">이 hello 플라스 개발 서버를 시작 하 고 웹 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="2ff98-168">다음 페이지 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-168">You should see hello following page.</span></span>
   
    ![hello 빈 Python 플라스 웹 개발 프로젝트 브라우저에 표시](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="2ff98-170">Hello 웹 사이트를 눌러 디버깅을 중지 **Shift**+**F5** Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="2ff98-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="2ff98-171">데이터베이스, 컬렉션 및 문서 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="2ff98-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="2ff98-172">이제 새 파일을 추가하고 다른 사용자를 업데이트하여 투표 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="2ff98-173">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **자습서** 프로젝트를 클릭 하 여 **추가**, 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2ff98-174">선택 **빈 Python 파일** hello 파일 이름 및 **forms.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="2ff98-175">다음 코드 toohello forms.py 파일 hello를 추가 하 고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="2ff98-176">필요한 hello imports tooviews.py 추가</span><span class="sxs-lookup"><span data-stu-id="2ff98-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="2ff98-177">솔루션 탐색기에서 확장 hello **자습서** 폴더를 찾아 열고 hello **views.py** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="2ff98-178">Hello 맨 문을 toohello 가져오기 뒤 hello 추가 **views.py** 파일을 다음 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="2ff98-179">이러한 Cosmos DB PythonSDK 가져와서 hello 플라스 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="2ff98-180">데이터베이스, 컬렉션 및 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="2ff98-180">Create database, collection, and document</span></span>
* <span data-ttu-id="2ff98-181">여전히 **views.py**, hello hello 파일의 코드 toohello 끝 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="2ff98-182">이 hello 양식에서 사용 하는 hello 데이터베이스를 만드는 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="2ff98-183">기존 코드 마이그레이션 hello 삭제 하지 마십시오 **views.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="2ff98-184">이 toohello 끝을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="2ff98-185">데이터베이스, 컬렉션, 문서 및 제출 폼 참고</span><span class="sxs-lookup"><span data-stu-id="2ff98-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="2ff98-186">여전히 **views.py**, hello hello 파일의 코드 toohello 끝 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="2ff98-187">이 처리 hello 데이터베이스, 컬렉션 및 문서를 읽는 hello 폼을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="2ff98-188">기존 코드 마이그레이션 hello 삭제 하지 마십시오 **views.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="2ff98-189">이 toohello 끝을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="2ff98-190">Hello HTML 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="2ff98-190">Create hello HTML files</span></span>
1. <span data-ttu-id="2ff98-191">Hello의 솔루션 탐색기에서 **자습서** 폴더 오른쪽 클릭 hello **템플릿** 폴더를 클릭 하 여 **추가**, 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="2ff98-192">선택 **HTML 페이지**, 다음 hello 이름 상자에 입력 하 고 **create.html**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="2ff98-193">1 단계와 2 toocreate 두 추가 HTML 파일 반복: results.html 및 vote.html 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="2ff98-194">추가 코드를 너무 다음 hello**create.html** hello에 `<body>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="2ff98-195">이 코드는 새 데이터베이스, 컬렉션 및 문서를 만들었다는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="2ff98-196">추가 코드를 너무 다음 hello**results.html** hello에 `<body`> 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="2ff98-197">Hello hello 설문 조사 결과 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="2ff98-198">추가 코드를 너무 다음 hello**vote.html** hello에 `<body`> 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="2ff98-199">Hello 설문 조사를 표시 하 고 hello 응답을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="2ff98-200">Hello 투표를 등록 하는 방법에 hello 제어가 tooviews.py 우리는 hello 투표 캐스트를 인식 하 고 그에 따라 hello 문서에 추가할를 통해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="2ff98-201">Hello에 **템플릿** 폴더, replace hello 내용의 **index.html** hello 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="2ff98-202">이 응용 프로그램 페이지를 방문 하는 hello로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="2ff98-203">구성 파일을 추가 하 고 hello 변경 \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="2ff98-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="2ff98-204">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **자습서** 프로젝트를 클릭 **추가**, 클릭 **새 항목**선택, **빈 Python 파일**, 한 다음 이름 hello 파일 **config.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="2ff98-205">이 구성 파일은 Flask의 폼에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="2ff98-206">Tooprovide 비밀 키도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="2ff98-207">하지만 이 자습서에서는 이 키가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="2ff98-208">Hello 다음 추가 코드 tooconfig.py 해야 tooalter hello 값 **DOCUMENTDB\_호스트** 및 **DOCUMENTDB\_키** hello 다음 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="2ff98-209">Hello에 [Azure 포털](https://portal.azure.com/), toohello 이동 **키** 블레이드를 클릭 하 여 **찾아보기**, **Azure Cosmos DB 계정**, hello 이름을 두 번 클릭 hello toouse, 계정 및 hello 클릭 **키** hello 단추 **Essentials** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="2ff98-210">Hello에 **키** 블레이드, 복사 hello **URI** 값 및 hello에 붙여 **config.py** hello에 대 한 hello 값으로 파일, **DOCUMENTDB\_호스트**  속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="2ff98-211">Hello hello에서 Azure 포털에 다시 **키** 블레이드에서 hello의 hello 값 복사 **기본 키** 또는 hello **보조 키**, hello에 붙여 넣습니다 **config.py**  hello에 대 한 hello 값으로 파일, **DOCUMENTDB\_키** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="2ff98-212">Hello에  **\_ \_init\_\_.py** 파일, hello 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="2ff98-213">되도록 hello 파일의 내용을 hello:</span><span class="sxs-lookup"><span data-stu-id="2ff98-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="2ff98-214">모든 hello 파일을 추가한 후 솔루션 탐색기는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Visual Studio 솔루션 탐색기 창 hello 스크린 샷](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="2ff98-216">4단계: 로컬에서 웹 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2ff98-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="2ff98-217">키를 눌러 hello 솔루션을 구축 **Ctrl**+**Shift**+**B**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="2ff98-218">Hello 빌드에 성공 hello 웹 사이트를 눌러 시작 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="2ff98-219">Hello 다음 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-219">You should see hello following on your screen.</span></span>
   
    ![스크린 샷 안녕하세요 Python + Azure Cosmos DB 투표 응용 프로그램이 웹 브라우저에 표시](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="2ff98-221">클릭 **만들기/지우기 hello 투표 데이터베이스** toogenerate hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![스크린 샷 hello hello 웹 응용 프로그램 – 개발 세부 정보 페이지 만들기](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="2ff98-223">그런 다음 **투표** 를 클릭하고 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-223">Then, click **Vote** and select your option.</span></span>
   
    ![제기 되 투표 질문 hello 웹 응용 프로그램의 스크린 샷](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="2ff98-225">캐스팅 하면 모든 투표에 대 한 hello 적절 한 카운터를 증가 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Hello 결과 표시 된 hello 투표 페이지의 스크린 샷](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="2ff98-227">Shift + f 5를 눌러 hello 프로젝트 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="2ff98-228">5 단계: 웹 응용 프로그램 tooAzure hello 배포</span><span class="sxs-lookup"><span data-stu-id="2ff98-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="2ff98-229">Cosmos DB에 대해 올바르게 작동 hello 전체 응용 프로그램 설정 했으므로 여기 toodeploy이이 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="2ff98-230">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello 프로젝트 (가 맞는지 확인 하지 여전히 로컬에서 실행) 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![솔루션 탐색기에서 강조 표시 하는 hello 게시 옵션으로 선택한 hello 자습서 스크린 샷](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="2ff98-232">Hello에 **게시** 대화 상자에서 **Microsoft Azure 앱 서비스**선택, **새로 만들기**, 클릭 하 고 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![강조 표시 하는 Microsoft Azure 앱 서비스와 웹 게시 창의 hello 스크린 샷](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="2ff98-234">Hello에 **응용 프로그램 서비스 만들기** 대화 상자와 함께 웹 앱에 대 한 hello 이름을 입력 합니다 프로그램 **구독**, **리소스 그룹**, 및 **앱 서비스 계획** , 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Microsoft Azure 웹 앱 창 창의 hello 스크린 샷](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="2ff98-236">몇 초 후에 Visual Studio에서 앱 서비스 게시를 완료하고, Azure에서 실행되는 작업 내용을 확인할 수 있는 브라우저가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Microsoft Azure 웹 앱 창 창의 hello 스크린 샷](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="2ff98-238">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2ff98-238">Troubleshooting</span></span>
<span data-ttu-id="2ff98-239">Hello 첫 번째 Python 응용 프로그램 컴퓨터에서 실행 한 경우 확인 hello 다음 해당 PATH 변수에 포함 된 폴더 (또는 hello 해당 설치 위치):</span><span class="sxs-lookup"><span data-stu-id="2ff98-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="2ff98-240">투표 페이지에 오류가 발생 하면 프로젝트가 아닌 다른 이름의 경우 **자습서**, 다음 사항을 확인  **\_ \_init\_\_.py** 참조 hello hello 줄에 올바른 프로젝트 이름이: `import tutorial.view`합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ff98-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ff98-241">Next steps</span></span>
<span data-ttu-id="2ff98-242">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-242">Congratulations!</span></span> <span data-ttu-id="2ff98-243">Cosmos DB를 사용 하 여 첫 번째 Python 웹 응용 프로그램을 완료 하 고 tooAzure 게시만 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="2ff98-244">이 항목은 사용자 피드백에 따라 자주 업데이트되고 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="2ff98-245">한 번 하십시오 hello 응답 hello 상단에이 페이지의 아래쪽 단추를 사용 하 여 hello 자습서를 완료 했으므로 하 고 있는지 tooinclude toosee 내용을 원하는 어떤 기능 향상에 대 한 사용자 피드백 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="2ff98-246">받을지 경우 toocontact를 직접 생각 될 전자 메일 주소 가능한 tooinclude 메모에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="2ff98-247">tooadd 추가 기능 tooyour 웹 응용 프로그램을 검토 hello hello에서 사용할 수 있는 Api [Azure Cosmos DB Python SDK](documentdb-sdk-python.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="2ff98-248">Azure, Visual Studio 및 Python에 대 한 자세한 내용은 참조 hello [Python 개발자 센터](https://azure.microsoft.com/develop/python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="2ff98-249">추가 Python 플라스 자습서를 참조 하십시오. [hello 플라스 메가-자습서에서는 일부 i: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff98-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
