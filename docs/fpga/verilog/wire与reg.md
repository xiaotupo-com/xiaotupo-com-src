## `wire `导线（组合逻辑）

`wire`是`Verilog`设计中的简单导线（或任意宽度的总线）。以下是使用导线时的语法规则

1. `wire`元素用于连接模块实例化的输入和输出端口设计中的其他元素。
2. `wire`元素用作实际模块声明中的输入和输出。
3. `wire`元素必须由某种东西驱动，并且在没有被驱动的情况下不能存储值。
4. `wire`元素不能用作`always@`块中`=`或`<=`符号的左侧。
5. `wire`元素是`assign`语句左侧的唯一合法类型。
6. 在基于`Verilog`的设计中，`wire`元素是连接两个`peice`的无状态方式。
7. `wire`元素只能用于对**组合逻辑**进行建模。


例子：
```verilog
wire A,B,C,D,E; // 定义1位wire
wire [8:0] Wide; // 定义9位wire

reg I;

assign A = B & C;

always @(B or C) begin
	I = B | C;
end
```

## `reg` 元素（组合逻辑和时序逻辑）

`reg`类似于`wire`，但可以像**寄存器**一样用于存储信息（“状态”）。以下是使用`reg`元素时的语法规则。

1. `reg`元素可以连接到模块实例化的输入端口。
2. `reg`元素不能连接到模块实例化的输出端口。
3. `reg`元素可以用作实际模块声明中的输出。
4. `reg`元素不能用作实际模块声明中的输入。
5. `reg`是位于`always@block=`或`<=`符号左侧的唯一合法类型。
6. `reg`是`initial block = sign`（用于测试台）左侧的唯一合法类型。
7. `reg`不能用于`assign`语句的左侧。
8. `reg`与`always@（posedge Clock）`块一起使用时，可用于创建寄存器。
9. 因此，`reg`可以用于创建组合逻辑和时序逻辑。

例子：
```verilog
wire A, B;
reg I, J, K; // 简单的1位宽reg元素
reg [8:0] Wide; // 9位宽reg元素

always @(A or B) begin
	I = A | B; // 使用reg作为always@7赋值的左手边
end

initial begin // 在初始块中使用reg
	J = 1'b1;
	#1
	J = 1'b0;
end

always @(posedge Clock) begin
	K <= I;

end

```

`wire`和`reg`元件可以在某些情况下可互换地使用：

1. 两者都可以出现在`assign`语句的右侧，并且总是`@block=`或`<=`符号。
2. 两者都可以连接到模块实例化的输入端口。