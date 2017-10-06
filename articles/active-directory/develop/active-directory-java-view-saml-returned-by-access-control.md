---
title: "액세스 제어 서비스 (Java) hello 여 aaaView SAML 반환"
description: "Azure에서 Java 응용 프로그램에 hello 액세스 제어 서비스에서 반환 되는 SAML tooview 호스팅 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="78e8f-103">SAML tooview hello Azure 액세스 제어 서비스에서 반환 하는 방법</span><span class="sxs-lookup"><span data-stu-id="78e8f-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="78e8f-104">이 가이드 SAML Security Assertion Markup Language () 기본 tooview hello hello Azure 액세스 제어 서비스 (ACS) 하 여 tooyour 응용 프로그램에 반환 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="78e8f-105">hello을 기반으로 하는 hello 가이드 [어떻게 tooAuthenticate Azure 액세스 제어 서비스를 사용 하 여 Eclipse 웹 사용자를](active-directory-java-authenticate-users-access-control-eclipse.md) hello SAML 정보를 표시 하는 코드를 제공 하 여 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="78e8f-106">완료 하는 hello 응용 프로그램은 유사한 toohello 다음 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-106">hello completed application will look similar toohello following.</span></span>

![예제 SAML 출력][saml_output]

<span data-ttu-id="78e8f-108">ACS에 대 한 자세한 내용은 참조 hello [다음 단계](#next_steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="78e8f-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="78e8f-109">hello Azure 액세스 서비스 제어 필터는 community technology preview 합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="78e8f-110">이 필터는 시험판 소프트웨어로서 Microsoft에서 공식적으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="78e8f-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="78e8f-111">Prerequisites</span></span>
<span data-ttu-id="78e8f-112">이 가이드에서는 완벽 toocomplete hello 작업 샘플은 hello [어떻게 tooAuthenticate Azure 액세스 제어 서비스를 사용 하 여 Eclipse 웹 사용자를](active-directory-java-authenticate-users-access-control-eclipse.md) hello이이 자습서의 시작 지점으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="78e8f-113">Hello JspWriter 라이브러리 tooyour 빌드 경로 배포 어셈블리 추가</span><span class="sxs-lookup"><span data-stu-id="78e8f-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="78e8f-114">Hello를 포함 하는 hello 라이브러리 추가 **javax.servlet.jsp.JspWriter** 클래스 tooyour 경로 배포 어셈블리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="78e8f-115">Hello 라이브러리는 Tomcat을 사용 하는 경우 **jsp api.jar**, Apache hello에 있는 **lib** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="78e8f-116">Eclipse의 프로젝트 탐색기에서 마우스 오른쪽 단추로 클릭 **MyACSHelloWorld**, 클릭 **빌드 경로**, 클릭 **빌드 경로 구성**, hello 클릭 **라이브러리** 탭을 클릭 한 다음 **외부 단지 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="78e8f-117">Hello에 **JAR 선택** 대화 상자에서 toohello 이동 필요한 JAR를 선택한 다음 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="78e8f-118">Hello로 **MyACSHelloWorld에 대 한 속성** 대화 계속 열려 클릭 **배포 어셈블리**합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="78e8f-119">Hello에 **웹 배포 어셈블리** 대화 상자를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="78e8f-120">Hello에 **새 어셈블리 지시문** 대화 상자에서 클릭 **Java 빌드 경로 항목** 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="78e8f-121">Hello 적절 한 라이브러리를 선택 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="78e8f-122">클릭 **확인** tooclose hello **MyACSHelloWorld에 대 한 속성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="78e8f-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="78e8f-123">Hello JSP 파일 toodisplay SAML 수정</span><span class="sxs-lookup"><span data-stu-id="78e8f-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="78e8f-124">수정 **index.jsp** 코드 다음 toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="78e8f-125">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78e8f-125">Run hello application</span></span>
1. <span data-ttu-id="78e8f-126">Hello 컴퓨터 에뮬레이터에서 응용 프로그램을 실행 또는 배포에서 설명 하는 hello 단계를 사용 하 여 tooAzure [어떻게 tooAuthenticate Azure 액세스 제어 서비스를 사용 하 여 Eclipse 웹 사용자를](active-directory-java-authenticate-users-access-control-eclipse.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="78e8f-127">브라우저를 실행하여 웹 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="78e8f-128">Tooyour 응용 프로그램에 로그인 하면 hello id 공급자에서 제공 하는 hello 보안 어설션은 등의 SAML 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78e8f-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78e8f-129">Next steps</span></span>
<span data-ttu-id="78e8f-130">toofurther ACS의 기능 및 보다 복잡 한 시나리오와 tooexperiment 탐색을 참조 하십시오. [액세스 제어 서비스 2.0][Access Control Service 2.0]합니다.</span><span class="sxs-lookup"><span data-stu-id="78e8f-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
