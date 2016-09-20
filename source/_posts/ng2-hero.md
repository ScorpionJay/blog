---
title: ng2-hero
date: 2016-09-09 11:48:44
tags:
- angularjs
---
Angularjs 2 demo
<!--more-->

AppComponent
~~~js
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<h1>{{title}}</h1>
    			<h2>{{hero}}</h2>`
})
export class AppComponent { 
	
	title = 'Tour of Heroes' 
	hero = 'windstorm'

}
~~~


双向数据绑定

导入FormsModule模块
语法 [(ngModel)] = '...'

ng-model=‘变量名’  换成了 [(ngModel)] = ‘变量名’  


循环
ng-repeat = 'hero in heros'
*ngFor = 'let hero of heros'

组件里定义样式
~~~css
styles: [`
  .selected {
    background-color: #CFD8DC !important;
    color: white;
  }`
]
~~~


click 事件

(click)="onSelect(hero)"

ngIf 隐藏空的
~~~html
<div *ngIf='selected'>
...
</div>
~~~


设置样式

class.selected 是括在一对方括号中的。 这就是“属性绑定”的语法

[class.selected]='hero === selectedHero'


多个组件

服务

路由

HTTP