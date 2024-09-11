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
   b. 그 외 다른 메서드의 이름은 카멜 표기법을 따른다.
     ```
     private:
         void doSomething();
     ```
6. 단, 단순히 불(bool) 상태를 반환하는 메서드의 동사 부분은 최대한 Is, Can, Has, Should를 사용하되 그러는 것이 부자연스러울 경우에는 상태를 나타내는 다른 3인칭 단수형 동사를 사용한다.
   ```
   public:
       bool IsAlive(const Person& person) const;
       bool HasChild(const Person& person) const;
       bool CanAccept(const Person& person) const;
       bool ShouldDelete(const Person& person) const;
       bool Exists(Person& person) const;
   ```
7. 상수 또는 #define으로 정의된 상수의 이름은 모두 대문자로 하되 밑줄로 각 단어를 분리한다.
   ```
   constexpr int SOME_CONSTANT = 1;
   ```
8. 네임스페이스는 모두 소문자로 작성한다.
   ```
   namespace abc{};
   ```
9. 불(boolean)형 변수는 앞에 b를 붙인다.
    ```
    bool bFired;    // 지역 변수와 public 멤버 변수의 경우
    bool mbFired;   // 클래스의 private 멤버 변수의 경우
    bool m_bFired;  // 클래스의 private 멤버 변수의 경우
    ```
10. 인터페이스를 선언할 때는 앞에 I를 붙인다.
   ```
   class ISomeInterface;
   ```
11. 열거형을 선언할 때는 앞에 e를 붙인다.
    ```
    enum class eDirection
    {
        North,
        South
    }
    ```
12. **클래스 멤버 변수명은 앞에 m or m_을 붙인다.**
    ```
    class Employee
    {
    protected:
        int mDepartmentID;
    private:
        int m_Age;
    }
    ``` 
13. ~~goto 레이블 명은 모두 대문자로 하되 밑줄로 각 단어를 분리한다.~~ (goto 지양!)
    ```
    goto MY_LABEL;

    // ...

    MY_LABEL:
        std::cout << "Magic!"" << std::endl;
        return 0;
    ```
14. 값을 반환하는 함수의 이름은 무엇을 반환하는지 알 수 있게 짓는다.
    ```
    uint32_t GetAge() const;
    ```
15. **단순히 반복문에 사용되는 변수가 아닌 경우에 i, e같은 변수명 대신 index, employee처럼 변수에 저장되는 데이터를 한 눈에 알아볼 수 있는 변수명을 사용한다.**
16. 뒤에 추가적인 단어가 오지 않는 경우 줄임말은 모두 대문자로 표기한다.
    ```
    int OrderID;
    int HttpCode;
    ```














































































