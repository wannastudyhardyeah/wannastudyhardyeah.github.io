---
title: 섹션4) MVC 프레임워크 - v1. 프론트 컨트롤러 도입
author: wannastudyhardyeah
date: 2023-10-09 08:20:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2 id="introduce-front-controller">1. 프론트 컨트롤러 V1 도입</h2>

<h3 id="structrue-h3">1.1. V1의 구조</h3>

1. 클라이언트의 HTTP 요청<br>
2. FrontController --> 매핑 정보<br>
\: URL 매핑 정보에서 컨트롤러 조회<br>
3. FrontController --> Controller<br>
\: 컨트롤러 호출<br>
4. Controller --> JSP<br>
\: 컨트롤러에서 JSP forward<br>
5. JSP는 HTML 응답.<br>

<h3 id="code-front-controller-v1-h3">1.2. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ControllerV1</code> 인터페이스</h3>

``/servlet/web/frontcontroller/v1``에서<br>
```java
public interface ControllerV1 {

    void process(HttpServletRequest request, 
                HttpServletResponse response)
            throws ServletException, IOException;
}
```

&nbsp;&nbsp;&nbsp;&nbsp;서블릿과 비슷한 모양의 Controller 인터페이스 도입.<br>
각 컨트롤러들은 이 인터페이스를 구현하면 됨.<br>
<b>==></b> 이 인터페이스 통하여 프론트 컨트롤러는<br>
&nbsp;&nbsp;구현과 관계없이 로직의 일관성 가져갈 수 있음.<br>

<h4 id="code-member-form-controller-v1-h4">1.2.1 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberFormControllerV1</code> - 회원 등록 컨트롤러</h4>

``/servlet/web/frontcontroller/v1/controller``에서<br>
```java
public class MemberFormControllerV1 implements ControllerV1 {

    @Override
    public void process(HttpServletRequest request, 
                        HttpServletResponse response)
            throws ServletException, IOException {
        String viewpath 
                = "/WEB-INF/views/new-form.jsp";
        RequestDispatcher dispatcher 
                = request.getRequestDispatcher(viewpath);
        dispatcher.forward(request, response);
    }
}
```

<h4 id="code-member-save-controller-v1-h4">1.2.2 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberSaveControllerV1</code> - 회원 저장 컨트롤러</h4>

``/servlet/web/frontcontroller/v1/controller``에서<br>
```java
public class MemberSaveControllerV1 implements ControllerV1 {

    private MemberRepository memberRepository 
            = MemberRepository.getInstance();
    
    @Override
    public void process(HttpServletRequest request, 
                        HttpServletResponse response) 
                    throws ServletException, IOException {

        String username 
                = request.getParameter("username");
        int age 
                = Integer.parseInt(request.getParameter("age"));

        Member member = new Member(username, age);
        memberRepository.save(member);
        
        //Model에 데이터 보관
        request.setAttribute("member", member);

        String viewPath 
                = "/WEB-INF/views/save-result.jsp";
        RequestDispatcher dispatcher 
                = request.getRequestDispatcher(viewPath);
        dispatcher.forward(request, response);
    }
}
```

<h4 id="code-member-list-controller-v1-h4">1.2.3 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberListControllerV1</code> - 회원 목록 컨트롤러</h4>

``/servlet/web/frontcontroller/v1/controller``에서<br>
```java
public class MemberListControllerV1 implements ControllerV1 {

    private MemberRepository memberRepository 
            = MemberRepository.getInstance();

    @Override
    public void process(HttpServletRequest request, 
                        HttpServletResponse response) 
                    throws ServletException, IOException {

        List<Member> members 
                = memberRepository.findAll();

        request.setAttribute("members", members);

        String viewPath 
                = "/WEB-INF/views/members.jsp";
        RequestDispatcher dispatcher 
                = request.getRequestDispatcher(viewPath);
        dispatcher.forward(request, response);
    }
}
```

<h4 id="code-front-controller-v1-h4">1.2.4 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">FrontControllerServletV1</code> - 프론트 컨트롤러</h4>

```java
@WebServlet(name = "frontControllerServletV1", 
            urlPatterns = "/front-controller/v1/*")
public class FrontControllerServletV1 
        extends HttpServlet {

    private Map<String, ControllerV1> controllerMap 
            = new HashMap<>();

    public FrontControllerServletV1() {
        controllerMap.put("/front-controller/v1/members/new-form",
                new MemberFormControllerV1());
        controllerMap.put("/front-controller/v1/members/save",
                new MemberSaveControllerV1());
        controllerMap.put("/front-controller/v1/members",
                new MemberListControllerV1());
    }

    @Override
    protected void service
        (HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        System.out.println("FrontControllerServletV1.service");

        String requestURI 
                = request.getRequestURI();

        ControllerV1 controller 
                = controllerMap.get(requestURI);
        if (controller == null) {
            response
                .setStatus(HttpServletResponse.SC_NOT_FOUND);
            return;
        }

        controller.process(request, response);
    }
}
```
<br>
- <b>``controllerMap``</b><br>
    - key<br>
    \: 매핑 URL<br>
    - value<br>
    \: 호출될 컨트롤러<br>
    &nbsp;&nbsp;(``ControllerV1``)<br>

- <b>``service()``</b><br>
    1. 먼저 ``requestURI`` 조회<br>
    2. 실제 호출할 컨트롤러를<br>
    ``controllerMap``에서 찾음.<br>
    3. 없을 시엔<br>
    ``404`` 상태 코드 반환.<br>
    4. 컨트롤러 찾고<br>
    ``controller.process(req, res) 호출하여<br>
    해당 컨트롤러 실행.<br>