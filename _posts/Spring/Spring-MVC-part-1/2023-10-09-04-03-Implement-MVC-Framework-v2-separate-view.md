---
title: 섹션4) MVC 프레임워크 - v3. Model 추가
author: wannastudyhardyeah
date: 2023-10-09 09:30:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">
<h2 id="add-model">1. Model 추가 - v3</h2>

<h3 id="feature-h3">1.1. 기능</h3>

<h4 id="remove-dependencies-for-servlet-h4">- 서블릿 종속성 제거</h4>

&nbsp;&nbsp;&nbsp;&nbsp;컨트롤러 입장에서<br>
``HttpServletRequest``, ``HttpServletResponse``는 불필요!<br>
&nbsp;&nbsp;&nbsp;&nbsp;요청 패러미터 정보는 자바 ``Map``으로 대신 넘기면<br>
현 구조에선 컨트롤러가 서블릿 몰라도 동작 가능<br>

&nbsp;&nbsp;&nbsp;&nbsp;``request`` 객체를 Model로 사용 부분<br>
<b>==></b> 별도의 ``Model`` 객체 만들어서 반환하기<br>

&nbsp;&nbsp;<b style="font-size:1.15rem">궁극적 목표</b><br>
\: 컨트롤러가 서블릿 기술 전혀 사용 않도록 변경하기!<br>

<h4 id="remove-duplicated-view-names-h4">- 뷰 이름 중복 제거</h4>

&nbsp;&nbsp;<b style="font-size:1.15rem">궁극적 목표</b><br>
\: 컨트롤러는 <b><i>뷰의 논리 이름</i></b> 반환하고,<br>
실제 물리 위치 이름은 프론트 컨트롤러에서 처리하도록<br>
단순화하기!!!<br>

<h3 id="structrue-h3">1.2. V3의 구조</h3>

1. 클라이언트의 HTTP 요청<br>
2. FrontController --> 매핑 정보<br>
\: URL 매핑 정보에서 컨트롤러 조회<br>
3. FrontController --> Controller<br>
\: 컨트롤러 호출<br>
4. Controller --> FrontController<br>
\: ``ModelView`` 반환<br>
5. FrontController --> viewResolver<br>
\: ``MyView`` 반환<br>
6. FrontController --> MyView<br>
\: ``render(model)`` 호출<br>
7. MyView<br>
\: HTML 응답.<br>

<h3 id="code-modelview-v2-h3">1.3. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ModelView</code></h3>

&nbsp;&nbsp;&nbsp;&nbsp;지금까지는<br>
서블릿에 종속적인 ``HttpServletRequest`` 사용했고,<br>
``Model``도 ``request.setAttribute()`` 통해<br>
데이터 저장하고 뷰에 전달.
&nbsp;&nbsp;&nbsp;&nbsp;Model 직접만들고,
View 이름 전달하는 객체 만들기

``/servlet/web/frontcontroller``에서<br>
```java
public class ModelView {
    private String viewName;
    private Map<String, Object> model = new HashMap<>();

    public ModelView(String viewName) {
        this.viewName = viewName;
    }

    public String getViewName() {
        return viewName;
    }

    public void setViewName(String viewName) {
        this.viewName = viewName;
    }

    public Map<String, Object> getModel() {
        return model;
    }

    public void setModel(Map<String, Object> model) {
        this.model = model;
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

<h4 id="code-member-form-controller-v2-h4">1.4.1 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberFormControllerV3</code> - 회원 등록 폼</h4>

``/servlet/web/frontcontroller/v3/controller``에서<br>
```java
public class MemberFormControllerV3 implements ControllerV3 {
    @Override
    public ModelView process(Map<String, String> paramMap) {
        return new ModelView("new-form");
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