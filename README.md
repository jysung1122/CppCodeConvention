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






































































