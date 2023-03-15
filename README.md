# Postman_HW_2

## :small_blue_diamond:HW during Vadim Ksendzov course:small_blue_diamond:

### /first
http://162.55.220.72:5005/first

1. Отправить запрос (GET).
> Response: This is the first responce from server!ss
2. Статус код 200.
```js
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Проверить, что в body приходит правильный string.
```js
const contentStr = "This is the first responce from server!";

pm.test("Body matches string", function () {
  pm.expect(pm.response.text()).to.include(contentStr);
});
```
************
### /user_info_3
http://162.55.220.72:5005/user_info_3

1. Отправить запрос (POST).
```
Body form-data:
name: Olga
age: 45
salary: 35000
```
> Response: { "age": "45", "family": { "children": [ [ "Alex", 24 ], [ "Kate", 12 ] ], "u_salary_1_5_year": 140000 }, "name": "Olga", "salary": 35000 }
2. Статус код 200
```js
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```js
const resp = pm.response.json();
```
4. Проверить, что name в ответе равно name s request (name вбить руками.)
```js
pm.test("Test name manually", function () {
  pm.expect(resp.name).to.eql("Olga");
});
```
5. Проверить, что age в ответе равно age s request (age вбить руками.)
```js
pm.test("Test age manually", function () {
  pm.expect(+resp.age).to.eql(45);
});
```
6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
```js
pm.test("Test salary manually", function () {
  pm.expect(+resp.salary).to.eql(35000);
});
```
7. Спарсить request.
```js
const req = request.data;
```
8. Проверить, что name в ответе равно name s request (name забрать из request.)
9. Проверить, что age в ответе равно age s request (age забрать из request.)
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```js
Object.keys(req).forEach((key) => {
  pm.test(`Test ${key} from request`, function () {
    pm.expect(resp[key].toString()).to.eql(req[key]);
  });
});
```
11. Вывести в консоль параметр family из response.
```js
console.log('Вывести в консоль параметр family из response', resp.family)
```
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```js
pm.test("Test family salary", function () {
  const salary_1_5 = resp.family["u_salary_1_5_year"];
  pm.expect(salary_1_5).to.eql(req.salary * 4);
});
```
************
### /object_info_3

1. Отправить запрос (GET).
```
Params:
name: Petr
age: 60
salary: 70000
```
> Response: { "age": "60", "family": { "children": [ [ "Alex", 24 ], [ "Kate", 12 ] ], "pets": { "cat": { "age": 3, "name": "Sunny" }, "dog": { "age": 4, "name": "Luky" } }, "u_salary_1_5_year": 280000 }, "name": "Petr", "salary": 70000 }
2. Статус код 200
```js
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```js
const resp = pm.response.json();
```
4. Спарсить request.
```js
const req = pm.request.url.query.toObject();
```
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age s request (age забрать из request.)
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```js
Object.keys(req).forEach((key) => {
  pm.test(`Test ${key}`, function () {
    pm.expect(resp[key].toString()).to.eql(req[key]);
  });
});
```
8. Вывести в консоль параметр family из response.
```js
console.log('Вывести в консоль параметр family из response', resp.family)
```
9. Проверить, что у параметра dog есть параметры name.
```js
pm.test("Dog has name", function () {
  pm.expect(resp.family.pets.dog).haveOwnProperty("name");
});
```
10. Проверить, что у параметра dog есть параметры age.
```js
pm.test("Dog has age", function () {
  pm.expect(resp.family.pets.dog).haveOwnProperty("age");
});
```
11. Проверить, что параметр name имеет значение Luky.
```js
pm.test("Dog name Luky", function () {
  pm.expect(resp.family.pets.dog.name).to.eql("Luky");
});
```
12. Проверить, что параметр age имеет значение 4.
```js
pm.test("Dog age is 4", function () {
  pm.expect(resp.family.pets.dog.age).to.eql(4);
});
```
************
### /object_info_4

http://162.55.220.72:5005/object_info_4

1. Отправить запрос (GET).
```
Params:
name: Anna
age: 37
salary: 55000
```
> Response: { "age": 37, "name": "Anna", "salary": [ 55000, "110000", "165000" ] }
2. Статус код 200
```js
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```js
const resp = pm.response.json();
```
4. Спарсить request.
```js
const req = pm.request.url.query.toObject();
```
5. Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("Test name", function () {
  pm.expect(resp.name).to.eql(req.name);
});
```
6. Проверить, что age в ответе равно age из request (age забрать из request.)
```js
pm.test("Test age", function () {
  pm.expect(resp.age).to.eql(+req.age);
});
```
7. Вывести в консоль параметр salary из request.
```js
console.log('Вывести в консоль параметр salary из request', req.salary);
```
8. Вывести в консоль параметр salary из response.
```js
console.log('Вывести в консоль параметр salary из response', resp.salary);
```
9. Вывести в консоль 0-й элемент параметра salary из response.
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
```js
resp.salary.forEach((item, i) => console.log(`Вывести в консоль ${i}-й элемент параметра salary из response`, item))
```
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
```js
for (let i = 0; i < resp.salary.length; i += 1) {
  pm.test(`Проверить, что ${i}-й элемент параметра salary равен salary * ${i + 1} из request`, function () {
    pm.expect(+resp.salary[i]).to.eql(req.salary * (i + 1));
  });
};
```
15. Создать в окружении переменную name
```js
pm.environment.set("name");
```
16. Создать в окружении переменную age
```js
pm.environment.set("age");
```
17. Создать в окружении переменную salary
```js
pm.environment.set("salary");
```
18. Передать в окружение переменную name
```js
pm.environment.set("name", req.name);
```
19. Передать в окружение переменную age
```js
pm.environment.set("age", req.age);
```
20. Передать в окружение переменную salary
```js
pm.environment.set("salary", req.salary);
```
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
```js
resp.salary.forEach((item, i) => console.log(`Вывести в консоль ${i}-й элемент параметра salary из response`, item))
```
************
### /user_info_2

1. Вставить параметр salary из окружения в request
2. Вставить параметр age из окружения в age
3. Вставить параметр name из окружения в name
4. Отправить запрос. (POST)
```
Body form-data:
name: {{name}}
age: {{age}}
salary: {{salary}}
```
> Response: { "person": { "u_age": 37, "u_name": [ "Anna", 55000, 37 ], "u_salary_5_years": 231000.0 }, "qa_salary_after_1.5_year": 181500.0, "qa_salary_after_12_months": 148500.0, "qa_salary_after_3.5_years": 209000.0, "qa_salary_after_6_months": 110000, "start_qa_salary": 55000 }
5. Статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
6. Спарсить response body в json.
```js
const resp = pm.response.json();
```
7. Спарсить request.
```js
const req = request.data;
```
8. Проверить, что json response имеет параметр start_qa_salary
```js
pm.test("json response имеет параметр start_qa_salary", function () {
  pm.expect(resp).haveOwnProperty("start_qa_salary");
});
```
9. Проверить, что json response имеет параметр qa_salary_after_6_months
```js
pm.test("json response имеет параметр qa_salary_after_6_months", function () {
  pm.expect(resp).haveOwnProperty("qa_salary_after_6_months");
});
```
10. Проверить, что json response имеет параметр qa_salary_after_12_months
```js
pm.test("json response имеет параметр qa_salary_after_12_months", function () {
  pm.expect(resp).haveOwnProperty("qa_salary_after_12_months");
});
```
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
```js
pm.test("JSON response имеет параметр qa_salary_after_1.5_year", function () {
  pm.expect(resp).haveOwnProperty("qa_salary_after_1.5_year");
});
```
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
```js
pm.test("JSON response имеет параметр qa_salary_after_3.5_years", function () {
  pm.expect(resp).haveOwnProperty("qa_salary_after_3.5_years");
});
```
13. Проверить, что json response имеет параметр person
```js
pm.test("JSON response имеет параметр person", function () {
  pm.expect(resp).haveOwnProperty("person");
});
```
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
```js
const salaryCoeffs = {
  "start_qa_salary": 1,
  "qa_salary_after_6_months": 2,
  "qa_salary_after_12_months": 2.7,
  "qa_salary_after_1.5_year": 3.3,
  "qa_salary_after_3.5_years": 3.8,
  "u_salary_5_years": 4.2
}

Object.entries(salaryCoeffs).forEach(([type, coeff]) => {
  pm.test(`Проверка правильности результата перемножения на коэффициент ${type}`, function () {
    if (type === "u_salary_5_years") {
      pm.expect(resp.person[type]).to.eql(req["salary"] * coeff);
    } else {
      pm.expect(resp[type]).to.eql(req["salary"] * coeff);
    }
  });
});
```
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
```js
pm.test("В параметре person, 1-й элемент из u_name равен salary из request", function () {
  pm.expect(resp.person["u_name"][1].toString()).to.eql(req["salary"]);
});
```
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
```js
pm.test("Параметр u_age равен age из request", function () {
  pm.expect(resp.person["u_age"].toString()).to.eql(req["age"]);
});
```
22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
```js
Object.entries(resp.person).forEach((item) => console.log(item));
```
