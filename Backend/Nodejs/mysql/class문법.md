# Sequelize Class 문법

## Model

기본 형태

```js
const { Sequelize, DataTypes, Model } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory');

class User extends Model {}
// init 함수는 Model class의 static 메서드이다. 
User.init({
  // Model attributes are defined here
  firstName: {
    type: DataTypes.STRING,
    allowNull: false
  },
  lastName: {
    type: DataTypes.STRING
    // allowNull defaults to true
  }
}, {
  // Other model options go here
  sequelize, 
  // We need to pass the connection instance
  modelName: 'User' 
  // We need to choose the model name
});
// the defined model is the class itself
console.log(User === sequelize.models.User); // true
```

내부적으로 `sequelize.define` 은 `Model.init`을 호출한다. 따라서 두 방식은 완전히 같은 방식이다.

오버라이딩 하는 방식

```js
const { Sequelize, DataTypes, Model } = require('sequelize');
const env = process.env.NODE_ENV || 'development';
const config = require('../config/config.js')[env];
const sequelize = new Sequelize(config.database, config.username, config.password, config);

class User extends Model{
  static init(){

  }
}

```
