# TDraymarchToolkit
A raymarch Toolkit for TouchDesigner

![alt text](img.PNG)

## Usage:
press shift+rightclick to open op create dialog for RTK. Place some ops, create a stanard touchdesigner render TOP, camera COMP and Light COMP to make use of RTKs render OP.

## Limitations/known Issues:
- You cannot rename OPs without running into problems.
- Material interpolation when using smoothUnion is broken at the moment
- only one light supported

## TODOs/next Steps:
- anti aliasing
- refine materials
- change datastructure to support mat. interpolation

## Make your own OPs
Let's go through an example, we want to create an OP that can only translate in Y for some reason.
1. Go to ```/project1/RTK/operators```. Here you can find all the ops that where created so far. 
2. Copy one of them. Copy something simple and similar to what you want to achieve, for example the ```Translate``` OP.
3. Rename your new OP. We'll rename it ```TranslateY```.
4. Make your changes:
	- Rewrite the function now located at ```/project1/RTK/operators/translateY/processfun```. We will change it to contain the code:
	``` 
	vec2 thismap(vec3 p){
	p.y -= @Translate;
	return inputOp1(p);
	}
	```
Please note: Your function needs to take a vec3 and return a vec2. Variables beginning with ```@``` are goingto be parsed to reference the components custom parameters. ```inputOP1``` will be parsed to reference the OP's input.

	- customize your coponent to have exactly the right parameters. In our case we delete the original Transformxyz and add a float named ```Translate```.

5. go to ```/project1/RTK/operators/translateY/filterSetup``` and run the ```filterSetup``` script.

## References
Thanks to [MERCURY](http://mercury.sexy), (their [library](http://mercury.sexy/hg_sdf) is included here) and [Inigo Quilez](https://www.iquilezles.org/index.html) for all the good articles and formulas. Please check MERCURY's licence.