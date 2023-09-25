---
title: 섹션3) 회원 관리 웹 애플리케이션 요구사항
author: wannastudyhardyeah
date: 2023-09-25 10:10:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

&nbsp;&nbsp;기본적인 "회원 관리 웹 애플리케이션"을 통해<br>
서블릿, JSP, MVC 패턴의 순서대로<br>
각각 적용하여 개발해본다!<br>

<h2 id="member-app-needs">1. 회원 관리 웹 애플리케이션 요구사항</h2>

<b style="font-size:1.2rem">회원 정보</b><br>
- 이름<br>
\: ``username``<br>
- 나이<br>
\: ``age``<br>

<b style="font-size:1.2rem">기능 요구사항</b><br>
- 회원 저장<br>

- 회원 목록 조회<br>

<h3 id="member-domain-model-h3">1.1. 회원 도메인 모델</h3>

``/main/~/hello/servlet/domain/member``에서<br>
``Member.java`` 생성하여 아래와 같이 작성.<br>

```java
@Getter @Setter
public class Member {
    // 필드(3가지)
    private Long id;
    private String username;
    private int age;

    // 기본 생성자
    public Member() {
    }

    // 생성자(2가지 요소 가짐)
    public Member(String username, int age) {
        this.username = username;
        this.age = age;
    }
}
```

<h3 id="member-repository-h3">1.2. 회원 저장소</h3>

동일 디렉터리에<br>
``MemberRepository.java`` 생성.<br>

```java
/*
 *  동시성 문제 고려되지 않음!
 *  실무에선 ConcurrentHashMap, AtomicLong 사용 고려
 */
public class MemberRepository {
    private static Map<Long, Member> store 
                    = new HashMap<>();
    private static long sequence = 0L;

    // 싱글톤으로 만들기
    private static final MemberRepository instance 
                    = new MemberRepository();

    public static MemberRepository getInstance() {
        return instance;
    }

    private MemberRepository() {
    }

    // 저장
    public Member save(Member member) {
        // id 값 추가 (1씩 증가)
        member.setId((++sequence));
        store.put(member.getId(), member);
        return member;
    }

    public Member findById(Long id) {
        return store.get(id);
    }

    // 회원 목록
    public List<Member> findAll() {
        // store 자체를 보호하기 위해 이렇게!
        return new ArrayList<>(store.values());
    }

    // 테스트용
    public void clearStore() {
        store.clear();
    }
}
```

테스트 코드 작성

```java
class MemberRepositoryTest {

    MemberRepository memberRepository = MemberRepository.getInstance();

    @AfterEach
    void afterEach() {
        // clearstore() 없이 실행 시 문제 생김
        // 데이터 저장 관련 문제 (순서 보장 X)
        memberRepository.clearStore();
    }

    @Test
    void getInstance() {
    }

    @Test
    void save() {
        // given
        Member member = new Member("hello", 20);

        // when
        Member savedMember = memberRepository.save(member);

        // then
        Member findMember = memberRepository.findById(savedMember.getId());
        Assertions.assertThat(findMember).isEqualTo(savedMember);
    }

    @Test
    void findById() {
    }

    @Test
    void findAll() {
        // given
        Member member1 = new Member("member1", 20);
        Member member2 = new Member("member2", 30);

        memberRepository.save(member1);
        memberRepository.save(member2);

        // when
        List<Member> result = memberRepository.findAll();

        // then
        Assertions.assertThat(result.size()).isEqualTo(2);
        Assertions.assertThat(result).contains(member1, member2);
    }

    @Test
    void clearStore() {
    }
}
```