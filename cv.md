![alt - RSSchool](/rsschool-cv/images/logo.jpg "RSSchool")
### 1. My name.


Hi, my name is Roman Goncharov.

### 2. My contacts.


You can contact me as follows:  
   * my phone number: ![alt - phone](/rsschool-cv/images/phone_icon.png "phone") +375297570176;
   * my e-mail: ![alt - mail](/rsschool-cv/images/mail_icon.png "mail") shaman.roman@tut.by;
   * my Skype: ![alt - Skype](/rsschool-cv/images/skype_icon.png "Skype") live:36eb6584d3d45c73;
   * my Telegram: ![alt - Telegram](/rsschool-cv/images/tel_icon.png "Telegram") @RomanSRS;
   * I also have social networks:  
   [![alt - logo](/rsschool-cv/images/vk_icon.png)][Vk]  [![alt - logo](/rsschool-cv/images/ok_icon.png)][Ok] [![alt - logo](/rsschool-cv/images/face_icon.png)][Facebook] [![alt - logo](/rsschool-cv/images/disc_icon.png)][Discord]  

   [Vk]: https://vk.com/id102971948
   [Ok]: https://ok.ru/profile420698075709
   [Facebook]: https://www.facebook.com/profile.php?id=100002427159955
   [Discord]: https://discordapp.com/channels/618148975958163644/618148976058826840  

### 3. Self-presentation.


My goal is to learn how to make web applications. I would also like to acquire a new profession in demand on the labor market, to meet new interesting people. I think it’s no secret that a good programmer makes - good money. This is my motivation.  
In recent years, I have been working as an analyst,working with databases. I always liked to analyze, try to find some solutions often in unusual situations.  
Diving into programming, I realize that I have to learn, learn something new every day, as technologies develop every day!

### 4. My skills.


I'm working with JavaScript, HTML and CSS, markdown syntax, working with Git in the terminal. I'm using Visual Studio Code and [Photopea](https://www.photopea.com) for working with images.

### 5. Code examples: 


```
n this Kata we are going to mimic the SQL syntax with JavaScript (or TypeScript).

To do this, you must implement the query() function. This function returns and object with the next methods:

{
  select: ...,
  from: ...,
  where: ...,
  orderBy: ...,
  groupBy: ...,
  having: ...,
  execute: ...
}

The methods are chainable and the query is executed by calling the execute() method.

SELECT * FROM numbers
var numbers = [1, 2, 3];
query().select().from(numbers).execute(); //[1, 2, 3]

//clauses order does not matter
query().from(numbers).select().execute(); //[1, 2, 3]

Of course, you can make queries over object collections:

var persons = [
  {name: 'Peter', profession: 'teacher', age: 20, maritalStatus: 'married'},
  {name: 'Michael', profession: 'teacher', age: 50, maritalStatus: 'single'},
  {name: 'Peter', profession: 'teacher', age: 20, maritalStatus: 'married'},
  {name: 'Anna', profession: 'scientific', age: 20, maritalStatus: 'married'},
  {name: 'Rose', profession: 'scientific', age: 50, maritalStatus: 'married'},
  {name: 'Anna', profession: 'scientific', age: 20, maritalStatus: 'single'},
  {name: 'Anna', profession: 'politician', age: 50, maritalStatus: 'married'}
];

//SELECT * FROM persons
query().select().from(persons).execute(); // [{name: 'Peter',...}, {name: 'Michael', ...}]

You can select some fields:

function profession(person) {
  return person.profession;
}

//SELECT profession FROM persons
query().select(profession).from(persons).execute(); //select receives a function that will be called with the values of the array //["teacher","teacher","teacher","scientific","scientific","scientific","politician"]

If you repeat a SQL clause (except where() or having()), an exception will be thrown

query().select().select().execute(); //Error('Duplicate SELECT');
query().select().from([]).select().execute(); //Error('Duplicate SELECT');
query().select().from([]).from([]).execute(); //Error('Duplicate FROM');
query().select().from([]).where([]).where([]) //This is an AND filter (see below)

You can omit any SQLclause:

var numbers = [1, 2, 3];

query().select().execute(); //[]
query().from(numbers).execute(); // [1, 2, 3]
query().execute(); // []

You can apply filters:

function isTeacher(person) {
  return person.profession === 'teacher';
}

//SELECT profession FROM persons WHERE profession="teacher" 
query().select(profession).from(persons).where(isTeacher).execute(); //["teacher", "teacher", "teacher"]

//SELECT * FROM persons WHERE profession="teacher" 
query().select().from(persons).where(isTeacher).execute(); //[{person: 'Peter', profession: 'teacher', ...}, ...]

function name(person) {
  return person.name;
}

//SELECT name FROM persons WHERE profession="teacher" 
query().select(name).from(persons).where(isTeacher).execute();//["Peter", "Michael", "Peter"]

Agrupations are also possible:

//SELECT * FROM persons GROUP BY profession <- Bad in SQL but possible in this kata
query().select().from(persons).groupBy(profession).execute(); 
[
  ["teacher",
     [
       {
        name: "Peter",
        profession: "teacher"
        ...
      },
      {
        name: "Michael",
        profession: "teacher"
        ...
      }
    ]
  ],
  ["scientific",
    [
       {
          name: "Anna",
          profession: "scientific"
        },
     ...
   ]
  ]
  ...
]

You can mix where() with groupBy():

//SELECT * FROM persons WHERE profession='teacher' GROUP BY profession
query().select().from(persons).where(isTeacher).groupBy(profession).execute();

Or with select():

function professionGroup(group) {
  return group[0];
}

//SELECT profession FROM persons GROUP BY profession
query().select(professionGroup).from(persons).groupBy(profession).execute(); //["teacher","scientific","politician"]

Another example:

function isEven(number) {
  return number % 2 === 0;
}

function parity(number) {
  return isEven(number) ? 'even' : 'odd';
}

var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]; 

//SELECT * FROM numbers
query().select().from(numbers).execute(); //[1, 2, 3, 4, 5, 6, 7, 8, 9]

//SELECT * FROM numbers GROUP BY parity
query().select().from(numbers).groupBy(parity).execute(); //[["odd",[1,3,5,7,9]],["even",[2,4,6,8]]]

Multilevel grouping:

function isPrime(number) {
  if (number < 2) {
    return false;
  }
  var divisor = 2;
  for(; number % divisor !== 0; divisor++);
  return divisor === number;
}

function prime(number) {
  return isPrime(number) ? 'prime' : 'divisible';
}

//SELECT * FROM numbers GROUP BY parity, isPrime
query().select().from(numbers).groupBy(parity, prime).execute(); // [["odd",[["divisible",[1,9]],["prime",[3,5,7]]]],["even",[["prime",[2]],["divisible",[4,6,8]]]]]

orderBy should be called after groupBy, so the values passed to orderBy function are the grouped results by the groupBy function.

Filter groups with having():

function odd(group) {
  return group[0] === 'odd';
}

//SELECT * FROM numbers GROUP BY parity HAVING odd(number) = true <- I know, this is not a valid SQL statement, but you can understand what I am doing
query().select().from(numbers).groupBy(parity).having(odd).execute(); //[["odd",[1,3,5,7,9]]]

You can order the results:

var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];

function descendentCompare(number1, number2) {
  return number2 - number1;
}

//SELECT * FROM numbers ORDER BY value DESC 
 query().select().from(numbers).orderBy(descendentCompare).execute(); //[9,8,7,6,5,4,3,2,1]

from() supports multiple collections:

var teachers = [
  {
    teacherId: '1',
    teacherName: 'Peter'
  },
  {
    teacherId: '2',
    teacherName: 'Anna'
  }
];


var students = [
  {
    studentName: 'Michael',
    tutor: '1'
  },
  {
    studentName: 'Rose',
    tutor: '2'
  }
];

function teacherJoin(join) {
  return join[0].teacherId === join[1].tutor;
}

function student(join) {
  return {studentName: join[1].studentName, teacherName: join[0].teacherName};
}

//SELECT studentName, teacherName FROM teachers, students WHERE teachers.teacherId = students.tutor
query().select(student).from(teachers, students).where(teacherJoin).execute(); //[{"studentName":"Michael","teacherName":"Peter"},{"studentName":"Rose","teacherName":"Anna"}]

Finally, where() and having() admit multiple AND and OR filters:

function tutor1(join) {
  return join[1].tutor === "1";
}

//SELECT studentName, teacherName FROM teachers, students WHERE teachers.teacherId = students.tutor AND tutor = 1 
query().select(student).from(teachers, students).where(teacherJoin).where(tutor1).execute(); //[{"studentName":"Michael","teacherName":"Peter"}] <- AND filter

var numbers = [1, 2, 3, 4, 5, 7];

function lessThan3(number) {
  return number < 3;
}

function greaterThan4(number) {
  return number > 4;
}

//SELECT * FROM number WHERE number < 3 OR number > 4
query().select().from(numbers).where(lessThan3, greaterThan4).execute(); //[1, 2, 5, 7] <- OR filter

var numbers = [1, 2, 1, 3, 5, 6, 1, 2, 5, 6];

function greatThan1(group) {
  return group[1].length > 1;
}

function isPair(group) {
  return group[0] % 2 === 0;
}

function id(value) {
  return value;
}

function frequency(group) {
  return { value: group[0], frequency: group[1].length };      
}

//SELECT number, count(number) FROM numbers GROUP BY number HAVING count(number) > 1 AND isPair(number)
query().select(frequency).from(numbers).groupBy(id).having(greatThan1).having(isPair).execute(); // [{"value":2,"frequency":2},{"value":6,"frequency":2}])

My  decision:


let query = function() {
	let self = {};
	
	let tables = [];
	let selector = null;

	let whereClauses = [];
	let havingClauses = [];
	
	let order = [];
	let group = [];
	
	let selectorAll = function(row) {
		return row;
	};
	
	self.select = function(e) {
		if (selector != null) throw new Error('Duplicate SELECT');
		selector = e || false; 
		return self; 
	};
	
	self.from = function() {
		if (tables.length > 0) throw new Error('Duplicate FROM');
		tables = Array.from(arguments);
		return self;
	};
	
	self.where = function() {
		whereClauses.push( Array.from(arguments) );
		return self;
	};
	
	self.having = function() {
		havingClauses.push( Array.from(arguments) );
		return self;
	};
	
	self.orderBy = function() {
		if (order.length > 0) throw new Error('Duplicate ORDERBY');
		order = Array.from(arguments);
		return self;
	};
	
	self.groupBy = function() {
		if (group.length > 0) throw new Error('Duplicate GROUPBY');
		group = Array.from(arguments);
		return self;
	};
	
	self.execute = function() {		
		let tmpdata = [];
		let gdata = [];

		let data = [];
		let t = 0;

		if (tables.length > 1) {

			tables.forEach(function() {
        			data.push([ ]);
     			});

			tables[0].forEach(function(row, i) {
				for (let t = 0; t < tables.length; t++) {
					data[t].push( tables[t][i] );
				}
			});

			tmpdata = [];
			(function traverseTable(D, t) {
				if (D.length === 0) {
					tmpdata.push( t.slice(0) );
				} else {
					for (let i = 0; i < D[0].length; i++) {
						t.push( D[0][i] );
						traverseTable( D.slice(1), t );
						t.splice(-1, 1);
					}
				}
			})(data, []);

			data = [];
			tmpdata.forEach(function(row, i) {
				if (whereClauses.every(function(orWhereClauses) {
					return orWhereClauses.some(function(whereClause) {
						return whereClause( row );
					});
				})) {
					data.push( row );
				}
			});

		} else if (tables.length === 1) {

			tables[0].forEach(function(row, i) {
				if (whereClauses.every(function(orWhereClauses) {
					return orWhereClauses.some(function(whereClause) {
						return whereClause( row );
					});
				})) {
					data.push( row );
				}
			});

		} else {
			data = [];
		}

		if (group.length > 0) {

			let T = {};

			data.forEach(function(row) {
				let t = T;
				group.forEach(fvar query = function() {
	let self = {};
	
	let tables = [];
	let selector = null;

	let whereClauses = [];
	let havingClauses = [];
	
	let order = [];
	let group = [];
	
	let selectorAll = function(row) {
		return row;
	};
	
	self.select = function(e) {
		if (selector != null) throw new Error('Duplicate SELECT');
		selector = e || false; 
		return self; 
	};
	
	self.from = function() {
		if (tables.length > 0) throw new Error('Duplicate FROM');
		tables = Array.from(arguments);
		return self;
	};
	
	self.where = function() {
		whereClauses.push( Array.from(arguments) );
		return self;
	};
	
	self.having = function() {
		havingClauses.push( Array.from(arguments) );
		return self;
	};
	
	self.orderBy = function() {
		if (order.length > 0) throw new Error('Duplicate ORDERBY');
		order = Array.from(arguments);
		return self;
	};
	
	self.groupBy = function() {
		if (group.length > 0) throw new Error('Duplicate GROUPBY');
		group = Array.from(arguments);
		return self;
	};
	
	self.execute = function() {		
		let tmpdata = [];
		let gdata = [];

		let data = [];
		let t = 0;

		if (tables.length > 1) {

			tables.forEach(function() {
        			data.push([ ]);
     			});

			tables[0].forEach(function(row, i) {
				for (let t = 0; t < tables.length; t++) {
					data[t].push( tables[t][i] );
				}
			});

			tmpdata = [];
			(function traverseTable(D, t) {
				if (D.length === 0) {
					tmpdata.push( t.slice(0) );
				} else {
					for (let i = 0; i < D[0].length; i++) {
						t.push( D[0][i] );
						traverseTable( D.slice(1), t );
						t.splice(-1, 1);
					}
				}
			})(data, []);

			data = [];
			tmpdata.forEach(function(row, i) {
				if (whereClauses.every(function(orWhereClauses) {
					return orWhereClauses.some(function(whereClause) {
						return whereClause( row );
					});
				})) {
					data.push( row );
				}
			});

		} else if (tables.length === 1) {

			tables[0].forEach(function(row, i) {
				if (whereClauses.every(function(orWhereClauses) {
					return orWhereClauses.some(function(whereClause) {
						return whereClause( row );
					});
				})) {
					data.push( row );
				}
			});

		} else {
			data = [];
		}

		if (group.length > 0) {

			let T = {};

			data.forEach(function(row) {
				let t = T;
				group.forEach(function(groupCallback) {
					let k = groupCallback(row);
					t[k] = t[k] || {}; t = t[k];
				});
				t._data = t._data || []; t._data.push(row);
			});

			(function traverse(node, R) {
				if (node._data != null) {
					node._data.forEach(function(e) { R.push(e); });
				} else {
					for (let k in node) {
						k = /\d+/.test(k) ? Number(k) : k;
						var row = [ k, [] ];
						traverse(node[k], row[1]);
						R.push(row);
					}
				}
			})(T, gdata);

			gdata.forEach(function(grow){ 
				if (havingClauses.every(function(orHavingClauses) {
					return orHavingClauses.some(function(havingClause) {
						return havingClause(grow);
					});
				})) {
					tmpdata.push(grow);
				}
			});
			data = tmpdata;

		}

		order.forEach(function(orderCallback) {
			data = data.sort(orderCallback);
		});
		
		return data.map( selector || selectorAll );
	};

	return self;
};
				t._data = t._data || []; t._data.push(row);
			});

			(function traverse(node, R) {
				if (node._data != null) {
					node._data.forEach(function(e) { R.push(e); });
				} else {
					for (let k in node) {
						k = /\d+/.test(k) ? Number(k) : k;
						var row = [ k, [] ];
						traverse(node[k], row[1]);
						R.push(row);
					}
				}
			})(T, gdata);

			gdata.forEach(function(grow){ 
				if (havingClauses.every(function(orHavingClauses) {
					return orHavingClauses.some(function(havingClause) {
						return havingClause(grow);
					});
				})) {
					tmpdata.push(grow);
				}
			});
			data = tmpdata;

		}

		order.forEach(function(orderCallback) {
			data = data.sort(orderCallback);
		});
		
		return data.map( selector || selectorAll );
	};

	return self;
};
```  
### 6. Experience.


I have no experience in programming, only solving any tasks in teaching JS and HTML. [Link to my projects:](https://happy-boyd-4e31bd.netlify.com/) 

### 7. Education.


I have higher education, graduated from the Belarusian National Technical University with a degree in optoelectronic and laser devices and systems. Engineer. I have completed courses from the Rolling Scopes and have a certificate of completion.
I also watched online webinars and layout intensives from Skillbox, OTUS.

### 8. English.


Unfortunately, I did not study English at school. I’m self-educating in this direction: Interner, various applications on the phone, watching videos on YouTube.