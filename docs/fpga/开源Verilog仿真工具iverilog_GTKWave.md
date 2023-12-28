---
sidebar_position: 1
description: Icarus Verilog是一个轻量、免费、开源的Verilog编译器，基于C++实现，开发者是 Stephen Williams ，遵循 GNU GPL license 许可证，安装文件中已经包含 GTKWave支持Verilog/VHDL文件的编译和仿真，命令行操作方式，类似gcc编译器，通过testbench文件可以生成对应的仿真波形数据文件，通过自带的GTKWave可以查看仿真波形图，支持将Verilog转换为VHDL文件。
---

下载地址：https://bleyer.org/icarus/

## 关于 Icarus Verilog
`Icarus Verilog`是一个轻量、免费、开源的`Verilog`编译器，基于`C++`实现，开发者是 `Stephen Williams` ，遵循 `GNU GPL license` 许可证，安装文件中已经包含 `GTKWave`支持`Verilog`/`VHDL`文件的编译和仿真，命令行操作方式，类似`gcc`编译器，通过`testbench`文件可以生成对应的仿真波形数据文件，通过自带的`GTKWave`可以查看仿真波形图，支持将`Verilog`转换为`VHDL`文件。

## 查看是否安装成功

安装成功后，可以通过命令窗口来查看命令所在的路径。

`Windows`环境可以通过`where`命令查看安装路径

```bash
where iverilog
where vvp
where gtkwave
```

`Linux`环境可以通过`which`命令查看安装路径

```bash
which iverilog
which vvp
which gtkwave
```

## 基本参数介绍

`Icarus Verilog`编译器主要包含`3`个工具：

* `iverilog`：用于编译`verilog`和`vhdl`文件，进行语法检查，生成可执行文件
* `vvp`：根据可执行文件，生成仿真波形文件
* `gtkwave`：用于打开仿真波形文件，图形化显示波形

在终端输入`iverilog`回车，可以看到常用参数使用方法的简单介绍：

```bash
$ iverilog
D:\iverilog\bin\iverilog.exe: no source files.

Usage: iverilog [-EiSuvV] [-B base] [-c cmdfile|-f cmdfile]
                [-g1995|-g2001|-g2005|-g2005-sv|-g2009|-g2012] [-g<feature>]
                [-D macro[=defn]] [-I includedir]
                [-M [mode=]depfile] [-m module]
                [-N file] [-o filename] [-p flag=value]
                [-s topmodule] [-t target] [-T min|typ|max]
                [-W class] [-y dir] [-Y suf] [-l file] source_file(s)

See the man page for details.
```

下面来详细介绍几个常用参数的使用方法。

## 参数-o

这是比较常用的一个参数了，和`GCC`中`-o`的使用几乎一样，用于指定生成文件的名称。如果不指定，默认生成文件名为`a.out`。如：`iverilog -o test test.v`

## 参数-y

用于指定包含文件夹，如果top.v中调用了其他的的.v模块，top.v直接编译会提示

```bash
led_demo_tb.v:38: error: Unknown module type: led_demo
2 error(s) during elaboration.
*** These modules were missing:
        led_demo referenced 1 times.
***
```

找不到调用的模块，那么就需要指定调用模块所在文件夹的路径，支持相对路径和绝对路径。

如：`iverilog -y D:/test/demo led_demo_tb.v`

如果是同一目录下：`iverilog -y ./ led_demo_tb.v`，另外，`iverilog`还支持`Xilinx`、`Altera`、`Lattice`等`FPGA`厂商的仿真库，需要在编译时通过`-y`参数指定库文件的路径，详细的使用方法可以查看官方用户指南：

https://iverilog.fandom.com/wiki/User_Guide


## 参数-tvhdl

`iverilog`还支持把`verilog`文件转换为`VHDL`文件，如`iverilog -tvhdl -o out_file.vhd in_file.v`

## Verilog 的编译仿真实际应用


新建`led_demo.v`源文件，内容如下：

```verilog
module led_demo(
    input clk,
    input rst_n,

    output reg led
);

reg [7:0] cnt;

always @ (posedge clk)
begin
    if(!rst_n)
        cnt <= 0;
    else if(cnt >= 10)
        cnt <= 0;
    else 
        cnt <= cnt + 1;
end

always @ (posedge clk)
begin
    if(!rst_n)
        led <= 0;
    else if(cnt == 10)
        led <= !led;
end

endmodule
```

功能非常简单，每10个时钟周期，led翻转一次。

仿真testbench文件led_demo_tb.v，内容如下：

```verilog
`timescale 1ns/100ps

module led_demo_tb;

parameter SYSCLK_PERIOD = 10;

reg SYSCLK;
reg NSYSRESET;

initial
begin
    SYSCLK = 1'b0;
    NSYSRESET = 1'b0;
end

/*iverilog */
initial
begin            
    $dumpfile("wave.vcd");        //生成的vcd文件名称
    $dumpvars(0, led_demo_tb);    //tb模块名称
end
/*iverilog */

initial
begin
    #(SYSCLK_PERIOD * 10 )
        NSYSRESET = 1'b1;
    #1000
        $stop;
end

always @(SYSCLK)
    #(SYSCLK_PERIOD / 2.0) SYSCLK <= !SYSCLK;

led_demo led_demo_ut0 (
    // Inputs
    .rst_n(NSYSRESET),
    .clk(SYSCLK),

    // Outputs
    .led( led)
);

endmodule
```

注意`testbench`文件中有几行`iverilog`编译器专用的语句，如果不加的话后面不能生成`vcd`文件。

```verilog
initial
begin            
    $dumpfile("wave.vcd");        //生成的vcd文件名称
    $dumpvars(0, led_demo_tb);    //tb模块名称
end
```

## 编译

通过`iverilog -o wave led_demo_tb.v led_demo.v`命令，对源文件和仿真文件，进行语法规则检查和编译。由于本示例比较简单，只有1个文件，如果调用了多个`.v`的模块，可以通过前面介绍的`-y`参数指定源文件的路径，否则编译报错。如果源文件都在同同一个目录，可以直接通过`./`绝对路径的方式来指定。

例如，`led_demo_tb.v`中调用了`led_demo.v`模块，就可以直接使用`iverilog -o wave -y ./ top.v top_tb.v`来进行编译。

如果编译成功，会在当前目录下生成名称为`wave`的文件。

## 生成波形文件

使用`vvp -n wave -lxt2`命令生成`vcd`波形文件，运行之后，会在当前目录下生成`.vcd`文件。

如果没有生成，需要检查testbench文件中是否添加了如下几行：

```verilog
initial
begin            
    $dumpfile("wave.vcd");        //生成的vcd文件名称
    $dumpvars(0, led_demo_tb);    //tb模块名称
end
```

## 打开波形文件

使用命令`gtkwave wave.vcd`，可以在图形化界面中查看仿真的波形图。

## Verilog转换为VHDL

虽然`VHDL`和`Verilog`都诞生于20世纪80年代，而且都属于硬件描述语言（`HDL`），但是二者的语法特性却不一样。`Icarus Verilog` 还有一个小功能就是支持把使用`Verilog`语言编写的`.v`文件转换为`VHDL`语言的`.vhd`文件。

如把`led_demo.v`文件转换为`VHDL`文件`led_demo.vhd`，使用命令`iverilog -tvhdl -o led_demo.vhd led_demo.v`。

## 批处理文件一键执行

通过批处理文件，可以简化编译仿真的执行过程，直接一键执行编译和仿真。

新建文本文档，输入以下内容：

```bash
echo "开始编译"
iverilog -o wave led_demo.v led_demo_tb.v
echo "编译完成"
vvp -n wave -lxt2
echo "生成波形文件"
cp wave.vcd wave.lxt
echo "打开波形文件"
gtkwave wave.lxt
```

文件扩展名需要更改，`Windows`系统保存为`.bat`文件，`Linux`系统保存为`.sh`文件。`Windows`直接双击运行，`Linux`在终端执行。