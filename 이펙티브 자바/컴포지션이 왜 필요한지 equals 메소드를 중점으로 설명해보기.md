## 컴포지션이 왜 필요한지 equals 메소드를 중점으로 설명해보기

**문제 상황 - 상속 구조에서의 equals 추이성 위반**

```java
public class Point {
    private final int x;
    private final int y;

    @Override
    public boolean equals(Object o) {
        if (!(o instanceof Point)) return false;
        Point p = (Point) o;
        return p.x == x && p.y == y;
    }
}
```

```java
public class ColoredPoint extends Point {
    private final Color color;

    @Override
    public boolean equals(Object o) {
        if (!(o instanceof ColoredPoint))
            return false;
        return super.equals(o) && ((ColoredPoint) o).color == color;
    }
}
```

<br/>

```java
Point p = new Point(1, 2);
ColoredPoint cp1 = new ColoredPoint(1, 2, Color.RED);
ColoredPoint cp2 = new ColoredPoint(1, 2, Color.BLUE);
```

- p.equals(cp1) -> true
- p.equals(cp2) -> true
- 하지만 cp1.equals(cp2) -> false
- 왜냐하면 color가 다르기 때문이다 이렇게 한다면 추이성에 위반된다
- **구체 클래스를 확장해 새로운 값을 추가하면서 equals 규약을 만족시킬 방법은 존재하지 않는다.**


<br/>

**해결책 - 상속 대신 컴포지션**
- 기존 클래스를 포함하는 새 클래스를 만들어라

```java
public class ColorPoint {
    private final Point point;
    private final Color color;

    public ColorPoint(int x, int y, Color color) {
        this.point = new Point(x, y);
        this.color = color;
    }

    public Point asPoint() {
        return point;
    }

    @Override
    public boolean equals(Object o) {
        if (!(o instanceof ColorPoint)) return false;
        ColorPoint cp = (ColorPoint) o;
        return point.equals(cp.point) && color.equals(cp.color);
    }
}
```

- ColorPoint 는 내부에 Point를 상속하지 않고 포함해서 Point의 equals 규약을 깨뜨리지 않고
- 자신만의 비교 로직을 추가할수 있다


<br/>

**왜 컴포지션이 필요한가(equals 관점에서)**
- 상위 하위 클래스의 equals 기준이 달라서 추이성을 깨뜨린다
- 부모는 일부 필드만 비교 하고 자식은 새로운 필드를 추가한다
- 기존 클래스를 포함시켜서 독립적인 equals 구현이 가능하다


<br/>

**나의 정리**

- equals 메소드의 규약은 상속 구조에서 깨질수 있다
- 구체 클래스를 상속하여 새로운 필드를 추가하면 상위와 하위 클래스의 비교 기준이 달라져서 추이성을 만족 시킬수 없게 된다
- 그래서 상속을 통해 equals를 확장하지 말고 기존 클래스를 필드로 포함하는 컴포지션을 사용하여 독립적이고 일관된 equals 로직을 구현해야한다
- 다시말해 상속은 규약을 깨뜨리지만 컴포지션은 규약을 지켜준다




