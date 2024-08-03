## Postman HW_1

## Создать запросы в Postman.
```
Protocol: http
IP: 162.55.220.72
Port: 5005
```
### EP_1 (/get_method)
```
Method: GET
EndPoint: /get_method
request url params: 
 name: str
 age: int

response: 
[
    “Str”,
    “Str”
]
```
#### Решение
```
{
					"name": "get_method",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5007/get_method?name=Julia&age=39",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5007",
							"path": [
								"get_method"
							],
							"query": [
								{
									"key": "name",
									"value": "Julia"
								},
								{
									"key": "age",
									"value": "39"
								}
							]
						}
					},
					"response": []
				}
```
==================
### EP_2 (/user_info_3)
```
Method: POST
EndPoint: /user_info_3
request form data: 
 name: str
 age: int
 salary: int

response: 
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}}
```
#### Решение
```
{
					"name": "user_info_3",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "formdata",
							"formdata": [
								{
									"key": "age",
									"value": "33",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "1000",
									"type": "text"
								},
								{
									"key": "name",
									"value": "Vadim",
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
==================
### EP_3 (/object_info_1)
```
Method: GET
EndPoint: /object_info_1
request url params: 
 name: str
 age: int
 weight: int

response: 
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}
```
#### Решение
```
{
					"name": "object_info_1",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5005/object_info_1?name=Julia&age=39&weight=58",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"object_info_1"
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
									"key": "weight",
									"value": "58"
								}
							]
						}
					},
					"response": []
				}
```
==================
### EP_4 (/object_info_2)
```
Method: GET
EndPoint: /object_info_2
request url params: 
 name: str
 age: int
 salary: int

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }
```
#### Решение
```
{
					"name": "object_info_2",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5005/object_info_2?name=Julia&age=39&salary=600",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
							"path": [
								"object_info_2"
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
				},
				{
					"name": "object_info_3",
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
==================
### EP_5 (/object_info_3)
```
Method: GET
EndPoint: /object_info_3
request url params: 
 name: str
 age: int
 salary: int

response: 
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
          }
```
#### Решение
```
{
					"name": "object_info_3",
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
==================
### EP_6 (/object_info_4)
```
Method: GET
EndPoint: /object_info_4
request url params: 
 name: str
 age: int
 salary: int

response: 
{'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}
```
#### Решение
```
{
					"name": "object_info_4",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "http://162.55.220.72:5005/object_info_4?name=Anna&age=36&salary=1000",
							"protocol": "http",
							"host": [
								"162",
								"55",
								"220",
								"72"
							],
							"port": "5005",
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
==================
### EP_7 (/user_info_2)
```
Method: POST
EndPoint: /user_info_2
request form data: 
 name: str
 age: int
 salary: int

response: 
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
```
#### Решение
```
{
			"name": "HW_1",
			"item": [
				{
					"name": "user_info_2",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "formdata",
							"formdata": [
								{
									"key": "name",
									"value": "Lesha",
									"type": "text"
								},
								{
									"key": "age",
									"value": "44",
									"type": "text"
								},
								{
									"key": "salary",
									"value": "3000",
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
```

