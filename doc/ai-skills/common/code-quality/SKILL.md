# Code Quality Skill - 代码质量优化规范

## 适用范围

本 skill 适用于处理本项目中与代码质量相关的所有任务，包括：
- 代码质量评估与优化
- 代码格式化与重构
- 变量命名、函数设计等最佳实践
- 代码可读性提升
- 遵循《代码整洁之道》等编码规范

## 执行流程

### 1. 代码质量评估

#### 1.1 评估标准

判断代码质量的基本标准：
- **可读性**：代码应像优秀的散文一样容易阅读，通过自身结构和命名表达意图
- **可维护性**：代码应易于修改和扩展，每个函数、变量和类都有明确目的
- **可测试性**：代码应便于编写单元测试，测试覆盖率应高
- **意义明确**：变量名、函数名等应清晰表达其用途，避免需要大量注释

#### 1.2 常见代码质量问题

**变量命名问题**：
```java
// 糟糕的代码
int d; // 天数？
int cnt; // 计数？
int tmp; // 临时变量

// 整洁的代码
int daysSinceCreation;
int customerCount;
int temporaryFileSize;
```

**函数设计问题**：
```java
// 糟糕的代码
public void doSomething() {
    // 负责多个职责的长函数
}

// 整洁的代码
public void calculateTotalPrice() {
    // 只做一件事，函数名明确表达功能
}
```

### 2. 变量命名规范

#### 2.1 命名原则

1. **有意义的命名**：变量名应表达其用途，而非类型
2. **避免缩写和单字母变量名**：除非在循环变量中，否则避免使用单字母变量
3. **使用驼峰命名法**：Java中使用驼峰命名法，首字母小写，后续单词首字母大写
4. **避免过度描述**：变量名应简洁明了，避免冗余
5. **避免歧义性命名**：变量名应避免有多种解释

#### 2.2 命名示例

```java
// 糟糕的代码
int d;              // 天数？
int cnt;            // 计数？
String str;         // 字符串
String customerNameString; // 过度描述

// 整洁的代码
int daysSinceCreation;
int customerCount;
String name;
String customerName;
```

### 3. 函数设计规范

#### 3.1 函数设计原则

1. **函数应短小精悍**：最好不超过 20 行，过长的函数说明负责了太多职责
2. **函数应只做一件事**：如果函数名包含"and"、"or"等连接词，说明负责了多个职责
3. **函数应有明确的名称**：函数名应准确表达其功能
4. **函数参数应尽量少**：最好不超过 3 个，过多参数说明负责了太多职责

#### 3.2 函数重构示例

```java
// 糟糕的代码
public void processOrder(Order order) {
    if (order == null) {
        throw new IllegalArgumentException("订单不能为空");
    }

    double total = 0;
    for (Item item : order.getItems()) {
        total += item.getPrice() * item.getQuantity();
    }

    order.setTotalPrice(total);
    saveToDatabase(order);
    sendEmailNotification(order);
}

// 整洁的代码
public void processOrder(Order order) {
    validateOrder(order);
    calculateTotalPrice(order);
    saveOrder(order);
    notifyCustomer(order);
}

private void validateOrder(Order order) {
    if (order == null) {
        throw new IllegalArgumentException("订单不能为空");
    }
}

private void calculateTotalPrice(Order order) {
    double total = 0;
    for (Item item : order.getItems()) {
        total += item.getPrice() * item.getQuantity();
    }
    order.setTotalPrice(total);
}

private void saveOrder(Order order) {
    saveToDatabase(order);
}

private void notifyCustomer(Order order) {
    sendEmailNotification(order);
}
```

### 4. 代码格式化规范

#### 4.1 格式化原则

1. **保持一致的缩进**：使用 4 个空格或 1 个制表符，保持一致
2. **保持一致的命名规范**：变量名、函数名、类名等应遵循统一规范
3. **保持一致的换行规范**：每个语句占一行，避免过长的单行代码

#### 4.2 格式化示例

```java
// 糟糕的代码
public class customer {
  private String Name;
    private String Email;
    private String phoneNumber;

  public customer(String name, String email, String phone) {
        Name = name;
        Email = email;
          this.phoneNumber = phone;
    }
}

// 整洁的代码
public class Customer {
    private String name;
    private String email;
    private String phoneNumber;

    public Customer(String name, String email, String phone) {
        this.name = name;
        this.email = email;
        this.phoneNumber = phone;
    }
}
```

### 5. 重构规范

#### 5.1 重构原则

1. **小步前进**：每次只修改一个功能，避免引入新错误
2. **测试驱动**：重构前先写好测试，确保重构后功能正常
3. **持续重构**：重构是一个持续过程，应在日常工作中不断进行

#### 5.2 常见重构技巧

##### 5.2.1 提炼函数

将长函数分解成多个小函数，每个函数负责一个职责。

##### 5.2.2 内联函数

如果函数内容非常简单，可以将其直接内联到调用处。

##### 5.2.3 提炼变量

将复杂的表达式提炼成变量，提高代码可读性。

```java
// 糟糕的代码
public double calculateTotalPrice(List<Item> items) {
    double total = 0;
    for (Item item : items) {
        total += item.getPrice() * item.getQuantity() * (1 - item.getDiscount() / 100);
    }
    return total;
}

// 整洁的代码
public double calculateTotalPrice(List<Item> items) {
    double total = 0;
    for (Item item : items) {
        double discountedPrice = item.getPrice() * (1 - item.getDiscount() / 100);
        total += discountedPrice * item.getQuantity();
    }
    return total;
}
```

### 6. 实施与验证

#### 6.1 代码优化流程

1. **识别问题**：通过代码质量评估，识别需要优化的代码段
2. **制定计划**：根据问题类型，选择合适的重构方法
3. **实施重构**：按照重构原则，小步前进进行优化
4. **验证测试**：确保重构后的代码功能正常，测试覆盖率达标
5. **提交变更**：使用清晰的提交信息，记录优化内容

#### 6.2 提交规范

```bash
# 代码优化提交示例
git commit -m "Optimize: 重构 processOrder 函数，提高代码可读性"
```

## 相关资源

- 参考书籍：《代码整洁之道》（Robert C. Martin）
- 工具推荐：
  - Java：Eclipse、IntelliJ IDEA 代码格式化工具
  - 前端：Prettier、ESLint
  - Python：Black、Flake8

## 行动指南

1. **每周重构一次**：每周抽出时间对项目代码进行重构，提高代码质量
2. **使用代码格式化工具**：在写代码时使用代码格式化工具，保持代码一致性
3. **写好测试**：在写代码之前，先写好测试，确保代码正确性
4. **学习新的编码技巧**：定期学习新的编码技巧，提高自己的编码水平

代码整洁是一个不断追求的过程，需要我们在日常工作中不断实践和总结。希望我们都能写出整洁、优雅的代码。
