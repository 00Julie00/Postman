## HW_2 Postman
### EP_1 (/first)  
`http://162.55.220.72:5005/first`
1. Отправить запрос.
2. Статус код 200
3. Проверить, что в body приходит правильный string.

#### Решение
```
{
					"name": "first",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"pm.test(\"The expected String comes to body\", function (){",
									"pm.expect(pm.response.text()).to.include(\"This is the first responce from server!ss\");",
									"});"
								],
								"type": "text/javascript"
							}
						},
						{
							"listen": "prerequest",
							"script": {
								"exec": [
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5005/first",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"first"
							]
						}
					},
					"response": []
				}
```
### EP_2 (/user_info_3)http://162.55.220.72:5005/user_info_3

1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Проверить, что name в ответе равно name s request (name вбить руками.)
5. Проверить, что age в ответе равно age s request (age вбить руками.)
6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
7. Спарсить request.
8. Проверить, что name в ответе равно name s request (name забрать из request.)
9. Проверить, что age в ответе равно age s request (age забрать из request.)
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
11. Вывести в консоль параметр family из response.
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)

#### Решение
```
{
					"name": "user_info_3_part1",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Спарсить response body в json.",
									"var jsonData=pm.response.json();",
									"",
									"//Проверить, что name в ответе равно name s request (name вбить руками.)",
									"pm.test(\"Check the name\",function() {",
									"    pm.expect(jsonData.name).to.eql(\"Vadim\");",
									"});",
									"",
									"//Проверить, что age в ответе равно age s request (age вбить руками.)",
									"pm.test(\"Check the age\",function() {",
									"    pm.expect(jsonData.age).to.eql('33');",
									"});",
									"",
									"//Проверить, что salary в ответе равно salary s request (salary вбить руками.)",
									"pm.test(\"Check the salary\",function() {",
									"    pm.expect(jsonData.salary).to.eql(1000);",
									"});",
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "formdata",
							"formdata": [
								{
									"key": "name",
									"value": "Vadim",
									"type": "text"
								},
								{
									"key": "age",
									"value": "33",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "1000",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://162.55.220.72:5005/user_info_3",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"user_info_3"
							]
						}
					},
					"response": []
				}
```

```
{
					"name": "user_info_3_part2",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"var jsonData=pm.response.json();",
									"//Спарсить request",
									"var req_body=request.data;",
									"",
									"//Проверить, что name в ответе равно name s request (name забрать из request.)",
									"console.log(\"request name==\",req_body.name,typeof req_body.name);",
									"pm.test(\"check the name\",function(){",
									"    pm.expect(jsonData.name).to.eql(req_body.name)",
									"});",
									"",
									"//Проверить, что age в ответе равно age s request (age забрать из request.)",
									"console.log(\"request age==\",req_body.age,typeof req_body.age);",
									"pm.test(\"check the age\",function(){",
									"    pm.expect(jsonData.age).to.eql(req_body.age)",
									"});",
									"",
									"//Проверить, что salary в ответе равно salary s request (salary забрать из request.)",
									"console.log(\"request salary == \",req_body.salary, typeof req_body.salary);",
									"pm.test(\"check the salary\", function() {",
									"    pm.expect(jsonData.salary).to.eql(Number(req_body.salary));",
									"});",
									"",
									"//Вывести в консоль параметр family из response",
									"console.log(\"family==\",jsonData.family);",
									"",
									"//Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)",
									"var u_salary_1_5_year=jsonData.family.u_salary_1_5_year;",
									"console.log(\"response salary 1.5 year == \",u_salary_1_5_year);",
									"pm.test(\"check the salary 1.5 year\", function() {",
									"    pm.expect(+req_body.salary*4).to.eql(+jsonData.family.u_salary_1_5_year);",
									"});",
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "formdata",
							"formdata": [
								{
									"key": "name",
									"value": "Vadim",
									"type": "text"
								},
								{
									"key": "age",
									"value": "33",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "1000",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://162.55.220.72:5005/user_info_3",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"user_info_3"
							]
						}
					},
					"response": []
				}
```
### EP_3 (/object_info_3)
`http://162.55.220.72:5005/object_info_3`
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age s request (age забрать из request.)
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
8. Вывести в консоль параметр family из response.
9. Проверить, что у параметра dog есть параметры name.
10. Проверить, что у параметра dog есть параметры age.
11. Проверить, что параметр name имеет значение Luky.
12. Проверить, что параметр age имеет значение 4.

#### Решение
```
					"name": "object_info_3",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Спарсить response body в json.",
									"var jsonData=pm.response.json();",
									"//Спарсить request",
									"var req_url=pm.request.url.query.toObject();",
									"",
									"//Проверить, что name в ответе равно name s request (name забрать из request.)",
									"console.log(\"request name==\",req_url.name,typeof req_url.name);",
									"pm.test(\"check the name\",function(){",
									"    pm.expect(req_url.name).to.eql(jsonData.name);",
									"});",
									"",
									"//Проверить, что age в ответе равно age s request (age забрать из request.)",
									"console.log(\"request age==\",req_url.age,typeof +req_url.age);",
									"pm.test(\"check the age\",function(){",
									"    pm.expect(req_url.age).to.eql(jsonData.age);",
									"});",
									"",
									"//Проверить, что salary в ответе равно salary s request (salary забрать из request.)",
									"console.log(\"request salary == \",req_url.salary, typeof +req_url.salary);",
									"pm.test(\"check the salary\", function() {",
									"    pm.expect(+req_url.salary).to.eql(+jsonData.salary);",
									"});",
									"",
									"//Вывести в консоль параметр family из response",
									"console.log(\"family==\",jsonData.family);",
									"",
									"//Проверить, что у параметра dog есть параметры name.",
									"console.log(\"response property name of dog == \",jsonData.family.pets.dog.name,typeof jsonData.family.pets.dog.name );",
									"pm.test(\"check the dog have property name\", function() {",
									"    pm.expect(jsonData.family.pets.dog).to.have.property('name');",
									"});",
									"",
									"//Проверить, что у параметра dog есть параметры age.",
									"console.log(\"response property age of dog == \",jsonData.family.pets.dog.age,typeof  jsonData.family.pets.dog.age);",
									"pm.test(\"check the dog have property age\", function() {",
									"    pm.expect(jsonData.family.pets.dog).to.have.property('age');",
									"});",
									"//Проверить, что параметр name имеет значение Luky.",
									"console.log(\"response name of dog == \",jsonData.family.pets.dog.name,typeof  jsonData.family.pets.dog.name);",
									"pm.test(\"check the dog have name Luky\", function() {",
									"    pm.expect(jsonData.family.pets.dog.name).to.eql(\"Luky\");",
									"});",
									"//Проверить, что параметр age имеет значение 4.",
									"console.log(\"response age of dog == \",jsonData.family.pets.dog.age,typeof  +jsonData.family.pets.dog.age);",
									"pm.test(\"check the dog have age 4\", function() {",
									"    pm.expect(jsonData.family.pets.dog.age).to.eql(4);",
									"});"
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5005/object_info_3?name=Julia&age=39&salary=600",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"object_info_3"
							],
							"query": [
								{
									"key": "name",
									"value": "Julia"
								},
								{
									"key": "age",
									"value": "39"
								},
								{
									"key": "salary",
									"value": "600"
								}
							]
						}
					},
					"response": []
				}
```
### EP_4 (/object_info_4)
`http://162.55.220.72:5005/object_info_4`
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age из request (age забрать из request.)
7. Вывести в консоль параметр salary из request.
8. Вывести в консоль параметр salary из response.
9. Вывести в консоль 0-й элемент параметра salary из response.
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
15. Создать в окружении переменную name
16. Создать в окружении переменную age
17. Создать в окружении переменную salary
18. Передать в окружение переменную name
19. Передать в окружение переменную age
20. Передать в окружение переменную salary
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.

#### Решение
```
{
					"name": "object_info_4",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Спарсить response body в json.",
									"var jsonData=pm.response.json();",
									"//Спарсить request",
									"var req_url=pm.request.url.query.toObject();",
									"",
									"//Проверить, что name в ответе равно name s request (name забрать из request.)",
									"console.log(\"request name==\",req_url.name,typeof req_url.name);",
									"pm.test(\"check the name\",function(){",
									"    pm.expect(req_url.name).to.eql(jsonData.name);",
									"});",
									"",
									"//Проверить, что age в ответе равно age s request (age забрать из request.)",
									"console.log(\"request age==\",req_url.age,typeof +req_url.age);",
									"pm.test(\"check the age\",function(){",
									"    pm.expect(Number(req_url.age)).to.eql(Number(jsonData.age));",
									"});",
									"",
									"//Вывести в консоль параметр salary из request.",
									"console.log(\"request salary==\",req_url.salary,typeof +req_url.salary);",
									"",
									"//Вывести в консоль параметр salary из response.",
									"console.log (\"response salary==\", jsonData.salary);",
									"",
									"//Вывести в консоль 0-й элемент параметра salary из response.",
									"console.log (\"response salary==\", jsonData.salary[0]);",
									"",
									"//Вывести в консоль 1-й элемент параметра salary параметр salary из response.",
									"console.log (\"response salary==\", jsonData.salary[1]);",
									"",
									"//Вывести в консоль 2-й элемент параметра salary параметр salary из response.",
									"console.log (\"response salary==\", jsonData.salary[2]);",
									"",
									"//Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)",
									"console.log (\"array salary==\", jsonData.salary[0], +req_url.salary);",
									"pm.test(\"check the 0 element of salary array = req salary\",function(){",
									"    pm.expect(jsonData.salary[0]).to.eql(+req_url.salary);",
									"});",
									"",
									"//Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)",
									"console.log (\"array salary==\", jsonData.salary[1], +req_url.salary*2);",
									"pm.test(\"check the 1 element of salary array = salary*2\",function(){",
									"    pm.expect(+jsonData.salary[1]).to.eql(+req_url.salary*2);",
									"});",
									"",
									"//Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)",
									"console.log (\"array salary==\", jsonData.salary[2], +req_url.salary*3);",
									"pm.test(\"check the 2 element of salary array = salary*3\",function(){",
									"    pm.expect(+jsonData.salary[1]).to.eql(+req_url.salary*2);",
									"});",
									"",
									"//Создать в окружении переменную name",
									"pm.environment.get(\"name\");",
									"//Создать в окружении переменную age",
									"pm.environment.get(\"age\");",
									"//Создать в окружении переменную salary",
									"pm.environment.get(\"salary\");",
									"",
									"//Передать в окружение переменную name",
									"pm.environment.set(\"name\", \"Anna\");",
									"//Передать в окружение переменную age",
									"pm.environment.set(\"age\", \"35\");",
									"//Передать в окружение переменную salary",
									"pm.environment.set(\"salary\", \"1000\");",
									"",
									"//Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.",
									"for (i in jsonData.salary) {",
									"    console.log(i, jsonData.salary[i]);",
									"};",
									"",
									""
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5006/object_info_4?name=Anna&age=36&salary=1000",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5006",
							"path": [
								"object_info_4"
							],
							"query": [
								{
									"key": "name",
									"value": "Anna"
								},
								{
									"key": "age",
									"value": "36"
								},
								{
									"key": "salary",
									"value": "1000"
								}
							]
						}
					},
					"response": []
				}
```
### EP_5(/user_info_2)
`http://162.55.220.72:5005/user_info_2`
1. Вставить параметр salary из окружения в request
2. Вставить параметр age из окружения в age
3. Вставить параметр name из окружения в name
4. Отправить запрос.
5. Статус код 200
6. Спарсить response body в json.
7. Спарсить request.
8. Проверить, что json response имеет параметр start_qa_salary
9. Проверить, что json response имеет параметр qa_salary_after_6_months
10. Проверить, что json response имеет параметр qa_salary_after_12_months
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
13. Проверить, что json response имеет параметр person
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.

#### Решение
```
{
					"name": "user_info_2",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Вставить параметр salary из окружения в request",
									"//Вставить параметр age из окружения в age",
									"//Вставить параметр name из окружения в name",
									"",
									"",
									"//Спарсить response body в json.",
									"var jsonData=pm.response.json();",
									"console.log(\"response ==\", jsonData);",
									"//Спарсить request.",
									"var req_body=request.data;",
									"console.log(\"request ==\", req_body);",
									"",
									"//Проверить, что json response имеет параметр start_qa_salary",
									"console.log(\"response have to start_qa_salary == \",jsonData.start_qa_salary,typeof jsonData.start_qa_salary);",
									"pm.test(\"check the response have to start_qa_salary\", function() {",
									"    pm.expect(jsonData).to.have.property('start_qa_salary');",
									"});",
									"",
									"//Проверить, что json response имеет параметр qa_salary_after_6_months",
									"console.log(\"response have to qa_salary_after_6_months == \",jsonData.qa_salary_after_6_months,typeof jsonData.qa_salary_after_6_months);",
									"pm.test(\"check the response have to qa_salary_after_6_months\", function() {",
									"    pm.expect(jsonData).to.have.property('qa_salary_after_6_months');",
									"});",
									"",
									"//Проверить, что json response имеет параметр qa_salary_after_12_months",
									"console.log(\"response have to qa_salary_after_12_months == \",jsonData.qa_salary_after_12_months,typeof jsonData.qa_salary_after_12_months);",
									"pm.test(\"check the response have to qa_salary_after_12_months\", function() {",
									"    pm.expect(jsonData).to.have.property('qa_salary_after_12_months');",
									"});",
									"",
									"//Проверить, что json response имеет параметр qa_salary_after_1.5_year",
									"console.log(\"response have to qa_salary_after_1.5_year == \",jsonData.qa_salary_after_1_5_year,typeof jsonData.qa_salary_after_1_5_year);",
									"pm.test(\"check the response have to qa_salary_after_1.5_year\", function() {",
									"    pm.expect(jsonData).to.have.property('qa_salary_after_1.5_year');",
									"});",
									"",
									"//Проверить, что json response имеет параметр qa_salary_after_3.5_years",
									"console.log(\"response have to qa_salary_after_3.5_year == \",jsonData.qa_salary_after_3_5_years,typeof jsonData.qa_salary_after_3_5_years);",
									"pm.test(\"check the response have to qa_salary_after_3.5_years\", function() {",
									"    pm.expect(jsonData).to.have.property('qa_salary_after_3.5_years');",
									"});",
									"",
									"//Проверить, что json response имеет параметр person",
									"console.log(\"response have to person == \",jsonData.person,typeof jsonData.person);",
									"pm.test(\"check the response have to person\", function() {",
									"    pm.expect(jsonData).to.have.property('person');",
									"});",
									"",
									"//Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)",
									"pm.test(\"check the start_qa_salary = salary from request\",function(){",
									"    pm.expect(Number(jsonData.start_qa_salary)).to.eql(Number(req_body.salary));",
									"});",
									"",
									"//Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)",
									"pm.test(\"check the qa_salary_after_6_months = salary*2\",function(){",
									"    pm.expect(Number(jsonData.qa_salary_after_6_months)).to.eql(Number(req_body.salary*2));",
									"});",
									"console.log(+jsonData.qa_salary_after_6_months, +req_body.salary*2);",
									"",
									"//Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)",
									"pm.test(\"check the qa_salary_after_12_months = salary*2.7\",function(){",
									"    pm.expect(Number(jsonData.qa_salary_after_12_months )).to.eql(Number(req_body.salary*2.7));",
									"});",
									"console.log(+jsonData.qa_salary_after_12_months, +req_body.salary*2.7 );",
									"",
									"//Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)",
									"pm.test(\"check the qa_salary_after_1.5_year = salary*3.3\",function(){",
									"    pm.expect(+jsonData[\"qa_salary_after_1.5_year\"]).to.eql(+req_body.salary*3.3);",
									"});",
									"console.log(+jsonData[\"qa_salary_after_1.5_year\"], +req_body.salary*3.3);",
									"",
									"//Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)",
									"pm.test(\"check the qa_salary_after_3.5_years= salary*3.8\",function(){",
									"    pm.expect(+jsonData[\"qa_salary_after_3.5_years\"]).to.eql(+req_body.salary*3.8);",
									"});",
									"console.log(+jsonData[\"qa_salary_after_3.5_years\"],+req_body.salary*3.8);",
									"",
									"//Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)",
									"pm.test(\"check the 1 element from u_name = salary from request\",function(){",
									"    pm.expect(+jsonData.person.u_name[1]).to.eql(+req_body.salary);",
									"});",
									"console.log(+jsonData.person.u_name[1], +req_body.salary);",
									"",
									"//Проверить, что что параметр u_age равен age из request (age забрать из request.)",
									"pm.test(\"check the u_age = age from request\",function(){",
									"    pm.expect(+jsonData.person.u_age).to.eql(+req_body.age);",
									"});",
									"console.log(+jsonData.person.u_age, +req_body.age);",
									"",
									"//Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)",
									"pm.test(\"check the u_salary_5_years = salary*4.2 from request\",function(){",
									"    pm.expect(+jsonData.person.u_salary_5_years).to.eql(+req_body.salary*4.2);",
									"});",
									"console.log(jsonData.person.u_salary_5_years, +req_body.salary*4.2);",
									"",
									"//***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.",
									"for (i in jsonData.person) {",
									"    console.log(i, jsonData.person[i]);",
									"};"
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "formdata",
							"formdata": [
								{
									"key": "name",
									"value": "{{name}}",
									"type": "text"
								},
								{
									"key": "age",
									"value": "{{age}}",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "{{salary}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://162.55.220.72:5005/user_info_2",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"user_info_2"
							]
						}
					},
					"response": []
				}
			]
		}
	],
	"event": [
		{
			"listen": "prerequest",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		}
```
