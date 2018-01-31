>我们常用的`node`的框架有`express`、`koa`、`Fastify`、`micro`、`keystone`、`nest`等,一般市场上比较流行的是`express`和`koa`,如果你熟悉`angular2+`及喜欢用`typescript`或者你是做`java`开发的,我推荐用`nest`,本人也是更喜欢`typescript`的语法,尝试用这个框架开发东西,不过在日常项目中还是用的`koa`,[官网地址](https://docs.nestjs.com/)

### 一、项目的基本创建(个人建议直接克隆官网的,俗称种子文件)
* 1、步骤

    ```javascript
    git clone https://github.com/nestjs/typescript-starter.git project
    cd project
    npm install
    npm run start:watch
    ```
    
* 2、具体目录结构
    ```javascript
    
    project
      |-src
        |-app.controller.ts
        |-app.module.ts
        |-main.ts
      |-index.js
      |-nodemon.json
      |-package.json
      |-README.md
      |-tsconfig.json
      |-tslint.json
      
    ```
* 3、`src`文件夹下几个重要文件介绍
    * `main.ts`是主入口文件
    * `app.module.ts`是总的`module`文件
    * `app.controller.ts`是官方提供输出一个`hello word`文件 

### 二、简单的使用
* 1、直接在`app.controller.ts`里面

    ```javascript
    import { Get, Controller, Post, Response, Param, HttpStatus, Request } from '@nestjs/common';
    
    @Controller()
    export class AppController {
    	@Get()
    	root(): string {
        return 'Hello World!';
      }
      @Get('/user/:id')
      user(@Response() res, @Param('id') id) {
        console.log(id)
        res.status(HttpStatus.OK).json({
          name: 'hello',
          age: 20
        });
      }
    }
    ```
    
### 三、关于客户端传递参数到服务器端的几种方式
* 1、`get`的情况下一

    ```javascript
    import { Controller, Get, Response, HttpStatus, Param } from '@nestjs/common'
    import { UsersService } from './users.service';
    
    @Controller('users')
    export class UsersController {
    
      @Get('/:id')
      getUser( @Response() res, @Param('id') id) {
        console.log(id);
        ...
      }
    
    }
    **访问方式**
    //http://localhost:4000/users/2
    ```
* 2、`get`的情况下二
    
    ```javascript
    import { Controller, Get, Response, Request } from '@nestjs/common'
    
    @Controller('users')
    export class UsersController {
    
      @Get('/')
      getUser( @Response() res, @Request() req) {
        console.log(req.query)
        ...
      }
    }
    **访问方式**
    //http://localhost:4000/users?age=10&name=hello
    ```
    
* 3、使用`post`获取数据

    ```javascript
    import { Controller, Post, Response, Request } from '@nestjs/common'
    
    @Controller('users')
    export class UsersController {
    
      @Post()
      addUser( @Response() res, @Request() req) {
        console.log(req.body, '///')
        ....
      }
    }
    ```
    
* 4、使用`post`获取数据

    ```javascript
    import { Controller, Post, Response, HttpStatus, Body } from '@nestjs/common'
    import { UsersService } from './users.service';
    
    @Controller('users')
    export class UsersController {
      @Post('/add')
      addUser1(@Response() res, @Body() user) {
        console.log(user);
        res.status(HttpStatus.CREATED).json({})
      }
    }
    ```
    
### 四、项目开发中使用组件化(`app`方式构建项目[`django`中叫`app`])
* 1、新增一个用户`users`的目录
* 2、在文件夹中创建三个(最基本的文件)
    * `users.module.ts`
    * `users.controller.ts`
    * `users.service.ts`

* 3、将`users.controller.ts`和`users.service.ts`注册到`users.module.ts`中
* 4、组件的`module`注入到`app.module.ts`里面
* 5、具体代码请查看`users`组件或者`food`组件

### 五、[代码见](https://github.com/kuangshp/nest-mongoose)
