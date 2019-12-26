# gin@v1.5.0源码学习_lzy

## 背景

- 入职公司前，没有接触过golang，公司项目用的是gin，一直以来只是会使用api，并不知道其实现原理。想通过读源码加深对gin的理解。
- 参考：
  - https://www.kancloud.cn/liuqing_will/the_source_code_analysis_of_gin/616921

## 目录结构

<details>
<summary>binding</summary>
</details>
<details>
<summary>examples  // 各种例子</summary>
</details>
<details>
<summary>ginS</summary>
</details>
<details>
<summary>internal</summary>
</details>
<details>
<summary>render</summary>
</details>
<details>
<summary>testdata</summary>
<p style="text-indent:2em; margin: 0;">222332.go</p>
<p style="text-indent:2em; margin: 0;">454656.go</p>
</details>
<div>
    auth.go
</div>
<div>
    context.go  // 上下文相关方法
</div>
<div>
    context_appengine.go
</div>
<div>
    debug.go
</div>
<div>
    deprecated.go
</div>
<div>
    errors.go
</div>
<div>
    fs.go
</div>
<div>
    gin.go
</div>
<div>
    logger.go
</div>
<div>
    mode.go
</div>
<div>
    path.go
</div>
<div>
    recovery.go
</div>
<div>
    response_writer.go
</div>
<div>
    routergroup.go
</div>
<div>
    tree.go
</div>
<div>
    utils.go
</div>

## 上下文context

- context.go

  ```go
  // context结构体
  type Context struct {
      {
  
  // 初识化context
  func (c *Context) reset() {}
          
  // 拷贝当前context，在goroutine中使用
  func (c *Context) Copy() *Context {}
          
  // 获取最后一个handler
  func (c *Context) Handler() HandlerFunc {}
          
  // 获取路由路径
  func (c *Context) FullPath() string {}
  
  /*
  只能在中间件中使用
  c.Next()之前代码在 Handler执行之前 就执行
  中间件执行c.Next()时，跳去执行Handler
  c.Next()之后代码在 Handler执行之后 才执行
  */
  func (c *Context) Next() {}
          
  // 判读当前上下文是否退出
  func (c *Context) IsAborted() bool {}
          
  // 终止本次请求
  func (c *Context) Abort() {}
          
  // 终止本次请求，并返回状态码
  func (c *Context) AbortWithStatus(code int) {}
          
  // 终止本次请求，并返回状态码和json信息
  func (c *Context) AbortWithStatusJSON(code int, jsonObj interface{}) {}
          
  // 终止本次请求，并返回状态码和error
  func (c *Context) AbortWithError(code int, err error) *Error {}
          
  // 在上下文中设置key/value
  func (c *Context) Set(key string, value interface{}) {}
          
          // 
          
  ```

  