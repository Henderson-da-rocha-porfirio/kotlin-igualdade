# Igualdade

Segue abaixo a versão equivalente desse código em **Java**, com as explicações das diferenças entre as implementações em Kotlin e Java.

---

### **Código em Java**

```java
package academy.learnprogramming.declarations;

import java.util.ArrayList;
import java.util.Set;

public class Main {

    public static void main(String[] args) {

        // Criação de objetos Employee
        Employee employeeOne = new Employee("Mary", 1);
        Employee employeeTwo = new Employee("John", 2);
        Employee employeeThree = new Employee("John", 2);

        // Comparações de referência e valores
        System.out.println(employeeOne == employeeTwo); // Referência
        System.out.println(employeeTwo == employeeThree); // Referência
        System.out.println(employeeOne.equals(employeeTwo)); // Valor
        System.out.println(employeeTwo.equals(employeeThree)); // Valor

        // Comparação de referência com atribuição
        Employee employeeFour = employeeTwo;
        System.out.println(employeeFour == employeeTwo); // Referência

        // Comparações com != (valor booleano)
        System.out.println(employeeFour != employeeTwo); // Sempre false
        System.out.println(employeeTwo != employeeThree); // True porque são diferentes

        // Declaração e manipulação de números
        int number = 10;
        number = 20;

        // Manipulação de listas
        ArrayList<String> names = new ArrayList<>();
        names.add("John");
        names.add("Jane");
        names.add("Mary");
        System.out.println(names.get(1)); // Acessa o índice 1 ("Jane")

        // Conjuntos (equivalente a typealias no Kotlin)
        Set<Employee> employees;

        // Manipulação de objetos Employee
        Employee employee1 = new Employee("Lynn Jones", 500);
        employee1.setName("Lynn Smith");

        Employee employee2;
        int number2 = 100;

        if (number < number2) {
            employee2 = new Employee("Jane Smith", 400);
        } else {
            employee2 = new Employee("Mike Watson", 150);
        }
    }
}

// Classe Employee
class Employee {

    private String name;
    private final int id;

    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }

    // Getter e Setter
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    // Sobrescrevendo equals para comparar valores
    @Override
    public boolean equals(Object obj) {
        if (obj instanceof Employee) {
            Employee other = (Employee) obj;
            return name.equals(other.name) && id == other.id;
        }
        return false;
    }
}
```

---

### **Diferenças Entre Kotlin e Java**

1. **`typealias` em Kotlin vs. Uso Direto em Java:**
   - Em Kotlin, `typealias EmployeeSet = Set<Employee>` cria um alias para um tipo.
   - Em Java, não há suporte para `typealias`, então usamos diretamente `Set<Employee>`.

2. **Comparações de Referências e Valores:**
   - Kotlin usa `===` para comparar referências e `==` para valores.
   - Java usa `==` para referências e o método `equals` para valores:
     - `employeeOne == employeeTwo` compara referências.
     - `employeeOne.equals(employeeTwo)` compara valores, desde que o método `equals` seja sobrescrito.

3. **Listas:**
   - Em Kotlin, `arrayListOf("John", "Jane", "Mary")` é uma construção nativa.
   - Em Java, usamos `new ArrayList<>()` e métodos como `add` para adicionar elementos.

4. **Manipulação de Propriedades:**
   - Em Kotlin, as propriedades de classe (`name` e `id`) são acessadas diretamente.
   - Em Java, você precisa usar métodos `getName` e `setName`.

5. **Segurança de Null (Null Safety):**
   - Kotlin é null-safe e oferece operadores como `?.`, `!!`, e `as?`.
   - Em Java, você precisa lidar com `null` manualmente, o que pode causar `NullPointerException`.

6. **Mais Verbosidade em Java:**
   - Java exige mais código boilerplate, como métodos `get` e `set` para acessar propriedades e inicialização explícita de variáveis.

7. **Estruturas Condicionais:**
   - Kotlin suporta inicialização direta dentro de expressões (`val employee2 = if (condition) ... else ...`).
   - Em Java, isso precisa ser feito com blocos `if-else`.

---

### **Saída do Programa**
A lógica e os resultados das operações são os mesmos em ambos os casos, apenas a sintaxe muda.

Exemplo de Saída:
```
false
false
false
true
true
false
true
Jane
```

---

A diferença entre **igualdade (equality)** em **Java** e **Kotlin** está principalmente na maneira como cada linguagem trata a comparação de referências e valores, e na simplificação introduzida pelo Kotlin. Vamos explorar isso em detalhes:

---

### **1. Igualdade em Java**
Em **Java**, existem dois tipos principais de igualdade:

- **Igualdade de Referências (`==`)**:
  - Verifica se duas variáveis referenciam o **mesmo objeto na memória**.
  - Exemplo:
    ```java
    String s1 = new String("Hello");
    String s2 = new String("Hello");

    System.out.println(s1 == s2); // false, porque são objetos diferentes na memória
    ```

- **Igualdade de Valores (`equals`)**:
  - Verifica se os valores de dois objetos são equivalentes.
  - Para isso, é necessário sobrescrever o método `equals` na classe.
  - Exemplo:
    ```java
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        MyClass myClass = (MyClass) obj;
        return this.value.equals(myClass.value);
    }
    ```
    - Aqui, `equals` deve ser chamado explicitamente:
      ```java
      System.out.println(s1.equals(s2)); // true, porque os valores são iguais
      ```

#### **Pontos de Atenção no Java:**
- O programador deve **sobrescrever o método `equals`** para comparar valores de objetos customizados.
- **`==` e `equals` têm finalidades diferentes.**
- Comparar strings ou objetos diretamente com `==` geralmente é um erro, pois compara referências, e não valores.

---

### **2. Igualdade em Kotlin**
Kotlin simplifica o conceito de igualdade, introduzindo dois operadores distintos:

- **Igualdade de Referências (`===`)**:
  - Funciona como o `==` de Java, verificando se duas variáveis referenciam o mesmo objeto na memória.
  - Exemplo:
    ```kotlin
    val s1 = "Hello"
    val s2 = String("Hello".toCharArray())

    println(s1 === s2) // false, pois são objetos diferentes
    ```

- **Igualdade de Valores (`==`)**:
  - É um **atalho para o método `equals`**.
  - Quando você usa `==` em Kotlin, ele chama o método `equals` por baixo dos panos.
  - Exemplo:
    ```kotlin
    println(s1 == s2) // true, porque os valores são iguais
    ```

#### **Por que Kotlin é mais simples?**
- O operador `==` já funciona automaticamente como uma comparação de valores, desde que o método `equals` seja implementado.
- Para tipos primitivos, `==` compara diretamente os valores, enquanto para objetos, chama `equals`.

---

### **3. Diferenças Entre Java e Kotlin**

| Aspecto                  | Java (`==` e `equals`)                                | Kotlin (`===` e `==`)                     |
|--------------------------|------------------------------------------------------|-------------------------------------------|
| **Comparação de Referências** | `==` compara referências.                           | `===` compara referências.                |
| **Comparação de Valores**    | `equals` precisa ser chamado explicitamente.       | `==` chama automaticamente `equals`.      |
| **Simplicidade**           | Mais verboso; requer `equals` manual.               | Menos verboso; `==` já chama `equals`.     |
| **Nulos**                  | Pode causar `NullPointerException` ao usar `equals`. | Seguro com `==` (`null == valor` é tratado). |
| **Tipos Primitivos**        | Comparados diretamente com `==`.                   | Comparados diretamente com `==`.          |

---

### **Exemplos Comparativos**

#### **Em Java:**
```java
String s1 = new String("Hello");
String s2 = new String("Hello");

System.out.println(s1 == s2);       // false (referências diferentes)
System.out.println(s1.equals(s2)); // true (valores iguais)
```

#### **Em Kotlin:**
```kotlin
val s1 = "Hello"
val s2 = String("Hello".toCharArray())

println(s1 === s2) // false (referências diferentes)
println(s1 == s2)  // true (valores iguais)
```

---

### **4. Segurança com Nulos**
Outra grande vantagem do Kotlin é sua segurança contra nulos:

#### **Em Java:**
```java
String s1 = null;
String s2 = "Hello";

System.out.println(s1.equals(s2)); // NullPointerException
```

#### **Em Kotlin:**
```kotlin
val s1: String? = null
val s2 = "Hello"

println(s1 == s2) // false, sem exceção
```

- Em Kotlin, `==` verifica automaticamente se algum dos lados é `null` antes de chamar `equals`, evitando exceções.

---

### **Resumo**
| Conceito                | Java                              | Kotlin                      |
|-------------------------|------------------------------------|-----------------------------|
| **Comparação de Referências** | `==`                          | `===`                       |
| **Comparação de Valores**    | `equals`                      | `==`                        |
| **Tratar nulos**          | Propenso a exceções (`NullPointerException`). | Seguro contra nulos.        |
| **Sintaxe**               | Verbosa e mais propensa a erros. | Simples e mais intuitiva.   |

Vamos explorar a **diferença entre Comparação de Valores e Comparação de Referências**, com exemplos em **Java** e **Kotlin**, para facilitar sua compreensão.

---

## **1. Comparação de Referências**

A **comparação de referências** verifica se **duas variáveis referenciam o mesmo objeto na memória**. Ela não considera os valores dentro dos objetos.

### **Exemplo em Java**
```java
public class Main {
    public static void main(String[] args) {
        String s1 = new String("Hello");
        String s2 = new String("Hello");
        String s3 = s1; // s3 é uma referência ao mesmo objeto que s1

        // Comparação de Referências
        System.out.println(s1 == s2); // false: objetos diferentes na memória
        System.out.println(s1 == s3); // true: s1 e s3 referenciam o mesmo objeto
    }
}
```

### **Exemplo em Kotlin**
```kotlin
fun main() {
    val s1 = String("Hello".toCharArray())
    val s2 = String("Hello".toCharArray())
    val s3 = s1 // s3 é uma referência ao mesmo objeto que s1

    // Comparação de Referências
    println(s1 === s2) // false: objetos diferentes na memória
    println(s1 === s3) // true: s1 e s3 referenciam o mesmo objeto
}
```

---

## **2. Comparação de Valores**

A **comparação de valores** verifica se os **conteúdos internos** dos objetos são equivalentes. Para objetos, isso depende da implementação do método `equals`.

### **Exemplo em Java**
```java
public class Main {
    public static void main(String[] args) {
        String s1 = new String("Hello");
        String s2 = new String("Hello");

        // Comparação de Valores
        System.out.println(s1.equals(s2)); // true: os valores (conteúdos) são iguais
    }
}
```

### **Exemplo em Kotlin**
```kotlin
fun main() {
    val s1 = String("Hello".toCharArray())
    val s2 = String("Hello".toCharArray())

    // Comparação de Valores
    println(s1 == s2) // true: os valores (conteúdos) são iguais
}
```

---

## **3. Diferenças em Objetos Personalizados**

Para objetos personalizados, você precisa sobrescrever o método `equals` para definir o que significa "igualdade de valores". Em Java, isso é feito manualmente, enquanto em Kotlin, o `data class` fornece uma implementação automática.

### **Java**
```java
class Employee {
    String name;
    int id;

    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Employee employee = (Employee) obj;
        return id == employee.id && name.equals(employee.name);
    }
}

public class Main {
    public static void main(String[] args) {
        Employee e1 = new Employee("John", 1);
        Employee e2 = new Employee("John", 1);
        Employee e3 = e1; // Referência ao mesmo objeto

        // Comparação de Referências
        System.out.println(e1 == e2); // false: referências diferentes
        System.out.println(e1 == e3); // true: mesmas referências

        // Comparação de Valores
        System.out.println(e1.equals(e2)); // true: valores iguais
    }
}
```

### **Kotlin**
```kotlin
data class Employee(val name: String, val id: Int)

fun main() {
    val e1 = Employee("John", 1)
    val e2 = Employee("John", 1)
    val e3 = e1 // Referência ao mesmo objeto

    // Comparação de Referências
    println(e1 === e2) // false: referências diferentes
    println(e1 === e3) // true: mesmas referências

    // Comparação de Valores
    println(e1 == e2) // true: valores iguais
}
```

---

## **4. Comportamento com Tipos Primitivos**

Para **tipos primitivos** como `Int` e `Double`, não há diferença entre referência e valor, pois eles são comparados diretamente em ambas as linguagens.

### **Exemplo em Java**
```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        int b = 10;

        // Comparação direta (valores)
        System.out.println(a == b); // true
    }
}
```

### **Exemplo em Kotlin**
```kotlin
fun main() {
    val a = 10
    val b = 10

    // Comparação direta (valores)
    println(a == b) // true
}
```

---

## **5. Comparação com Objetos Nulos**

### **Java**
```java
public class Main {
    public static void main(String[] args) {
        String s1 = null;
        String s2 = "Hello";

        // Comparação de Valores
        // Isso pode causar NullPointerException
        if (s1 != null && s1.equals(s2)) {
            System.out.println("Valores iguais");
        } else {
            System.out.println("Valores diferentes ou nulo");
        }
    }
}
```

### **Kotlin**
```kotlin
fun main() {
    val s1: String? = null
    val s2 = "Hello"

    // Comparação de Valores (Seguro contra null)
    println(s1 == s2) // false, sem NullPointerException
}
```

---

## **Resumo**

| Aspecto                  | Java                                 | Kotlin                     |
|--------------------------|---------------------------------------|----------------------------|
| **Comparação de Referências** | `==`                              | `===`                      |
| **Comparação de Valores**    | `equals`                          | `==`                       |
| **Null Safety**           | Manual (propenso a exceções)         | Seguro por padrão           |
| **Objetos Personalizados** | Necessita sobrescrever `equals`.    | `data class` já implementa. |
