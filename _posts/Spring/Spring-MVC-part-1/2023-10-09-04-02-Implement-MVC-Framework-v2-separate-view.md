---
title: 섹션4) MVC 프레임워크 - v2. View 분리
author: wannastudyhardyeah
date: 2023-10-09 09:20:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">
<h2 id="separate-view">1. View 분리 - v2</h2>

<h3 id="problem-for-previous-h3">1.1. 이전 문제점</h3>

```java
String viewPath 
        = "/WEB-INF/views/new-form.jsp";
RequestDispatcher dispatcher 
        = request.getRequestDispatcher(viewPath); 
dispatcher.forward(request, response);
```

&nbsp;&nbsp;&nbsp;&nbsp;모든 컨트롤러에서<br>
뷰로 이동하는 부분에 중복이 있고 깔끔하지 않음!<br>

<b>==></b> 별도로 뷰를 처리하는 객체 만들기!!!<br>

<h3 id="structrue-h3">1.2. V1의 구조</h3>

1. 클라이언트의 HTTP 요청<br>
2. FrontController --> 매핑 정보<br>
\: URL 매핑 정보에서 컨트롤러 조회<br>
3. FrontController --> Controller<br>
\: 컨트롤러 호출<br>
4. Controller --> FrontController<br>
\: ``MyView`` 반환<br>
5. FrontController --> MyView<br>
\: ``render()`` 호출<br>
6. MyView --> JSP<br>
\: JSP forward<br>
7. JSP는 HTML 응답.<br>

<h3 id="code-myview-v2-h3">1.3. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MyView</code></h3>

``/servlet/web/frontcontroller``에서<br>
```java
public class MyView {
    private String viewPath;

    public MyView(String viewPath) {
        this.viewPath = viewPath;
    }

    public void render(HttpServletRequest request, 
                       HttpServletResponse response)
            throws ServletException, IOException {
        RequestDispatcher dispatcher 
                = request.getRequestDispatcher(viewPath);
        dispatcher.forward(request, response);
    }
}
```

``MyView``의 객체는 다른 버전에서도 함께 사용 예정.<br>

<h3 id="code-controller-v2-h3">1.4. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ControllerV2</code></h3>

``/servlet/web/frontcontroller/v2``에서<br>
```java
public interface ControllerV2 {

    MyView process(HttpServletRequest request, 
                   HttpServletResponse response)
            throws ServletException, IOException;
}
```

<h4 id="code-member-form-controller-v2-h4">1.4.1 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberFormControllerV2</code> - 회원 등록 폼</h4>

``/servlet/web/frontcontroller/v2/controller``에서<br>
```java
public class MemberFormControllerV2 
        implements ControllerV2 {
    @Override
    public MyView process(HttpServletRequest request, 
                          HttpServletResponse response) 
                    throws ServletException, IOException {
        return new MyView("/WEB-INF/views/new-form.jsp");
    }
}
```

&nbsp;&nbsp;&nbsp;&nbsp;``dispatcher.forward()`` 직접 생성 및 호출<br>
<b>==></b> ``MyView`` 객체 생성 후 뷰 이름만 넣고 반환<br>

<h4 id="code-member-save-controller-v2-h4">1.4.2. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberSaveControllerV2</code> - 회원 저장</h4>

``/servlet/web/frontcontroller/v2/controller``에서<br>
```java
public class MemberSaveControllerV2 implements ControllerV2 {

    private MemberRepository memberRepository 
            = MemberRepository.getInstance();

    @Override
    public MyView process(HttpServletRequest request, 
                          HttpServletResponse response) 
                    throws ServletException, IOException {
        String username 
                = request.getParameter("username");
        int age 
                = Integer.parseInt(request.getParameter("age"));

        Member member 
                = new Member(username, age);
        memberRepository.save(member);

        // Model에 데이터를 보관한다.
        request.setAttribute("member", member);

        return new MyView("/WEB-INF/views/save-result.jsp");
    }
}
```

<h4 id="code-member-list-controller-v2-h4">1.4.3 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberListControllerV2</code> - 회원 목록</h4>

``/servlet/web/frontcontroller/v2/controller``에서<br>
```java
public class MemberListControllerV2 
        implements ControllerV2 {
    private MemberRepository memberRepository 
            = MemberRepository.getInstance();

    @Override
    public MyView process(HttpServletRequest request, 
                          HttpServletResponse response) 
                    throws ServletException, IOException {
        List<Member> members 
                = memberRepository.findAll();
        request.setAttribute("members", members);
        return new MyView("/WEB-INF/views/members.jsp");
    }
}
```

<h4 id="code-front-controller-v2-h4">1.4.4 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">FrontControllerServletV2</code> - 프론트 컨트롤러</h4>

``/servlet/web/frontcontroller/v2``에서<br>
```java
@WebServlet(name = "frontControllerServletV2", 
            urlPatterns = "/front-controller/v2/*")
public class FrontControllerServletV2 
        extends HttpServlet {

    private Map<String, ControllerV2> controllerMap 
            = new HashMap<>();

    public FrontControllerServletV2() {
        controllerMap
            .put("/front-controller/v2/members/new-form",
                new MemberFormControllerV2());
        controllerMap
            .put("/front-controller/v2/members/save",
                new MemberSaveControllerV2());
        controllerMap
            .put("/front-controller/v2/members",
                new MemberListControllerV2());
    }

    @Override
    protected void service(HttpServletRequest request, 
                           HttpServletResponse response)
            throws ServletException, IOException {

        String requestURI 
                = request.getRequestURI();

        ControllerV2 controller 
                = controllerMap.get(requestURI);
        if (controller == null) {
            response
                .setStatus(HttpServletResponse
                                .SC_NOT_FOUND);
            return;
        }

        MyView view 
                = controller.process(request, 
                                    response);
        view.render(request, response);
    }
}
```