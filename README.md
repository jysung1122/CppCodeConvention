# CppCodeConvention

[C++ 코드 컨벤션 참고](https://docs.popekim.com/ko/coding-standards/cpp)
----
회사와 집에서 계속해서 읽기 위해 작성함.

## 기본 원칙
1. 가독성을 최우선으로 삼는다. (대부분의 경우 코드는 그 자체가 문서의 역할을 해야 함)
2. 문제가 있을 경우 최대한 빨리 크래시가 나거나 assert에 걸리도록 코드를 작성한다. 어떻게든 프로그램이 돌게 만들다가 나중에 크래시가 나는 것보다 나쁜 상황은 없다.
3. 정말 합당한 이유가 있지 않는 한, IDE의 자동 서식을 따른다. (비주얼 스튜디오의 Ctrl + K + D 기능)
4. 본 코딩 표준을 따라 잘 짜여진 기존의 코드에서 배운다.

## I. 메인 코딩 표준
1. **클래스와 구조체의 이름은 파스칼 표기법을 따른다.**
   ```
   class PlayerManager;
   struct AnimationInfo;
   ```
2. **지역 변수 그리고 함수의 매개 변수의 이름은 카멜 표기법을 따른다.**
   ```
   void SomeMethod(const int someParameter)
   {
       int someNumber;
       int id;
   }
   ```
3. 정적(static) 변수의 이름 앞에는 s를 붙인다.
   ```
   static int sNumMonsters;    // 지역 변수와 public 멤버 변수의 경우
   static bool sbInitialized;  // 클래스의 private static 변수의 경우
   ```
4. **메서드의 이름은 동사-목적어 쌍으로 표기한다.**

   a. public 메서드의 이름은 파스칼 표기법을 따른다.
     ```
     public:
         void DoSomething();
     ```
   b. ~~그 외 다른 메서드의 이름은 카멜 표기법을 따른다.~~
     ```
     private:
         void doSomething();
     ```
5. 단, 단순히 불(bool) 상태를 반환하는 메서드의 동사 부분은 최대한 Is, Can, Has, Should를 사용하되 그러는 것이 부자연스러울 경우에는 상태를 나타내는 다른 3인칭 단수형 동사를 사용한다.
   ```
   public:
       bool IsAlive(const Person& person) const;
       bool HasChild(const Person& person) const;
       bool CanAccept(const Person& person) const;
       bool ShouldDelete(const Person& person) const;
       bool Exists(Person& person) const;
   ```
6. 상수 또는 #define으로 정의된 상수의 이름은 모두 대문자로 하되 밑줄로 각 단어를 분리한다.
   ```
   constexpr int SOME_CONSTANT = 1;
   ```
7. 네임스페이스는 모두 소문자로 작성한다.
   ```
   namespace abc{};
   ```
8. 불(boolean)형 변수는 앞에 b를 붙인다.
    ```
    bool bFired;    // 지역 변수와 public 멤버 변수의 경우
    bool mbFired;   // 클래스의 private 멤버 변수의 경우
    bool m_bFired;  // 클래스의 private 멤버 변수의 경우
    ```
9. 인터페이스를 선언할 때는 앞에 I를 붙인다.
    ```
    class ISomeInterface;
    ```
10. 열거형을 선언할 때는 앞에 e를 붙인다.
    ```
    enum class eDirection
    {
        North,
        South
    }
    ```
11. **클래스 멤버 변수명은 앞에 m or m_을 붙인다.**
    ```
    class Employee
    {
    protected:
        int mDepartmentID;
    private:
        int m_Age;
    }
    ``` 
12. ~~goto 레이블 명은 모두 대문자로 하되 밑줄로 각 단어를 분리한다.~~ (goto 지양!)
    ```
    goto MY_LABEL;

    // ...

    MY_LABEL:
        std::cout << "Magic!"" << std::endl;
        return 0;
    ```
13. 값을 반환하는 함수의 이름은 무엇을 반환하는지 알 수 있게 짓는다.
    ```
    uint32_t GetAge() const;
    ```
14. **단순히 반복문에 사용되는 변수가 아닌 경우에 i, e같은 변수명 대신 index, employee처럼 변수에 저장되는 데이터를 한 눈에 알아볼 수 있는 변수명을 사용한다.**
15. 뒤에 추가적인 단어가 오지 않는 경우 줄임말은 모두 대문자로 표기한다.
    ```
    int OrderID;
    int HttpCode;
    ```
16. 클래스 멤버 변수에 접근할 때는 항상 setter와 getter를 사용한다.

      틀린 방식
      ```
      class Employee
      {
      public:
         string Name;
      }
      ```
      올바른 방식
      ```
      class Employee
      {
      public:
         const string& GetName() const;
         void SetName(const string& name);
      private:
         string m_Name;
      }
      ```
17. 구조체는 오직 public 멤버 변수만 가질 수 있다. 구조체의 멤버 변수명은 파스칼 표기법을 따르며, 구조체 안에서 함수는 사용하지 않는다.
      ```
      struct MeshData
      {
         int32_t VertexCount;
      }
      ```
18. 외부 헤더 파일을 인클루드할 때는 #include<>을 사용. 자체적으로 만든 헤더 파일을 인클루드할 때는 #include ""를 사용한다.
19. 외부 헤더 파일을 먼저 인클루드한 뒤, 내부 헤더 파일을 인클루드 한다. 인클루드를 할 때, 가능하다면 알파벳 순서를 따른다.
      ```
      #include <vector>
      #include <unordered_map>

      #include "AnimationInfo.h"
      ```
20. 모든 헤더 파일 첫 번째 줄에 #pragma once를 기재한다.
21. 지역 변수를 선언할 때는 그 지역 변수를 사용하는 코드와 동일한 줄에 선언하는 것을 원칙으로 한다.
      ```
      int a = 10;
      ```
22. double이 반드시 필요한 경우가 아닌 이상 부동 소수점 값에 f를 붙여준다.
      ```
      float f = 0.5f;
      ```
23. switch case 문에는 항상 default:를 넣는다.
      ```
      switch (number)
      {
      case 0:
         ...
         break;
      default:
         break;
      }
      ```
24. switch case 문 끝에 break;를 넣지 않고 그 바로 아래 case문의 코드를 실행하고 싶은 경우, 미리 정의해둔 FALLTHROUGH 매크로를 추가한다. 단 case 문 안에 코드가 없는 경우는 예외이다. 이는 C++ 사양에서 [[fallthrough]] 애트리뷰트로 대체될 것이다.
      ```
      switch (number)
      {
      case 0:
         DoSomeThing();
         FALLTHROUGH
      case 1:
         DoFallthrough();
         break;
      case 2:
      case 3:
         DoNotFallthrough();
         break;
      default:
         break;
      }
      ```
25. default case가 절대 실행될 일이 없는 경우, default case 안에 Assert(false); 란 코드를 추가한다. Assert()를 직접 구현하면 그 안에서 릴리즈 빌드 시 최적화 힌트를 추가할 수 있다.
      ```
      switch (type)
      {
      case 1:
         ...
         break;
      default:
         Assert(false, "unknown type");
         break;
      }
      ```
26. 원칙적으로 모든 곳에 const를 사용한다. 여기에는 지역 변수와 함수 매개 변수도 포함된다.
27. **개체를 수정하지 않는 멤버 함수에는 모두 const를 붙인다.**
      ```
      int GetAge() const;
      ```
28. **값(value) 형식의 변수를 const로 반환하지 않는다. 포인터나 참조(reference)를 반환할 경우에만 const 반환을 한다.**

      - 값 반환 시 const를 쓰지 않는 예시
      ```
      int getValue()
      {
         return 42; // 값 반환, const를 붙일 필요 없음
      }
      ```
      - 참조 반환 시 const를 사용하는 예시
      ```
      class MyClass
      {
      private:
         int value;
      public:
         // 생성자: 외부에서 값을 받아와 멤버 변수 value에 초기화
         Myclass(int v) : value(v) {}  // v 값을 멤버 변수 value에 초기화 (value = v;)

         // 값이 바뀌지 않도록 const 참조로 변환
         cont int& getValue() const
         {
            return value;
         }
      };
      ```
      - 포인터 변환 시 const를 사용하는 예시
      ```
      class MyClass
      {
      private:
         int value;
      public:
         MyClass(int v) : value(v) {}

         // 값이 바뀌지 않도록 const 포인터로 변환
         const int* getPointer() const
         {
            return &value;
         }
      };
      ```
29. 재귀 함수는 이름 뒤에 Recursive를 붙인다.
      ```
      void FibonacciRecursive();
      ```
30. **클래스 안에서 멤버 변수와 메서드의 등장 순서는 다음을 따른다.**
      - ~~friend 클래스들~~
      - public 메서드들
      - protected 메서드들
      - private 메서드들
      - public 변수들
      - protected 변수들
      - private 변수들
31. 대부분의 경우 함수 오버로딩을 피한다.

      틀린 방식
      ```
      const Anim* GetAnim(const int index) const;
      const Anim* GetAnim(const char* name) const;
      ```
      올바른 방식
      ```
      const Anim* GetAnimByIndex(const int index) const;
      const Anim* GetAnimByName(const char* name) const;
      ```
32. const 반환을 위한 함수 오버로딩은 허용한다.
      ```
      Anim* GetAnimByIndex(const int index);
      const Anim* GetAnimByIndex(const int index) const;
      ```
33. const_cast를 직접적으로 사용하지 않는다. 대신 const인 개체를 수정 가능한 형태로 변환해서 반환하는 함수를 만든다.
34. 클래스는 가각 독립된 소스파일에 있어야 한다. 단, 작은 클래스 몇 개를 한 파일 안에 같이 넣어두는 것이 상식적일 경우 예외를 허용한다.
35. **파일 이름은 대소문자까지 포함해서 반드시 클래스 이름과 일치해야 한다.**
      ```
      class PlayerAnimation;

      PlayerAnimation.cpp
      PlayerAnimation.h
      ```
36. 여러 파일이 하나의 클래스를 이룰 때, 파일 이름은 클래스 이름으로 시작하고, 그 뒤에 밑줄과 세부 항목 이름을 붙인다.
      ```
      class RenderWorld;

      RenderWorld_load.cpp
      RenderWorld_demo.cpp
      RemderWorld_portals.cpp
      ```
37. Reverse OOP 패턴을 사용할 때, 플랫폼 전용 클래스는 위 항목과 비슷한 명명 규칙을 사용한다.
      ```
      class Renderer;

      Renderer.h         // 게임에서 호출되는 모든 Renderer 인터페이스
      Renderer.cpp       // 모든 플랫폼 용 Renderer 구현 소스
      Renderer_gl.h      // Renderer가 호출하는 RendererGL 인터페이스
      Renderer_gl.cpp    // RendererGL 구현 소스
      ```
38. 표준 C assert 대신에 자신만의 Assert 버전을 구현한다.
39. 특정 조건이 반드시 충족되어야 한다고 가정(assertion)하고 짠 코드 모든 곳에 assert를 사용한다. Assert는 복구 불가능한 조건이다. Assert는 릴리즈 빌드에서 __assume 키워드로 대체하여 컴파일러에 최적화 힌트를 줄 수 있다.
40. 모든 메모리 할당은 직접 구현한 New, Delete 키워드를 통해 호출한다.
41. memset, memcpy, memmove와 같은 메모리 연산 역시 우리 고유의 MemSet, MemCpy, MemMove 키워드를 통해 호출해야 한다.
42. 어떤 이유로든 매개변수로 nullptr가 넘어올 수 있는 경우가 아니라면, 포인터 대신 참조자(&)를 사용하는 것을 원칙으로 한다. (예외는 다음 항목을 참고)
43. 함수에서 매개변수를 통해 값을 반환할 때(out 매개변수)는 포인터를 사용하며, 매개변수 이름 앞에 out을 붙인다.

      함수
      ```
      void GetSreenDimension(uint32_t* const outWidth, uint32_t* const outHeight)
      {
      }
      ```
      호출
      ```
      uint32_t width;
      uint32_t height;
      GetScreenDimension(&width, &height);
      ```
44. 위 항목의 out 매개 변수는 반드시 null이 아니어야 한다. (함수 내부에서 if 문 대신 assert를 사용할 것)
      ```
      void GetScreenDimension(uint32_t const outWidth, uint32_t const outHeight)
      {
         Assert(outWidth);
         Assert(outHeight);
      }
      ```
45. **매개 변수가 클래스 내부에서 저장될 때는 포인터를 사용한다.**
      ```
      void AddMesh(Mesh* const mesh)
      {
         mMeshCollection.push_back(mesh);
      }
      ```
46. 매개 변수가 void 포인터여야 하는 경우는 포인터를 사용한다.
      ```
      void Update(void* const something)
      {
      }
      ```
47. 비트 플래그 열거형은 이름 뒤에 Flags를 붙인다.
      ```
      enum class eVisibilityFlags
      {
      }
      ```
48. 특정 크기(예를 들어, 데이터 멤버의 직렬화를 위한 크기)가 필요하지 않은 한 열거형에 크기 지정자를 추가하지 않는다.
      ```
      enum class eDirection : uint8_t
      {
         North,
         South
      }
      ```
49. 디폴트 매개 변수 대신 함수 오버로딩을 선호한다.
50. 디폴트 매개 변수를 사용하는 경우, nullptr이나 false, 0 같이 비트 패턴이 0인 값을 사용한다.
51. 가능한 한 고정된 크기(size)의 컨테이너를 사용한다.
52. 동적 컨테이너를 사용해야 한다면 가능한 한 미리 reserve()를 호출한다.
53. #define으로 정의된 상수는 항상 괄호로 감싸준다.
      ```
      #define NUM_CLASSES (1)
      ```
54. 상수는 #define 보다 const 상수 변수로 선언한다.
55. 클래스를 상호 참조할 때는 #include보다 전방선언(foward declaration)을 최대한 이용한다.
56. 모든 컴파일러 경고는 반드시 고친다.
57. 변수 가리기(variable shadowing)는 허용되지 않는다. 외부 변수가 동일한 이름을 사용중이라면 내부 변수에는 다른 이름을 사용한다.
      ```
      class SomeClass
      {
      public:
         int32_t Count;
      public:
         void Func(const int32_t Count)
         {
            for (int32_t count = 0; count != 10; ++count)
            {
               //Use Count
            }
         }
      }
      ```
58. 한 줄에 변수 하나만 선언한다.

      틀린 방식
      ```
      int counter = 0, index = 0;
      ```
      올바른 방식
      ```
      int counter = 0;
      int index = 0;
      ```
59. 지역 객체를 반환할 때 NRVO의 이점을 활용한다. 이는 함수 내에 하나의 return문 만 쓴다는 것을 의미하며, 이것은 값으로 객체를 반환할 때만 적용된다.
60. struct나 class에서 초기화 후 값 변경을 막으려고 const 멤버 변수를 쓰지 않는다. 참조(&) 멤버 변수의 경우도 마찬가지
61. 멤버 변수를 초기화할 때는 초기화 리스트를 사용하는 것을 기본으로 한다.


## II. 소스 코드 포맷팅
1. include 전처리문 블록과 코드 본문 사이에 반드시 빈 줄이 있어야 한다.
2. 탭(tab)은 비주얼 스튜디오 기본값을 사용하며, 비주얼 스튜디오를 사용하지 않을 시 띄어쓰기 4칸을 탭으로 사용한다.
3. 중괄호( { )를 열 때는 언제나 새로운 줄에 연다
4. 중괄호 안 ( { } )에 코드가 한 줄만 있더라도 반드시 중괄호를 사용한다.
      ```
      if (bSomething)
      {
         return;
      }
      ```
5. 포인터나 참조 기호는 자료형에 붙인다.
      ```
      int& number;
      int* number;
      ```
5. 초기화 리스트를 이용해 멤버 변수를 초기화할 때는 아래와 같은 포맷을 따라 한 줄에 변수 하나씩 초기화 한다.

      틀린 방식
      ```
      MyClass::Myclass(const int var1, const int var2)
         :mVar(var1), mVar(var2), mVar(0)
      {
      ```
      올바른 방식
      ```
      MyClass::MyClass(const int var1, const int var2)
         : mVar1(var1)
         , mVar2(var2)
         , mVar3(0)
      {
      ```

## III. 최신 C++ 기능 관련
1. override 와 final 키워드를 반드시 사용한다.
2. 항상 enum class를 사용한다.
      ```
      enum class eDirection
      {
         North,
         South
      }
      ```
3. 가능한 Assert 대신 static_assert를 사용한다.
4. 포인터에 NULL 대신 nullptr를 사용한다.
5. 개체의 수명이 클래스 내에서만 처리되는 경우 unique_ptr를 사용한다. (즉, 개체 생성은 생성자에서, 개체 파괴는 소멸자에서)
6. 적용 가능한 곳이라면 범위 기반 for 문을 사용한다.
7. 반복자나 new 키워드가 같은 줄에 있어서, 어떤 개체가 만들어지는 지 명확하게 드러나는 경우가 아니라면 auto 키워드를 사용하지 않는다.
8. std::move 를 사용하여 수동으로 반환 값을 최적화하지 않는다. 이럴 경우, 자동 NRVO 최적화가 적용되지 않는다.
9. 이동 생성자(move constructor)와 이동 대입 연산자(move assignment operator)를 사용해도 된다.
10. 단순 상수 변수에는 const 대신 constexpr을 사용한다.

      적용 전
      ```
      const int DEFUALT_BUFFER_SIZE = 65536;
      ```
      적용 후
      ```
      constexpr int DEFULT_BUFFER_SIZE = 65536;
      ```

## IV. 프로젝트 설정 및 프로젝트 구조
1. Visual c++: 프로젝트 설정을 변경하려면 항상 속성 시트(property sheets)에서 변경한다.
2. 프로젝트 설정에서 컴파일 경고를 비활성화 하지 않는다. 그 대신, 코드에서 #prage를 사용한다.



















































