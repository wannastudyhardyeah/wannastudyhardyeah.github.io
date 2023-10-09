---
title: 섹션4) MVC 프레임워크 - v4. 단순, 실용적인 컨트롤러
author: wannastudyhardyeah
date: 2023-10-09 09:40:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">
<h2 id="add-model">1. 단순하고 실용적인 컨트롤러 - v4</h2>

<h3 id="feature-h3">1.1. V4 구조</h3>

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

<h3 id="code-modelview-v3-h3">1.3. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ModelView</code></h3>

&nbsp;&nbsp;&nbsp;&nbsp;지금까지는<br>
서블릿에 종속적인 ``HttpServletRequest`` 사용했고,<br>
``Model``도 ``request.setAttribute()`` 통해<br>
데이터 저장하고 뷰에 전달.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Model 직접만들고,<br>
View 이름 전달하는 객체 만들기<br>

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

<h3 id="code-controller-v3-h3">1.4. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ControllerV3</code></h3>

``/servlet/web/frontcontroller/v3``에서<br>
```java
public interface ControllerV3 {

    ModelView process(Map<String, String> paramMap);
}
```
&nbsp;&nbsp;&nbsp;&nbsp;이 컨트롤러에선 서블릿 전혀 사용 안 함!<br>
<b>==></b> 그 대신,<br>
&nbsp;&nbsp;``HttpServletRequest``가 제공하는 패러미터는<br>
&nbsp;&nbsp;프론트 컨트롤러가 ``paramMap`` 인자로 담아 호출함.<br>


<h4 id="code-member-form-controller-v3-h4">1.4.1 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberFormControllerV3</code> - 회원 등록 폼</h4>

``/servlet/web/frontcontroller/v3/controller``에서<br>
```java
public class MemberFormControllerV3 
        implements ControllerV3 {
    @Override
    public ModelView process
            (Map<String, String> paramMap) {
        return new ModelView("new-form");
    }
}
```

&nbsp;&nbsp;&nbsp;&nbsp;``ModelView`` 생성 시,<br>
``new-form``이라는 view의 논리적 이름을 지정함.<br>
(실제 물리적 이름 ==> 프론트 컨트롤러에서 처리)<br>

<h4 id="code-member-save-controller-v3-h4">1.4.2. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberSaveControllerV3</code> - 회원 저장</h4>

``/servlet/web/frontcontroller/v3/controller``에서<br>
```java
public class MemberSaveControllerV3 
        implements ControllerV3 {

    private MemberRepository memberRepository 
            = MemberRepository.getInstance();

    @Override
    public ModelView process
            (Map<String, String> paramMap) {
        String username 
                = paramMap.get("username");
        int age 
                = Integer
                    .parseInt(paramMap.get("age"));

        Member member 
                = new Member(username, age);
        memberRepository.save(member);

        ModelView mv 
                = new ModelView("save-result");
        mv.getModel().put("member", member);
        return mv;
    }
}
```

<h4 id="code-member-list-controller-v3-h4">1.4.3 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberListControllerV3</code> - 회원 목록</h4>

``/servlet/web/frontcontroller/v3/controller``에서<br>
```java
public class MemberListControllerV3 
        implements ControllerV3 {

    private MemberRepository memberRepository 
            = MemberRepository.getInstance();

    @Override
    public ModelView process
            (Map<String, String> paramMap) {
        List<Member> members 
                = memberRepository.findAll();
        ModelView mv 
                = new ModelView("members");
        mv.getModel()
            .put("members", members);

        return mv;
    }
}
```

<h4 id="code-front-controller-v3-h4">1.4.4 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">FrontControllerServletV3</code> - 프론트 컨트롤러</h4>

``/servlet/web/frontcontroller/v3``에서<br>
```java
@WebServlet(name = "frontControllerServletV3", 
            urlPatterns = "/front-controller/v3/*")
public class FrontControllerServletV3 
        extends HttpServlet {

    private Map<String, ControllerV3> controllerMap 
                                        = new HashMap<>();

    public FrontControllerServletV3() {
        controllerMap
            .put("/front-controller/v3/members/new-form",
                new MemberFormControllerV3());
        controllerMap
            .put("/front-controller/v3/members/save",
                new MemberSaveControllerV3());
        controllerMap
            .put("/front-controller/v3/members",
                new MemberListControllerV3());
    }

    @Override
    protected void service(HttpServletRequest request, 
                           HttpServletResponse response)
            throws ServletException, IOException {

        String requestURI 
                = request.getRequestURI();

        ControllerV3 controller 
                = controllerMap.get(requestURI);
        if (controller == null) {
            response.setStatus(HttpServletResponse
                                    .SC_NOT_FOUND);
            return;
        }

        // 여기서 오류 발생(일종의 시그니처)
//        MyView view = controller.process(request, response);

        Map<String, String> paramMap 
                            = createParamMap(request);
        ModelView mv 
                = controller.process(paramMap);

        String viewName 
                = mv.getViewName();
        MyView view 
                = viewResolver(viewName);

        view.render(mv.getModel(), 
                    request, response);
    }

    // 논리 이름 -> 물리 이름
    //  이렇게 변환하는 역할
    private static MyView viewResolver(String viewName) {
        return new MyView("/WEB-INF/views/" 
                        + viewName 
                        + ".jsp");
    }

    private static Map<String, String> 
            createParamMap(HttpServletRequest request) {
        Map<String, String> paramMap 
                            = new HashMap<>();
        request.getParameterNames()
                .asIterator()
                .forEachRemaining(
                    (paramName -> paramMap
                                    .put(paramName, 
                                        request
                                            .getParameter(paramName)
                                    )
                    )
                );
        return paramMap;
    }
}
```

- <b>``viewResolver()``</b><br>
\: 컨트롤러가 반환한 논리 뷰 이름을<br>
실제 물리 뷰 경로로 변경하고,<br>
실제 물리 경로가 있는 `MyView` 객체 반환함.<br>
    - 논리 뷰 이름: ``members``<br>
    - 물리 뷰 이름: ``/WEB-INF/views/members.jsp``<br>

- <b>``view.render(mv.getModel(), request, response)``</b><br>
    - 뷰 객체 통하여 HTML 화면 렌더링.<br>
    - 뷰 객체의 ``render()``는<br>
    모델 정보도 함께 받음.<br>
    - JSP는 ``request.getAttribute()``로<br>
    데이터를 조회함.<br>
    <b>--></b> 모델의 데이터를 꺼내서<br>
    &nbsp;&nbsp;``request.setAttribute()``에 담음.<br>
    - JSP로 포워드 하여<br>
    JSP를 렌더링 함.<br>

<h3 id="code-myview-v3-h3">1.5. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MyView</code></h3>

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
                            = request
                                .getRequestDispatcher(viewPath);
        dispatcher.forward(request, response);
    }

    public void render(Map<String, Object> model, 
                       HttpServletRequest request, 
                       HttpServletResponse response)
                throws ServletException, IOException {
        // model에 있는 데이터를 req. attribute로 바꿈
        modelToRequestAttribute(model, request);
        RequestDispatcher dispatcher 
                            = request
                                .getRequestDispatcher(viewPath);
        dispatcher.forward(request, response);
    }

    private static void modelToRequestAttribute
        (Map<String, Object> model, 
         HttpServletRequest request) {
        model.forEach((key, value) 
                        -> request
                            .setAttribute(key, value));
    }
}
```
