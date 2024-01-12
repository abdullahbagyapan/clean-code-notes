# Chapter 3 - *Functions*

### Small!

- The first rule of functions is that they should be <b>small</b>.
- Functions should hardly ever be *20* lines long.

### Do One Thing

- FUNCTIONS SHOULD <b>DO ONE THING</b>. THEY SHOULD <b>DO IT WELL</b>. THEY SHOULD <b>DO IT ONLY</b>.

### One Level of Abstraction per Function

- In order to make sure our functions are doing “one thing,” we need to make sure that the statements within our function are all at the <b>same level of abstraction</b>
 
- Mixing levels of abstraction within a function is always confusing.

### Switch Statements

- It’s hard to make a small switch statement. By their nature, switch statements always do *N* things.
- But we can make sure that each switch statement is buried in a <b>low-level class</b> and is never repeated.

```java
public Money calculatePay(Employee e) throws InvalidEmployeeType {
    switch (e.type) {
        case COMMISSIONED:
            return calculateCommissionedPay(e);
        case HOURLY:
            return calculateHourlyPay(e);
        case SALARIED:
            return calculateSalariedPay(e);
        default:
            throw new InvalidEmployeeType(e.type);
    }
}
```

<br>

There are <b>*several problems*</b> with this function.

- <b>It’s large</b>, and when new employee types are added, it will grow.
- It very clearly but <b>does more than one thing</b>.
- <b>It violates the Single Responsibility Principle</b> (SRP) because there is more than one
reason for it to change.
- <b>It violates the Open Closed Principle</b> (OCP) because it must change whenever new types are added. 

The solution to this problem is to bury the switch statement in the basement of an <b>ABSTRACT FACTORY</b>.

```java
public abstract class Employee {
    public abstract boolean isPayday();
    public abstract Money calculatePay();
    public abstract void deliverPay(Money pay);
}

public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}

public class EmployeeFactoryImpl implements EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
    switch (r.type) {
        case COMMISSIONED:
            return new CommissionedEmployee(r) ;
        case HOURLY:
            return new HourlyEmployee(r);
        case SALARIED:
            return new SalariedEmploye(r);
        default:
            throw new InvalidEmployeeType(r.type);
        }
    }
}
```