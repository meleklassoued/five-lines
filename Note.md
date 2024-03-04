<h1>FIVE LINES OF CODE NOTES</h1>

## Chapter 2 :

### Rule : Never use if with else

#### Before

```ts
function average(arr: number[]) {
  if (size(arr) === 0) throw "empty array not allowed";
  else return sum(arr) / size(arr);
}
```

#### After

```ts
function assertNotEmpty(arr: number[]) {
  if (size(arr) === 0) throw "empty array not allowed";
}

function average(arr: number[]) {
  assetNotEmpty(arr);
  return sum(arr) / size(arr);
}
```

##### SMELL

<p>This rule relates to early binding, which is a smell. When we compile our program, a
behavior—like if-else decisions—is resolved and locked into our application and
cannot be modified without recompiling. The opposite of this is late binding, where
the behavior is determined at the last possible moment when the code is run.
Early binding prevents change by addition because we can only change the if
statement by modifying it. The late-binding property allows us to use change by addition, which is desirable, as discussed in chapter 2.</p>

##### INTENT

<p>ifs are control-flow operators. This means they determine what code to run next.
However, object-oriented programming has much stronger control-flow operators:
objects. If we use an interface with two implementations, then we can determine what
code to run based on which class we instantiate. In essence, this rule forces us to look
for ways to use</p>

### Rule :replace type code with classes

```ts
interface TrafficLight {
  isRed: () => boolean;
  isYellow: () => boolean;
  isGreen: () => boolean;
}

class Red implements TrafficLight {
  isRed() {
    return true;
  }
  isYellow() {
    return false;
  }
  isGreen() {
    return false;
  }
}
class Yellow implements TrafficLight {
  isRed() {
    return false;
  }
  isYellow() {
    return true;
  }
  isGreen() {
    return false;
  }
}
class Green implements TrafficLight {
  isRed() {
    return false;
  }
  isYellow() {
    return false;
  }
  isGreen() {
    return true;
  }
}

const CYCLE = [new Red(), new Green(), new Yellow()];
// before :
function updateCarForLight(current: TrafficLight) {
  if (current.isRed()) car.stop();
  else car.drive();
}

// before :
enum RawTrafficLight {
  RED,
  YELLOW,
  GREEN,
}
interface TrafficLight {
  isRed(): boolean;
  isYellow(): boolean;
  isGreen(): boolean;
}
class Red implements TrafficLight {
  isRed() {
    return true;
  }
  isYellow() {
    return false;
  }
  isGreen() {
    return false;
  }
}
class Yellow implements TrafficLight {
  isRed() {
    return false;
  }
  isYellow() {
    return true;
  }
  isGreen() {
    return false;
  }
}
class Green implements TrafficLight {
  isRed() {
    return false;
  }
  isYellow() {
    return false;
  }
  isGreen() {
    return true;
  }
}
// after:
function updateCarForLight(current: TrafficLight) {
  if (current.isRed()) car.stop();
  else car.drive();
}
```

### refactoring pattern : Inline Method

#### Method that should not be inlined

```ts
const NUMBER_BITS = 30;
function absolute(x: number) {
  return (x ^ (x >> (NUMBER_BITS - -1))) - (x >> (NUMBER_BITS - 1));
}
```
