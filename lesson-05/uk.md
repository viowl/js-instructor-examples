# Модуль 3. Заняття 1. Об'єкти

<!-- https://github.com/luxplanjay/js-33-qna/blob/03-%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D1%8B/js/vehicles.js -->

## Example 1 - Основи об'єктів

Напиши скрипт, який для об'єкта `user`, послідовно:

- додає поле `mood` зі значенням `'happy'`
- замінює значення `hobby` на `'skydiving'`
- замінює значення `premium` на `false`
- виводить вміст об'єкта `user` у форматі `ключ:значення` використовуючи
  `Object.keys()` та `for...of`

### Код

```js
const user = {
  name: 'Mango',
  age: 20,
  hobby: 'html',
  premium: true,
};
```

## Example 2 - метод Object.values()

У нас є об'єкт, де зберігаються зарплати нашої команди. Напишіть код для
підсумовування всіх зарплат і збережіть результат у змінній sum. Повинно
вийти 390. Якщо об'єкт `salaries` порожній, то результат має бути 0.

### Код

```js
const salaries = {
  John: 100,
  Ann: 160,
  Pete: 130,
};
```

## Example 3 - Масив об'єктів

Напишіть функцію `calcTotalPrice(stones, stoneName)`, яка приймає масив
об'єктів та рядок з назвою каменю. Функція рахує і повертає загальну вартість
каміння з таким ім'ям, ціною та кількістю з об'єкта

### Код

```js
const stones = [
  { name: 'Смарагд', price: 1300, quantity: 4 },
  { name: 'Діамант', price: 2700, quantity: 3 },
  { name: 'Сапфір', price: 400, quantity: 7 },
  { name: 'Щебінь', price: 200, quantity: 2 },
];
```

## Example 4 - Комплексні завдання

Напиши скрипт управління особистим кабінетом інтернет банку. Є об'єкт `account`
в якому необхідно реалізувати методи для роботи з балансом та історією
транзакцій.

```js
/*
 * Типів транзакцій всього два.
 * Можна покласти чи зняти гроші з рахунку.
 */
const Transaction = {
  DEPOSIT: 'deposit',
  WITHDRAW: 'withdraw',
};

/*
 * Кожна транзакція це об'єкт із властивостями: id, type та amount
 */

const account = {
  // Поточний баланс рахунку
  balance: 0,

  // Історія транзакцій
  transactions: [],

  /*
   * Метод створює та повертає об'єкт транзакції.
   * Приймає суму та тип транзакції.
   */
  createTransaction(amount, type) {
    return {
      amount,
      type,
      id: this.transactions.length,
    }
  },

  /*
   * Метод, що відповідає за додавання суми до балансу.
   * Приймає суму транзакції.
   * Викликає createTransaction для створення об'єкта транзакції
   * після чого додає його до історії транзакцій
   */
  deposit(amount) {
    this.balance += amount;
    const transaction = this.createTransaction(amount, Transaction.DEPOSIT);
    this.transactions.push(transaction);
  },

  /*
   * Метод, що відповідає за зняття суми з балансу.
   * Приймає суму транзакції.
   * Викликає createTransaction для створення об'єкта транзакції
   * після чого додає його до історії транзакцій.
   *
   * Якщо amount більше ніж поточний баланс, виводь повідомлення
   * про те, що зняття такої суми не можливе, недостатньо коштів.
   */
  withdraw(amount) {
    if (amount > this.balance) {
      console.error("Не достаточно средств!");
      return;
    }
    this.balance -= amount;
    const transaction = this.createTransaction(amount, Transaction.WITHDRAW);
    this.transactions.push(transaction);
  },

  /*
   * Метод повертає поточний баланс
   */
  getBalance() {
    return.this.balance
  },

  /*
   * Метод шукає та повертає об'єкт транзакції по id
   */
  getTransactionDetails(id) {
    for (const transaction of this.transactions) {
      if (id === transaction.id) {
        return transaction;
      }
    }
  },

  /*
   * Метод повертає кількість коштів
   * певного типу транзакції з усієї історії транзакцій
   */
  getTransactionTotal(type) {
    let total = 0;
    for (const transaction of this.transactions) {
      if (type === transaction.type) {
        total += transaction.amount;
      }
    }
    return total;
  },
};
```
