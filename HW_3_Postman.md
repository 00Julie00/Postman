## HW_3_Postman

### EP_1 (/login) 
необходимо залогиниться
```
POST
http://162.55.220.72:5005/login
login : str (кроме /)
password : str
```
Приходящий токен необходимо передать во все остальные запросы.

#### Решение
```
{
					"name": "login",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"var jsonData= pm.response.json();",
									"pm.environment.set(\"auth_token\", \"/s34lfgbj/None/jjd909/93862kjkWpqc1993None62317evny\");"
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5005/login?login=mooncake&password=qwery",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"login"
							],
							"query": [
								{
									"key": "login",
									"value": "mooncake"
								},
								{
									"key": "password",
									"value": "qwery"
								}
							]
						}
					},
					"response": []
				}
```
#### Дальше все запросы требуют наличие токена. 

### EP_2 (/user_info)
```
http://162.55.220.72:5005/user_info
req. (RAW JSON)
POST
age: int
salary: int
name: str
auth_token

resp.
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }
```
Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user

#### Решение
```
{
					"name": "user_info",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Статус код 200",
									"",
									"//Проверка структуры json в ответе.",
									"var jsonData=pm.response.json();",
									"",
									"var schema = {",
									"    \"type\": \"object\",",
									"    \"default\": {},",
									"    \"title\": \"Root Schema\",",
									"    \"required\": [",
									"        \"person\",",
									"        \"qa_salary_after_12_months\",",
									"        \"qa_salary_after_6_months\",",
									"        \"start_qa_salary\"",
									"    ],",
									"    \"properties\": {",
									"        \"person\": {",
									"            \"type\": \"object\",",
									"            \"default\": {},",
									"            \"title\": \"The person Schema\",",
									"            \"required\": [",
									"                \"u_age\",",
									"                \"u_name\",",
									"                \"u_salary_1_5_year\"",
									"            ],",
									"            \"properties\": {",
									"                \"u_age\": {",
									"                    \"type\": \"integer\",",
									"                    \"default\": 0,",
									"                    \"title\": \"The u_age Schema\"",
									"                },",
									"                \"u_name\": {",
									"                    \"type\": \"array\",",
									"                    \"default\": [],",
									"                    \"title\": \"The u_name Schema\",",
									"                    \"items\": {",
									"                        \"anyOf\": [{",
									"                            \"type\": \"string\",",
									"                            \"default\": \"\",",
									"                            \"title\": \"A Schema\"",
									"                        },",
									"                        {",
									"                            \"type\": \"integer\",",
									"                            \"title\": \"A Schema\"",
									"                        }]",
									"                    }",
									"                },",
									"                \"u_salary_1_5_year\": {",
									"                    \"type\": \"integer\",",
									"                    \"default\": 0,",
									"                    \"title\": \"The u_salary_1_5_year Schema\"",
									"                }",
									"            }",
									"        },",
									"        \"qa_salary_after_12_months\": {",
									"            \"type\": \"number\",",
									"            \"default\": 0.0,",
									"            \"title\": \"The qa_salary_after_12_months Schema\"",
									"        },",
									"        \"qa_salary_after_6_months\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The qa_salary_after_6_months Schema\"",
									"        },",
									"        \"start_qa_salary\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The start_qa_salary Schema\"",
									"        }",
									"    }",
									"}",
									"pm.test(\"Schema is valid\", function() { ",
									"    pm.response.to.have.jsonSchema(schema); });",
									"",
									"console.log (jsonData)",
									"console.log (schema )",
									"",
									"//В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.",
									"var req_body = pm.request.body;",
									"var req = JSON.parse(req_body.raw);",
									"",
									"",
									"pm.test(\"Payroll check_qa_salary_after_6_months\", function(){",
									"    if (jsonData.qa_salary_after_6_months == jsonData.start_qa_salary*2){",
									"    console.log ('Result == TRUE');",
									"}",
									"else {",
									"    console.log ('Result == FALSE');",
									"}",
									"});",
									"",
									"pm.test(\"Payroll check_qa_salary_after_12_months\", function(){",
									"    if (jsonData.qa_salary_after_12_months == jsonData.start_qa_salary*2.9){",
									"    console.log ('Result == TRUE');",
									"}",
									"else {",
									"    console.log ('Result == FALSE');",
									"}",
									"});",
									"",
									"pm.test(\"Payroll check_qa_salary_after_12_months\", function(){",
									"    if (jsonData.person[\"u_salary_1_5_year\"] == jsonData.start_qa_salary*4){",
									"    console.log ('Result == TRUE');",
									"}",
									"else {",
									"    console.log ('Result == FALSE');",
									"}",
									"});",
									"",
									"//Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user",
									"console.log(jsonData.person[\"u_salary_1_5_year\"], typeof jsonData.person[\"u_salary_1_5_year\"]);",
									"pm.environment.set(\"salary\", jsonData.person[\"u_salary_1_5_year\"]);"
								],
								"type": "text/javascript"
							}
						}
					],
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n\"age\":39,\n\"salary\":1000,\n\"name\":\"Julia\",\n\"auth_token\":\"{{auth_token}}\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "http://162.55.220.72:5005/user_info",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"user_info"
							]
						}
					},
					"response": []
				}
```
### EP_3 (/new_data)
```
http://162.55.220.72:5005/new_data
req.
POST
age: int
salary: int
name: str
auth_token

Resp.
{'name':name,
  'age': int(age),
  'salary': [salary, str(salary*2), str(salary*3)]}
```
Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
4) проверить, что 2-й элемент массива salary больше 1-го и 0-го

#### Решение
```
				{
					"name": "new_data",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Статус код 200",
									"//Проверка структуры json в ответе.",
									"var jsonData=pm.response.json();",
									"",
									"var schema = {",
									"    \"type\": \"object\",",
									"    \"default\": {},",
									"    \"title\": \"Root Schema\",",
									"    \"required\": [",
									"        \"age\",",
									"        \"name\",",
									"        \"salary\"",
									"    ],",
									"    \"properties\": {",
									"        \"age\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The age Schema\"",
									"        },",
									"        \"name\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The name Schema\"",
									"        },",
									"        \"salary\": {",
									"            \"type\": \"array\",",
									"            \"default\": [],",
									"            \"title\": \"The salary Schema\",",
									"            \"items\": {",
									"                \"anyOf\": [{",
									"                    \"type\": \"integer\",",
									"                    \"default\": 0,",
									"                    \"title\": \"A Schema\"",
									"                },",
									"                {",
									"                    \"type\": \"string\",",
									"                    \"title\": \"A Schema\"",
									"                }]",
									"            }",
									"        }",
									"    }",
									"}",
									"",
									"pm.test(\"Schema is valid\", function() { ",
									"    pm.response.to.have.jsonSchema(schema); });",
									"",
									"console.log (jsonData)",
									"console.log (schema)",
									"",
									"//В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.",
									"pm.test(\"Payroll check_second coefficient\",function(){",
									"    if (jsonData.salary[1] == jsonData.salary[0]*2){",
									"    console.log ('Result == TRUE');",
									"}",
									"else {",
									"    console.log ('Result == FALSE');",
									"}",
									"});",
									"",
									"pm.test(\"Payroll check_third coefficient\", function(){",
									"    if (jsonData.salary[2] == jsonData.salary[0]*3){",
									"    console.log ('Result == TRUE');",
									"}",
									"else {",
									"    console.log ('Result == FALSE');",
									"}",
									"});",
									"",
									"//Проверить, что 2-й элемент массива salary больше 1-го и 0-го",
									"pm.test(\"Check that second coefficient > first coefficient\", function(){",
									"    pm.expect(Number(jsonData.salary[2])).to.greaterThan(Number(jsonData.salary[1]));",
									"});",
									"pm.test(\"Check that second coefficient > zero coefficient\", function(){",
									"    pm.expect(Number(jsonData.salary[2])).to.greaterThan(Number(jsonData.salary[0]));",
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
									"value": "Julia",
									"type": "text"
								},
								{
									"key": "age",
									"value": "39",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "1000",
									"type": "text"
								},
								{
									"key": "auth_token",
									"value": "{{auth_token}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://162.55.220.72:5005/new_data",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"new_data"
							]
						}
					},
					"response": []
				}
```
### EP_4 (/test_pet_info)
```
http://162.55.220.72:5005/test_pet_info
req.
POST
age: int
weight: int
name: str
auth_token


Resp.
{'name': name,
 'age': age,
 'daily_food':weight * 0.012,
 'daily_sleep': weight * 2.5}
```
Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.

#### Решение
```
{
					"name": "test_pet_info",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Статус код 200",
									"//Проверка структуры json в ответе.",
									"var jsonData=pm.response.json();",
									"var req_body=request.data;",
									"",
									"var schema ={",
									"    \"type\": \"object\",",
									"    \"default\": {},",
									"    \"title\": \"Root Schema\",",
									"    \"required\": [",
									"        \"age\",",
									"        \"daily_food\",",
									"        \"daily_sleep\",",
									"        \"name\"",
									"    ],",
									"    \"properties\": {",
									"        \"age\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The age Schema\"",
									"        },",
									"        \"daily_food\": {",
									"            \"type\": \"number\",",
									"            \"default\": 0.0,",
									"            \"title\": \"The daily_food Schema\"",
									"        },",
									"        \"daily_sleep\": {",
									"            \"type\": \"number\",",
									"            \"default\": 0.0,",
									"            \"title\": \"The daily_sleep Schema\"",
									"        },",
									"        \"name\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The name Schema\"",
									"        }",
									"    }",
									"}",
									"",
									"pm.test(\"Schema is valid\", function() { ",
									"    pm.response.to.have.jsonSchema(schema); });",
									"",
									"console.log (jsonData)",
									"console.log (schema)",
									"",
									"//В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.",
									"pm.test(\"verification of the correctness of the result of multiplication by a coefficient daily_food\",function(){",
									"    pm.expect(Number(jsonData.daily_food)).to.eql(Number(req_body.weight*0.012))",
									"});",
									"",
									"pm.test(\"verification of the correctness of the result of multiplication by a coefficient daily_sleep\",function(){",
									"    pm.expect(Number(jsonData.daily_sleep)).to.eql(Number(req_body.weight*2.5))",
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
									"key": "age",
									"value": "39",
									"type": "text"
								},
								{
									"key": "weight",
									"value": "57",
									"type": "text"
								},
								{
									"key": "name",
									"value": "Julia",
									"type": "text"
								},
								{
									"key": "auth_token",
									"value": "{{auth_token}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://162.55.220.72:5005/test_pet_info",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"test_pet_info"
							]
						}
					},
					"response": []
				}
```
### EP_5 (/get_test_user)
```
http://162.55.220.72:5005/get_test_user
req.
POST
age: int
salary: int
name: str
auth_token

Resp.
{'name': name,
 'age':age,
 'salary': salary,
 'family':{'children':[['Alex', 24],['Kate', 12]],
 'u_salary_1.5_year': salary * 4}
  }
```
Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.
3) Проверить что занчение поля name = значению переменной name из окружения
4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age

#### Решение
```
{
					"name": "get_test_user",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Статус код 200",
									"//Проверка структуры json в ответе.",
									"var jsonData=pm.response.json();",
									"var req_body=request.data;",
									"",
									"var schema ={",
									"    \"type\": \"object\",",
									"    \"default\": {},",
									"    \"title\": \"Root Schema\",",
									"    \"required\": [",
									"        \"age\",",
									"        \"family\",",
									"        \"name\",",
									"        \"salary\"",
									"    ],",
									"    \"properties\": {",
									"        \"age\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The age Schema\"",
									"        },",
									"        \"family\": {",
									"            \"type\": \"object\",",
									"            \"default\": {},",
									"            \"title\": \"The family Schema\",",
									"            \"required\": [",
									"                \"children\",",
									"                \"u_salary_1_5_year\"",
									"            ],",
									"            \"properties\": {",
									"                \"children\": {",
									"                    \"type\": \"array\",",
									"                    \"default\": [],",
									"                    \"title\": \"The children Schema\",",
									"                    \"items\": {",
									"                        \"type\": \"array\",",
									"                        \"title\": \"A Schema\",",
									"                        \"items\": {",
									"                            \"anyOf\": [{",
									"                                \"type\": \"string\",",
									"                                \"title\": \"A Schema\"",
									"                            },",
									"                            {",
									"                                \"type\": \"integer\",",
									"                                \"title\": \"A Schema\"",
									"                            }]",
									"                        }",
									"                    }",
									"                },",
									"                \"u_salary_1_5_year\": {",
									"                    \"type\": \"integer\",",
									"                    \"default\": 0,",
									"                    \"title\": \"The u_salary_1_5_year Schema\"",
									"                }",
									"            }",
									"        },",
									"        \"name\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The name Schema\"",
									"        },",
									"        \"salary\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The salary Schema\"",
									"        }",
									"    }",
									"}",
									"",
									"pm.test(\"Schema is valid\", function() { ",
									"    pm.response.to.have.jsonSchema(schema); });",
									"",
									"console.log (jsonData);",
									"console.log (schema);",
									"",
									"//Проверить что занчение поля name = значению переменной name из окружения",
									"pm.test(\"Check that name from response = name from environments\", function(){",
									"    pm.expect(jsonData.name).to.eql(pm.environment.get(\"name\"));",
									"});",
									"",
									"//Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age",
									"pm.test(\"Check that age from response = age from request\", function(){",
									"    pm.expect(jsonData.age).to.eql(req_body.age);",
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
									"key": "age",
									"value": "{{age}}",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "{{salary}}",
									"type": "text"
								},
								{
									"key": "name",
									"value": "{{name}}",
									"type": "text"
								},
								{
									"key": "auth_token",
									"value": "{{auth_token}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://162.55.220.72:5005/get_test_user",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"get_test_user"
							]
						}
					},
					"response": []
				}
```
### EP_6 (/currency)
```
http://162.55.220.72:5005/currency
req.
POST
auth_token

Resp. Передаётся список массив объектов.
[
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
…
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
]
```
Тесты:
1) Можете взять любой объект из присланного списка, используйте js random.
В объекте возьмите Cur_ID и передать через окружение в следующий запрос.

#### Решение
```
{
					"name": "currency",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Можете взять любой объект из присланного списка, используйте js random.",
									"var jsonData=pm.response.json();",
									"var len=jsonData.length;",
									"",
									"// Получаем случайный объект массива",
									"var rand = Math.floor(Math.random() * len);",
									"console.log(jsonData[rand]);",
									"",
									"//В объекте возьмите Cur_ID и передать через окружение в следующий запрос.",
									"pm.environment.set(\"Cur_ID\", jsonData[rand].Cur_ID);",
									"",
									"",
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
									"key": "auth_token",
									"value": "{{auth_token}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://54.157.99.22:80/currency",
							"protocol": "http",
							"host": [
								"54",
								"157",
								"99",
								"22"
							],
							"port": "80",
							"path": [
								"currency"
							],
							"query": [
								{
									"key": "",
									"value": "",
									"disabled": true
								}
							]
						}
					},
					"response": []
				}
```
### EP_7 (/curr_byn)
```
http://162.55.220.72:5005/curr_byn
req.
POST
auth_token
curr_code: int

Resp.
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
```
Тесты:
1) Статус код 200
2) Проверка структуры json в ответе.

#### Решение
```
{
					"name": "curr_byn",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//Статус код 200",
									"//Проверка структуры json в ответе.",
									"var jsonData=pm.response.json();",
									"var schema ={",
									"    \"type\": \"object\",",
									"    \"default\": {},",
									"    \"title\": \"Root Schema\",",
									"    \"required\": [",
									"        \"Cur_Abbreviation\",",
									"        \"Cur_ID\",",
									"        \"Cur_Name\",",
									"        \"Cur_OfficialRate\",",
									"        \"Cur_Scale\",",
									"        \"Date\"",
									"    ],",
									"    \"properties\": {",
									"        \"Cur_Abbreviation\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The Cur_Abbreviation Schema\"",
									"        },",
									"        \"Cur_ID\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The Cur_ID Schema\"",
									"        },",
									"        \"Cur_Name\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The Cur_Name Schema\"",
									"        },",
									"        \"Cur_OfficialRate\": {",
									"            \"type\": \"number\",",
									"            \"default\": 0.0,",
									"            \"title\": \"The Cur_OfficialRate Schema\"",
									"        },",
									"        \"Cur_Scale\": {",
									"            \"type\": \"integer\",",
									"            \"default\": 0,",
									"            \"title\": \"The Cur_Scale Schema\"",
									"        },",
									"        \"Date\": {",
									"            \"type\": \"string\",",
									"            \"default\": \"\",",
									"            \"title\": \"The Date Schema\"",
									"        }",
									"    }",
									"}",
									"",
									"pm.test(\"Schema is valid\", function() { ",
									"    pm.response.to.have.jsonSchema(schema); });",
									"",
									"console.log (jsonData);",
									"console.log (schema);"
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
									"key": "auth_token",
									"value": "{{auth_token}}",
									"type": "text"
								},
								{
									"key": "curr_code",
									"value": "{{Cur_ID}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://54.157.99.22:80/curr_byn",
							"protocol": "http",
							"host": [
								"54",
								"157",
								"99",
								"22"
							],
							"port": "80",
							"path": [
								"curr_byn"
							]
						}
					},
					"response": []
				}
```
### Additional task ***
1) получить список валют
2) итерировать список валют
3) в каждой итерации отправлять запрос на сервер для получения курса каждой валюты
4) если возвращается 500 код, переходим к следующей итреации
5) если получаем 200 код, проверяем response json на наличие поля "Cur_OfficialRate"
6) если поле есть, пишем в консоль инфу про фалюту в виде response
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
7) переходим к следующей итерации

#### Решение
```
{
					"name": "Additional Task***",
					"event": [
						{
							"listen": "test",
							"script": {
								"exec": [
									"//получить список валют",
									"var jsonData=pm.response.json();",
									"",
									"var array_length= jsonData.length;",
									"var token= pm.environment.get(\"auth_token\");",
									"",
									"//итерировать список валют",
									"for ( let i= 0; i< array_length; i++){",
									"    //в каждой итерации отправлять запрос на сервер для получения курса каждой валюты",
									"    let postRequest= {",
									"        url: 'http://54.157.99.22:80/curr_byn',",
									"        method: 'POST',",
									"        header:{\"Content-Type\":\"application/json\"},",
									"        body:{",
									"            mode: 'formdata',",
									"            formdata: [",
									"                {key: 'auth_token', value: 'token'},",
									"                {key: 'curr_code', value: jsonData[i].Cur_ID}",
									"            ]",
									"        },",
									"    }",
									"    //если возвращается 500 код, переходим к следующей итреации",
									"    pm.sendRequest(postRequest,function(err,response){",
									"       if (response.code == 500){",
									"           console.log(err);",
									"       }",
									"       //если получаем 200 код, проверяем response json на наличие поля \"Cur_OfficialRate\"",
									"       else if (response.code == 200){",
									"           pm.test(\"Cur_OfficialRate existing\", function(){",
									"               pm.expect(response.json()).to.have.property('Cur_OfficialRate');",
									"           });",
									"           if (pm.expect(response.json()).to.have.property('Cur_OfficialRate')){",
									"               //если поле есть, пишем в консоль инфу про фалюту в виде response",
									"               console.log(response.json());",
									"           }",
									"       }",
									"    }); //переходим к следующей итерации",
									"}"
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
									"key": "auth_token",
									"value": "{{auth_token}}",
									"type": "text"
								}
							]
						},
						"url": {
							"raw": "http://54.157.99.22:80/currency",
							"protocol": "http",
							"host": [
								"54",
								"157",
								"99",
								"22"
							],
							"port": "80",
							"path": [
								"currency"
							]
						}
					},
					"response": []
				}
```
