---
title: 섹션4) MVC 프레임워크 - v4. 단순, 실용적인 컨트롤러
author: wannastudyhardyeah
date: 2023-10-09 09:40:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">
<h2 id="simple-and-useful-controller">1. 단순하고 실용적인 컨트롤러 - v4</h2>

&nbsp;&nbsp;&nbsp;&nbsp;컨트롤러 인터페이스 구현하는 개발자 입장에서<br>
항상 ``ModelView`` 객체를 생성 및 반환해야 하는 점이 번거로움!<br>
<b>==></b> 개발자가 단순, 편리하게 사용 가능하도록!!!<br>
&nbsp;&nbsp;&nbsp;(즉, 실용성!)<br>

<h3 id="structrue-h3">1.1. V4의 구조</h3>

1. 클라이언트의 HTTP 요청<br>
2. FrontController --> 매핑 정보<br>
\: URL 매핑 정보에서 컨트롤러 조회<br>
3. FrontController --> Controller<br>
\: 호출(``paramMap``, ``model``)<br>
4. Controller --> FrontController<br>
\: ``viewName`` 반환<br>
5. FrontController --> viewResolver<br>
\: ``viewResolver`` 호출<br>
6. viewResolver --> FrontController<br>
\: ``MyView`` 반환<br>
7. FrontController --> MyView<br>
\: ``render(model)`` 호출<br>
8. MyView<br>
\: HTML 응답<br>

&nbsp;&nbsp;&nbsp;&nbsp;기본적 구조는 V3와 동일<br>
<b>But,</b> 컨트롤러가 ``ModelView`` 반환하는 대신에,<br>
&nbsp;&nbsp;&nbsp;``ViewName``만 반환함.<br>

<h3 id="code-controller-v4-h3">1.2. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ControllerV4</code></h3>

``/servlet/web/frontcontroller/v4``에서<br>
```java
public interface ControllerV4 {
    /**
     *
     * @param paramMap
     * @param model
     * @return
     */
    String process(Map<String, String> paramMap, Map<String, Object> model);
}
```
&nbsp;&nbsp;&nbsp;&nbsp;V4에서는 인터페이스에 ``ModelView`` 없음!<br>
``model`` 객체는 패러미터로 전달되는 것.<br>
결과로는 ``view``의 이름만 반환.<br>


<h4 id="code-member-form-controller-v4-h4">1.2.1 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberFormControllerV4</code> - 회원 등록 폼</h4>

``/servlet/web/frontcontroller/v4/controller``에서<br>
```java
public class MemberFormControllerV4 
        implements ControllerV4 {

    @Override
    public String process
            (Map<String, String> paramMap, 
             Map<String, Object> model) {
        // 여기선 model도 만들 필요가 없다!
        // FrontController에서 만들어서 넘겨줄 거라서
        return "new-form";
    }
}
```

&nbsp;&nbsp;&nbsp;&nbsp;``new-form``이라는<br>
view의 논리적 이름만 반환함.<br>

<h4 id="code-member-save-controller-v4-h4">1.2.2. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberSaveControllerV4</code> - 회원 저장</h4>

``/servlet/web/frontcontroller/v4/controller``에서<br>
```java
public class MemberSaveControllerV4 
        implements ControllerV4 {

    private MemberRepository memberRepository 
                        = MemberRepository.getInstance();

    @Override
    public String process
            (Map<String, String> paramMap, 
             Map<String, Object> model) {
        String username 
                = paramMap.get("username");
        int age 
                = Integer
                    .parseInt(paramMap
                                .get("age"));

        Member member 
                = new Member(username, age);
        memberRepository.save(member);

        model.put("member", member);
        return "save-result";
    }
}
```

<h4 id="code-member-list-controller-v4-h4">1.2.3 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MemberListControllerV4</code> - 회원 목록</h4>

``/servlet/web/frontcontroller/v4/controller``에서<br>
```java
public class MemberListControllerV4 
        implements ControllerV4 {

    private final MemberRepository 
        memberRepository = MemberRepository.getInstance();

    @Override
    public String process
            (Map<String, String> paramMap, 
             Map<String, Object> model) {
        List<Member> members 
                        = memberRepository.findAll();

        model.put("members", members);
        return "members";
    }
}
```

<h4 id="code-front-controller-v4-h4">1.2.4 <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">FrontControllerServletV4</code> - 프론트 컨트롤러</h4>

``/servlet/web/frontcontroller/v4``에서<br>
```java
@WebServlet(name = "frontControllerServletV4", 
            urlPatterns = "/front-controller/v4/*")
public class FrontControllerServletV4 
        extends HttpServlet {

    private Map<String, ControllerV4> 
        controllerMap = new HashMap<>();

    public FrontControllerServletV4() {
        controllerMap
            .put("/front-controller/v4/members/new-form", 
                new MemberFormControllerV4());
        controllerMap
            .put("/front-controller/v4/members/save", 
                new MemberSaveControllerV4());
        controllerMap
            .put("/front-controller/v4/members", 
                new MemberListControllerV4());
    }

    @Override
    protected void service
            (HttpServletRequest request, 
             HttpServletResponse response) 
            throws ServletException, IOException {
        String requestURI 
                = request.getRequestURI();

        ControllerV4 controller 
                        = controllerMap.get(requestURI);
        if (controller == null) {
            response
                .setStatus(HttpServletResponse
                                .SC_NOT_FOUND);
            return;
        }

        Map<String, String> paramMap 
                            = createParamMap(request);
        /* 추가된 부분 */
        Map<String, Object> model 
                            = new HashMap<>();
        /* ----------- */
        String viewName = controller
                            .process(paramMap, model);

        MyView view 
                = viewResolver(viewName);
        view.render(model, 
                    request, response);
    }

    private MyView viewResolver(String viewName) {
        return new MyView("/WEB-INF/views/" 
                        + viewName 
                        + ".jsp");
    }

    private Map<String, String> createParamMap
                (HttpServletRequest request) {
        Map<String, String> paramMap 
                                = new HashMap<>();
        request
            .getParameterNames()
                .asIterator()
                .forEachRemaining(
                    paramName 
                        -> paramMap
                                .put(paramName, 
                                     request
                                        .getParameter(paramName)
                                )
                );
        return paramMap;
    }
}
```

- <b>``Map<String, Object> model = new HashMap<>()``</b><br>
\: 모델 객체를<br>
프론트 컨트롤러에서 생성하여 넘겨줌.<br>