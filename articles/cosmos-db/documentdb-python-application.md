---
title: "Azure Cosmos DB의 Python Flask 웹 응용 프로그램 자습서 | Microsoft Docs"
description: "Azure Cosmos DB를 사용하여 Azure에 호스트된 Python Flask 웹 응용 프로그램에서 데이터를 저장하고 액세스하는 방법에 대한 데이터베이스 자습서를 검토합니다. 응용 프로그램 개발 솔루션을 찾습니다."
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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="cb4f5-105">Azure Cosmos DB를 사용하여 Python Flask 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="cb4f5-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb4f5-106">.NET</span><span class="sxs-lookup"><span data-stu-id="cb4f5-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="cb4f5-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="cb4f5-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="cb4f5-108">Java</span><span class="sxs-lookup"><span data-stu-id="cb4f5-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="cb4f5-109">Python</span><span class="sxs-lookup"><span data-stu-id="cb4f5-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="cb4f5-110">이 자습서에서는 Azure Cosmos DB를 사용하여 Azure에 호스트된 Python 웹 응용 프로그램에서 데이터를 저장하고 액세스하는 방법을 보여주며 이전에 Python 및 Azure Websites를 사용한 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="cb4f5-111">이 데이터베이스 자습서에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="cb4f5-112">Cosmos DB 계정 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="cb4f5-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="cb4f5-113">Python Flask 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cb4f5-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="cb4f5-114">웹 응용 프로그램에서 Cosmos DB에 연결 및 사용</span><span class="sxs-lookup"><span data-stu-id="cb4f5-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="cb4f5-115">Azure에 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="cb4f5-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="cb4f5-116">이 자습서를 따르면 설문 조사에 투표할 수 있는 간단한 투표 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![이 데이터베이스 자습서에서 만든 투표 응용 프로그램의 스크린샷](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="cb4f5-118">데이터베이스 자습서 필수 조건</span><span class="sxs-lookup"><span data-stu-id="cb4f5-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="cb4f5-119">이 문서의 지침을 따르기 전에 다음이 설치되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="cb4f5-120">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-120">An active Azure account.</span></span> <span data-ttu-id="cb4f5-121">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cb4f5-122">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="cb4f5-123">또는</span><span class="sxs-lookup"><span data-stu-id="cb4f5-123">OR</span></span> 

    <span data-ttu-id="cb4f5-124">[Azure Cosmos DB 에뮬레이터](local-emulator.md)의 로컬 설치</span><span class="sxs-lookup"><span data-stu-id="cb4f5-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="cb4f5-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="cb4f5-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="cb4f5-126">[Visual Studio용 Python 도구](https://github.com/Microsoft/PTVS/)</span><span class="sxs-lookup"><span data-stu-id="cb4f5-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="cb4f5-127">[Python 2.7용 Microsoft Azure SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="cb4f5-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="cb4f5-128">[Python 2.7.13](https://www.python.org/downloads/windows/)</span><span class="sxs-lookup"><span data-stu-id="cb4f5-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cb4f5-129">처음으로 Python 2.7을 설치하는 경우 사용자 지정 Python 2.7.13 화면에서 **경로에 python.exe 추가**를 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![사용자 지정 Python 2.7.11 화면의 스크린샷에서 경로에 python.exe 추가를 선택해야 합니다.](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="cb4f5-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)</span><span class="sxs-lookup"><span data-stu-id="cb4f5-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="cb4f5-132">1단계: Azure Cosmos DB 데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cb4f5-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="cb4f5-133">Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="cb4f5-134">계정이 있거나 이 자습서에 Azure Cosmos DB 에뮬레이터를 사용하고 있는 경우 [2단계: 새 Python Flask 웹 응용 프로그램 만들기](#step-2-create-a-new-python-flask-web-application)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="cb4f5-135">이제 새 Python Flask 웹 응용 프로그램을 처음부터 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="cb4f5-136">2단계: 새 Python Flask 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cb4f5-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="cb4f5-137">Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 가리킨 후 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="cb4f5-138">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="cb4f5-139">왼쪽 창에서 **템플릿** 및 **Python**을 확장하고 **웹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="cb4f5-140">가운데 창에서 **Flask 웹 프로젝트**를 선택한 다음 **이름** 상자에 **자습서**를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="cb4f5-141">[Python 코드에 대한 스타일 가이드](https://www.python.org/dev/peps/pep-0008/#package-and-module-names)에 설명한 대로 Python 패키지 이름은 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="cb4f5-142">Python Flask를 처음 사용하는 경우 Python에서 웹 응용 프로그램을 더 빨리 작성하는 데 도움이 되는 웹 응용 프로그램 개발 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![왼쪽에서 Python이 강조 표시되고, 가운데에서 Python Flask 웹 프로젝트가 선택되고, 이름 상자에 tutorial 이름이 포함된 Visual Studio 새 프로젝트 창의 스크린샷](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="cb4f5-144">**Visual Studio용 Python 도구** 창에서 **가상 환경에 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![데이터베이스 자습서의 스크린샷 - Python Tools for Visual Studio 창](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="cb4f5-146">**가상 환경 추가** 창에서 PyDocumentDB가 현재 Python 3.x을 지원하지 않기 때문에 기본값을 적용하고 Python 2.7을 기본 환경으로 사용한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="cb4f5-147">프로젝트에 필요한 Python 가상 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![데이터베이스 자습서의 스크린샷 - Python Tools for Visual Studio 창](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="cb4f5-149">환경이 성공적으로 설치될 때 출력 창은 `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` 을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="cb4f5-150">3단계: Python Flask 웹 응용 프로그램 수정</span><span class="sxs-lookup"><span data-stu-id="cb4f5-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="cb4f5-151">프로젝트에 Python Flask 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="cb4f5-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="cb4f5-152">프로젝트가 설정된 후 DocumentDB용 Python 패키지인 pydocumentdb를 포함해서 프로젝트에 필요한 Flask 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="cb4f5-153">솔루션 탐색기에서 **requirements.txt** 파일을 열고 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="cb4f5-154">**requirements.txt** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="cb4f5-155">솔루션 탐색기에서 **환경**을 마우스 오른쪽 단추로 클릭하고 **requirements.txt에서 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![목록에서 강조 표시된 requirements.txt에서 설치를 사용하여 선택한 env(Python 2.7)를 보여주는 스크린샷](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="cb4f5-157">성공적으로 설치한 후에 출력 창이 다음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="cb4f5-158">출력 창에 실패가 표시되는 경우가 드물게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="cb4f5-159">그런 경우 오류가 정리와 관련이 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="cb4f5-160">때때로 정리는 실패하지만 설치는 성공하는 경우가 있습니다(이를 확인하려면 출력 창에서 위로 스크롤).</span><span class="sxs-lookup"><span data-stu-id="cb4f5-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="cb4f5-161">[가상 환경 확인](#verify-the-virtual-environment)에서 설치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="cb4f5-162">설치에 실패했지만 확인이 성공한 경우 계속해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="cb4f5-163">가상 환경 확인</span><span class="sxs-lookup"><span data-stu-id="cb4f5-163">Verify the virtual environment</span></span>
<span data-ttu-id="cb4f5-164">모두 올바르게 설치되었는지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="cb4f5-165">**Ctrl**+**Shift**+**B**를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="cb4f5-166">빌드가 성공하면 **F5**키를 눌러 웹 사이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="cb4f5-167">그러면 Flask 개발 서버가 실행되고 웹 브라우저가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="cb4f5-168">다음 페이지를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-168">You should see the following page.</span></span>
   
    ![브라우저에 표시된 빈 Python Flask 웹 개발 프로젝트](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="cb4f5-170">Visual Studio에서 **Shift**+**F5**를 눌러 웹 사이트의 디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="cb4f5-171">데이터베이스, 컬렉션 및 문서 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="cb4f5-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="cb4f5-172">이제 새 파일을 추가하고 다른 사용자를 업데이트하여 투표 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="cb4f5-173">솔루션 탐색기에서 **자습서** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="cb4f5-174">**빈 Python 파일**을 선택하고 파일 이름을 **forms.py**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="cb4f5-175">다음 코드를 forms.py 파일에 추가한 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="cb4f5-176">필요한 가져오기를 views.py에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="cb4f5-177">솔루션 탐색기에서 **tutorial** 폴더를 확장하고 **views.py** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="cb4f5-178">**views.py** 파일 맨 위에 다음 import 문을 추가하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="cb4f5-179">이렇게 하면 Cosmos DB의 PythonSDK 및 Flask 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="cb4f5-180">데이터베이스, 컬렉션 및 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="cb4f5-180">Create database, collection, and document</span></span>
* <span data-ttu-id="cb4f5-181">**views.py**에서 파일의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="cb4f5-182">이 코드는 폼에서 사용되는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="cb4f5-183">**views.py**의 기존 코드를 삭제하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="cb4f5-184">단순히 끝 부분에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="cb4f5-185">데이터베이스, 컬렉션, 문서 및 제출 폼 참고</span><span class="sxs-lookup"><span data-stu-id="cb4f5-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="cb4f5-186">**views.py**에서 파일의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="cb4f5-187">이 코드는 데이터베이스, 컬렉션 및 문서를 읽고 폼을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="cb4f5-188">**views.py**의 기존 코드를 삭제하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="cb4f5-189">단순히 끝 부분에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-189">Simply append this to the end.</span></span>

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

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
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


### <a name="create-the-html-files"></a><span data-ttu-id="cb4f5-190">HTML 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="cb4f5-190">Create the HTML files</span></span>
1. <span data-ttu-id="cb4f5-191">솔루션 탐색기의 **tutorial** 폴더에서 **templates** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 항목**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="cb4f5-192">**HTML 페이지**를 선택한 다음 이름 상자에 **create.html**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="cb4f5-193">1단계 및 2단계를 반복하여 results.html 및 vote.html과 같은 추가 HTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="cb4f5-194">`<body>` 요소의 **create.html**에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="cb4f5-195">이 코드는 새 데이터베이스, 컬렉션 및 문서를 만들었다는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="cb4f5-196">`<body`> 요소의 **results.html**에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="cb4f5-197">설문 조사 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
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
6. <span data-ttu-id="cb4f5-198">`<body`> 요소의 **vote.html**에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="cb4f5-199">설문 조사를 표시하고 투표를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="cb4f5-200">투표를 등록하면 제어가 views.py로 전달되며, 여기서 투표 완료를 인식하고 그에 따라 문서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="cb4f5-201">**templates** 폴더에서 **index.html**의 내용을 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="cb4f5-202">이 코드는 응용 프로그램의 방문 페이지 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="cb4f5-203">구성 파일 추가 및 \_\_init\_\_.py 변경</span><span class="sxs-lookup"><span data-stu-id="cb4f5-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="cb4f5-204">솔루션 탐색기에서 **자습서** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** 및 **새 항목**을 차례로 클릭한 다음 **빈 Python 파일**을 선택하고 파일의 이름을 **config.py**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="cb4f5-205">이 구성 파일은 Flask의 폼에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="cb4f5-206">이 파일을 사용하여 암호 키를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="cb4f5-207">하지만 이 자습서에서는 이 키가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="cb4f5-208">Config.py에 다음 코드를 추가하고 다음 단계에서 **DOCUMENTDB\_HOST** 및 **DOCUMENTDB\_KEY**의 값을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="cb4f5-209">[Azure Portal](https://portal.azure.com/)에서 **찾아보기**, **Azure Cosmos DB 계정**을 클릭하여 **키** 블레이드를 탐색하고 사용할 계정 이름을 두 번 클릭한 다음 **Essentials** 영역에서 **키** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="cb4f5-210">**키** 블레이드에서 **URI** 값을 복사하고 **DOCUMENTDB\_HOST** 속성에 대한 값으로 **config.py** 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="cb4f5-211">다시 Azure Portal의 **키** 블레이드에서 **기본 키** 또는 **보조 키** 값을 복사하고 **DOCUMENTDB\_KEY** 속성에 대한 값으로 **config.py** 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="cb4f5-212">**\_\_init\_\_.py** 파일에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="cb4f5-213">파일의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="cb4f5-214">모든 파일을 추가한 후에 솔루션 탐색기는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Visual Studio 솔루션 탐색기 창의 스크린샷](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="cb4f5-216">4단계: 로컬에서 웹 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="cb4f5-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="cb4f5-217">**Ctrl**+**Shift**+**B**를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="cb4f5-218">빌드가 성공하면 **F5**키를 눌러 웹 사이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="cb4f5-219">스크린에 다음이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-219">You should see the following on your screen.</span></span>
   
    ![웹 브라우저에 표시된 Python + Azure Cosmos DB 투표 응용 프로그램의 스크린샷](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="cb4f5-221">**투표 데이터베이스 만들기/지우기** 를 클릭하여 데이터베이스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![웹 응용 프로그램 만들기 페이지의 스크린샷 - 개발 세부 정보](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="cb4f5-223">그런 다음 **투표** 를 클릭하고 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-223">Then, click **Vote** and select your option.</span></span>
   
    ![게시된 투표 질문이 있는 웹 응용 프로그램의 스크린샷](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="cb4f5-225">투표할 때마다 해당 카운터가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![표시된 투표 페이지의 결과 스크린샷](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="cb4f5-227">Shift+F5를 눌러 프로젝트의 디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="cb4f5-228">5단계: Azure에 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="cb4f5-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="cb4f5-229">이제 완료된 응용 프로그램이 Cosmos DB에 대해 올바르게 작동하므로 Azure에 배포하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="cb4f5-230">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고(로컬에서 실행하고 있지 않도록 확인) **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![강조 표시된 게시 옵션을 사용하여 솔루션 탐색기에서 선택된 자습서의 스크린샷](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="cb4f5-232">**게시** 대화 상자에서 **Microsoft Azure App Service**, **새로 만들기**를 차례로 선택한 다음, **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![강조 표시된 Microsoft Azure App Service가 포함된 웹 게시 창의 스크린샷](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="cb4f5-234">**App Service 만들기** 대화 상자에서 웹앱에 대한 이름과 함께 **구독**, **리소스 그룹** 및 **앱 서비스 계획**을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Microsoft Azure 웹앱 창 창의 스크린샷](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="cb4f5-236">몇 초 후에 Visual Studio에서 앱 서비스 게시를 완료하고, Azure에서 실행되는 작업 내용을 확인할 수 있는 브라우저가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Microsoft Azure 웹앱 창 창의 스크린샷](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="cb4f5-238">문제 해결</span><span class="sxs-lookup"><span data-stu-id="cb4f5-238">Troubleshooting</span></span>
<span data-ttu-id="cb4f5-239">컴퓨터에서 실행하는 첫 번째 Python 앱인 경우 다음 폴더(또는 동등한 설치 위치)가 경로 변수에 포함되어 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="cb4f5-240">투표 페이지에 오류가 발생하고 **자습서**가 아닌 다른 이름으로 프로젝트의 이름을 지정한 경우 **\_\_init\_\_.py**가 줄에서 올바른 프로젝트 이름을 참조하도록 합니다. `import tutorial.view`</span><span class="sxs-lookup"><span data-stu-id="cb4f5-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb4f5-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb4f5-241">Next steps</span></span>
<span data-ttu-id="cb4f5-242">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-242">Congratulations!</span></span> <span data-ttu-id="cb4f5-243">지금까지 Cosmos DB를 사용하여 첫 Python 웹 응용 프로그램을 완성하고 Azure에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="cb4f5-244">이 항목은 사용자 피드백에 따라 자주 업데이트되고 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="cb4f5-245">자습서를 완료했으면 이 페이지 상단과 하단에 있는 응답 단추를 사용하여 개선되었으면 하는 사항에 대한 피드백을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="cb4f5-246">직접 연락을 받고 싶은 경우 설명에 메일 주소를 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="cb4f5-247">웹 응용 프로그램에 다른 기능을 추가하려면 [Azure Cosmos DB Python SDK](documentdb-sdk-python.md)에서 사용할 수 있는 API를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="cb4f5-248">Azure, Visual Studio 및 Python에 대한 자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="cb4f5-249">추가 Python Flask 자습서는 [Flask Mega-자습서 1부: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb4f5-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
