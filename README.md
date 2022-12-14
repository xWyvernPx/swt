[![Demo Jest Framework CI](https://github.com/xWyvernPx/swt/actions/workflows/project-ci.yml/badge.svg)](https://github.com/xWyvernPx/swt/actions/workflows/project-ci.yml)

# **This project is a demo for SWT presentation about Framework Jest**

## **1. How to start using project**

- ### **Project link: https://github.com/xWyvernPx/swt**

  > Make sure that you have installed Node on your system <br>
  > You can install it here: [Node](https://nodejs.org/en/download/)

  **1. Install jest as global**

  ```
  npm install -g jest
  ```

  or

  ```
  yarn global add jest
  ```

  **2. Clone project**

  ```git
  git clone https://github.com/xWyvernPx/swt.git
  ```

  **3. Install dependencies**

  ```
  npm install
  ```

  or

  ```
  yarn install
  ```

  > That's oke right now, lest open project in VS Code and start to demo

## **2. Comparing in JavaScript**

- Data Type in JavaScript :
  - Primary Type :
    <span style="color:orange"><strong>number</strong></span>,
    <span style="color:orange"><strong>boolean</strong></span>,
    <span style="color:orange"><strong>string</strong></span> ,
    <span style="color:orange"><strong>null</strong></span> ,
    <span style="color:orange"><strong>undefined</strong></span> ,...
  - Reference Type :
    <span style="color:orange"><strong>Object</strong></span>,
    <span style="color:orange"><strong>Array</strong></span>,
    <span style="color:orange"><strong>Function</strong></span>.
- 2 Types of Comparison :

  - Loose equality : <span style="color:orange"><strong>==</strong></span>
  - Strict equality : <span style="color:orange"><strong>===</strong></span>

  ### a. Problem with loose equality <span style="color:orange">**==**</span>

  Loose equality will only check the **value** neither the **type** <br>
  Example :

  > using to `node comparing.js /* or */ npm run comparing`

  ```js
  /* Case 1 */
  const expected = 3;
  const actual = "3";
  console.log(
    `Expected value: ${expected}\nActual value: ${actual}\nCompare value: ${
      expected == actual
    }`
  );

  /* Result log : 
  Expected value: 3
  Actual value: 3
  Compare value: true
  */
  ```

  ```js
  /* Case 2 */
  const expected = true;
  const actual = "1";

  console.log(
    `Expected value: ${expected}\nActual value: ${actual}\nCompare value: ${
      expected == actual
    }`
  );
  /* Result log : 
  Expected value: true
  Actual value: 1
  Compare value: true
  */
  ```

  ### b. Problem with strict equality <span style="color:orange">**===**</span>

  > With **Reference Type** this comparison will only compare the address

  ```js
  /* Case 1 */

  const studentA = {
    name: "A",
    age: 20,
  };
  const studentA2 = {
    name: "A",
    age: 20,
  };

  log(
    "Expected value: ",
    studentA,
    "\nActual value: ",
    studentA2,
    `\nCompare value: ${studentA === studentA2}`
  );

  /* Result log : 
  Expected value:  { name: 'A', age: 20 } 
  Actual value:  { name: 'A', age: 20 } 
  Compare value: false
  */
  ```

  ```js
  /* Case 2 */

  const expected = [1, 2, 3];
  const actual = [1, 2, 3];

  log(
    `Expected value: ${expected}\nActual value: ${actual}\nCompare value: ${
      expected === actual
    }`
  );

  /* Result log : 
  Expected value: 1,2,3
  Actual value: 1,2,3
  Compare value: false
  */
  ```

## **3. Start to testing with Jest**

To started to using Jest we will have a simple function in <span style="color:orange">isPrime.js</span> :

```js
function isPrime(number) {
  if (!Number.isInteger(number)) {
    throw Error(
      "Argument must be an integer"
    ); /* Tr?????ng h???p cho v??o m???t chu???i, m???t s??? th???c kh??ng ph???i s??? nguy??n */
  }
  let result = true;
  if (number < 1) {
    throw Error(
      "Argument must be larger than 1"
    ); /* Theo ?????nh ngh??a th?? s??? nguy??n t??? ph???i l?? s??? nguy??n d????ng l???n h??n 1 */
  } else if (number == 1) return false;
  /* 1 kh??ng ph???i s??? nguy??n t??? d???a v??o ?????nh ngh??a tr??n */
  for (let index = 2; index <= Math.sqrt(number); index++) {
    if (number % index === 0) {
      result = false;
      return result;
    }
  } //Gi???i thu???t ki???m tra m???t s??? c?? ph???i s??? nguy??n t??? hay kh??ng
  return result;
}

const findPosPrimeNum = (number) => {
  /*
  H??m n??y ????? t??m v??? tr?? c???a m???t s??? nguy??n t??? */
  let count = 0;
  for (let index = 2; index <= number; index++) {
    if (isPrime(index)) ++count;
  }
  return count;
};
const checkPrimeAndGetPosition = (number) => {
  /* H??m n??y d??ng ????? TEST , th???c hi???n ki???m tra m???t s??? c?? ph???i s??? nguy??n t??? kh??ng , n???u ph???i th?? t??m v??? tr??  */
  const checkResult = {
    isPrime: isPrime(number),
    position: isPrime(number) ? findPosPrimeNum(number) : -1,
  };
  return checkResult; /* Tr??? v??? m???t Object g??m k???t qu??? ki???m ra nguy??n t??? v?? n???u l?? s??? nguy??n t??? th?? tr??? v??? v??? tr??, c??n kh??ng ph???i s??? nguy??n t??? th?? v??? tr?? l?? -1 */
};

module.exports = { checkPrimeAndGetPosition }; // xu???t ra ????? c?? th??? s??? d???ng ch??? kh??c, s??? d???ng trong h??m test
```

Let's test itttt. <br>
There is a file <span style="color:orange">isPrime.test.js</span>
Run this file test by

```
  jest isPrime.test.js
```

```js
const {
  checkPrimeAndGetPosition,
} = require("./isPrime"); /* L???y c??i h??m ??? b??n kia ra ????? test ??? ????y */
describe("Testing function checkPrimeAndGetPosition", () => {
  /* Describe s??? ????a ra m???t c??i scope ????? test v?? n?? c?? t??n, nh?? l?? trong m???t "v??ng" ???? th?? ch??? test m???t th??? th??i. V?? ??? trong c??i callback function n??y l?? c??i "v??ng " ???? */
  test("Test function checkPrimeAndGetPosition with valid param", () => {
    /* Test th?? c??ng ?????nh ngh??a m???t "v??ng" ???????c ?????t t??n v?? ch??a c??c test case , m???i Test gi???ng nh?? m???t method trong class b??n Java v?? d??? "testcheckPrimeWithValidParameters" , "testcheckPrimeWithInvalidParameters" */

    /* ????y l?? c??ch khai b??o m???t test case trong Jest
    V???i expect() s??? nh???n m???t tham s??? l?? actual value (gi?? tr??? th???c t??? c???a h??m mu???n test tr??? v???) v?? c??c method ????? x??c ?????nh expected value (gi?? tr??? mong mu???n n?? s??? tr??? v???) : toBe() cho c??c Primative Type , toEqual() cho c??c ki???u Reference Type ngo??i ra c??n c??c method kh??c s??? x??c ?????nh domain c???a expected value thay v?? mu???n n?? b???ng m???t gi?? tr???  toBeGreaterThan(),toBeLessThan(), toMatch() 
    c?? nhi???u s??? l???a ch???n
    */
    /*  ??? ????y h??m c???n test tr??? v??? m???t Object l?? Reference Type n??n l?? d??ng toEqual */

    expect(checkPrimeAndGetPosition(2)).toEqual({ isPrime: true, position: 1 });
    // C?? th??? c?? nhi???u test case ????y
    expect(checkPrimeAndGetPosition(3)).toEqual({ isPrime: true, position: 2 });
    expect(checkPrimeAndGetPosition(4)).toEqual({
      isPrime: false,
      position: -1,
    });
    expect(checkPrimeAndGetPosition(5)).toEqual({ isPrime: true, position: 3 });
    expect(checkPrimeAndGetPosition(6)).toEqual({
      isPrime: false,
      position: -1,
    });
    expect(checkPrimeAndGetPosition(7)).toEqual({ isPrime: true, position: 4 });
  });

  /* Tr?????ng h???p tham s??? truy???n v??o kh??ng ph???i ki???u Integer th?? n?? s??? qu??ng ra Error
  s??? d???ng toThrow() ????? b???t Error 
  L??u ?? t??? Jest :  c??i h??m c???n Test c???n ???????c b???c l???i b???ng m???t function th?? m???i b???t ???????c l???i
  */
  test("Test function checkPrimeAndGetPosition with valid param", () => {
    expect(() => checkPrimeAndGetPosition("asdfgh")).toThrow();
  });
});
```

> If already install extension click on symbol????.

> If not install extension use cli `jest isPrime.test.js`

## **4. Data Driven Testing in Jest**

Test scripts with Data Driven Testing at <span style="color:orange">isPrimeDDT.test.js</span> <br>
Running this file test by
`jest isPrimeDDT.test.js`
or click on symbol ???? to test each test function/test suit

```js
const { checkPrimeAndGetPosition } = require("./isPrime");
/* v???n l???y h??m h???i n??y ???? xu???t kh???u ra ????? test */
const data = [
  /* Khai b??o b??? data ????? test b???ng m???t m???ng hai chi???u nh?? ch??i b??n Java g???m input v??o v??o expected value */
  [2, { isPrime: true, position: 1 }],
  [3, { isPrime: true, position: 2 }],
  [4, { isPrime: false, position: -1 }],
  [5, { isPrime: true, position: 3 }],
  [6, { isPrime: false, position: -1 }],
  [7, { isPrime: true, position: 3 }],
];

describe("Testing function checkPrimeAndFindPos with Data Driven Testing", () => {
  /* khai b??o Test v???i b??? data (each) v?? t???ng c???p input , expected value s??? ???????c nh??t v??o cho ta x??i 
    Ch??i ????? ch??i ???? c??i kh??ng c???n nh??? c?? ph??p  : Jest Snippet
  snippet : g?? teste -> tab
  */
  test.each(data)(
    "Testing function checkPrimeAndFindPos with DDT type 1",
    (input, expected) => {
      expect(checkPrimeAndGetPosition(input)).toEqual(expected);
    }
  );

  /*     C??ch n??y l???`y h??n kh??ng c???n khai b??o b??? data b???ng m???ng hai chi???u m??   ch??i vi???t theo format FW quy ?????nh nh?? v???y lu??n
     V???n nh?? tr??n n?? s??? nh??t t???ng b??? input v?? expected v??o cho ta x??i 
     Kh??ng c???n nh??? c?? ph??p, s??? d???ng ????? ch??i ???? c??i ( Jest Snippet ) 
     g?? testet  -> tab 
     */
  test.each`
    input | expected
    ${2}  | ${{ isPrime: true, position: 1 }}
    ${3}  | ${{ isPrime: true, position: 2 }}
    ${4}  | ${{ isPrime: false, position: -1 }}
    ${5}  | ${{ isPrime: true, position: 3 }}
    ${6}  | ${{ isPrime: false, position: -1 }}
    ${7}  | ${{ isPrime: true, position: 4 }}
  `(
    "Testing function checkPrimeAndFindPos with DDT type 2)",
    ({ input, expected }) => {
      expect(checkPrimeAndGetPosition(input)).toEqual(expected);
    }
  );
});
```

> If already install extension click on symbol ????

> If not install extension use cli `jest isPrimeDDT.test.js`

## **5. Test services with connecting database(MSSQL)**

To connect to database in Nodejs there are many ORM library.
We choose **Sequelize** here because it is really famous and its syntax is quite similar to almost others ORM or ODM in Javascript

### **1. Defined a model**

    We will need to have a entity to mapping to database table

> File at : **src/model/product.model.js**

```js
const { Sequelize, DataTypes } = require("sequelize");
// ORM l?? nh???ng th?? vi???n h??? tr??? mapping c??c b???ng trong database v???i c??c ?????i t?????ng c???a ng??n ng??? l???p tr??nh, ngo??i ra c??n gi??p ch??ng ta t??? sinh code SQL v?? th???c thi th??ng qua nh???ng methods v?? configs thay v?? vi???t c??u l???nh SQL th??? c??ng v?? t??? c???p nh???t d??? li???u d????i database khi c?? thay ?????i ??? object ???? mapping v???i database(migration).

const sequelize = new Sequelize({
  host: "localhost",
  database: "swt",
  port: 1433,
  username: "sa",
  password: "WyvernP2506",
  dialect: "mssql",
}); // new m???i m???t instance c???a th?? vi???n ????? s??? d???ng, khai b??o host , password , username,... ????? n?? s??? t??? ?????ng k???t n???i khi n??o s??? d???ng

const productModel = sequelize.define(
  /*?????nh ngh??a m???t model trong javascript ????? th???ng th?? vi???n s??? mapping v???i table d?????i database ????? khi m?? t??? sinh SQL ????? th???c thi */
  "product",
  {
    /* c??c thu???c t??nh t????ng ???ng v???i v???i c??c fields ??? d?????i database */
    id: {
      type: DataTypes.INTEGER,
      autoIncrement: true,
      primaryKey: true,
    },
    name: DataTypes.STRING,
    desc: DataTypes.STRING,
    price: DataTypes.INTEGER,
    stock: DataTypes.INTEGER,
    status: DataTypes.BOOLEAN,
  },
  {
    tableName: "product", //T??n table t????ng ???ng khi mapping
    timestamps: false, // c?? c??c fields createdAt modifiedAt kh??ng
  }
);
module.exports = productModel;
// xu???t model n??y ra ????? s??? d???ng ??? ch??? kh??c
```

### **2. Write a simple service**

After having defined a model Product, we will have a simple service with that product model

> Source : **src/service/product.service.js**

```js
const productModel = require("../model/product.model");
class ProductService {
  //function ki???m tra xem s???n ph???m c?? c??n  trong kho hay kh??ng
  async checkProductStockIfAvailable(product_id) {
    if (!Number.isInteger(product_id))
      // T????ng t??? ??? demo checkPrime n???u truy???n v??o product_id kh??ng ph???i integer th?? qu??ng Error ra
      throw Error("Product id must be Interger");

    const product = await productModel.findOne({ where: { id: product_id } });
    //ki???m s???n ph???m d???a tr??n product id truy???n v??o
    if (product === null) return false;
    //n???u kh??ng c?? product th?? product ???? b??? x??a => kh??ng c??n trong kho
    return product.stock > 0;
    // n???u c?? product v?? stock > 0 ngh??a l?? c??n => true c??n kh??ng => false
  }
}

module.exports = new ProductService();
```

### 3. Let test that service

Now we start to testing above service. But first, there is a problem that we need to consider when testing a service which connect to database :

- Is the data used for testing same on different systems ?
  => No

Solution :

> Jest support us a concept Setup & TearDown with hooks **_beforeAll()_** and **_afterAll()_** <br> > **Idea** :
>
> - Open connection, create database, create table, insert sample data for testing => Init database before starting to test with **beforeAll()**
> - Drop database, close connection => Clear database after testing done with **afterAll()**

> Source : **src/service/product.service.test.js**
> Test this file by running :
> <br> > `jest src/service/product.service.test.js` > <br>
> or click on symbol ????

```js
const ProductService = require("./product.service");
const { Sequelize } = require("sequelize");
const productModel = require("../model/product.model");
jest.setTimeout(120000);
const productService = new ProductService();
const sequelize = new Sequelize({
  // ORM
  host: "localhost",
  port: 1433,
  dialect: "mssql",
  username: "sa",
  password: "WyvernP2506",
});

beforeAll(async () => {
  await sequelize
    .authenticate() // Open connection
    .then(async () => {
      // N???u k???t n???i th??nh c??ng
      await sequelize.query(`
      IF NOT EXISTS (
        SELECT [name]
        FROM sys.databases
        WHERE [name] = N'swt'
      )
      CREATE DATABASE swt`);
      await sequelize.query("USE swt");
      // T???o database t??n swt n???u ch??a c?? , n???u c?? r???i th?? th??i x??i lu??n
      await sequelize.query(`
      IF OBJECT_ID('[dbo].[product]', 'U') IS NOT NULL
      DROP TABLE [dbo].[product]
      CREATE TABLE [dbo].[product]
      (
         id int IDENTITY ,
          name VARCHAR(50),
          [desc] VARCHAR(250),
          stock int ,
          [status] bit ,
          price float,
          CONSTRAINT PK_Product PRIMARY KEY (id)
      );`); // T???o b???ng n???u ch??a c??
    });

  await Promise.all([
    // INSERT d??? li???u m???u ????? testing v??o database
    productModel.create({
      name: "Product 1",
      desc: "Demo Product 1",
      stock: 100,
      status: 1,
      price: 200000,
    }),
    productModel.create({
      name: "Product 2",
      desc: "Demo Product 2",
      stock: 0,
      status: 1,
      price: 200000,
    }),
  ]);
});

afterAll(async () => {
  await sequelize.query("use master");
  await sequelize.query("DROP DATABASE swt");
  // Clear database
  sequelize.close();
  // Close connection
});

describe("Testing Product Service", () => {
  test("Testing method checkIfProductAvailable with valid params and Product is exist", async () => {
    expect(await productService.checkProductStockIfAvailable(1)).toBe(true);
    expect(await productService.checkProductStockIfAvailable(2)).toBe(false);
  });
  test("Testing method checkIfProductAvailable with valid params and Product not exist", async () => {
    const data = await productService.checkProductStockIfAvailable(3);
    expect(data).toEqual(false);
  });
});
```

## **6. Test RestAPIs**

> Everyone can visit this site to get detail tutorial of testing RestAPI with Jest and supertest alongs with demos

> **[Testing RestAPI with Jest and supertest](https://dev.to/franciscomendes10866/testing-express-api-with-jest-and-supertest-3gf)**

## **7. Report testing result**

The testing result only print on terminal log screen.
The demand of us is have a file that saves testing result every testing process.

So we will use a plugin of Jest **_jest-html-report_** by install from npm(Node Package Management)

Install CLI :

```
npm install jest-html-report
```

or

```
yarn add jest-html-report
```

Because it is a plugin so we have a config file for Jest to notice it that we want to use report plugin.

Create a config file at root : **jest.config.json**

```json
{
  "reporters": [
    "default",
    [
      "./node_modules/jest-html-reporter",
      {
        "pageTitle": "Test Report",
        "outputPath": "./test-report.html",
        "append": true
      }
    ]
  ]
}
```

> Try to test with Jest again and feel the result

> There would be a file named : **test-report.html** <br>
> Let open this page and you can see the report

## **8. CI project with GitAction**

> <span style="color:orange">.github/workflows/project-ci.yml</span>

```yml
name: demo Jest Framework CI

on:
  # M???i khi code push l??n nh??nh master l?? th???c hi???n CI
  push:
    branches: ["master"]
    #M???i khi c?? pull_request  v??o nh??nh master l?? th???c hi???n CI
  pull_request:
    branches: ["master"]

jobs:
  build:
    # xin server ubuntu b???n m???i nh???t ????? s??? d???ng
    runs-on: ubuntu-latest

    strategy:
      matrix:
        # ????a ra danh s??ch m??i tr?????ng ????? th???c hi???n c??c jobs trong CI m???i phi??n b???n m??i tr?????ng ( Node) s??? l?? m???t nh??nh th???c hi???n c??c jobs v?? c??c nh??nh n??y th???c hi???n song song nhau
        node-version: [16.x, 18.x]

    steps:
      #C??i m??i tr?????ng Node cho c??c nh??nh kh??c nhau
      - uses: actions/checkout@v3
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          cache: "npm"
      # T???i c??c dependencies ( hay packages , library ) cho c??i d??? ??n b???ng c??u l???nh CLI npm install
      - name: Install dependencies
        run: npm install
      # B???t ?????u Testing to??n b??? d??? ??n b???ng CLI  : npm  test
      # B???n ch???t c??u l???nh tr??n s??? g???i  c??u l???nh  jest -> jest s??? ??i ki???m to??n b??? file n??o c?? ??u??i *.test.js ho???c *.spec.js ????? th???c hi???n t???t c??? c??c test trong c??c file ???? , n???u Passed h???t => XANH ; Ch??? c???n 1 test case fail -> test tr??n file ???? Fail =>  ?????
      - name: Run test
        run: npm test
```
