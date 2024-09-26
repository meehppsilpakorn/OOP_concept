# OOP Concept

### Java

```java
class Animal {
    // Constructor
    Animal() {
        System.out.println("create animal");
    }

    // Destructor (ไม่มีใน Java โดยตรง, ใช้ finalize แทน)
    protected void finalize() {
        System.out.println("delete animal");
    }

    // Method sound
    void sound() {
        System.out.println("animal makes a sound");
    }
}

class Dog extends Animal {
    // Constructor
    Dog() {
        System.out.println("dog");
    }

    // Destructor
    @Override
    protected void finalize() {
        System.out.println("delete dog");
    }

    // Override method sound
    @Override
    void sound() {
        System.out.println("dog barks");
    }
}

class Cat extends Animal {
    // Constructor
    Cat() {
        System.out.println("cat");
    }

    // Destructor
    @Override
    protected void finalize() {
        System.out.println("delete cat");
    }

    // Override method sound
    @Override
    void sound() {
        System.out.println("cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        // Create object a of class Animal
        Animal a = new Animal();
        a.sound();

        // Create object d of class Dog
        Dog d = new Dog();
        d.sound();

        // Create object c of class Cat
        Cat c = new Cat();
        c.sound();
        
        a = null;
        b = null;
        c = null;
        // garbage collector
        System.gc();
    }
}
```

#### ผลลัพธิ์โปรแกรม

```
create animal
animal makes a sound
create animal
dog
dog barks
create animal
cat
cat meows
delete cat
delete dog
delete animal
```

### C++

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    // Constructor
    Animal() {
        cout << "create animal" << endl;
    }

    // Destructor
    ~Animal() {
        cout << "delete animal" << endl;
    }

    // Method sound
    virtual void sound() {
        cout << "animal makes a sound" << endl;
    }
};

class Dog : public Animal {
public:
    // Constructor
    Dog() {
        cout << "dog" << endl;
    }

    // Destructor
    ~Dog() {
        cout << "delete dog" << endl;
    }

    // Override method sound
    void sound() override {
        cout << "dog barks" << endl;
    }
};

class Cat : public Animal {
public:
    // Constructor
    Cat() {
        cout << "cat" << endl;
    }

    // Destructor
    ~Cat() {
        cout << "delete cat" << endl;
    }

    // Override method sound
    void sound() override {
        cout << "cat meows" << endl;
    }
};

int main() {
    // Create object a of class Animal
    Animal* a = new Animal();
    a->sound();

    // Create object d of class Dog
    Dog* d = new Dog();
    d->sound();

    // Create object c of class Cat
    Cat* c = new Cat();
    c->sound();

    // Clean up
    delete a;
    delete d;
    delete c;

    return 0;
}
```

#### ผลลัพธ์โปรแกรม

```
create animal
animal makes a sound
create animal
dog
dog barks
create animal
cat
cat meows
delete animal
delete dog
delete animal
delete cat
delete animal
```

### Python

```python
class Animal:
    # Constructor
    def __init__(self):
        print("create animal")

    # Destructor
    def __del__(self):
        print("delete animal")

    # Method sound
    def sound(self):
        print("animal makes a sound")


class Dog(Animal):
    # Constructor
    def __init__(self):
        print("dog")
    
    # Destructor
    def __del__(self):
        print("delete dog")

    # Override method sound
    def sound(self):
        print("dog barks")


class Cat(Animal):
    # Constructor
    def __init__(self):
        print("cat")

    # Destructor
    def __del__(self):
        print("delete cat")

    # Override method sound
    def sound(self):
        print("cat meows")

a = Animal()
a.sound()
d = Dog()
d.sound()
c = Cat()
c.sound()
del a, d, c
```

#### ผลลัพธิ์โปรแกรม

```
create animal
animal makes a sound
dog
dog barks
cat
cat meows
delete animal
delete dog
delete cat
```

### เปรียบเทียบผลรันโปรแกรม

เห็นได้ว่าผลรันของทั้ง 3 ภาษาไม่เหมือนกันทั้งที่โปรแกรมทำงานแบบเดียวกันทั้งหมด

#### Java

1. มีการพิมพ์ "create animal" ทุกครั้งเมื่อมีการสร้างวัตถุ Animal, Dog, Cat กล่าวคือ เมื่อสร้างวัตถุที่สืบทอด(Inheritance) อย่าง Dog, Cat ที่สืบทอดคุณสมบัติจาก Animal จะเรียกใช้ constructor ของ คลาสพ่อ(Parent Class) ก่อนแล้วจึงใช้ constructor ของตัวเอง
2. Destructor ในภาษา Java ไม่ได้มีให้ใช้โดยตรง แต่สามารถใช้ `finalize()` แทนได้เมื่อมีการกำจัดขยะ(Garbage collector) คำสั่ง`finalize()` จะถูกทำงานก่อนที่จะลบออกไป
3. Garbage collector ในภาษา Java ทำงานอัตโนมัติอยู่แล้ว หรือ สามารถสั่งให้ทำได้โดย `System.gc()`

#### C++

1. มีการพิมพ์ "create animal" เช่นเดียวกับ Java และสังเกตได้ว่า เมื่อมีการลบวัตถุเกิดขึ้น ใช้เรียกใช้ destructor ของตัวเอง และตามด้วย destructor ของคลาสพ่อ ซึ่งเป็นจุดที่แตกต่างจาก Java และ Python&#x20;
2. Destructor ใน C++ ใช้คำสั่ง `~Class()` และไม่มีการกำจัดขยะ จึงต้องใช้การลบด้วยคำสั่งจากนักพัฒนาเอด้วยคำสั่ง `delete object` แล้วจึงเรียกใช้ destructor ในต่อมา

#### Python

1. ไม่มีการพิมพ์ "create animal" ซ้ำๆ เหมือนกับ Java และ C++ แสดงได้ว่า Python ไม่มีการเรียกใช้ constructor ของคลาสพ่อ เมื่อมีการสร้างวัตถุของคลาสลูก
2. Garbage collector ใน Python มีทั้งแบบอัตโนมัติ และ เรียกใช้ เช่นเดียวกับ Java ซึ่งกำหนด destructor โดย `__del__(self)` และเมื่อต้องการลบวัตถุสามารถใช้คำสั่ง `del` ได้

### ส่วนประกอบของโค้ดเกับ concept ของ OOP

ในที่นี้ยกตัวอย่างในภาษา Java เป็นหลัก

#### **Class**

**Concept:**

* คลาสซึ่งเป็นส่วนประกอบหลักของแนวคิด OOP เปรียบเสมือนพิมพ์เขียว(blueprints) ภายในประกอบด้วย คุณลักษณะ(Attribute) และพฤติกรรม(Method) ใช้สำหรับสร้างวัตถุหลายๆชิ้น โดยไม่ต้องเขียนซ้ำหลายๆรอบ
* **ตัวอย่างโค้ด**

```java
class Animal {
    // Constructor
    Animal() {
        System.out.println("create animal");
    }

    // Method sound
    void sound() {
        System.out.println("animal makes a sound");
    }
}
```

#### **Object, Instance**

**Concept:**

* ออบเจ็กต์ (Object) หรืออินสแตนซ์ (Instance) คือสิ่งที่ถูกสร้างจากคลาส และใข้ในโปรแกรม
* **ตัวอย่างโค้ด**

```java
Animal a = new Animal();  // สร้าง object a ของ class Animal
Dog d = new Dog();        // สร้าง object d ของ class Dog
Cat c = new Cat();        // สร้าง object c ของ class Cat
```

#### **Subclass, Derived Class**

**Concept:**

* Subclass หรือ Derived Class คือคลาสที่สืบทอด (inherit) คุณสมบัติและพฤติกรรมจากคลาสอื่น  สามารถแก้ไขคุณสมบัติหรือ พฤติกรรมได้ ซึ่งทำให้คลาสใหม่แตกต่างไปจากเดิมและมีบางอย่างเหมือนกับต้นฉบับ
* **ตัวอย่างโค้ด**

```java
class Dog extends Animal {    // Dog เป็น subclass ของ Animal 
    Dog() {
        System.out.println("Dog");
    }

    @Override
    void sound() {            //แก้ไขพฤติกรรม ทำให้คลาส Dog แตกต่างจาก Animal
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {    // Cat เป็น subclass ของ Animal 
    Cat() {
        System.out.println("Cat");
    }

    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}
```

#### **Message**

**Concept:**

* Message คือการส่งคำสั่งหรือการเรียกใช้ method ของ object ผ่าน dot notation`object.method()`ใน OOP การเรียก method คือการส่ง message ไปยัง object เพื่อให้ทำงานตามคำสั่ง
* **ตัวอย่างโค้ด**

```java
a.sound();  // ส่ง message ให้ object a เรียกใช้ method sound() ของ Animal
d.sound();  // ส่ง message ให้ object d เรียกใช้ method sound() ของ Dog
c.sound();  // ส่ง message ให้ object c เรียกใช้ method sound() ของ Cat
```

#### **Inheritance**

**Concept:**

* Inheritance (การสืบทอด) คือความสามารถในการสร้างคลาสใหม่ที่สืบทอดคุณสมบัติและพฤติกรรมจากคลาสอื่น โดย subclass สามารถเพิ่มหรือลบความสามารถจากคลาสพ่อได้
* **ตัวอย่างโค้ด**

```java
class Dog extends Animal {    // คลาส Dog สืบทอดคุณสมบัติจากคลาส Animal
    Dog() {
        System.out.println("Dog");
    }

    @Override                // และแก้ไขพฤติกรรม sound()
    void sound() {
        System.out.println("Dog barks");
    }
}
```

#### **Polymorphism**

**Concept:**

* Polymorphism (การทำให้หลากหลาย) คือ ความสามารถในการใช้ method เดียวกันกับ object ที่มีชนิดต่างกัน โดย object แต่ละชนิดจะให้ผลลัพธ์ที่ต่างกัน
* **ตัวอย่างโค้ด**

```java
Animal a;
a = new Dog();
a.sound();  // เรียกใช้ sound() ของ Dog

a = new Cat();
a.sound();  // เรียกใช้ sound() ของ Cat
```

### Abstract Class

* **Abstract class** คือ คลาสที่ไม่สามารถสร้างวัตถุได้โดยตรง โดยทั่วไปแล้ว abstract class ถูกใช้เพื่อเป็นแม่แบบ (template) สำหรับคลาสอื่นๆ ที่จะสืบทอดไป
* Abstract class มักจะมี **abstract method** ซึ่งเป็นเมธอดที่ไม่มีการกำหนดการทำงานในคลาสพ่อ แต่จะกำหนดให้ subclass ที่สืบทอดมาทำการ `@override` เพื่อกำหนดการทำงานของ method นั้น
* Abstract class ถูกใช้เพื่อบังคับให้คลาสลูก (subclass) ต้อง implement เมธอดบางอย่างที่จำเป็นเท่านั้น
* ในภาษา  Java ใช้คีย์เวิร์ด `abstract` ในการประกาศคลาสและ method ที่เป็น abstract
* **ตัวอย่างโค้ด**

```java
abstract class Animal {
    abstract void sound();  // abstract method ไม่มีการระบุการทำงานที่นี่

    // Constructor
    Animal() {
        System.out.println("Create animal");
    }
}

class Dog extends Animal {
    // Override method sound
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```
