

## es6新语法

1. let const 
2. 模板语法
3. 箭头函数
4. 对象属性的简写
5. Promise
6. import/export/export defalut


##　原型指向一个对象实例

1. fn.proptotype=new Object()
2. Son.prototype=new Person()


## es7新语法

1. async/await


## let const

1. 都是块级作用域
2. const 声明的变量不可以重新覆盖
3. let声明的变量可以重新赋值


## 模板语法

1. `${name}已经${age}`

## 对象方法的简写和属性的简写

	
	const name="zhang"
	const obj={
		name,
        run(){
           console.log(this.name)
           }
	}
	
	console.log(obj.name)


## es6属性名表达式

const name="zhang"
	const obj={
		[name]:name,
        run(){
           console.log(this.name)
           }
	}
	
	console.log(obj.name)


## 箭头函数 箭头函数中的this指向上下文

	setTimeout(()=>{
		console.log('箭头函数')
	},1000)


## 回调函数处理异步 获取异步方法中的数据 在异步函数中调用回调函数

	function getDate(){
	  
	  const callback=function(data){
	  	console.log(data)
	  }
	
	  setTimeout(()=>{
	
	    const name="zhangsan"
	    callback(name)
	
	  },1000)
	
	
	}
	
	getDate()


	 function getDate(callback){
	  
	  setTimeout(()=>{
	    const name="zhangsan"
	    callback(name)
	
	  },1000)
	
	}
	
	// 回调函数获取异步方法中的数据
	
	getDate((data)=>{
		console.log(data)
	})

## Promise处理异步函数中的数据 在异步中调用回调函数


1. new Promise((resolve,reject)=>{})
2. resolve() 成功的回调函数
3. reject()  失败的回调函数

	new Promise((resolve,reject)=>{
	      
	      setTimeout(()=>{
	      	const name="zhangsan"
	      	// 回调函数获取 异步方法中的数据
	      	resolve(name)
	      },1000)
	
		}).then((data)=>{
			console.log(data)
		})


 ## Promise 获取异步方法中的数据
		
		function getDate(resolve,reject){
		  
		  setTimeout(()=>{
		    const name="zhangsan"
		    resolve(name)
		
		  },1000)
		
		}
		
		// 函数外面可以读取函数里面的
		
		new Promise(getDate).then((data)=>{
			console.log(data)
		})


## async await

1. async是"异步"的简写 而await可以认为是async wait 的简写。所以应该很好理解async用于声明function函数是异步的，而await用于等待一个异步方法执行完成
2. async 是让方法变成异步
3. await 是等待异步方法执行完成
4. async 是让方法变成异步，在终端里用node执行这段代码，你会发现输出了Promise{‘Hello async’},这时候会发现它返回的是Promise


## async 让一个普通方法变成异步方法


	async function getState(){
	
		return '这是一个数据'
	}
	
	console.log(getState())  // Promise {<resolved>: "这是一个数据"}


## async function getState(){} === new Promise()


## 获取async 异步方法中的数据 第一种方法

	async function getState(){
		return '这是一个数据ss'
	}
	
	getState().then((data)=>{
		console.log(data)
	})


## await 是等待异步方法执行完成 可以获取异步方法里面的数据 但是必须得用在异步方法里面

1. await在等待async异步方法执行完毕 其实await等待的只是一个表达式，这个表达式在官方文档说的是Promise对象。但是他是可以接受普通值的
2. 注意：await必须在异步方法中才可以使用因为await访问本身就会造成程序停止堵塞，所以必须在异步方法中才可以使用


	async function getState(){
		return '这是一个数据ss'
	}
	
	async function getStore(){
	   const data=await getState()
	   console.log(data)
	}
	
	getStore()

##await 可以直接获取异步返回的Promise对象 必须执行在异步的函数中

1. async function getDate(){const data=await async function getState(){ return xxx }}  data=xxx
2. async function getDate(){const data=await Promise}  data=resolve(xxx)



## await阻塞的功能 把异步函数改成同步函数


	async function getState(){
		console.log(2)
		return '这是一个数据ss'
	}
	
	async function getStore(){
	
		console.log(1)
	   // await把异步函数改成同步函数  从上至下 依次执行
	   const data=await getState()
	
	   console.log(data)
	
	   console.log(3)
	}
	
	getStore()  // 1 2  这是一个数据ss 3


## 用await 获取异步函数中的数据

		// 返回的是一个Promise对象
		function getState(){
		    // resolve是函数对象 resolve对象的标识符
			return new Promise((resolve,reject)=>{
				// 异步函数
				setTimeout(()=>{
		           // 异步函数中的数据
		          const name="zhansagn"
		          // 把异步函数中的数据 用回调函数带出去
		          resolve(name)
				})
			})
		}
		
		
		async function getStore(){
		    //await 接收一个Promise对象  把异步转换成同步
			const data=await getState()
			console.log(data)
		}
		
		// 调用函数获取数据
		getStore()



## 没有用await 获取异步函数中的数据


	function getState(){
	    // resolve是函数对象 resolve对象的标识符
		return new Promise((resolve,reject)=>{
			// 异步函数
			setTimeout(()=>{
	           // 异步函数中的数据
	          const name="zhansagn"
	          // 把异步函数中的数据 用回调函数带出去
	          resolve(name)
			})
		})
	}
	
	
	
	getState().then((data)=>{
	
		console.log(data)
	
	 })



## 在异步方法中获取其他异步方法的数据


     async function getStore(){
		    //getState() 其他异步的方法
			const data=await getState()
			console.log(data)
		}

## nodejs中的所有的方法都是异步的



## es6中类的写法


	class Person{
      
       
        //实例对象的属性 实例化对象时 自动调用constructor函数
	    constructor(name,age){

	        this.name = name;//this代表的是实例对象

	        this.age=age;
	    }
        //实例对象的方法  对象方法的简写
	    say(){

           //这是一个类的方法，注意千万不要加上function

	        return "我的名字叫" + this.name+"今年"+this.age+"岁了";
	    }
	}

	var obj=new Person("laotie",88);

	console.log(obj.say());


## 类中函数的简写

	class Person{
	  constructor(name,age){
	  	this.name=name
	  	this.age=age
	  }
      //对象函数的简写
	  sun=()=>{
	  	console.log(this.name)
	  }
	}
	var p=new Person('zhang')
	p.sun()


## 类中函数简写

	class Person{
	  constructor(name,age){
	  	this.name=name
	  	this.age=age
	  }
	  sun(){
	  	console.log(this.name)
	  }
	}
	var p=new Person('zhang')
	p.sun()


## 对象中函数写法


	var obj={
		name:'zhansan',
		sun:function sun(){
				console.log(this.name)
			}
	}
	
	obj.sun()


## 对象中函数的简写


	var obj={
		name:'zhansan',
		sun(){
			console.log(this.name)
		}
	}
	
	obj.sun()


## 配置对象

1. 对象中的属性是固定不能修改
2. 属性对应的值 可以任意指定



## React组件对象中的方法和自定义的方法

	export default class Pie extends Component{
	
		//自定义的方法
		
		handOk=()=>{}
		handClick=()=>{}
		
       //或者
        handOk(){}
        handClick(){}
        
		//对象的方法
		componentWillMount(){}
		componentDidMount(){}
		render(){}
	
	}


## Vue组件中对象的方法和自定义的方法

	
	export default {
	
		//对象的属性
		
		methods:{
            //采用对象方法的简写
            handOk(){}
           }
		props:{}
		computed:{
          fullName(){
            return xxx
           }
         }
		watch:{
          fullname(value){
             
           }
          }
		components:{}
		filters:{}
		directives:{}
		
		// 采用对象方法的简写
		
		data(){}
		created(){}
		mounted(){}
	
	
	}



## try{}catch(){}


1. try  错误检测
2. catch  语句允许我们定义当 try 代码块发生错误时，所执行的代码块


## 操作数组的方法


1. reduce((pre,item)=>{  pre[item]='xxx' return pre },{})  返回一个新对象
2. reduce((pre.item)=>{ return pre},[]) 返回一个新数组
3. reduce((pre,item)=>{ pre+=1 return pre},0) 返回一个总和
4. map((pre,index)=>{return pre+1}) 返回一个新数组



## es5 类 静态方法 以及单例模式


## 在es5中的构造函数里面的方法和属性以及原型链上的方法和属性 都叫做实例的属性和方法

1. 实例的方法必须通过实例调用
2. 实例化完成构造函数才能调用实例的方法



## es5中的静态方法 通过类名直接调用 不会被实例继承

1. 直接绑定在类上的方法叫做静态方法
2. 静态方法是通过类名直接调用

	
	<script>
		
			//es5中的类 通过定义构造函数来实现的
		
			function Person(name,age){
		
		   //构造函数里面的属性和方法
		   this.name=name
		   this.age=age
		   this.run=function(){
		      console.log(`我叫${this.name}`)
		   }
		
			}
		  //原型链上的属性和方法
			Person.prototype.sex="man"
			Person.prototype.eat=function(){
				console.log(`我今年${this.age}`)
			}
		//类的静态方法
		Person.setName=function(){
			console.log('静态方法')
		}
		
		
		var p=new Person('lisi',20)
		p.run()
		p.eat()
		
		//执行静态方法
		Person.setName()
	
	</script>


## 构造函数里面的属性和方法与原型链链上的属性和方法的区别

1. 原型链上的属性和方法可以被多个实例共享
2. 构造函数里面的方法和属性不可以被多个实例共享


## 实例的属性和方法

1. 构造函数里面的属性和方法以及原型链上的属性和方法都是实例的方法


## 实例的方法和属性与静态方法的区别

1. 实例的属性和方法只能通过实例调用
2. 静态方法只能被Person.run()这样调用


## es5中继承是通过原型链+对象冒充的组合继承 prototype call


	<script>
		
			//原型链+对象冒充的组合继承
		
			// 对象冒充:没办法继承原型链上的属性和方法
			// 原型链:可以继承实例的方法和属性以及原型链上的方法和属性 但是实例化子类的时候没办法给父类传惨
		
			function Person(name,age){
				// 实例的方法和属性
				this.name=name
				this.age=age
				this.run=function(){
					console.log(`我是${this.name}`)
				}
			}
		
		// 原型链的方法
		Person.prototype.work=function(){ 
		   console.log(`我今年${this.age}`)
		}
		function Son(name,age){
		  // 对象冒充 实例继承 实例化的时候 可以给父类传参 
          //把参数传递给父类
		  Person.call(this,name,age)
		}
		// 原型继承
		Son.prototype=new Person()
		
		var s=new Son('lisi',10)
		
		s.run()
		s.work()
	</script>




## 原型链+对象冒充=组合继承模式


	<script>
		
		 //es5的类 
		
		 function Person(name,age){
		    //实例的属性和方法
		   this.name=name
		   this.age=age
		   this.run=function(){
		   	console.log(this.name)
		   }
		
		 }
		
		//原型的属性和方法
		Person.prototype.eat=function(){
		   console.log(this.age)
		}
		
		// 类的静态方法 只能通过类来调用
		Person.work=function(){
			console.log('我是静态的方法')
		}
		
		//实例的方法和属性以及原型链上的方法和属性都必须通过实例来调用
		
		// var p=new Person('zhangsan',10)
		// //通过实例调用方法
		// p.run()
		// p.eat()
		
		//通过类来调用静态方法
		
		Person.work()
		
		// es5中的继承 通过原型链和对象冒充 组合继承模式
		
		function Son(name,age,sex){
			//对象冒充 实例子类时 可以给父类传递参数 对象冒充不能继承原型上的方法
		  Person.call(this,name,age)
		  this.sex=sex
		}
		
		// 原型链继承 不能再子类实例化得时候向父类传递参数
		Son.prototype=new Person()
		Son.prototype.play=function(){
			console.log(this.sex)
		}
		var s=new Son('zhangsan',10,'man')
		//实例调用方法
		s.run()
		s.eat()
		s.play()
	
	
	</script>


## Es6 中的类、继承


	<script>
		
			//es6中的类
		
			class Person{
		    //构造函数 实例化的时候 会直接调用 初始化里面的属性
		    constructor(name,age){
		    	this.age=age
		    	this.name=name
		    }
		   
		   run(){
		   	console.log(this.name)
		   }
		   eat(){
		   	console.log(this.age)
		   }
		    
			}
		//自动调用constructor方法
		var p=new Person('lis',10)
		
		p.run()
		p.eat()
	</script>


## es6中的继承 extends继承 super()实例化子类时 把子类的数据传递给父类
	<script>
		
		//es6中的类
	
		class Person{
	    //构造函数 实例化的时候 会直接调用 初始化里面的属性
	    constructor(name,age){
	    	this.age=age
	    	this.name=name
	    }
	    //实例方法
	   run(){
	   	console.log(this.name)
	   }
       //实例方法
	   eat(){
	   	console.log(this.age)
	   }
	    
		}
	 // Son继承Person
	class Son extends Person{
	   constructor(name,age,sex){
	   	// 把参数传递给父类
	   	super(name,age)
	   	// Son自身的属性
	   	this.sex=sex
	   }
	   //实例方法
	   work(){
	     console.log(this.sex)
	   }
	  
		}
	
	 const s=new Son('lisi',10,'man')
	 s.run()
	 s.eat()
	 s.work()
	
	
	</script>



## es6中的静态方法和静态属性 static


	<script>
		
			//es6中的类
		
			class Person{
		    //构造函数 实例化的时候 会直接调用 初始化里面的属性
		    constructor(name,age){
		    	this.age=age
		    	this.name=name
		    }
		   
		  static run(){
		   	console.log('这是静态方法')
		   }
		   eat(){
		   	console.log(this.age)
		   }
		    
			}
		 const s=new Person('lisi',10,'man')
		//es6的静态方法
		Person.run()
		s.eat()
	</script>



## es6的类 和 继承

	<script>
			
			// es6中的类
		
			class Person{
		    //实例的属性  每一次实例都会调用constructor()方法
		    constructor(name,age){
		    	this.name=name
		    	this.age=age
		    }
		    //实例的方法
		    eat(){
		    	console.log(this.name)
		    }
		    work(){
		    	console.log(this.age)
		    }
		    //类的静态方法
		    static play(){
		    	console.log('这是静态方法')
		    }
			}
		
		var p=new Person('zhangsan',10)
		//实例调用方法
		p.eat()
		p.work()
		//类调用静态方法
		Person.play()
		
		// 类的继承 extends
		class Son extends Person{
			constructor(name,age,sex){
				//子类实例化时 传递参数给父类
				super(name,age)
		
				this.sex=sex
			}
			//实例的方法
		  run(){
		  	console.log(this.sex)
		  }
		
		}
		
		
		// 实例化子类
		
		var s=new Son('lisi',10,'woman')
		
		//实例调用方法
		s.eat()
		s.work()
		s.run()

	</script>


## es6中的实例的属性和实例的方法以及静态的属性和静态的方法


	<script>
		
		// es6中的类
	
		class Person{
		    //实例的属性
		    constructor(name,age){
		    	this.name=name
		    	this.age=age
		    }
		    //实例的方法
		    eat(){
		    	console.log(this.name)
		    }
		    work(){
		    	console.log(this.age)
		    }
		    //类的静态方法
		    static play(){
		    	console.log('这是静态方法')
		    }
		}
		
		
			//静态的属性
			Person.instance="这是静态的属性"
			
			var p=new Person('zhangsan',10)
			//实例调用方法
			p.eat()
			p.work()
			//类调用静态方法
			Person.play()
		
		console.log(Person.instance)
	
	</script>


## Es6 中的单例模式 一个类只能创建一个对象

1. 单例模式的定义是：保证一个类仅有一个一个实例，并提供一个访问它的全局访问点
2. 无论执行多少次实例 构造函数只执行一次
3. 执行多次实例化得时候 只执行一次构造函数=====>就叫做单例


	<script>
			
			class Db{
		
				static getInstance(){
					//第一次执行没有这个静态属性Db.instance
		     if(!Db.instance){
		       //实例化对象时 只执行一次构造函数
		     	 Db.instance=new Db() //执行构造函数
		     	 return Db.instance
		     }
		
		     	return Db.instance //直接返回对象的引用
		
				}
		
				constructor(){
					console.log('每次实例化时都会触发构造函数')
		      this.connect()
				}
				connect(){
					console.log('链接数据库')
				}
				find(){
					console.log('查询数据库')
				}
			}
		
		var db=Db.getInstance()
		var db1=Db.getInstance()
		
		db.find()
		db1.find()
	</script>


## 连接数据库单列模式

			
			
		// 引入数据库
		const MongoClient = require('mongodb').MongoClient;
		
		const Config=require('./config.js')
		
		class Db{
		
		  static getInstance(){ //无论实例化多少个实例 都指向同一个实例 即单例
		
		    if(!Db.instance){
		     return	Db.instance=new Db()
		    }else{
		    	return Db.instance
		    }
		
		  }
		
			constructor(){
		    this.dbConnect=''
			  this.connect()	
			}
		
			//链接数据库
		  connect(){
		     
		    return new Promise((resolve,reject)=>{
		
		      //解决数据库多次连接的问题
		    	if(!this.dbConnect){
		    		const  client = new MongoClient(Config.url);
				    client.connect((err)=>{
				    	if(err){
				    		reject(err)
				    	}else{
				    		// 链接成功返回db对象 
				    		 const db = client.db(Config.dbName);
				    		 this.dbConnect=db
				    		 // 返回db
				    		 resolve(this.dbConnect)
				    	}
				    })
		    	}else{
		    		// 再次链接数据 直接返回db 不用再执行一次链接操作
		    		resolve(this.dbConnect)
		    	}
		 
		    })
		
		
		    }
		   // 插入数据
			insert(table,json){
		
		     this.connect().then((db)=>{
		       
		       db.collection(table).insertOne(json)
		
		     }) 
		
			}
			// 更新数据
			update(){}
		  
		  // 查询数据
			find(table,json){
		   
		   return new Promise((resolve,reject)=>{
			   	this.connect().then((db)=>{
				    const result=db.collection(table).find(json)
				    result.toArray((err,docs)=>{
				    	if(err){
				    		reject(err)
				    	}else{
				    		//返回数据
				    	 resolve(docs)
				    	}
				      
				    })
		
			   })
		   })
		
			}
			// 删除数据
			delete(){}
		
		
		}
		
		
		// 第一次实例化
		
		const mydb=Db.getInstance()
		
		setTimeout(()=>{
			console.time('testForEach');
			mydb.find('user').then((data)=>{
				console.timeEnd('testForEach');
			})
		})
		
		setTimeout(()=>{
			console.time('testForEach1');
			mydb.find('user').then((data)=>{
				console.timeEnd('testForEach1');
			})
		},300)
		
		
		// 第二次实例化
		const mydb1=Db.getInstance()
		
		setTimeout(()=>{
			console.time('testForEach2');
			mydb1.find('user').then((data)=>{
				console.timeEnd('testForEach2');
			})
		},100)
		
		setTimeout(()=>{
			console.time('testForEach3');
			mydb1.find('user').then((data)=>{
				console.timeEnd('testForEach3');
			})
		},400)





## koa操作Mongodb数据库


1. 基于官方的node-mongodb-navtive驱动 封装更小 更快 更灵活的DB模块，让我们用nodejs操作Mongodb数据库更方便 更灵活
2. mkdir myproject 创建项目目录
3. cd myproject
4. npm init 初始化package.json
5. npm install mongodb --save 按装数据库


## koa操作Mongodb数据库步骤

1. 安装mongodb
2. 引入mongodb下面的MongoClient
3. 定义数据库连接地址 以及配置数据库
4. node连接数据库
5. 操作数据库



## 插入数据的三个方法


1. db.collection('table').insertOne({})  单个文档插入到一个集合
2. db.collection('table').insertMany({}) 将文档数组插入到一个集合
3. db.collection('table').insert({}) 将单个或多个文档到一个集合。要插入一个单一的文件，传递文档;插入多个文件，传递文档数组




## mongoose 封装了mongoDB对文档的一些增删改查等常用方法，让nodejs操作mongoDB数据库变得更加容易

## hph操作mysql



## commonjs模块

1. module.export=导出模块
2. const mo=require('') 引入模块


## es6js 模块

1. export/export default 导出模块
2. import {xxx}/xxx from '' 引入模块


## 模块化利于团队分工 互不干扰

1. 路由模块化 
2. 视图模块化