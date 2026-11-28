---
title: '## C++과 Java의 다형성 차이C++과 Ja...'
---

````markdown
## C++과 Java의 다형성 차이

C++과 Java는 상속을 통한 다형성을 제공하는 방식에 차이가 있다.

Java에서는 일반적인 인스턴스 메서드를 오버라이딩하면, **부모 타입의 참조로 자식 객체의 메서드를 호출해도 실제 객체인 자식 클래스의 메서드가 실행된다.**

단, `static` 메서드나 `private` 메서드는 이와 같은 오버라이딩 대상이 아니며, `final` 메서드는 오버라이딩할 수 없다.

C++에서는 **부모 클래스의 함수를 `virtual`로 선언해야** 부모 타입의 포인터나 참조를 통해 호출할 때 실제 자식 객체의 재정의된 함수가 실행된다.

부모 함수가 가상 함수가 아니라면, 부모 타입의 포인터나 참조를 통한 호출에서는 부모 함수가 실행된다.

### `virtual`과 `override`의 역할

```cpp
class monster {
public:
    virtual void attack_special(player target_player);
};

class monster_a : public monster {
public:
    void attack_special(player target_player) override;
};
```

- **`virtual`**: 부모 클래스에서 함수를 가상 함수로 선언한다. 부모 타입의 포인터나 참조로 호출해도 실제 객체의 타입에 따라 실행할 함수가 결정된다.
- **`override`**: 자식 클래스의 함수가 부모의 가상 함수를 올바르게 재정의했는지 컴파일러가 검사하도록 한다. 매개변수 타입 등을 잘못 작성하여 재정의가 성립하지 않으면 컴파일 오류가 발생한다.

**`override` 자체가 다형성을 켜는 것은 아니다.** 부모 함수가 이미 가상 함수라면, 자식에서 `override`를 생략해도 올바르게 재정의한 함수는 가상 함수로 동작한다. 다만 실수를 잡기 위해 `override`를 명시하는 것이 좋다.

### 예제에서 두 키워드를 모두 붙인 이유

예제의 자식 클래스에서는 다음처럼 두 키워드를 함께 사용한다.

```cpp
virtual void attack_special(player target_player) override;
```

이는 올바른 문법이며 다음 두 가지를 명시적으로 보여 준다.

- `virtual`: 이 함수는 가상 함수이다.
- `override`: 이 함수는 부모의 가상 함수를 재정의한다.

다만 **부모에서 한 번 `virtual`로 선언한 함수는 자식에서 재정의해도 가상 함수의 성질을 유지한다.** 따라서 자식에서는 `virtual`을 다시 붙일 필요가 없다.

```cpp
// 권장하는 작성 형태
void attack_special(player target_player) override;

// 예제의 작성 형태: 위 선언과 같은 의미
virtual void attack_special(player target_player) override;
```

저자의 정확한 의도는 알 수 없지만, 교육용 예제에서 가상 함수라는 점과 재정의한다는 점을 모두 강조한 것으로 볼 수 있다.

클래스 바깥에서 함수의 내용을 정의할 때는 `virtual`과 `override`를 다시 붙이지 않는다.

```cpp
void monster_a::attack_special(player target_player) {
    cout << "인텡글 공격 : 데미지 - 15 hp" << endl;
}
```

### 부모 참조로 자식 함수 호출하기

```cpp
monster_a forest_monster;

// 부모 타입의 참조로 자식 객체를 가리킨다.
monster& mon = forest_monster;

// 부모 함수가 virtual이므로 실제 객체인 monster_a의 함수가 실행된다.
mon.attack_special(player_1);
```

여기서 `mon`의 선언된 타입은 `monster&`이지만, 참조하는 실제 객체는 `monster_a`이다. 따라서 `monster_a::attack_special()`이 실행된다. 이를 **동적 바인딩**이라고 한다.

이 방식의 다형성은 부모 타입의 **포인터 또는 참조**를 통해 사용할 수 있다. 부모 객체에 자식 객체를 값으로 복사하면 자식 부분이 잘려 나가는 **객체 슬라이싱**이 발생하므로 주의해야 한다.

### 부모 함수를 명시적으로 호출하기

가상 함수여도 범위 지정 연산자 `::`로 부모 함수를 지정하면 부모의 구현을 직접 실행할 수 있다.

```cpp
monster_a& mon_a = forest_monster;

// monster_a의 함수 실행
mon_a.attack_special(player_1);

// 부모인 monster의 함수 실행
mon_a.monster::attack_special(player_1);
```
````
