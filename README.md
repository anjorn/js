##### 题目1
	function Parent() {
	    this.a = 1;
	    this.b = [1, 2, this.a];
	    this.c = { demo: 5 };
	    this.show = function () {
	      console.log(this.a , this.b , this.c.demo);
	    }
	  }
	  function Child() {
	    this.a = 2;
	    this.change = function () {
	      this.b.push(this.a);
	      this.a = this.b.length;
	      this.c.demo = this.a++;
	    }
	  }
	  Child.prototype = new Parent();
	  var parent = new Parent();
	  var child1 = new Child();
	  var child2 = new Child();
	  child1.a = 11;
	  child2.a = 12;
	  parent.show();
	  child1.show();
	  child2.show();

	  child1.change();
	  child2.change();
	  parent.show();
	  child1.show();
	  child2.show();

##### 题目2
	function Foo() {
	    getName = function () { alert (1); };
	    return this;
	}
	Foo.getName = function () { alert (2);};
	Foo.prototype.getName = function () { alert (3);};
	var getName = function () { alert (4);};
	function getName() { alert (5);}
	 
	//请写出以下输出结果：
	Foo.getName();
	getName();
	Foo().getName();
	getName();
	new Foo.getName();
	new Foo().getName();
	new new Foo().getName();


##### 题目3
	var A = function() {
	    this.name = 'apple';
	}
	A.prototype.getName = function() {
	    return this.name;
	}

	// 补充代码

	var B = A.extend({
	    initialize: function() {
	        this.superclass.initialize.call(this);
	        this.total = 3;
	    },
	    say: function() {
	        return '我有' + this.total + '个' + this.getName()
	    }
	});
	var b = new B();
	console.log(b.say()); //我有3个apple
	
##### 题目4
	const HardMan = (name) => {
	class HardMan {
		contructor (name) {
			this.tasks = [this.init(name)]
			setTimeout(async () => {
				for (const task of this.tasks) {
					await task()
				}
			}, 0)
		}
		init (name) {
			return () => console.log(`I am ${name}`)
		}

		sleep (time) {
			return () => new Promise(
				resolve => setTimeout( () => {
					resolve(console.log(`Start learning after ${time} seconds` ))
				}, time * 1000),
			)
		}
		rest (time) {
			this.tasks.push(this.sleep(time))
			return this
		}
		restFirst (time) {
			this.tasks.unshift(this.sleep(time))
			return this
		}
		learn (skill) {
			this.tasks.push(() => {
				console.log(`Learning ${sth}`)
			})
			return this
		}
		return new HardMan(name)
	}
}
