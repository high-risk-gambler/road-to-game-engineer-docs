# 상속과 다형성



```cpp
class player : public character {
public:
  player() {};
};
```

위는 C++ 다중상속 문법임 상속에도 접근 지정자가 있는데 , public private 이 있다.

기본적으로 모든 클래스에 private 을 적용함, 따라서 만약에 다중상속을 하는데 , 전부다 public 으로 상속 받으려면&#x20;

```cpp
class player : public character , public Tset{
public:
  player() {};
};
```



위 코드 처럼 둘다 접근 지정자를 public 으로 명시해야한다.





C++ 에서는 다형성을 JAVA 랑 다른 방식으로 제공한다C++과 Java의 다형성

Java는 일반적인 인스턴스 메서드를 오버라이딩하면, 부모 타입의 참조로 호출해도 실제 자식 객체의 메서드가 실행된다.

C++은 **부모 함수를 `virtual`로 선언해야** 부모 타입의 포인터나 참조로 호출할 때 자식의 재정의된 함수가 실행된다.

* **부모의 `virtual`**: 실제 객체의 타입에 따라 호출할 함수를 결정하게 한다.
* **자식의 `override`**: 부모의 가상 함수를 올바르게 재정의했는지 컴파일러가 검사한다. 필수는 아니지만 사용하는 것이 좋다.

부모에서 가상 함수로 선언하면 자식에서도 그 성질이 유지된다. 따라서 자식에서는 `void attack_special(player target_player) override;`로 작성하면 충분하다.

예제처럼 앞에 `virtual`까지 붙여도 올바른 문법이지만, **자식의 `virtual`은 생략해도 동작이 같다.**



#### 생성자에서 다른 생성자 호출



```cpp
class monster {
public:
  monster() {
    cout << "monster 클래스 생성자" << endl;
  };
  virtual ~monster() {
    //~monster() {
    cout << "monster 클래스 소멸자" << endl;
  };
};

//몬스터 A는 기본 Monster 클래스로부터 상속
class monster_a : public monster, character {
public:
  monster_a() : monster_a(10, 10) {
    cout << "monster_a 클래스 생성자" << endl;
  };

  monster_a(int x, int y) : location{ x, y } {
    cout << "monster_a 클래스 생성자 (매개변수 추가)" << endl;
  };

  void show_location() {
    cout << "위치(" << location[0] << " , " << location[1] << ")" << endl;
  };

private:
  int location[2];
};
```
