# MySQL

## 기초

1. MySQL Server 시작
   기본적으로 homebrew를 통해 설치하였으므로, 이를 통해서 실행을 해준다. 아래의 명령어는 mysql server를 시작하는 것이다.

```bash
brew services start mysql@5.7
// brew services stop ~
// brew services restart ~
```

2. MySQL Server에 연결하기

```bash
mysql -u root -p
// 입력시 비밀번호 입력 enter password:
mysql>
```

3. 나가기

```bash
mysql> quit
```

## 기본적인 Command Line

```bash
mysql> CREATE DATABASE menagerie; --> 데이터 베이스 생성

mysql> show databases;  // -> 데이터 베이스 확인
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| nodejs             |
| performance_schema |
| sys                |
+--------------------+

mysql> USE nodejs // 사용할 데이터 베이스 선택
Database changed

mysql>  SHOW tables; // -> 테이블 확인
+------------------+
| Tables_in_nodejs |
+------------------+
| comments         |
| users            |
+------------------+

mysql>DESCRIBE comments; --> 상세 정보
+------------+--------------+------+-----+-------------------+----------------+
| Field      | Type         | Null | Key | Default           | Extra          |
+------------+--------------+------+-----+-------------------+----------------+
| id         | int(11)      | NO   | PRI | NULL              | auto_increment |
| comment    | varchar(100) | NO   |     | NULL              |                |
| created_at | datetime     | NO   |     | CURRENT_TIMESTAMP |                |
| commenter  | int(11)      | YES  | MUL | NULL              |                |
+------------+--------------+------+-----+-------------------+----------------+

```

## Sequelize

### 설치

`npm i sequelize mysql2` --> 프로젝트 단위

여기서 mysql2는 'This is a node.js driver for mysql.'
`npm i -g sequelize-cli` --> 전역 설치(한번)

`sequelize init`
위 명령어를 수행시, 기본적으로 `config`, `models` 등의 폴더가 생성된다.

---

**note**

아래의 방식이 더 선호? 되는 것 같다. 글로벌로 설치를 하고 sequelize init을 하면 package.json에 기록이 안남는다.  
하지만 아래와 같은 방식으로 설치를 하면 package.json에 기록을 남길 수 있다.

```bash
npm i -D sequelize-cli
npx sequelize init
npx sequelize db:creat  // database 만드는 작업. config에 설정된 database 이름으로 생성된다.
```

---

`models/index.js` 에서 sequelize 모듈 import, db 객체 생성 등을 한다.
sequelize에서 단수형으로 모델을 만들면, table은 복수형으로 만들어진다.

```js
const Sequelize = require('sequelize');

const env = process.env.NODE_ENV || 'development';
const config = require('../config/config.json')[env];
// config.json에 [env] 키의 value값을 cofing에 넣는다.
const sequelize = new Sequelize(
  config.database,
  config.username,
  config.password,
  config,
);
// sequelize 인스턴스 생성
const db = {};

// 모듈을 가져온 다음에 바로 함수를 호출하는 것..!
db.User = require('./User')(sequelize, Sequelize);
db.Comment = require('./Comment')(sequelize, Sequelize);

db.User.hasMany(db.Comment, { foreignKey: 'commenter', sourceKey: 'id' });
db.Comment.belongsTo(db.User, { foreignKey: 'commenter', targetKey: 'id' });

db.Sequelize = Sequelize; // 패키지
db.sequelize = sequelize; // 인스턴스

module.exports = db;
```

### connection

`models/index.js` 에서 sequelize 인스턴스를 가져온다.

```js
// app.js
const { sequelize } = require('./models');

const app = express();
sequelize.sync();
```

### Model 정의

sequelize의 모델은 `js의 객체 인스턴스`이다.
An instance of the class represents one object from that model (which maps to one row of the table in the database).

sequelize.define() : Model;

```js
// models/user.js
module.exports = (sequelize, DataTypes) => {
  const User = sequelize.define(
    'users',
    {
      name: {
        type: DataTypes.STRING(20),
        allowNull: false,
        unique: true,
      },
      age: {
        type: DataTypes.INTEGER.UNSIGNED,
        allowNull: false,
      },
      married: {
        type: DataTypes.BOOLEAN,
        allowNull: false,
      },
      comment: {
        type: DataTypes.TEXT,
        allowNull: true,
      },
      created_at: {
        type: DataTypes.DATE,
        allowNull: false,
        defaultValue: sequelize.literal('now()'),
      },
    },
    {
      timestamps: false,
      underscored: false,
    },
  );
  return User;
};
```

```js
// option의 예시
name:{
  type: Sequelize.STRING,
  allowNull: false,
  defaultValue: 'a' | 0 | true ...,
  autoIncrement: true // 자동으로 값이 올라감.. type이 숫자일때
  primaryKey: true,
  unique: true,
  charset: 'utf8',
  collate: 'utf8_general_ci',
}
```

### 모델(스키마) 변경

```js
// app.js
db.sequelize.sync({ force: true });
// 뒤에 force 옵션을 붙이게 되면, 스키마 변경시 기존의 데이터가 싹 날아가고
// 새롭게 정의된 스키마가 생성된다. 개발환경에서만 사용.
```

만약 실제로 스키마를 변경하려면 마이그레이션에 대해 공부해야한다.

### config

```json
{
  "development": {
    "username": "root",
    "password": "***", // 비밀번호
    "database": "nodejs", // 데이터베이스 이름
}
```

데이터 베이스 스키마가 생성됨.

models가 table과 대응되는 개념.

### 기본 data_type

Sequelize.STRING
Sequelize.TEXT // TEXT

Sequelize.INTEGER // INTEGER

Sequelize.FLOAT // FLOAT

Sequelize.DOUBLE // DOUBLE

Sequelize.DATE

## 관계 설정

### PK 참고 (중요)

헷갈리는 개념이라서 따로 빼서 설명.  
기본적으로 sequelize는 pk가 없으면 `id` column을 추가하여 pk로 설정한다.

```js
sequelize.define('users', {
  name: {
    type: DataTypes.STRING(20),
    allowNull: false,
    primaryKey: true,
    // unique: true,
  },
  age: {
    type: DataTypes.INTEGER.UNSIGNED,
    allowNull: false,
  },
});
```

```bash
mysql> describe users;
+------------+------------------+------+-----+-------------------+-------+
| Field      | Type             | Null | Key | Default           | Extra |
+------------+------------------+------+-----+-------------------+-------+
| name       | varchar(20)      | NO   | PRI | NULL              |       |
| age        | int(10) unsigned | NO   |     | NULL              |       |
+------------+------------------+------+-----+-------------------+-------+
```

pk를 주석처리 하면 아래와 같다.

```bash
+------------+------------------+------+-----+-------------------+----------------+
| Field      | Type             | Null | Key | Default           | Extra          |
+------------+------------------+------+-----+-------------------+----------------+
| id         | int(11)          | NO   | PRI | NULL              | auto_increment |
| name       | varchar(20)      | NO   | UNI | NULL              |                |
| age        | int(10) unsigned | NO   |     | NULL              |                |
+------------+------------------+------+-----+-------------------+----------------+
```

### 관계 설명

(db책 7장 참고)
1:1 hasOne, belongsTo
1:N hasMany, belongsTo
N:N belongsToMany

이 부분은 relationshipt 부분을 따로 스키마로 빼느냐, 아니면 한쪽의 스키마로 합치느냐의 문제에서 한쪽으로 합치는 방향으로 되어있다.  
1:N 의 경우 relationship이 N쪽의 primary key를 취하는데, 이를 한쪽의 스키마로 합친다면, 1쪽의 primary key를 N 쪽에서 가지게 되고
N에서 이 속성은 foreign key가 된다.

하지만 sequelize에는 primary key가 없어도 관계를 설정할 수 있게 되어 있다.  
(내 생각에는 이게 맞나라는 생각은 든다... 어쨋든 하나의 relation은 튜플들을 식별할 수 있는 키를 가져야하는데, 이 경우에는 그렇지 않기 때문이다.)

### pk가 있을때

```js
Team.hasMany(Player);
Player.belongsTo(Team);
```

외래키의 이름을 바꾸고 싶거나, 관계를 의무적일 때는 아래와 같이 옵션을 통해 명시한다.

```js
Team.hasMany(Player, {
  foreignKey: 'clubId',
});
Player.belongsTo(Team);
```

### 관계 없을때

- For belongsTo relationships

```js
const Ship = sequelize.define(
  'ship',
  { name: DataTypes.TEXT },
  { timestamps: false },
);
const Captain = sequelize.define(
  'captain',
  {
    name: { type: DataTypes.TEXT, unique: true },
  },
  { timestamps: false },
);
```

```js
Ship.belongsTo(Captain, { targetKey: 'name', foreignKey: 'captainName' });
// This creates a foreign key called `captainName` in the source model (Ship)
// which references the `name` field from the target model (Captain).
```

- For hasMany relationships

```js
const Bar = sequelize.define(
  'bar',
  {
    title: { type: DataTypes.TEXT, unique: true },
  },
  { timestamps: false },
);
const Baz = sequelize.define(
  'baz',
  { summary: DataTypes.TEXT },
  { timestamps: false },
);
Bar.hasMany(Baz, { sourceKey: 'title', foreignKey: 'barTitle' });
// Baz에
```

### 코드 분석

어쨋든 index.js에서 다음과 같이 하면 many 쪽은 기본적으로 pk + foreignKey를 가지게 된다.  
위의 코드는 User(1) : Comment(N)에서 Comment쪽에 commenter라는 foreignKey를 User의 id를 `source`로 가지게 하라는 뜻이다.
아래의 코드는 Comment(N)이 foreignKey로 commenter를 가지는데 그 foreignKey는 User의 id가 `target`이라는 뜻이다.

```bash
db.User.hasMany(db.Comment, { foreignKey: 'commenter', sourceKey: 'id' });
db.Comment.belongsTo(db.User, { foreignKey: 'commenter', targetKey: 'id' });
```

comment의 pk는 자동으로 생성된 것이고, commenter가 user의 id와 이어지는 것이다.

```bash
mysql> describe comments;
+------------+--------------+------+-----+-------------------+----------------+
| Field      | Type         | Null | Key | Default           | Extra          |
+------------+--------------+------+-----+-------------------+----------------+
| id         | int(11)      | NO   | PRI | NULL              | auto_increment |
| comment    | varchar(100) | NO   |     | NULL              |                |
| created_at | datetime     | NO   |     | CURRENT_TIMESTAMP |                |
| commenter  | int(11)      | YES  | MUL | NULL              |                |
+------------+--------------+------+-----+-------------------+----------------+
4 rows in set (0.00 sec)

mysql> describe users;
+------------+------------------+------+-----+-------------------+----------------+
| Field      | Type             | Null | Key | Default           | Extra          |
+------------+------------------+------+-----+-------------------+----------------+
| id         | int(11)          | NO   | PRI | NULL              | auto_increment |
| name       | varchar(20)      | NO   | UNI | NULL              |                |
| age        | int(10) unsigned | NO   |     | NULL              |                |
| married    | tinyint(1)       | NO   |     | NULL              |                |
| comment    | text             | YES  |     | NULL              |                |
| created_at | datetime         | NO   |     | CURRENT_TIMESTAMP |                |
+------------+------------------+------+-----+-------------------+----------------+
```
