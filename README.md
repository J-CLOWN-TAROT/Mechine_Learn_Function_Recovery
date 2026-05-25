# Mechine_Learn_Function_Recovery

该项目用于多架构二进制文件符号表恢复，采用机器学习方法，参考文献为《Revisiting Binary Code Similarity Analysis using Interpretable Features》，训练集为 Binkit1.0(链接 https://github.com/SoftSec-KAIST/BinKit)支持 x86 / x86_64, ARM / ARM64, MIPS / MIPS64 三种主流架构。

本项目侧重于去符号表信息的 elf 文件的函数名称恢复。

项目中/preprocess 中代码与 Binkit 仓库的预处理代码一致

在/main/helper 中，我们仿照论文，并且修改了一些对于无符号表文件恢复无法提取的参数

参数如下：

**CFG features  CFG 特点**

cfg_size

cfg_avg_degree

cfg_num_degree

cfg_avg_loopintersize

cfg_avg_loopsize

cfg_avg_sccsize

cfg_num_backedges

cfg_num_loops

cfg_num_loops_inter

cfg_num_scc

cfg_sum_loopintersize

cfg_sum_loopsize

cfg_sum_sccsize

**CG features  CG 特色**

cg_num_callees

cg_num_callers

cg_num_imported_callees

cg_num_incalls

cg_num_outcalls

cg_num_imported_calls

**Instruction features  指令特性**

inst_avg_abs_dtransfer

inst_avg_abs_arith

inst_avg_abs_ctransfer

inst_num_abs_dtransfer (dtransfer + misc)

inst_num_abs_arith (arith + shift)

inst_num_abs_ctransfer (ctransfer + cond ctransfer)

inst_avg_inst

inst_avg_floatinst

inst_avg_logic

inst_avg_dtransfer

inst_avg_arith

inst_avg_cmp

inst_avg_shift

inst_avg_bitflag

inst_avg_cndctransfer

inst_avg_ctransfer

inst_avg_misc

inst_num_inst

inst_num_floatinst

inst_num_logic

inst_num_dtransfer

inst_num_arith

inst_num_cmp

inst_num_shift

inst_num_bitflag

inst_num_cndctransfer

inst_num_ctransfer

inst_num_misc

**Type features  类型特征**

data_mul_arg_type

data_num_args

data_ret_type

其中 Type features  类型特征的提取不再依赖源码了，而是依靠ida软件解析的函数的形参



项目整体的流程为

①修改/config/path_variables.py为自己本地路径

②提取需要恢复符号表信息的elf文件特征，指令请见/main/example/example.sh

③根据符号需要恢复的程度，可以自己选择需要参与训练文件，详情请见/main/example/input_list_find.txt

PS:不用担心训练时间，训练时间非常短，而提取特征的流程较长，因此如果需要更完善的恢复，需要尽可能多的选择训练集

④用/main/helper/test_roc.py训练模型，训练指令如下

```C++
python3 helper/test_roc.py \
    --input_list "example/input_list_find.txt" \
    --config "config/gnu/config_gnu_normal_all.yml"
```

⑤训练完之后，调用/main/helper/test_topk.py即可查看函数恢复的效果以及对应的函数名称



