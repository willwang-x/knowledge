# Object-oriented Design 

## Why?

Good design is paramount to extensible, bug-free, long-lived code. It’s possible to solve any given software problem in an almost limitless number of ways, but when software needs to be extensible and maintainable, good software design is critical to success. Using Object-oriented design best practices is one way to build lasting software. 

You should have a working knowledge of a few common and useful design patterns as well as know how to write software in an object-oriented way, with appropriate use of **inheritance** and **aggregation**. You probably won’t be asked to describe the details of how specific design patterns work, but expect to have to defend your design choices.

## What 

OO Design的题目一般需要UML相关的知识做准备：

* class diagram (类图): 最常用
* sequence diagram (时序图): 最常用
* state machine diagram (状态机图): 在分析系统中某实体的状态时可能会用到。

## How 


* 澄清题目中**含糊不清**的地方。
* 定义出核心的**对象**。 (名词)
* 分析对象之间的关系，例如**包含与被包含**关系，**数量上**的关系，**继承上**的关系，等等。
* 分析对象可以具有的**行为**(也就是各个class的methods)。 （动词）


## Practice  


* [**Design a hash map**](https://github.com/donnemartin/system-design-primer/blob/master/solutions/object_oriented_design/hash_table/hash_map.ipynb)
	* Constraints and assumptions
		* For simplicity, are the keys integers only?
		* For collision resolution, can we use chaining?
		* Do we have to worry about load factors?
		* Can we assume inputs are valid or do we have to validate them?
		* Can we assume this fits memory? 
 	
* [Design a least **recently used cache**](https://github.com/donnemartin/system-design-primer/blob/master/solutions/object_oriented_design/lru_cache/lru_cache.ipynb)	
	* Constraints and assumptions
		* What are we caching?
		* Can we assume inputs are valid or do we have to validate them?
		* Can we assume this fits memory?
 
* [Design **a call center**](https://github.com/donnemartin/system-design-primer/blob/master/solutions/object_oriented_design/call_center/call_center.ipynb)
	* Constraints and assumptions
		* What levels of employees are in the call center?
		* Can we assume operators always get the initial calls?
		* If there is no available operators or the operator can't handle the call, does the call go to the supervisors?
		* If there is no available supervisors or the supervisor can't handle the call, does the call go to the directors?
		* Can we assume the directors can handle all calls?
		* What happens if nobody can answer the call?
		* Do we need to handle 'VIP' calls where we put someone to the front of the line?
		* Can we assume inputs are valid or do we have to validate them?

* [Design a deck of cards](https://github.com/donnemartin/system-design-primer/blob/master/solutions/object_oriented_design/deck_of_cards/deck_of_cards.ipynb)
	* Constraints and assumptions
		* Is this a generic deck of cards for games like poker and black jack?
		* Can we assume the deck has 52 cards (2-10, Jack, Queen, King, Ace) and 4 suits?
		* Can we assume inputs are valid or do we have to validate them?
* [Design a parking lot](https://github.com/donnemartin/system-design-primer/blob/master/solutions/object_oriented_design/parking_lot/parking_lot.ipynb)
	* Constraints and assumptions
		* What types of vehicles should we support?
		* Does each vehicle type take up a different amount of parking spots?
		* Does the parking lot have multiple levels? 
* [Design a chat server	](https://github.com/donnemartin/system-design-primer/blob/master/solutions/object_oriented_design/online_chat/online_chat.ipynb)  
* Design a circular array	


## More 

* [ ] [如何准备OO Design](https://github.com/yaobinwen/job_hunting/blob/master/README.md) 
* [ ] [面向对象设计面试笔记](https://wdxtub.com/interview/14520596997643.html)
* [ ] [Youtube: Object Oriented Design](https://www.youtube.com/watch?v=fJW65Wo7IHI&index=1&list=PLGLfVvz_LVvS5P7khyR4xDp7T9lCk9PgE): 一个OOD教程。
* [ ] [OOD-电梯系统](https://jiayi797.github.io/2018/07/08/OOD-%E7%94%B5%E6%A2%AF%E7%B3%BB%E7%BB%9F/): 一个例子。
* [ ] [Object-oriented design interview questions with solutions
](https://github.com/donnemartin/system-design-primer#object-oriented-design-interview-questions-with-solutions)