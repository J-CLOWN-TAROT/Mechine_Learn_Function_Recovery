# Mechine_Learn_Function_Recovery

该项目用于多架构二进制文件符号表恢复，采用机器学习方法，参考文献为《Revisiting Binary Code Similarity Analysis using Interpretable Features》，训练集为Binkit1.0(链接https://github.com/SoftSec-KAIST/BinKit)支持x86 / x86_64, ARM / ARM64, MIPS / MIPS64三种主流架构。

本仓库与https://github.com/SoftSec-KAIST/TikNib差异在于，TikNib主要是进行代码溯源比对，依赖源代码和符号表信息；而本项目更多侧重于无符号表信息的elf文件的函数名称恢复。



项目中/preprocess文件夹与Binkit仓库的预处理代码一致



在

