# System View
Another javascript application framework based on d3.js


## Why?
To simplify the visual representation of interacting systemss.


## How?
By structuring the app with systems that can intercommunicate via the mastermind.


Each system has :
* a data field (model)
* a parent (another system or the mastermind)
* a `create function(div)` that `return function refreshFcn(dt)`
* a removeFunction `rmFcn(args)`
* an `active` property -> if `active`, call `refreshFcn`, if not, dont.


A system can be a controller, a view, a model, a visual-coding tool, ...
A system can be a collection of systems.


## Mastermind?
Mastermind holds all the systems.
It calls the refreshFcns.
It is the center node.


# svc
- [ ] finding how to write a good README
- [ ]
- [ ] this is an incomplete item



# Exemple
```javascript
SYSTEM_X = function(){
	var that = this;
	that.id = 'system_x';
	that.data = {x:0};
	//that.parentId = 'another_sys';
	that.createFcn = function(div){
	  	var p = div.append('p')
	  		.on('click', function(){
	  			that.active = !that.active;
	  		});
	  	
		return function refreshFcn(dt){
			that.data.x += dt/1000;
			p.html(that.data.x);
		}
	}
}


master = new MASTERMIND(d3.select("#mastertest"))

master.newSys(SYSTEM_X);
master.loadSys('system_x')


master.begin();

```
