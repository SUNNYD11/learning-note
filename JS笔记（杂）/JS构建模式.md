//工厂模式，解决了创建多个相似对象的问题，没有解决对象识别问题
//，不知道是哪个对象的实例
function createPerson(name, age, job) {
  var a = new Object();
  a.name = name;
  a.age = age;
  a.job = job;
  a.exWay = function() {
    console.log(a);
  }
  return a;
}
var zz = createPerson("zz", 22, "txt");
zz.exWay();

//构造函数模式，解决对象识别问题
//使用构造函数的最大问题在于每次创建实例的时候都要重新创建一次方法
//(理论上每次创建对象的时候对象的属性均不同,而对象的方法是相同的)
//然而创建两次完全相同的方法是没有必要的,这个问题可以用原型来解决
function person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.show = function() {
    console.log(this)
  };
}
var aa = new person("aa", 123, "123");
aa.show();

//原型模式，所有实例共享属性和方法
function per() {}
per.prototype.name = "bb";
per.prototype.age="11";
per.prototype.job="321";
per.prototype.show2 = function() {
  console.log(this)
  console.log(this.job)
}
var bb = new per();
bb.show2();
//原型+构造组合模式，构造函数定义实例属性，原型定义方法和共享属性
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ["1", "2"]
}
Person.prototype = {
  constructor : Person,
  sayName: function() {
    console.log(123)
  }
};
var cc = new Person("cc",123,"ccc");
var dd = new Person("dd","ddd","dddd");

cc.friends.push("3");
console.log(cc.friends);
console.log(dd.friends);
